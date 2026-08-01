---
title: AEM Sites Optimizer プリフライト
description: 公開前にページを評価するために実行されるプリフライトと監査について説明します。
TQID: https://experienceleague.adobe.com/pZrPXBAaroTlpEsfSluFiLW2Noy4y5sD4dZHTsXgSfA
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cc72dcf1-72e1-48cc-b434-e7c27d62d67c
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: 300
ht-degree: 28%

---

# AEM Sites Optimizer プリフライト

![&#x200B; プリフライトの準備状況ダッシュボード &#x200B;](./assets/overview/hero.png){align="center"}

>[!NOTE]
>
>[AEM 2026.7.0 （リリース 27083） &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/release-notes/maintenance/2026/2026-7-0#release-27083)以降、プリフライトはAEM Sites ページエディターツールバーに組み込まれています。 詳しくは、[&#x200B; プリフライト設定](./setup.md)を参照してください。

AEM Sites Optimizerのプリフライト機能は、コンテンツや構造を分析し、実用的なレコメンデーションを提示することで、公開前にページを検証および最適化するのに役立ちます。 手戻りを減らしながらページの品質、パフォーマンス、公開の準備を整えたいと考えている作成者、マーケター、開発者向けに設計されています。

オーサリング環境からプリフライトを開始し、**ページを分析**&#x200B;を選択して監査を実行します。 監査では、メタデータや見出し構造など、ページの1つの側面を評価し、関連する監査を&#x200B;**SEO**&#x200B;や&#x200B;**アクセシビリティ**&#x200B;などのカテゴリにグループ化します。 次に、Preflightは、ページの準備状況スコアと機会（改善可能な具体的なもの）を報告し、実用的な推奨事項を提示します。

## プリフライトの基本を学ぶ

プリフライトの開始は簡単です。 Preflightを設定し、オーサリング環境で開き、ページの監査を実行し、残りはPreflightが行います。

1. [プリフライトの設定](./setup.md) - AEM インスタンスにプリフライトを設定する方法について説明します
1. [プリフライトへのアクセス](./access-preflight.md) - オーサリング環境でプリフライトが表示される場所について説明します
1. [監査の実行](./audits.md) - プリフライト監査を開始する方法について説明します
1. [監査結果と機会](./audit-results.md) - 監査結果を解釈する方法について説明します

## 監査カテゴリのプリフライト

<!--
CARDS

* ./opportunities/accessibility.md
* ./opportunities/seo.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Preflight Accessibility Audits">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/accessibility.md" title="アクセシビリティ監査のプリフライト" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="opportunities/assets/accessibility/hero.png" alt="アクセシビリティ監査のプリフライト"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/accessibility.md" target="_blank" rel="referrer" title="アクセシビリティ監査のプリフライト"> プリフライトアクセシビリティ監査</a>
                    </p>
                    <p class="is-size-6">Sites Optimizerのプリフライトアクセシビリティ監査について説明します。</p>
                </div>
                <a href="./opportunities/accessibility.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Preflight SEO Audits">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/seo.md" title="SEO監査のプリフライト" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="opportunities/assets/seo/hero.png" alt="SEO監査のプリフライト"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/seo.md" target="_blank" rel="referrer" title="SEO監査のプリフライト">SEO監査のプリフライト </a>
                    </p>
                    <p class="is-size-6">Sites Optimizerのプリフライト SEO監査について説明します。</p>
                </div>
                <a href="./opportunities/seo.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
