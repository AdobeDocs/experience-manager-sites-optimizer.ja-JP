---
title: Web サイト権限の商談ドキュメント
description: Web サイトの権限の機会と、それを使用して Web サイト上ののセキュリティを強化する方法について説明します。
badgeSecurityPosture: label="セキュリティ態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="セキュリティ態勢"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 2%

---


# Web サイト権限のオポチュニティ

![Web サイト権限のオポチュニティ ](./assets/website-permissions/hero.png){align="center"}

Web サイトの権限のオポチュニティは、安全で管理しやすいAEM環境を維持するために重要な、web サイトの権限を最適化します。 この機会を利用すると、過度に広範な権限（`/` や `/content` などの汎用パスに対する `jcr:all` など）を削除し、最小権限の原則に合わせてユーザーアクセスを調整することで、アクセス制御を絞り込むことができます。 権限を効率化し重複を排除することで、セキュリティリスクを軽減し、メンテナンス性を向上させ、将来的な設定ミスを防ぐことができます。 AEMのセキュリティ権限コンソールまたはコードリポジトリで権限を確認および更新して、アクションを実行し、サービスユーザーが本当に必要なアクセス権のみを持つようにします。

## 自動識別

![Web サイトの権限の自動識別 ](./assets/website-permissions/auto-identify.png){align="center"}

**Web サイト権限のオポチュニティ** 機能は、自動的に識別およびリスト表示します

* **ユーザー** – 疑わしい権限を持つユーザーアカウント。
* **Path** – 権限の影響を受けるAEM内のパス。
* **権限** – 疑わしい権限。
* **問題** – 権限に影響を与える問題のタイプを示します。

## 自動候補

![Web サイトの脆弱性の自動候補 ](./assets/website-permissions/auto-suggest.png){align="center"}

自動提案では、「**推奨権限**」フィールドに AI によって生成されたレコメンデーションが提供され、フラグが設定された権限を安全な代替値に置き換えることができます。

## 自動最適化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Web サイトの権限の自動最適化 ](./assets/website-permissions/auto-optimize.png){align="center"}

Sites Optimizer Ultimateには、検出された脆弱性を自動最適化デプロイする機能が追加されています。

>[!BEGINTABS]

>[!TAB  最適化のデプロイ ]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 承認のリクエスト]

{{auto-optimize-request-approval}}

>[!ENDTABS]
