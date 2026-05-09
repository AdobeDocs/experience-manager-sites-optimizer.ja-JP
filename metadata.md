---
solution: Experience Manager
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
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
source-git-commit: ffd43deb5e5e763bd9a0f2cec87ae0ebd8cbe6c3
workflow-type: tm+mt
source-wordcount: 85
ht-degree: 2%

---


# 内部使用のためのメタデータ

GitHub オーサリングシステムは、メタデータを階層的に整理し、以下の前例を使用します。

1. metadata.md
1. ToC
1. 記事

metadata.md ファイルで定義されたメタデータは、リポジトリ全体に適用されますが、ToC レベルとアーティクルレベルで上書きできます。 メタデータの上書きは、可能な限り低いレベルで行う必要があります。

`experience-manager-cloud-service.en` リポジトリ内のメタデータは、必要最小限です。

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
* `contentOwner` （`/help/assets`以下のコアアセットコンテンツに対してのみ）

