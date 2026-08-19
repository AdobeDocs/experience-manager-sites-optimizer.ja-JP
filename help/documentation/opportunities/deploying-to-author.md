---
title: オーサードキュメントへのデプロイ
description: AEM Sites Optimizerが選択した最適化をオーサリング環境にデプロイする方法と、その後の最適化方法について説明します。
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 1d55c607aab6c820d014b9a57bfae20b8170c672
workflow-type: tm+mt
source-wordcount: 245
ht-degree: 6%

---

# 作成者ドキュメントへのデプロイ

<!--![Deploying to author](./assets/deploying-to-author/hero.png){align="center"}-->

AEM Sites Optimizerがオポチュニティを特定し、最適化を提案したら、選択した最適化をレビューしてデプロイし、さらにアクションを実行できます。

## オーサーにデプロイ

商談リストから1つ以上の提案を選択し、**作成者にデプロイ**&#x200B;をクリックして選択内容をデプロイするか、**作成者にすべてをデプロイ**&#x200B;して、利用可能なすべての提案を一度にデプロイします。 AEM Sites Optimizerでは、選択した最適化はオーサリング環境にのみ適用されます。ライブサイトには変更は公開されません。 その後、AEMの作成者は、各商談の[自動最適化](/help/documentation/opportunities/missing-alt-text.md#auto-optimize) ワークフローに従って、Content Management System （CMS）から変更内容を確認して公開できます。

このアクションは、デプロイの権限がない場合、またはサイトがデプロイ用に完全に設定されていない場合（コードリポジトリがまだ接続されていない場合など）は無効になります。 いずれの場合も、Sites Optimizerは、無効なボタンの横に理由を説明します。

## デプロイされた最適化の追跡

<!--![Deployed tab](./assets/deploying-to-author/deployed-tab.png){align="center"}-->

選択した最適化をデプロイしたら、それらの最適化を管理し、商談の詳細ページの「**デプロイ済み**」タブから、**現在** タブおよび&#x200B;**無視** タブと並べて、次の手順を実行できます。

具体的なデプロイメントの仕組み（Edge Delivery Services、AEM as a Cloud Service、Digital Asset Managementのアップデートの適用方法など）は、オポチュニティの種類によって異なります。 詳しくは、商談の独自の&#x200B;**自動最適化** セクションを参照してください。

## 関連トピック

* [欠落している代替テキストの機会](/help/documentation/opportunities/missing-alt-text.md#auto-optimize)
* [コア web バイタルの機会](/help/documentation/opportunities/core-web-vitals.md#auto-optimize)
* [破損したバックリンクの機会](/help/documentation/opportunities/broken-backlinks.md#auto-optimize)
