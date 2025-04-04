---
title: コア web バイタルの機会ドキュメント
description: コア web バイタルの機会と、これを使用してトラフィックの獲得を向上させる方法について説明します。
badgeSiteHealth: label="サイトの健全性" type="Caution" url="../../opportunity-types/site-health.md" tooltip="サイトの健全性"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 99%

---


# コア web バイタルの機会

![コア web バイタルの機会](./assets/core-web-vitals/hero.png){align="center"}

コア web バイタルの機会は、web ページのユーザーエクスペリエンスとオーガニック検索のパフォーマンスを低下させる場合のある問題を特定します。これらの問題は、カスタムフォント、最適化されていない JavaScript 依存関係、サードパーティスクリプトなど、様々な要因から発生します。コア web バイタルの機会は、これらの障害のある要素を指摘し、web ページのパフォーマンスを向上させる修正を提案します。1000 ページビュー数以上があるページのみを分析できます。

まず、コア web バイタルの機会では、ページの上部に、問題の概要と、サイトやビジネスに与える影響を含む概要が表示されます。

* **見込みトラフィック損失** - パフォーマンスしきい値を下回るコア web バイタルによる推定トラフィック損失。
* **見込みトラフィック値** - 損失したトラフィックの推定値。

## 自動特定

![コア web バイタルの自動特定](./assets/core-web-vitals/auto-identify.png){align="center"}

ページの下部には、現在のすべての問題が次のようにグループ化されて一覧表示されます。

* **モバイルの問題** - ページのモバイルバージョンに影響を与える問題のリスト。
* **デスクトップの問題** - ページのデスクトップバージョンに影響を与える問題のリスト。

各問題はテーブルに表示され、影響を受けるページエントリが&#x200B;**ページ**&#x200B;列で特定されます。

さらに、これらの問題は、コア web バイタルレポートの標準パフォーマンス指標（最大コンテンツペイント **LCP**、次のペイントへのインタラクション **INP**、累積レイアウトシフト **CLS**）別にもグループ化されます。

## 自動提案

![コア web バイタルの機会の自動提案](./assets/core-web-vitals/auto-suggest.png){align="center"}

コア web バイタルの機会は、AI 生成の修正提案を提供します。提案ボタンをクリックすると、パフォーマンス指標 **LCP**、**INP**、**CLS** がカテゴリとして含まれる新しいウィンドウが表示されます。これらのカテゴリを切り替えると、特定の問題のリストを表示できます。

各カテゴリには複数の問題が含まれている場合があるので、問題とレコメンデーションの完全なリストを表示するには、下にスクロールします。また、各指標にはモバイルとデスクトップの両方に 2 つのパフォーマンスゲージがあります。

## 自動最適化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![コア web バイタルの機会の自動最適化](./assets/core-web-vitals/auto-optimize.png){align="center"}

Sites Optimizer Ultimate には、コア web バイタルの機会によって検出された問題に対して自動最適化をデプロイする機能が追加されています。<!--- TBD-need more in-depth and opportunity specific information here. What does the auto-optimization do?-->

>[!BEGINTABS]

>[!TAB 最適化のデプロイ]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 承認のリクエスト]

{{auto-optimize-request-approval}}

>[!ENDTABS]

