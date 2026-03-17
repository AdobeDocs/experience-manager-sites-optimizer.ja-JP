---
solution: Experience Manager
product: adobe experience manager
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
type: Documentation
description: AEM Sites Optimizerのドキュメント。
index: true
git-repo: https://github.com/AdobeDocs/experience-manager-sites-optimizer.ja-JP
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 4cf02d5c9d44ed00bb3b284330b2d553d54ba8d3
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---


# 内部使用のメタデータ

GitHub オーサリングシステムは、次に示す増加する前例に従って、メタデータを階層的に整理します。

1. metadata.md
1. から C
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。 メタデータの上書きは、できるだけ低いレベルで行う必要があります。

最低限必要なのは、`experience-manager-cloud-service.en` リポジトリ内のメタデータです。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`
* `contentOwner` （`/help/assets` 下のコアアセットコンテンツのみ）

