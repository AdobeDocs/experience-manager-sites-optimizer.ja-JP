---
title: Web サイト権限の機会ドキュメント
description: Web サイト権限の機会と、これを使用して web サイトのセキュリティを強化する方法について説明します。
badgeSecurityPosture: label="セキュリティ態勢" type="Caution" url="../../opportunity-types/security-posture.md" tooltip="セキュリティ態勢"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 99%

---


# Web サイト権限の機会

![Web サイト権限の機会](./assets/website-permissions/hero.png){align="center"}

Web サイト権限の機会では、安全で管理しやすい AEM 環境を維持するために重要な web サイト権限を最適化します。この機会では、`/` や `/content` のような汎用パス上の `jcr:all` などの過度に広範な権限を削除し、ユーザーアクセスを最小権限の原則に合わせることで、アクセス制御を絞り込むことができます。権限を効率化し、冗長性を排除することで、セキュリティリスクを軽減し、保守性を向上させ、今後の設定ミスを防ぐことができます。AEM セキュリティ権限コンソールまたはコードリポジトリで権限を確認して更新し、サービスユーザーが本当に必要なアクセス権のみを持つようにします。

## 自動特定

![Web サイト権限の自動特定](./assets/website-permissions/auto-identify.png){align="center"}

**Web サイト権限の機会**&#x200B;機能は、自動的に特定して一覧表示します。

* **ユーザー** - 疑わしい権限を持つユーザーアカウント。
* **パス** - 権限の影響を受ける AEM 内のパス。
* **権限** - 疑わしい権限。
* **問題** - 権限に影響を与える問題のタイプを示します。

## 自動提案

![Web サイトの脆弱性の自動提案](./assets/website-permissions/auto-suggest.png){align="center"}

自動提案では、「**提案された権限**」フィールドに AI 生成のレコメンデーションが提供され、フラグが付けられた権限を安全な代替権限に置き換えることができます。

## 自動最適化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![Web サイト権限の自動最適化](./assets/website-permissions/auto-optimize.png){align="center"}

Sites Optimizer Ultimate には、見つかった脆弱性に対して自動最適化をデプロイする機能が追加されています。

>[!BEGINTABS]

>[!TAB 最適化のデプロイ]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 承認のリクエスト]

{{auto-optimize-request-approval}}

>[!ENDTABS]
