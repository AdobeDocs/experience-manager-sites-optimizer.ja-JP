---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---
# ASO Doc Agent – 使用状況

これは何か、どのように機能するのか、必要なときに何をすべきかなどです。

## 動作

このエージェントは、毎日、ドキュメントされていないASO機能の中から最優先度が最も高いものを
[SITES-49539](https://jira.corp.adobe.com/browse/SITES-49539)のバックログ （39 チケット、例：
「Canonical opportunity how-to」、「Slack notifications」）は、1つのドキュメントを記述します
割り当てることでPRが開きます
設定済みのレビュー担当者（`sandsinh_adobe` / `kanishka_adobe`）は現在開いている数が少なくなっています
このエージェントからのリクエストを確認します。 この機能でスクリーンショットや動画が必要な場合は、次の情報が必要です
PRを終える前にSlackに一本。

また、毎回の実行で、オープンなPRのレビューステータスも確認されます。承認済みのPRがマージされます
要求された変更のフィードバックが読み取られ、一般化可能な場合
レッスン（1回限りのタイプミスではありません）を記録するので、今後のドラフトでは同じ間違いを繰り返すことはありません。

1回の実行= 1つの機能=最大1つのPR。 1回の実行で複数のチケットに触れることはなく，
同時に3つ以上のPRを開くことはありません（既存のPRが最初に結合/閉じるのを待ちます）。

## あらゆるものが存在する場所

| 何を | パス |
|---|---|
| 今後の施策の決定方法 | `.claude/skills/aso-doc-agent/SKILL.md` |
| ステップバイステップの詳細や | `.claude/skills/aso-doc-agent/references/pipeline.md` |
| チーム固有の設定（レビュー担当者、キャップ、エスカレーションのタイミングを変更するには、これを編集します） | `.claude/skills/aso-doc-agent/config.yml` |
| PR レビューフィードバックから得られた教訓（Gitで追跡、ドラフトの前に読む） | `.claude/skills/aso-doc-agent/references/review-learnings.md` |
| ローカル実行状態（gitignored – 削除しても安全、再構築されます） | `.claude/skills/aso-doc-agent/state/` |
| 日別スケジュールインストーラー | `.claude/scripts/aso-doc-agent-setup.sh` |
| 権限ヘッドレス実行のアクセス許可の許可リストに加える | `.claude/settings.local.json` （gitignored、machine-local） |

## 実行

- **手動、通常のセッション：** `/aso-doc-agent` （または`/aso-doc-agent --ticket SITES-XXXXX`）
- **ヘッドレス、1回限り：** `claude -p "/aso-doc-agent"` （リポジトリルートから）
- **日別、無人：**&#x200B;はすでに`launchctl`経由でインストールされています（以下を参照）。毎日、現地時間の07:53に実行されます。アクションは必要ありません

### 日次スケジュールのインストール/変更

```bash
bash .claude/scripts/aso-doc-agent-setup.sh
```

次の`launchd` ジョブ （`~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist`）をインストールします
このリポジトリから`claude -p "/aso-doc-agent"`を毎日実行します。 いつでもスクリプトを再実行します
その中でスケジュールを編集します（デフォルト：07:53 ローカル）。 これは、お持ちの装置が以下の間のみ作動します：
その時点で起動および起動 – launchdは失敗したジョブを過去にさかのぼって実行するのではなく、実行されます
次回の予定時刻は通常どおりです。

```bash
launchctl list | grep com.sandsinh.aso-doc-agent   # confirm it's loaded
launchctl start com.sandsinh.aso-doc-agent         # trigger a run right now, don't wait for 07:53
launchctl unload ~/Library/LaunchAgents/com.sandsinh.aso-doc-agent.plist  # stop it
```

スケジュールされた実行のログが表示されます `.claude/skills/aso-doc-agent/state/launchd.out.log`
および`launchd.err.log`。

## 何をするよう求められるか

- **担当者からのSlack DM** （送信者は送信者です。最初にsandsinh、kanishkaが送信先
エスカレーション）正確なキャプチャ手順とURLを含むスクリーンショットまたはビデオを求める
使用： **Slackではなく、リンクされたJira チケットで返信**：スクリーンショットを直接添付します。
またはビデオの場合は、通常のExperience League ビデオフォームからアップロードします
（`experience-league-video-upload` スキル）を入力し、結果を貼り付けます `video.tv.adobe.com`
jira コメントとしてリンクします。 次の実行で自動的にピックアップされます。
- **5日以内に誰も応答しない場合**、リクエストはsandsinhからkanishkaにエスカレーションされます
施策例。 **10日後**&#x200B;に、いずれかの担当者からの応答がない場合、担当者はドキュメントを出荷します
メディアを使用せずに、インラインノートを追加します。 タイムアウトベースの自動結合やPRは存在しません
実際の人間によるレビューを待つことになります。
- **レビューするPR** — エージェントが開いたPRの数が少ない2人のうち、いずれかに割り当てられます
現在審査待ちの状態です。 ドラフト PRは、メディアがまだ保留中であることを意味します。彼らは
アセットが表示されたら、自動的にレビューの準備が整います。 承認すると、エージェントがマージされます
次回の実行でも可能です。個別の結合ステップは必要ありません。
- **変更をリクエストすると**、次回の実行時にエージェントがコメントを読み取ります。 一般化可能
フィードバック （タイプミスやリンクの修正ではありません）が`references/review-learnings.md`に書き込まれるため、
同じ修正を繰り返す必要はありません。

## 動作の調整

`.claude/skills/aso-doc-agent/config.yml`を編集（Gitで追跡 – 変更内容は毎回に影響します
future run （このマシン上か、リポジトリをクローンする他のユーザー上で）:

- `pr.max_open` — エージェントが新しいチケットのピッキングを一時停止する前のオープン PRの数（デフォルトは3）
- `pr.stale_after_hours` — `CHANGES_REQUESTED` PRが`pr.max_open`に向かってカウントを停止するまでの待機時間（デフォルトは336 = 14日）。開いたままなので、新しいピックのブロックのみが解除されます
- `github.reviewers` – 割り当てられたユーザー、およびバランス
- `media.contacts_in_order` / `escalate_after_hours` （デフォルト 120 = 5日） / `give_up_after_hours` （デフォルト 240 = 10日） – 質問されたユーザー、順序、忍耐強さ。どちらも元のリクエストから測定されるため、エスカレーションによってギブアップ日がプッシュされることはありません
- `pr.check_reviews_every_run` — レビューと確認の手順をオフにします（推奨されません。これは、結合と学習の実行方法です）

## 権限プロンプトで停止した場合

ヘッドレス （`claude -p`, launchd）実行には、プロンプトを表示するターミナルがありません。リストに登録されていないツール呼び出しです
ぶら下がるのではなく失敗するだけです。 実行のログにコマンドに対する権限の拒否が表示される場合
パイプラインが必要です。次の`permissions.allow` リストに追加してください：
`.claude/settings.local.json` （gitで追跡されない – machine-local；実行中のすべての開発者
この担当者は、独自のスコープ付きコピー（許可リスト）を必要とします。

## 進歩を完全に止めれば

次の順序で確認します。
1. `gh pr list --repo Adobe-Enterprise-Docs/experience-manager-sites-optimizer.en --label aso-doc-agent --state open` – これが3と表示されている場合、レビュー待ちであり、停止していません。
2. Jira: SITES-49539の下に残っている`New` チケットのうち、まだ`aso-doc-agent-picked`になっていないチケットはありますか？ ラベルは、ブランチ+PRが存在する場合にのみ適用されます（pipeline.md ステップ 6.10）。そのため、クラッシュした実行でラベル付きの未公開のチケットが残らないようにしてください。まだ見つかった場合（手書きで追加されたラベルなど）、手動で削除して、チケットを再度有効にします。
3. 最新の実行のエラーの`.claude/skills/aso-doc-agent/state/launchd.err.log`。
4. 実行の概要に「エピック バックログが完全にカバーされている」または「ここでは何もしない」と表示されていても、対象となる作業が必要であることがわかっている場合は、疑わしいものとして扱います。それらのメッセージは実際には空の結果のために予約されています。 実際のJira/GitHub/Slack エラーは個別にログに記録され、メッセージの1つの背後に隠れるのではなく、`launchd.err.log`に独自の行として表示されます。
