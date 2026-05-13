---
title: クロスサイトスクリプティングの機会ドキュメント
description: クロスサイトスクリプティングの機会と、サイトのセキュリティの脆弱性を特定して修正する方法について説明します。
badgeSecurityPosture: label="セキュリティ態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="セキュリティ態勢"
TQID: https://experienceleague.adobe.com/8ZpnC3XTmcz1uPeyJM0UqR97PfvekI3QHGf6xDT5Tcc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 252f5292d6dc62711b4ebeb8ce5a2707857fd674
workflow-type: ht
source-wordcount: 144
ht-degree: 100%

---

# クロスサイトスクリプティングの機会

![クロスサイトの機会](./assets/cross-site-scripting/hero.png){align="center"}

クロスサイトスクリプティングの機会は、サイトのコードの脆弱性を特定します。 次に、攻撃者が悪用して、他のユーザーが閲覧する web ページに悪意のあるスクリプトを挿入する可能性がある問題を修正します。 これらのスクリプトは、セッション Cookie などの機密情報を盗んだり、ユーザーのパスワードの変更などのアクションをユーザーに代わって実行したりする場合があります。

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
