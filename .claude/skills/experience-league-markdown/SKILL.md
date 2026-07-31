---
name: experience-league-markdown
description: Adobe Experience League / Adobe-Enterprise-Docs リポジトリ（help/**/*.md）でMarkdown ファイルを作成または編集する際に使用します。frontmatter、見出し、メモ（メモ/TIP/IMPORTANT/WARNING/etc.）、タブ（BEGINTABS/TAB/ENDTABS）、ビデオ埋め込み、バッジ、画像、リンク/相互参照、テーブル、リスト、コードブロック、およびExperience Leagueのバリデーションパイプラインが適用される制限されたHTML タグの許可リストに加えるを管理します。
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---


# Experience League Markdown

## 概要

Experience Leagueドキュメントでは、GitHub風のMarkdownと一連のカスタム拡張機能（blockquote ベースのショートコード、バッジ、タブ、動画埋め込み）が使用されます。 オーサリングパイプライン **では、これらのファイルが**&#x200B;検証されます。サポートされていない構文（生の`<video>` タグ、`<hr>`、タスクリスト、混合箇条書き文字、スキップされた見出しレベル、サイズが大きすぎる画像）を使用すると、スタイルのnitだけでなく、ビルド/検証エラーが発生します。

Source of truth: https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax （ローカルのreference.mdが古いと思われる場合は、このページを取得します。

すべてのショートコードとルールを含む完全な構文参照：[reference.md](reference.md) 面倒ではない何かを書く前にそれを読んでください（タブ、ビデオ、バッジ、HTMLを使用したテーブル）。

## クイックリファレンス

| 要素 | 構文 | メモ |
|---|---|---|
| Frontmatter | `---\ntitle: ...\ndescription: ...\n---` | 空白行を入力すると、`# Title`が次に来なければなりません |
| 見出しレベル | `#`, `##`, `###` | `#` = title （frontmatter `title`と一致）、`##` = ミニ目次エントリ。 決してレベルをスキップしない。 空白行の前後。 最大69文字（EN） |
| ヘッダーID | `## Heading text {#custom-id}` | 見出しが数字で始まる/含まれる場合は必須（例：`## 2026 release notes {#2026-release-notes}`） |
| メモ/ヒントなど。 | `>[!NOTE]`、`>`、`>Text` （それぞれ自分の行） | 種類：メモ、ヒント、重要、警告、注意、管理者、可用性、前提条件、情報、エラー、成功 |
| タブ | `>[!BEGINTABS]` / `>[!TAB Title]` / `>[!ENDTABS]` | タブセットをネストできません。リスト内にネストできません |
| ビデオ | `>[!VIDEO](https://video.tv.adobe.com/v/ID/?learn=on&enablevpops)` | video.tv.adobe.comでホストする必要があります – 生の`<video>`/ファイルリンクはありません |
| 画像 | `![alt text](assets/img.png "hover text"){width="300" align="center"}` | `align`は`center`または`right`のみです（`left`ではなく、`valign`ではありません） |
| リンク （相対） | `[Text](../folder/file.md)` | ソースファイルの場所のアカウント |
| リンク （ルート） | `[Text](/help/guide/file.md)` | リポジトリ内の任意の場所から作業できます。TOC.md バッジ URLに必要です |
| ディープリンク | `[Text](file.md#heading-id)` | ターゲット見出しには明示的な`{#heading-id}`が必要です |
| 外部リンク （裸のURL） | `<https://example.com>` | 裸のURLは自動リンクされていません。`< >`で折り返すか、`[text](url)`を使用してください |
| 箇条書きリスト | `* item` （`*`/`-`/`+`のいずれかを選択し、一貫性を維持） | リストの前後に空白行が表示されます。混合マーカー=検証エラー |
| 番号付きリスト | `1. item` （1行ごとに`1.`を繰り返します） | GitHubは実際の数値を |
| コード （インライン） | `` `code` `` | ファイル名、コマンド、値、未検証のサンプル URL |
| コード （フェンス付き） | ` ```language ` ... ` ``` ` | 常に言語を指定してください。前後に空白行があります。`{line-numbers="true" start-line="n" highlight="n-m"}` オプション |
| バッジ （インライン） | `[!BADGE Beta]{type=Informative url="..." tooltip="..."}` | `type`：有益/肯定的/否定的/中立的/注意 |
| 折りたたみ可能 | `+++Summary` ... `+++` | ネストされた折りたたみ可能はありません。内側のリスト/コードの周りに空白行があります |
| 空白線ハック | `<br>&nbsp;`を自分の行に設定 | プレーンな余分な空白行は、レンダラーによって折りたたまれるか無視されます |
| コメント | `<!-- text -->` | `<!--> text <-->`が表示されない – GitHub上のRAW ファイルを表示しているユーザーには表示されないので、シークレットはありません |

## よくある間違い

- **生の`<video>`、`<iframe>`またはその他の許可リストに加えるされないHTML**&#x200B;が検証エラー→発生しました。 HTMLの許可リスト: `table tbody td tfoot thead th tr col colgroup p ul ol li br b caption i strong u s span sub sup a img div em pre code codeblock`。 その他（`<video>`/`<source>`を含む）は拒否されます。代わりに`>[!VIDEO]` ショートコードを使用します。この場合、ビデオは既にvideo.tv.adobe.comでホストされている必要があります。
- **`<hr>`/ `***`の水平ルール、絵文字ショートコード （`:bowtie:`）、タスクリスト （`- [x]`）** – どれもサポートされていません。ローカルプレビューでレンダリングする場合でも、使用しないでください。
- **箇条書き記号** （`*`と`-`を同じリストに混在） – 検証エラー。 記事ごとに1つずつ選択してください。
- **見出しレベル** （`##`から`####`へ）をスキップすることはできません。
- **明示的なID** （例：`## 2026 release notes`）を持たない先頭の数字見出し – `{#some-id}`を追加するか、自動スラグが衝突/ブレークする可能性があります。
- 散文&#x200B;**（`Visit https://example.com for more`）の**&#x200B;裸のURLは、リンクとしてレンダリングされません。 `< >`で折り返すか、`[text](url)`を使用してください。
- **視覚的な間隔のための余分な空白行** — レンダラーによって折りたたまれます。 裸の`<br>`や繰り返し改行の代わりに`<br>&nbsp;`を使用します。
- **最大5 MBを超える画像** — 5 MBでの検証警告、20 MBでのエラー。 1つの記事に100を超える画像があると、レンダリングが中断される（EDS制限）。
- **frontmatter メタデータ**&#x200B;内の2つ以上のバッジ – デフォルトでは許可されていません。
- **問題をエスケープ中**: バックスラッシュエスケープは`` # { } [ ] * + - . ! ``でのみ機能します。 `<` `>`のプレースホルダー`<filename>`などでは、バックスラッシュではなく、インラインコードブロックまたはHTML エンティティ（`&lt;filename&gt;`）を使用します。

## Markdownの変更をコミットする前に

1. Frontmatter present, `# Title`はすぐに（空白行の後に）続きます。
2. すべての見出しには、前後に空白の行があります。スキップされたレベルはありません。
3. ビデオは`>[!VIDEO](https://video.tv.adobe.com/...)`です。生の`<video>` タグではありません。
4. カスタムショートコード （`>[!NOTE]`、`>[!BEGINTABS]`、`>[!BADGE ...]`）は、[reference.md](reference.md)の構文と完全に一致します（複数行ブロック内の空白`>`行を含む）。
5. リストは、リスト全体に空白行を含む、1つの一貫した箇条書きスタイルを使用します。
6. リンク：相対リンクは&#x200B;*source* ファイルのフォルダーから解決されます。クロスリポジトリまたは目次/バッジリンクは、ルート相対（`/help/...`）フォームを使用します。
7. 上記の「よくある間違い」セクションの「HTML」タグが許可リストに加えるのタグ以外に表示されない。
