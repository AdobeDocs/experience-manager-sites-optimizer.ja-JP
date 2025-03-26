---
title: Web サイトの脆弱性の機会に関するドキュメント
description: Web サイトの脆弱性の機会と、それを使用して Web サイト上ののセキュリティを強化する方法について説明します。
badgeSecurityPosture: label="セキュリティ態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="セキュリティ態勢"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# Web サイトの脆弱性の機会

![Web サイトの脆弱性の機会 ](./assets/website-vulnerabilities/hero.png){align="center"}

Web サイトの脆弱性の機会は、アプリケーションコードで使用されるサードパーティライブラリのセキュリティの脆弱性を特定します。 これらの脆弱性は、悪意のある攻撃者によって悪用される可能性があり、Web サイトのリスクを高め、セキュリティ態勢を低下させる可能性があります。

Web サイトの脆弱性オポチュニティでは、ページの上部に次のような概要が表示されます。

* **見つかった問題** – 検出された脆弱性の数。セキュリティリスクによって分類（低、中、高）。
* **集計されたセキュリティリスク** – 機会によって見つかった脆弱性に基づく、Web サイトの全体的なセキュリティリスク。

## 自動識別

![Web サイトの脆弱性の自動識別 ](./assets/website-vulnerabilities/auto-identify.png){align="center"}

**Web サイト脆弱性オポチュニティ** 機能は、アプリケーションコードで使用されるサードパーティライブラリで見つかった脆弱性を自動的に特定し、リストします。 次の詳細が提供されます。

* **ライブラリ** – 脆弱性を含むサードパーティライブラリ。 1 つのライブラリに複数の脆弱性が存在する場合があります。
* **現在のバージョン** – 現在使用中のライブラリのバージョン。
* **推奨バージョン** – 脆弱性を解決する推奨バージョン。
* **スコア** – 脆弱性の重症度評価。ページ上部にもまとめられています。
* **脆弱性** – 脆弱性の識別子、簡単な説明、および詳細については、全国脆弱性データベース（NVD）へのリンク。 識別子または説明の横にあるリンクをクリックして、NVD リンクにアクセスします。

## 自動候補

![Web サイトの脆弱性の自動候補 ](./assets/website-vulnerabilities/auto-suggest.png){align="center"}

自動提案は、アップグレードが必要な脆弱なライブラリの **推奨バージョン** に対して、AI によって生成された提案を提供します。 各エントリには、全体的な重大度を示す **スコア** が付くので、最も重要な脆弱性の優先順位を付けることができます。

>[!BEGINTABS]

>[!TAB  脆弱性の詳細 ]

各脆弱性には、[National Vulnerability Database （NVD） ](https://nvd.nist.gov/) の詳細情報へのリンクが含まれています。 脆弱性の ID または説明の右側にあるリンク項目をクリックすると、その脆弱性の NVD ページに移動します。

>[!TAB  エントリを無視 ]

脆弱性リストのエントリを無視するように選択できます。 **無視アイコン** を選択すると、リストからエントリが削除されます。 無視されたエントリは、商談ページ上部の **無視** タブから再エンゲージできます。<!---right now it does not seem to be implemented, but the page description mentions this functionality-->

>[!ENDTABS]


## 自動最適化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Web サイトの脆弱性の自動最適化 ](./assets/website-vulnerabilities/auto-optimize.png){align="center"}

Sites Optimizer Ultimateには、検出された脆弱性を自動最適化デプロイする機能が追加されています。

>[!BEGINTABS]

>[!TAB  最適化のデプロイ ]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 承認のリクエスト]

{{auto-optimize-request-approval}}

>[!ENDTABS]