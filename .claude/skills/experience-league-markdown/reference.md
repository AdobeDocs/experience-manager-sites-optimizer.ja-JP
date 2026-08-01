---
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---
# Experience League Markdown – 完全な構文リファレンス

https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntaxから凝縮（最終確認は「最終更新日：2026年6月17日（PT）」のページ）。 古いページが表示された場合は、ライブページをリフェッチします。

## Frontmatterとtitle

```markdown
---
title: Title for search optimization
description: This is the article description used for search optimization.
---
# Article title
```

クロージング `---`の直後の行（および1つの空白行）は`# Title`である必要があり、フロントマターの`title:`と一致する必要があります。

## 基本テキスト書式設定

- 太字：`**bold**`
- 斜体：`*italic*`
- 太字+斜体：`***both***`
- フォーマット文字をエスケープします：`\*not italic\*`
- 段落には特別な構文は必要ありません。段落の間に空白行を挿入するだけです。

## 見出し

```markdown
# This is level 1 (article title)
## This is level 2 (mini-TOC entry)
### This is level 3
```

- `#` （H1） =記事のタイトル。frontmatter `title`と一致する必要があります。
- `##` （H2） = ミニ目次にデフォルトで表示されます（`mini-toc-levels: 3` in frontmatter to show more levels）。
- レベルをスキップしない（`##` → `####`は無効です）。
- 見出しごとに&#x200B;**および**&#x200B;の前に空白行が必要です。
- 見出しの最大長：69文字（EN）、120文字（ローカライズ）。
- 見出しID / アンカー：`## Creating processing rules {#processing-rules}` – 小文字、ハイフネーション付き。 見出しテキストが数値（年など）で始まる場合は必須です。 明示的なIDがない場合、デフォルトのアンカーは自動的にスラジフィケーション化された見出しテキストになります。

## 注意/注意

標準タイプ：`NOTE`、`TIP`、`IMPORTANT`、`WARNING`。 新しいEXL専用タイプ：`ADMIN`、`AVAILABILITY`、`PREREQUISITES`、`INFO`、`ERROR`、`SUCCESS`。

```markdown
>[!NOTE]
>
>This is a standard NOTE block.
>
>It can include multiple paragraphs.
```

ブロックの各行は`>`で始まります。 文字マーカーの直後に裸の`>`行を含めます。

## タブ

```markdown
>[!BEGINTABS]

>[!TAB iOS]

Content for the iOS tab.

>[!TAB Android]

Content for the Android tab.

>[!ENDTABS]
```

- タブセット内またはリスト内のタブセットをネストすることはできません。
- タブタイトルは略語でレンダリングされます（`>[!TAB ...]`内ではマークダウン形式は使用されません）。
- 1つのページに複数のタブセットを配置することもできます。

## ビデオ

```markdown
>[!VIDEO](https://video.tv.adobe.com/v/27069/?learn=on&enablevpops)
```

- ビデオは既に`video.tv.adobe.com` （Adobe TV/MPC）でホストされている必要があります。生のビデオファイルのリンクまたは`<video>` タグはサポートされていません。
- 推奨されるクエリパラメーター：`?learn=on&enablevpops` （このリポジトリ内のすべての埋め込みで使用される正規フォーム）。 自動再生に`&autoplay=true`を追加します。
- 文字起こし：`{transcript=true}`をショートコードに追加するか、ガイド/リポジトリ全体に`TOC.md`/`metadata.md`で`auto-video-transcripts: true`を設定します。

## バッジ

インラインバッジ（配置された場所でレンダリング）:

```markdown
[!BADGE Beta]{type=Informative url="https://www.example.com" tooltip="Go to example.com"}
```

メタデータバッジ（H1より上にレンダリング） — frontmatterで：

```yaml
badgePremium: label="Premium" type="Positive" url="https://www.premium-product.com" tooltip="Download Premium"
```

- `type` （大文字と小文字を区別しない）: `Informative` （デフォルト/青）、`Positive` （緑）、`Negative` （赤）、`Neutral` （濃い灰色）、`Caution` （黄色）。
- ラベルのみが必要です。オプションは`type`/`url`/`tooltip`です。
- 記事ごとに最大&#x200B;**2**&#x200B;個のメタデータバッジ （設定可能ですが、例外に依存する前に確認してください）。
- メタデータバッジ値は引用符で囲む必要があります。 インラインバッジ `url`/`tooltip`は引用符で囲む必要があります。
- `TOC.md`から使用されるバッジ URLは、相対ではなくルート相対（`/help/guide/article.md`）である必要があります。目次エントリはフォルダー間で適用されます。
- `before-title="false"`は、H1の下にメタデータバッジを移動します。
- `newtab=true`を追加して、バッジ URLを新しいタブで開きます。

## 画像

```markdown
![alt text](assets/logo.png "Hover text"){width="300" align="center"}
```

- `align`: `center`または`right`のみ – `left`ではなく、`valign`ではありません。
- `width`: ピクセル （`"300"`）または表示領域の割合（`"50%"`）。
- `zoomable="yes"`は、画像をクリックして拡大します（リンクでもある画像と組み合わせないでください。リンクが優先されます）。
- 共有イメージのルート相対パス：`/help/assets/imagename.png`。
- 制限：100 MBのハードキャップ（GitHub）、ケアを開始する前に5 MB、20 MBのトリガーが検証エラーを発生します。 記事ごとに最大100枚の画像（EDS レンダリング制限）。

## リンクと相互参照

- 外部：`[Adobe](https://www.adobe.com)`
- リンクとしての裸URL: `<https://www.adobe.com>` – ラップされていない裸のURLは&#x200B;**not**&#x200B;自動リンクを行います。
- 相対相互参照：`[Overview](collaborative-doc-instructions/overview.md)` — *ソース* ファイルの場所から解決します。`./`、`../`、`../../`をサポートしています。
- ルート相対の相互参照：`[Overview](/help/using/docile-rules/introduction.md)` — ソースの場所に関係なく、リポジトリ内の任意のファイルから機能します。
- 見出しのディープリンク：targetには`{#heading-id}`が必要です。`[Text](file.md#heading-id)`とリンクする必要があります（同じページの場合は`#heading-id`のみ）。
- 新しいタブで開く：`[See What's new](whats-new.md){target="_blank"}`。

## リスト

```markdown
1. This is step 1.
1. This is the next step.
   1. Sub-step (indent 3 spaces for numbered lists)
   1. Sub-step
```

```markdown
* First item.
* Second item.
```

- 番号付きリスト：常に`1.` （または常に`1)`）を書き込む – GitHubは実際のシーケンスをレンダリングします。 1つのスタイル （`.`対`)`）を選択し、記事の中で一貫性を保ちます。
- 箇条書きリスト：`*`、`-`、`+`のいずれかを選択して一貫性を維持します。同じ記事に箇条書きを混在させるのは、検証エラーです。 ほとんどのリポジトリでの規則：`*`。
- リストの前後に空白行が必要です。
- リスト項目（画像、表、メモ）間のコンテンツは、テキストの先頭（番号付きリストの場合は3つのスペース、箇条書きリストの場合は2つのスペース）にインデントする必要があります。そうしないと、リストが壊れます。 インデント（6つのスペース）を使用すると、代わりにコードブロックに変換されます。

## コードブロック

インライン：`` `code` `` – または、リテラルバックティックが必要な場合は、トリプルバックティックをインラインで折り返します。

フェンス：

&grave;&grave;&grave;&grave;markdown

```javascript
var x = 1;
```

&grave;&grave;&grave;&grave;

- 構文の強調表示に使用する言語を必ず指定し、「コピー」ボタンを押します。
- フェンスで囲まれたブロックの上下に必要な空白行。
- 行番号：`` ``&#x200B;`html {line-numbers="true"} `&#x200B;&grave;
- 別の場所で番号を付けます：`` ``&#x200B;`html {line-numbers="true" start-line="7"} `&#x200B;&grave;
- ハイライト行：`` ``&#x200B;`html {line-numbers="true" start-line="7" highlight="11-13, 16"} `&#x200B;&grave;
- コードブロックコンテンツはローカライズされません（ただし、公開時に削除される`!UICONTROL`/`!DNL` タグを除きます）。
- コードブロック内でマークダウン/HTMLのフォーマット（`<i>`など）が機能しません。プレースホルダーには、角括弧またはプレーンテキストを使用します。

## テーブル

- 標準的なGFM パイプテーブルは、単純なケースでも機能します。
- HTML テーブルは、特殊なケース（ヘッダー行のないテーブルなど）に使用できます。それ以外の場合はmarkdownを優先します。
- 制限付きHTMLは、マークダウンテーブルセル内で許可されています：`<p>`、`<br>`、`<ul>`、`<ol>`。
- 表は自動レンダリングまたは固定レンダリングに設定できます。そのレベルの制御が必要な場合は、構文ガイドからリンクされている「表」の記事を参照してください。

## 折りたたみ可能なセクション

```markdown
+++See details

This is text inside a collapsible section.

* Bullet one
* Bullet two

+++
```

- 折りたたみ可能なセクションをネストしないでください。正しくレンダリングされません（検証に失敗しないため、バグはサイレントに出荷されます）。
- セクション内の内側のリスト/コードブロックの周りに空白行が必要です。他の場所と同じです。

## テキストの強調表示

```markdown
This sentence is normal. <span class="preview">This text is highlighted.</span>
```

インライン/段落の強調表示には`<span class="preview">`、複数の段落/コンポーネントには`<div class="preview">`を使用します。

## スニペットとインクルード

- リポジトリの`help/snippets.md`から共有されたH2 アンカー：`{{anchor-id}}`を参照しています。
- `help/_includes/*.md`からの共有インクルードファイル：`{{$include /help/_includes/filename.md}}`を参照しています。

## コメント

```markdown
<!-- standard comment code -->
```

- `<!--> bad comment syntax <-->` （欠落しているダッシュ）は使用しないでください。テキストを非表示にするのではなく、目に見える形でレンダリングされます。
- レンダリングされたドキュメントにはコメントは表示されませんが、**GitHub**&#x200B;で生の.mdを表示している人には表示されます。秘密や機密情報はありません。
- 箇条書きリスト内のコメントは避けます（リストのレンダリングが壊れる可能性があります）。 `TOC.md`では、ファイルの最後の行のみをコメントアウトし、リストの中央には絶対にコメントしません。

## ブランクラインの回避策

ソース内の余分な空白行は、レンダラーによって折りたたまれます。 垂直方向のスペースを強制的に表示するには、ギャップを必要とする独自の行に`<br>&nbsp;`を配置します。

## エスケープ文字

- バックスラッシュで使用可能な文字：`` # { } [ ] * + - . ! `` – 例：`\# not a heading`。
- 角括弧（`<placeholder>`）の場合、バックスラッシュは機能しません。インラインコードブロック（`` `<placeholder>` ``）またはHTML エンティティ（`&lt;placeholder&gt;`）を使用してください。
- コードブロック内のHTML エンティティは&#x200B;**not**&#x200B;文字に変換されました – `&gt;`はリテラルテキストをそこに残します。
- メタデータ （YAML frontmatter）には、独自のエスケープルールがあります。値が`:`や`[`などの特殊文字で始まる場合は、値全体を引用符で囲みます：`title: "Processing rules: A new beginning"`。

## 制限付きHTMLの許可リストに加える

markdownの任意の場所では、これらのHTML タグのみが許可されます。それ以外は検証エラーです。

```
table  tbody  td  tfoot  thead  th  tr  col  colgroup
p  ul  ol  li  br
b  i  strong  u  s  em  sub  sup  span
caption  a  img  div
pre  code  codeblock
```

Markdownで実行できる場合は、HTMLよりもMarkdown構文を優先します。HTMLは、ヘッドレステーブルのようなエッジケースにのみ使用されます。

## 明示的にサポートされていません（ローカルプレビューでレンダリングされる場合でも使用しないでください）

- 水平方向のルール （`***`, `<hr>`）
- 絵文字ショートコード （`:bowtie:`）
- タスクリスト （`- [x] done`）
- ブロック引用&#x200B;*コンポーネント*&#x200B;は、メモ/タブ/ビデオのショートコードを超えています（プレーン `>` ブロック引用は、スタイル設定されたコンポーネントではなく、引用符としてレンダリングされます）
- Markdown definition-list構文（代わりに手動の太字+ダッシュ形式を使用：`**Frog** - An amphibious green creature.`）
- 画像の`valign`

## ファイルサイズ/数の制限を把握する価値がある

| Thing | 制限 |
|---|---|
| 画像/ダウンロードのファイルサイズ | 5 MBでの検証警告、20 MBでのエラー、ハード GitHub キャップ 100 MB |
| 記事ごとの画像 | 100 （EDS レンダリング制限） |
| 記事ごとのメタデータバッジ | 2 （デフォルト） |
