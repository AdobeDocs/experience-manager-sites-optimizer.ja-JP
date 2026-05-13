---
title: コア web バイタルの機会ドキュメント
description: コア web バイタルの機会と、これを使用してトラフィックの獲得を向上させる方法について説明します。
badgeSiteHealth: label="サイトの健全性" type="Caution" url="../../opportunity-types/site-health.md" tooltip="サイトの健全性"
TQID: https://experienceleague.adobe.com/3h-Xas767zUk-Sod7JEr9Lh767r5S3LKpbwJZFZU2kg
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 84a1ae98d67bc02ab272131194511efbeccab492
workflow-type: ht
source-wordcount: 533
ht-degree: 100%

---

# コア web バイタルの機会

<!--![core web vitals opportunity](./assets/core-web-vitals/hero.png){align="center"}-->

>[!VIDEO](https://video.tv.adobe.com/v/3483372/?captions=jpn&learn=on&enablevpops)

Core Web Vitals の機会は、web サイト上でパフォーマンスが低く、ユーザーエクスペリエンスとオーガニック検索のパフォーマンスに影響を与えているページを特定します。 これらの問題は、カスタムフォント、最適化されていない JavaScript の依存関係、サードパーティのスクリプトなどの要因から発生する場合があります。 Core Web Vitals は、コンテンツの読み込み速度、ページレイアウトの安定性、ユーザーインタラクションに対するページの応答性を測定します。

AEM Sites Optimizer は、これらの問題の影響を受けるページを検出し、コードレベルで特定の AI レコメンデーションを提供し、既存の開発ワークフローを通じて修正を適用します。 1000 ページビュー数以上があるページのみを分析できます。

## 自動特定

<!--![Auto-identify core web vitals](./assets/core-web-vitals/auto-identify.png){align="center"}-->

AEM Sites Optimizer は、[運用上のテレメトリ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service)を使用してサイトのパフォーマンスを継続的に監視し、最大コンテンツの描画（LCP）、累積レイアウトシフト（CLS）、次の描画までのインタラクション（INP）などのコア web バイタル指標の回帰を検出します。 実際のユーザーデータを使用して、パフォーマンスの回帰を特定し、ユーザーエクスペリエンスへの影響に基づいて問題の優先順位を付けます。

AEM Sites Optimizer には、現在のすべての問題のリストが、モバイルとデスクトップで詳細に表示されます。 **ページ**&#x200B;列は影響を受けるページエントリを示し、問題は LCP、INP、CLS 別に分類されます。

## 自動提案

<!--![Auto-suggest core web vitals opportunity](./assets/core-web-vitals/auto-suggest.png){align="center"}-->

AEM Sites Optimizer は、特定された各問題に対して、コア web バイタルのパフォーマンスを向上させるための規範的なコードレベルのレコメンデーションを生成します。 コードリポジトリにアクセスすることで、基になる実装を評価します。 これにより、コンポーネント、スクリプト、スタイルの実装方法を分析し、パフォーマンス上の問題の根本原因を特定できます。 この分析に基づいて、システムはターゲットとなるレコメンデーションを提供し、パフォーマンスを向上させるために必要な変更を指定するコードパッチを生成します。 各レコメンデーションは、適用前にレビューできます。

提案ボタンをクリックすると、パフォーマンス指標 LCP、INP、CLS がカテゴリとして含まれる新しいウィンドウが表示されます。 これらのカテゴリを切り替えると、特定の問題のリストを表示できます。 各カテゴリには複数の問題が含まれている場合があるので、問題とレコメンデーションの完全なリストを表示するには、下にスクロールします。 また、各指標にはモバイルとデスクトップの両方に 2 つのパフォーマンスゲージがあります。

## 自動最適化

<!--[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}-->

レコメンデーションをレビューして承認したら、「**最適化をデプロイ**」をクリックできます。 AEM Sites Optimizer は、特定された問題に基づいてコードパッチを生成し、バージョン管理プロセスを通じて使用できるようにします。 最適化プロセスには、次の手順が含まれます。

* **問題の作成** - 各修正に対して、明確な説明と影響を受ける URL を含む、ラベル付きの GitHub 問題を作成します。
* **プルリクエストの配信** - 正確なコード修正を含むリンクされたプルリクエストを自動的に開き、レビュー、テスト、結合の準備を整えます。
* **ステータスのトラッキング** - 各修正の完了までを追跡し、フォローアップのために部分的な試行または失敗した試行にフラグを付けます。

これらの更新を使用できるようにする前に、AEM Sites Optimizer は検証を実行し、修正で基になる問題に対処し、回帰が発生しないことを確認します。 すべての更新は、標準的な開発手法に従っており、本番環境に結合される前にレビューと承認が必要です。

これにより、パフォーマンスの最適化が正確で検証済みであり、既存の開発およびガバナンスプロセスに統合されることが確保されます。
