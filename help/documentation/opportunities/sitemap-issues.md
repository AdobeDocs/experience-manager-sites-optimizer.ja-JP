---
title: サイトマップの問題の商談ドキュメント
description: サイトマップの問題の機会と、それを使用してトラフィック獲得を改善する方法について説明します。
badgeTrafficAcquisition: label="トラフィックの獲得" type="Caution" url="../../opportunity-types/traffic-acquisition.md" tooltip="トラフィックの獲得"
source-git-commit: c99bd0ab418c1eb0693f39ea16ee41f8a1263099
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---


# サイトマップの問題のオポチュニティ

![ サイトマップに関する問題のオポチュニティ ](./assets/sitemap-issues/hero.png){align="center"}

完全で正確なサイトマップは、検索エンジンが web サイトページを効率的にクロールしてインデックスを作成するのに役立ち、検索結果の可視性を高めることができます。 サイトマップのオポチュニティは、サイトマップに関する潜在的な問題を特定します。 これらの問題を修正すると、サイト上での検索エンジンのインデックス作成とコンテンツの検出性が大幅に向上します。

問題の概要と、その問題がサイトやビジネスに与える影響を含む概要がページ上部に表示されます。

* **予想トラフィック損失** - サイトマップの問題に起因する推定トラフィック損失。
* **予測トラフィック値** – 失われたトラフィックの予測値。

## 自動識別

サイトマップの問題は、次の条件を使用してフィルタリングできます。

* **問題のあるサイトマップ** – 潜在的な問題を含む分析済みのサイトマップ URL。
* **イシュータイプ** - サイトマップで識別されるイシューのタイプ。
   * **クライアントエラー** - `200 Success` 応答を返さないエントリ。
   * **リダイレクト** – 障害が発生したリダイレクトや設定が正しくないリダイレクト。

>[!BEGINTABS]

>[!TAB  クライアントエラー ]

![ サイトマップのクライアントエラーの自動識別 ](./assets/sitemap-issues/auto-identify-client-errors.png){align="center"}

サイトマップ内の URL がこれらを返す場合、検索エンジンは、サイトマップが古いか、ページが誤って削除されたと見なす場合があります。 クライアントは、クライアント（ブラウザーまたはクローラー）からのリクエストが無効であることを示します。 一般的なプロパティを次に示します。

* **404 Not Found** - リクエストされたページが存在しません。
* **403 Forbidden** - サーバーはリクエストされたページへのアクセスを拒否します。
* **410 Gone** - ページは意図的に削除されており、戻りません。
* **401 Unauthorized** – 認証が必要ですが、提供されていません。

これらのエラーは、特に重要なページが **404 または 410** を返す場合、検索エンジンがインデックスを解除する可能性があるので、SEO に悪影響を与える可能性があります。

各イシューはテーブルに表示され、影響を受けるサイトマップエントリを識別する **ページ** 列が示されます。

* **ページ** – 問題が発生したサイトマップエントリの URL。

>[!TAB  リダイレクト ]

![ サイトマップのクライアントエラーの自動識別 ](./assets/sitemap-issues/auto-identify-redirects.png){align="center"}

サイトマップには、最終的な宛先 URL のみを含め、リダイレクトする URL は含めないでください。 リダイレクトは、ユーザーやクローラーを正しい場所に誘導することを目的としていますが、設定を誤ると問題が発生する可能性があります。

* **302 が見つかりました（一時的なリダイレクト）** - **301** の代わりに誤って使用すると、SEO の問題が発生する可能性があります。
* **307 一時的なリダイレクト** - 302 に似ていますが、HTTP メソッドを保持します。
* **リダイレクトループ** - ページが自分自身にリダイレクトするか、無限ループを作成した場合。
* **リダイレクトの破損** - リダイレクトによって存在しないページまたは 4xx ページが表示される場合。

各イシューはテーブルに表示され、影響を受けるサイトマップエントリを識別する **ページ** 列が示されます。

* **ページ** – 問題が発生したサイトマップエントリの URL。

>[!ENDTABS]

## 自動候補

サイトマップの各イシュー [ フィルター条件を満たす ](#auto-identify) が、次の列を含むテーブルに一覧表示されます。

* **ページ** – 問題が発生したサイトマップエントリの URL。
* **提案** – 問題に対して推奨される修正。

候補には通常、サイトマップエントリを修正するための更新されたサイトパスが含まれています。 場合によっては、正しいリダイレクトターゲットの指定など、より詳細な手順が提供される場合もあります。

## 自動最適化

[!BADGE Ultimate]{type=Positive tooltip="Ultimate"}

![ サイトマップの問題を自動最適化 ](./assets/sitemap-issues/auto-optimize.png){align="center"}

Sites Optimizer Ultimateには、サイトマップの自動最適化をデプロイする機能が追加されています。

>[!BEGINTABS]

>[!TAB  最適化のデプロイ ]

{{auto-optimize-deploy-optimization-slack}}

>[!TAB 承認のリクエスト]

{{auto-optimize-request-approval}}

>[!ENDTABS]
