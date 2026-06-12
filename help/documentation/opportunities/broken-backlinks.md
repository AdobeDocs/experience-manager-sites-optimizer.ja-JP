---
title: 破損したバックリンクの機会ドキュメント
description: 破損したバックリンクの機会と、これを使用してトラフィックの獲得を向上させる方法について説明します。
badgeTrafficAcquisition: label="トラフィックの獲得" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="トラフィックの獲得"
TQID: https://experienceleague.adobe.com/HTgcPKBO-r-NRgdUdqS6ZOklYRaLM8pQbr3KbaYD4nQ
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 84a1ae98d67bc02ab272131194511efbeccab492
workflow-type: tm+mt
source-wordcount: 655
ht-degree: 100%

---

# 破損したバックリンクの機会

<!--![Broken backlinks opportunity](./assets/broken-backlinks/hero.png){align="center"}-->

>[!VIDEO](https://video.tv.adobe.com/v/3483250/?learn=on&enablevpops)

破損したバックリンクの機会は、サイト上の存在しない（404）ページを指している外部リンクを特定します。 これらのリンクは、検索エンジンがバックリンクに依存して関連性と信頼性を評価するので、リファラルトラフィックの損失と SEO 価値の低下につながります。 これらの問題は、URL が変更された場合、コンテンツが削除された場合、適切なリダイレクトがないままページが利用できなくなった場合に発生します。 AEM Sites Optimizer は、すべての破損したバックリンクを特定し、特定のAI レコメンデーションを提供し、ワンクリックで修正できるデプロイメントを単一の一元的なビューで実現します。

## 自動特定

<!--![Auto-identify broken backlinks](./assets/broken-backlinks/auto-identify.png){align="center"}-->

AEM Sites Optimizer は、外部データソースを継続的にスキャンし、サイト上の存在しない 404 ページを指しているバックリンクを検出します。 データは、Google Search Console、[運用上のテレメトリ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service)、サードパーティの SEO プラットフォームなど、複数のソースから集計されます。 自動特定の機会は、破損した URL にリンクしている外部ドメインを特定し、ドメイン権限、予想されるトラフィック、リンクエクイティの損失などの影響に基づいて優先順位を付けます。

この機会では、次の詳細を含む、特定されたすべての問題を一覧表示します。

* **参照ドメインとページ** - 破損したリンクが含まれている外部ページまたはドメイン。
* **優先度** - 高、中、低。破損したリンクが SEO プロセスに与える影響を示します。
* **破損したターゲット URL** - リンク先のサイト上の存在しない URL。

## 自動提案

<!--![Auto-suggest broken backlinks](./assets/broken-backlinks/auto-suggest.png){align="center"}-->

AEM Sites Optimizer は、それぞれの特定された破損したバックリンクに対して、トラフィックと SEO の価値を復元するための最適な宛先を推奨します。 次を分析して、バックリンクのインテントを判断します。

* URL 構造とトークン
* アンカーテキスト
* 参照ページのタイトルとコンテキスト

このインテントは、既存のサイトコンテンツと照合され、最も関連性の高い宛先ページを特定します。 それぞれの破損した URL は、正確な代替ページまたは最も近い関連ページにマッピングされます。 適切な宛先を決定できない場合、手動レビューの問題が明らかになります。

>[!BEGINTABS]

>[!TAB AI の論理的根拠]

<!--![AI rationale on autosuggestion of broken backlinks](./assets/broken-backlinks/auto-suggest-ai-rationale.png){align="center"}-->

提案された URL の AI の論理的根拠を表示するには、**情報** アイコンを選択します。 論理的根拠では、提案された URL が破損したリンクに最適であると AI が判断する理由を説明します。 AI の意思決定プロセスを理解し、提案を受け入れるか却下するかについて情報に基づく決定を下すのに役立ちます。

>[!TAB ターゲット URL の編集]

<!--![Edit suggested URL of broken backlinks](./assets/broken-backlinks/edit-target-url.png){align="center"}-->

AI 生成の提案に同意できない場合は、**編集アイコン** を選択して、提案された URL を編集できます。 編集により、破損したリンクに最も適している URL を手動で入力できます。 また、Sites Optimizer は、破損したリンクに適しているサイト上の他の URL も一覧表示します。

>[!TAB エントリを無視]

<!--![Ignore broken backlinks](./assets/broken-backlinks/ignore.png){align="center"}-->

ターゲットとなる破損した URL を含むエントリを無視することを選択できます。 ![削除アイコンまたは無視アイコン](https://spectrum.adobe.com/static/icons/ui_18/CrossSize500.svg) を選択すると、機会リストから破損したバックリンクが削除されます。 無視された破損したバックリンクは、機会ページの上部にある「**無視**」タブから再度関与できます。

>[!ENDTABS]

## 自動最適化

<!--[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}-->

提案をレビューして承認したら、「**最適化をデプロイ**」をクリックできます。 その後、AEM Sites Optimizer は、実装内でのリダイレクトの管理方法に基づいて、修正をオーサリング環境に適用します。 その後、AEM オーサーは、コンテンツ管理システム（CMS）から変更を公開できます。

設定に応じて、修正は既存のデプロイメントワークフロー内のコンテンツまたはコードの変更として適用されます。 最適化プロセスには、次の手順が含まれます。

* **検証** - 変更が期待どおりに機能し、デプロイメント前に回帰が発生しないことを確認します。
* **デプロイメント** - AEM でのコンテンツの更新や CI/CD パイプライン経由のコードのデプロイメントなど、既存のプロセスを通じて変更を適用します。
* **権限チェック** - ユーザーが変更をデプロイするための適切な権限を持っていることを検証します。 権限がない場合は、ダウンロード可能なリダイレクトリストやコードパッチなどの代替出力が提供されます。

このプロセスにより、リダイレクトが正確に実装され、リリース前に検証され、既存の設定やガバナンスプロセスと一致することが確保されます。
