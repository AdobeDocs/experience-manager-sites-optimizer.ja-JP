---
title: コードパッチドキュメントの準備
description: AEM Sites OptimizerがCore Web Vitalsの修正プログラム用のコードパッチを準備する方法と、その後のパッチの追跡方法について説明します。
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: a86d83ee226055e6401b13fd421b40d449b96fa8
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 2%

---

# コードパッチドキュメントの準備

<!--![Preparing code patches](./assets/preparing-code-patches/hero.png){align="center"}-->

[Core Web Vitals商談](/help/documentation/opportunities/core-web-vitals.md)に対して、AEM Sites Optimizerは、特定されたパフォーマンスの問題に対するコードレベルの修正を生成します。 これらの修正は、直接デプロイするのではなく、コードパッチとして確認して準備します。

## コードパッチの準備

Core Web Vitals リストから1つ以上の問題を選択し、**コードパッチの準備**&#x200B;をクリックして選択を準備するか、**すべてのコードパッチを準備**&#x200B;して、利用可能なすべてのパッチを一度に準備します。 AEM Sites Optimizerでは、修正ごとにラベル付きのGitHub イシューが作成され、コードが変更されたリンクされたプルリクエストが自動的に開き、チームがレビュー、テスト、結合する準備が整います。

このアクションは、コードリポジトリを作成する権限がない場合や、サイトが完全に設定されていない場合（コードリポジトリが接続されていない場合や、パッチの生成中など）は無効になります。 それぞれの場合、Sites Optimizerは、無効なボタンの横にある理由を説明します。

## 準備されたコードパッチの追跡

コードパッチを準備したら、それらを管理し、Core Web Vitalsの詳細ページの「**デプロイ済み**」タブと、**現在** タブおよび&#x200B;**無視** タブから次の手順を実行できます。 パッチのステータスは、プルリクエストが生成されただけでなく、マージされたかどうかを反映します。問題は、修正が実際にコードベースにマージされた後にのみ&#x200B;**Deployed**&#x200B;に移動します。

## 関連トピック

* [コア web バイタルの機会](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [作成者ドキュメントへのデプロイ](/help/documentation/opportunities/deploying-to-author.md)
