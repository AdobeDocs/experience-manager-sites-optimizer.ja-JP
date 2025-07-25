---
title: クロスサイトスクリプティングの機会ドキュメント
description: クロスサイトスクリプティングの機会と、サイトのセキュリティの脆弱性を特定して修正する方法について説明します。
badgeSecurityPosture: label="セキュリティ態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="セキュリティ態勢"
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: ht
source-wordcount: '132'
ht-degree: 100%

---


# クロスサイトスクリプティングの機会

![クロスサイトの機会](./assets/cross-site-scripting/hero.png){align="center"}

クロスサイトスクリプティングの機会は、サイトのコードの脆弱性を特定します。次に、攻撃者が悪用して、他のユーザーが閲覧する web ページに悪意のあるスクリプトを挿入する可能性がある問題を修正します。これらのスクリプトは、セッション Cookie などの機密情報を盗んだり、ユーザーのパスワードの変更などのアクションをユーザーに代わって実行したりする場合があります。

## 自動特定

![クロスサイトの機会の自動特定](./assets/cross-site-scripting/auto-identify.png){align="center"}

* **脆弱なコード** - クロスサイトスクリプティング攻撃に対して脆弱なコード。
* **再現するためのリンク** - 脆弱性が発見されたページへのリンク。

## 自動提案

![クロスサイトの機会の自動提案](./assets/cross-site-scripting/auto-suggest.png){align="center"}

* **提案された修正** - 脆弱性を修正する方法に関する AI 生成の提案。

## 自動最適化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

>[!BEGINTABS]

>[!TAB 最適化のデプロイ]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 承認のリクエスト]

{{auto-optimize-request-approval}}

>[!ENDTABS]
