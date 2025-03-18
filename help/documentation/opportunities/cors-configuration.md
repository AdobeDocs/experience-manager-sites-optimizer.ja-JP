---
title: CORS 設定商談ドキュメント
description: CORS 設定の機会について、およびサイトのセキュリティの脆弱性を特定して修正する方法について説明します。
badgeSecurityPosture: label="セキュリティ態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="セキュリティ態勢"
source-git-commit: ab2d75b1d986d83e3303e29a25d2babd1598394a
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---


# CORS 設定機会

![CORS 設定のオポチュニティ ](./assets/cors-configuration/hero.png){align="center"}

Web アプリケーションを不正なデータアクセスから保護するには、クロスオリジンリソース共有（CORS）を適切に設定することが不可欠です。 `Access-Control-Allow-Origin` ヘッダーを `*` に設定すると、任意のドメインが応答を要求および受信でき、機密情報が攻撃者に公開される可能性があります。 これは、信頼できるドメインの制御された許可リストを実装するか、必要のない場合は CORS を無効にすることで、セキュリティを強化する機会となります。 安全な CORS 設定を確保することで、許可されたユーザーに対するシームレスなアクセスを維持しながら、プライベートコンテンツを保護できます。

## 自動識別

![CORS 設定のオポチュニティの自動識別 ](./assets/cors-configuration/auto-identify.png){align="center"}

自動識別は、web サイトをスキャンして CORS の設定ミスを調べ、不正アクセスの可能性がある URL を検出します。 これらの URL は、次の詳細と共に一番上の表に一覧表示されます。

* **ページプレフィックス** - CORS の設定ミスに対して脆弱な URL パスプレフィックス。
* **ページ例** – 不正アクセスの影響を受けやすい URL の例。

## 自動候補

![CORS 設定のオポチュニティを自動提案 ](./assets/cors-configuration/auto-suggest.png){align="center"}

自動候補は、レビューの対象となる **アプリケーションコードファイル** およびその **行** を提供します。これにより、CORS ポリシーの設定が緩くなる可能性があります。


## [!BADGE Ultimate] を自動最適化{type=Positive tooltip="Ultimate"}



>[!BEGINTABS]

>[!TAB  最適化のデプロイ ]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 承認のリクエスト]

{{auto-optimize-request-approval}}

>[!ENDTABS]
