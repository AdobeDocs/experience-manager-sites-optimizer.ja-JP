---
source-git-commit: ed1960cc0364dc4169a454a4860b7463890e3b74
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 0%

---
# ASO Doc Agent — パイプライン

`SKILL.md`から参照されています。 これは実行順序の信頼できる唯一の情報源です。SKILL.mdは
概要。 開始する前に`config.yml`を読み取ります。以下の`{braces}`のすべての値は
config キー。

**エラー処理（以下のすべての手順に適用）。** エラーが発生するツール/API呼び出し（認証
failure, timeout, malformed query, unexpected schema）は
正当な空虚な結果であり、無言でAJOに落ちることを許してはなりません
&quot;empty&quot; or &quot;nothing to do&quot; branch （例：ステップ 1.2の&quot;nothing to do here&quot;、ステップ 3.3の
&quot;epic backlog fully covered or all in flight&quot;）。 呼び出しエラーが発生した場合は、を停止して記録します。
実行サマリーの実際のエラーは、クリーンに返されたかのように続行する代わりに発生します。

## ステップ 0 - プリフライト

1. `pwd`とチェック `guidelines.md` + `.claude/skills/aso-doc-agent/config.yml`の両方が存在します。 そうでない場合は、間違ったディレクトリを停止します。
2. `gh auth status` – このホストで`sandsinh_adobe` アカウントに有効なトークンがあることを確認します。 **実行しない`gh auth switch`** – 機械全体のアクティブな`gh` アカウントを副作用として反転します。これにより、このマシン上の他のターミナル/プロセスが間違ったアカウントで停止し、無人で毎日の実行を実行する可能性があります。 代わりに、この実行の範囲は開始時に1回のみ設定します。そのため、以下の`gh`呼び出しでは、グローバルにアクティブなアカウントに関係なく、`GH_TOKEN`環境変数を介してこのトークンが使用されます。`export GH_TOKEN=$(gh auth token --user sandsinh_adobe)`
3. `mkdir -p {state_dir}`が見つからない場合。
4. `{state_dir}/run-state.json`が存在する場合は読み取ります（それ以外は`{"runs_completed": 0, "tracked_prs": []}`として扱います）。 `tracked_prs`は、このエージェントが開いたPRに対する`{number, headRefName, key}`の独自のリストです。結合せずに閉じたPRを検出するためにのみ使用されます（ステップ 1.5）。`gh pr list --state open`だけでは、消えたPRを確認できません。 メディア要求のタイミングは別のファイル `{state_dir}/media-requests.json` （ステップ 5）にあります。GitHubとJiraは他のすべての情報（PR ステータス、チケットステータス）の情報源のままです。
5. `--ticket KEY`が存在します – > ステップ 3の自動選択をスキップし、キーを直接使用します（手順4 ～ 7を実行します）。 それ以外は、手順3で自動選択します。

## ステップ 1 – 以前の実行を調整する

キャップ付きの実行でも、それ以外の場合は空の実行でも、毎回実行します。

1. `gh pr list --repo {github.repo} --label {github.pr_label} --state open --json number,url,isDraft,headRefName,title,reviewDecision`
2. **レビューの確認 – 開いているすべてのPR、実行** （`pr.check_reviews_every_run`）:
   - `gh pr view <number> --repo {github.repo} --json reviewDecision,reviews,comments`
   - `reviewDecision == "APPROVED"` ->今すぐ結合：`gh pr merge <number> --repo {github.repo} --merge`。 結合が完了として処理される前に、実際に着地した（`gh pr view <number> --json state,mergedAt` — `state == "MERGED"`）を確認します。保護されたブランチの拒否または保留中の必須チェックは、`gh pr merge`が呼び出された後でもPRを開いたままにしておくことができ、これは失敗として記録する必要があり、Jiraに結合として報告されません（これはタイムアウトベースではなく、通常の人間が承認した結合です）。 確認された結合について：結合されたリンクされたJira チケットにコメントし、`tracked_prs`からPRをドロップします。
   - `reviewDecision == "CHANGES_REQUESTED"` ->このバージョンで&#x200B;**not**&#x200B;がPRを自動修正します。 レビューコメント（`gh api repos/{github.repo}/pulls/<number>/comments`）を読み、`reviews` フィールドのトップレベルのレビュー本文を追加して、以下の&#x200B;**フィードバックから学習**&#x200B;します。 実行サマリーに、PRをオーサーアクションを待機中として記録します。 このPRが更新なしで`pr.stale_after_hours`より長い期間`CHANGES_REQUESTED`続いている場合は、ステップ 2のキャップゲートに対して古いフラグを付けます。人間には開いたままですが、キャップスロットを占有しなくなりました。
   - その他（まだレビューなし、レビューが投稿されていない`REVIEW_REQUIRED`件） ->ここでは何もできません。
3. **フィードバックから学習します。** トーン、構造、またはコンテンツに関する&#x200B;*一般化可能*&#x200B;のメモとして読み取られる各レビューコメントまたはレビュー本文について、そのPRに固有の一回限りの修正ではなく（「無視されたタブを無視サポート付きの機会について常に言及する」と「12行目のタイプミス」を比較）、日付のあるチケットにリンクされたエントリを`references/review-learnings.md`に追加します。 純粋に機械的なフィードバック（タイプミス、リンク切れ、リンク切れ）をスキップ - PR自体のそれらを修正し、彼らは耐久性のあるレッスンを必要としません。 正確なエントリ形式はそのファイルに記載されています。
4. リスト内の各&#x200B;**ドラフト** PRについて、ブランチ名（`{github.branch_prefix}<KEY>-...`）からJira キーを抽出します。
   - そのキーの`mcp__Corp-Jira__list_attachments` + `mcp__Corp-Jira__get_jira_comments`。
   - 検索：要求されたキャプチャに一致する新しい画像の添付ファイル、または`video.tv.adobe.com` URLを含むコメントを探します。
   - 見つかった場合：`git fetch`/`checkout`分岐、画像を`help/**/assets/`に追加（画像の添付ファイルの場合は`download_attachment`経由でダウンロード）、または`>[!VIDEO](...)` プレースホルダーを入力（動画のURL コメントの場合）、`experience-league-markdown`に対して検証、コミット、プッシュ、`gh pr ready <number>`、PRに対するコメント「追加されたメディア – レビューの準備ができました」、`{state_dir}/media-requests.json`のエントリを`resolved`に更新します。
   - 見つからない場合：`{state_dir}/media-requests.json`のリクエストからの経過時間を確認してください。 ここでも、手順5のエスカレーション/ギブアップロジックを適用します（実行の途中で開いたままになっているドラフト PRには、引き続きメディアが必要です）。ギブアップパスの`gh pr ready`呼び出しを含めます。これにより、特定のアップドラフトは引き続きレビュー可能になります。
5. **結合せずに閉じたPRを検出します。** この実行のオープン PR リスト （手順1）を`run-state.json`の`tracked_prs`と比較します。 開いているリストからトラッキングされたPRが見つからず、ステップ 2でマージが確認されていない場合は、マージせずに閉じられました。マージをドロップする前に、最終状態（`gh pr view <number> --repo {github.repo} --json reviews,comments`）を取得し、**最後に1回フィードバック**&#x200B;から学習します。したがって、人間の拒否理由が失われることはありません。 追跡から削除します。 チケット自体に追加のアクションは必要ありません。クレームのラベルは公開時にのみ適用されるので（ステップ 6.10）、クローズされていないマージされたチケットには既にラベルがなく、ステップ 3.2のチェック（オープン/マージされたPRなし）により、今後の実行時に再度選択される資格が自然に得られます。
6. 次の実行の手順5で比較する場合は、`run-state.json`の`tracked_prs`を現在のオープン PR リスト （`number`、`headRefName`、およびブランチ名から解析されたJira キー）に設定します。

## ステップ 2 - PR キャップゲート

1. 手順1.2で古い`CHANGES_REQUESTED`としてフラグ付けされたPRを除き、手順1の`gh pr list`出力から開いたPRをカウントします（`pr.stale_after_hours`より長く開いて更新なし）。これらは人間に対して開いたままですが、キャップスロットを占有しなくなります。
2. カウント >= `{pr.max_open}` （3）の場合：ログ `"cap reached ({count}/{pr.max_open} open) — skipping new ticket this run"`、手順7に移動します。
3. その他の手順3に進みます。

## ステップ 3 - チケットを選択する

`--ticket KEY`が渡された場合は完全にスキップします（KEYを使用）。

```
JQL: "Epic Link" = {jira.epic} AND status = "{jira.open_status}"
     ORDER BY priority DESC, created ASC
```

1. 検索を実行します（`mcp__Corp-Jira__search_jira_issues`、`minimizeOutput: true`、`key,summary,priority,status,labels`に制限されたフィールド）。
2. 結果を順番に確認します。 次のチケットをスキップします。
   - 既に`{jira.picked_label}` ラベルがあります。または
   - リモート （`git ls-remote --heads origin '{github.branch_prefix}<KEY>-*'`）に既存のブランチ `{github.branch_prefix}<KEY>-*`が既に存在します。または
   - 既にオープンまたは結合されたPRがあります（手順1のリスト / `gh pr list --state all --search <KEY>`に対してクロスチェック）。
3. 3つのチェックをすべて通過する最初のチケットはピックです。 検索で対象となるチケットが0件が返されたため&#x200B;**に合格しない場合は、`"epic backlog fully covered or all in flight"`とログを記録し、手順7に進みます。**&#x200B;検索自体が失敗した場合（認証エラー、タイムアウト、形式が正しくないJQL）は、実際のエラーを代わりにログに記録します（上記のエラー処理を参照）。
4. まだ&#x200B;**not**&#x200B;でチケットにラベルを付けてください。クレームのラベルはステップ 6.10で適用されます。ブランチとPRが実際に存在する場合にのみ適用されます。 ステップ 4-5 （リサーチ/ドラフト/メディア）は、チケット上にトレースを残さずに失敗またはクラッシュする可能性があります。ステップ 6の前の唯一の進行中のシグナルは、上記のブランチ存在/PR存在チェックです。これは、実際の同時実行がない単一のマシンから実行されるので、十分です。

## ステップ 4 – 調査+ドラフト

調査は最初に行われ、**マルチソース** – 単一の入力からドラフトを作成しない（Jira
チケットのみ、または兄弟ドキュメントを読むだけ）。 以下のすべてのソースが確認または
他の問題を修正します。ソースコードを信頼することで矛盾を解決します> Wiki/PR docs >
Slackのディスカッション > doc-writer自身の推論をその順序で行い、インラインでフラグを立てます
解決できない場合は`<!-- CONFIRM -->`として処理します。

0. **レビューレッスンの累積。** 最初に`references/review-learnings.md`をお読みください。 このチケットのトピックに関連するものは、ドラフトの前に適用します。これは、過去のPR レビューからのフィードバックが、同じ修正を繰り返す代わりに将来のドラフトを改善する方法です。

### 調査（当てはまることをすべて実行する。そのままドラフトに進めないでください）

1. **Source コード （実際の動作の根拠）。** プライマリ UI リポジトリ （`research.code_repos` in config.yml）で、機能のアダプター/ハンドラー（`*OpportunityAdapter.tsx`, `*SuggestionAdapter.tsx`）、そのデータフック（`use*Data.ts`）、およびその`.l10n.ts`/`.I10n.ts` タイトル/説明文字列を検索します。 このように、フィールド名、データ形状、カテゴリー、製品コピーを正確に管理できます。データソースが一致しない場合は、他のコピーよりも優先する必要があります。
2. **Wiki （デザインの意図、仕様、決定）。** 機能/商談名とエピック/チケットキーを持つ`mcp__Adobe-Wiki__search_wiki_content`。 一致するページ（`get_wiki_content`）を読み取ります。次の点は、機能が存在する理由、製品チームが使用する用語、文書化されたUX フローまたはエッジケース、および実際のUIの外観を確立する埋め込みスクリーンショットです（手順5のメディアキャプチャ仕様に通知します。ページが最新でない限り、実際の新しいスクリーンショットに置き換わりません）。
3. **Slack（チームが実際にそれについて話す方法、質問を開く、最近の変更）。** 機能/商談名とチケットキーを含む`mcp__Slack__slack_search_messages`は、`research.slack_channels`がconfig.ymlで絞り込まない限り、チャネルによって制限されません。 お知らせメッセージ（多くの場合、クリーンな顧客向けフレーミングを持っています）、デザインのディスカッションスレッド、および機能が最近変更されたことを示す何かを、兄弟ドキュメントやコードコメントがまだ反映されない方法で探します。
4. **GitHub PR履歴（実装根拠、スクリーンショット、レビューディスカッション）。** `research.code_repos`全体で`gh search prs --repo <repo> "<feature name>"`または`gh pr list --repo <repo> --search "<ticket key OR feature name>" --state all`。 コードだけでは説明できない動作を明確にする根拠、リンクされたデザインドキュメント、スクリーンショットに関する結合されたPR説明を読みます（例：修正タイプがゲート化された理由、UIでのエッジケースの表示）。
5. **トーンアナログ。** チケットの概要にもとづいて、最も近い2～3 ページを特定します。
   - 「。..商談のハウツー」チケット -> `help/documentation/opportunities/`の2つの兄弟ファイルを読み取ります（実際の商談ごとのハウツーの場所 – `help/opportunity-types/*.md`は、ハウツーのコンテンツ自体ではなく、これらの場所にカードグリッドがリンクされているカテゴリのランディングページです）。
   - 設定/ワークフロー/接続チケット -> `help/documentation/`の1 ～ 2個の兄弟ファイルを読み取ります（最も近い一致については、`setup/`、`opportunities/`、`settings.md`、`basics.md`を確認してください）。
     ミラー見出しの構造、ノートボックスの使用状況、文の長さ、技術的な詳細のレベル。
6. **形式ルール。** 書き込む前に、`experience-league-markdown` スキルのクイックリファレンスを再度読み直してください。 すべての見出し/メモ/画像/リンクは、その構文と正確に一致する必要があります。

### ドラフト

7. **対象ファイルの決定。** チケットが既存のスタンドアロンページの細分性と一致しない限り、既存のページの関連セクションを新しいファイルを作成するよりも拡張することを好む（例えば、各商談は`help/documentation/opportunities/`の下に独自のファイルを取得します。新しいページは、既存の兄弟の正確な構造に従います）。 既存のページを拡張する場合は、このチケットの1つのセクションのみをタッチします。古く見える関連のないセクションは編集しないでください。 新しいスタンドアロンページの場合は、そのカードを関連する`help/opportunity-types/*.md` ランディングページ（ソースコメントリスト +生成されたHTML ブロック、既存のカードの正確なパターンに一致）に追加し、`help/main-toc/TOC.md`に登録します。
8. **下書きv1.** コンテンツを今すぐ書き込みます（メモリ/スクラッチで、リポジトファイルには書き込みません。これは、メディアの決定後の手順6で行われるため、メディア保留ドキュメントとメディア解決ドキュメントは同じ書き込みパスを経由します）。 手順1～6をすべて合成します。Jira チケットの説明を変更するだけではありません。
9. **反復。** 手順1～4の調査結果ごとにv1のドラフトを再読みする：ドラフトはSlackやWikiが浮上した何かを見落としましたか？ ソースコードが実際に行うものと矛盾しますか？ 兄弟のトーンにできる限り近づいているか？ 先に進む前に修正します。これは、形式的なものではなく、実際の2回目のパスです。 このパスの後、まだ確認されていない内容（4つのソースのいずれにも見つかりません）は、推測ではなくインライン `<!-- CONFIRM -->`のコメントを受け取ります。
10. **メディア決定。** `mediaNeeded: true|false`を決定します。
    - 機能がマルチステップのUI ワークフローで、テキストの説明だけでは実質的に追跡が困難な場合（`guidelines.md`の「テキストの説明が不十分な場合に慎重に使用する」と一致する）、`true`。
    - `true`が生成する場合：`mediaType` （`screenshot`または`video`）、`captureSteps` （キャプチャする状態を再現するための正確な手順）、`urls` （顧客向けアプリのURL）および/またはその状態に到達するために必要な内部ページのURL。Jira チケットの説明/コメント、Wiki、または`open-aso-devmode-url`規則から実際のURLを取得します。URLを作成しないでください）。
    - `false`の場合は、このチケットの手順5をスキップします。

## ステップ 5 - メディアゲート

手順4で`mediaNeeded: true`を設定した場合にのみ実行されます。 内のすべてのタイムスタンプ
`{state_dir}/media-requests.json`はUTC ISO-8601 （`date -u +%Y-%m-%dT%H:%M:%SZ`） —
以下の経過時間の計算があいまいにならないように、常にこの形式で書いて比較します
複数の実行。

1. このチケットキーの既存のエントリについて`{state_dir}/media-requests.json`を確認してください。 Noneの場合、これは新しいリクエストです。
2. **新しいリクエスト：**
   - `media.contacts_in_order[0].email` （sandsinh）の`mcp__Slack__slack_lookup_user`からSlack ユーザーIDを取得します。
   - `mcp__Slack__slack_send_dm`に次のメッセージが含まれています：Jira チケット キー+ リンク、正確に取得する内容（`captureSteps`）、使用するURL、回答の場所（「Jira チケットに返信 – スクリーンショットを直接添付するか、ビデオの場合は、通常のExperience League ビデオ フォームを使用してアップロードし、結果の`video.tv.adobe.com` リンクをコメントとして貼り付ける」）。
   - `{state_dir}/media-requests.json[KEY] = {requestedTo: "sandsinh", requestedAt: <UTC ISO-8601 now>, escalated: false}`を書き込みます。
3. **以下の既存の要求：**&#x200B;両方のしきい値が元の`requestedAt`から測定されます。エスカレーションしても、時計はリセットされません。
   - `now - requestedAt` &lt; `media.escalate_after_hours` ->この実行では何もしません。メディアがまだ保留中（ドラフト PR）の状態で公開に進みます。
   - `now - requestedAt` >= `media.escalate_after_hours`とまだエスカレーションされていない – > DM `media.contacts_in_order[1]` （kanishka）、メッセージメモ sandsinhはN時間前に既に尋ねられましたが、応答はありません。 エントリを更新：`escalated: true, escalatedAt: <UTC ISO-8601 now>`。
   - `now - requestedAt` >= `media.give_up_after_hours` （エスカレーション状態に関係なく） ->公開目的で`mediaNeeded: false`を設定し、ドラフトにインラインノートを挿入します：`>[!TIP]\n>\n>A screenshot for this step is being added in a follow-up update.`このチケットにPRが既に存在し、ドラフトである場合（新しいステップ 6の公開ではなく、ステップ 1.4を介してここに到達した場合）、`git fetch`/ブランチをチェックアウトしてメモを適用し、コミット、プッシュ、呼び出します`gh pr ready <number>` – 特定されたドラフトはがレビュー可能可能になっても、無期限のままのままになることはありません。 エントリ `gaveUp: true`をマークします。

## ステップ 6 – 公開

手順3でチケットが完全にスキップされた場合はスキップします（公開するものはありません）。

1. `git fetch origin`と`git checkout -B {github.branch_prefix}<KEY>-<short-slug> origin/main` — `-B` （`-b`ではなく）したがって、チェックアウトをブロックするのではなく、クラッシュした以前の実行から残ったローカルブランチがリセットされます。`origin/main`から直接分岐すると、以前のクラッシュからダーティローカルステートも破棄されます。
2. 手順4のドラフトを、手順4.3で決定したターゲットファイルに書き込みます。 `experience-league-markdown`の「マークダウンの変更をコミットする前」チェックリストを行ごとに再検証します。
3. マークダウンリンターが設定されており（`markdownlint_custom.json` at repo root）、`markdownlint-cli`/`npx markdownlint`が使用可能な場合は、変更されたファイルに対して実行し、違反を修正してからコミットします。
4. コミット：`docs(aso): <ticket summary, lowercase, no trailing period>\n\nSITES-XXXXX`。
5. `git push -u origin <branch>`.
6. レビュアーの選択：`gh pr list --repo {github.repo} --label {github.pr_label} --state open --json reviewRequests` – 現在設定されている2人のレビューアーのリストを数えます。割り当てるレビューアーの数が少ない場合（タイ -> `sandsinh_adobe`）。
7. PR本文：

   ```
   ## Summary
   [1-2 sentence description of the feature now documented]
   
   ## Source
   Closes documentation gap tracked in [SITES-XXXXX](https://jira.corp.adobe.com/browse/SITES-XXXXX)
   
   ## Media
   [either "No media needed for this update." OR "Screenshot/video requested from {contact} on {date} — PR opened as draft until resolved." OR "Media follow-up pending — shipped without it; see inline note."]
   
   > 🤖 Drafted by aso-doc-agent
   ```
8. メディアがまだ保留中の場合は`gh pr create --repo {github.repo} --title "<ticket summary>" --body "<above>" --label {github.pr_label} --reviewer <chosen-github-handle> --draft`、そうでない場合は`--draft`を省略します。
9. ラベルフラグが使用されなかった場合`gh pr edit <number> --add-label {github.pr_label}` （ベルトとサスペンダーは、この組織のツールの他の場所で使用されているパターンと一致します）。
10. Jira: `add_jira_comment`がPR URLをリンクしています。この実行では初めて`{jira.picked_label}`を追加します（`update_jira_issue`、既存のラベルと結合）。 これは、ブランチとPRの両方が存在する場合にのみ意図的に適用される主張です。手順3～5のどこかでクラッシュすると、チケットが完全にラベル付けされず、安全に再選択できなくなり、永続的にスタックする代わりに。 チケットのステータスを移行しないでください。このステータスは、ドキュメント チームの独自のトリアージに残します。`{jira.picked_label}`は、このエージェントが書き込む唯一のステータス シグナルです。

## ステップ 7 – 概要の実行

1. 更新`{state_dir}/run-state.json`: `runs_completed += 1`、タイムスタンプ、チケット選択（または「なし」+理由）、PRの開封済み/更新済み（または「なし」+理由）、キャップステータス。
2. 人間が判読可能な短い要約（チケット、アクションの実行、PR リンク、メディアステータス）を印刷します。
