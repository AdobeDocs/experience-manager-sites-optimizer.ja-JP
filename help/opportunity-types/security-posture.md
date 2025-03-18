---
title: Sites Optimizerでセキュリティの態勢を最適化
description: Sites Optimizerを使用してサイトのセキュリティを向上させる方法を説明します。
source-git-commit: ab2d75b1d986d83e3303e29a25d2babd1598394a
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 13%

---


# セキュリティ対策の機会

![ セキュリティ態勢の好機 ](./assets/security-posture/hero.png){align="center"}

AEM Sites Optimizerで強力なセキュリティ体制を維持することは、デジタルエクスペリエンスとユーザーデータを保護するために重要です。 チームは、CORS 構成、クロスサイトスクリプティング、Web サイトの権限、Web サイトの脆弱性など、改善の機会を特定することにより、潜在的なセキュリティリスクにプロアクティブに対処し、ベストプラクティスに従ってコンプライアンスを確保することができます。 セキュリティ対策の強化は、機密情報を保護するだけでなく、ユーザーの信頼とサイトの信頼性を高めます。 AEM Sites Optimizerのインサイトを活用すると、組織はセキュリティスタンスを継続的に監視および改善し、リスクを軽減し、安全なデジタル環境を維持するのに役立ちます。

## 機会


<!-- CARDS

* ../documentation/opportunities/cors-configuration.md
  {title=CORS configuration}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/cross-site-scripting.md
  {title=Cross-site scripting}
  {image=../assets/common/card-gear.png}
* ../documentation/opportunities/website-permissions.md  
  {title=Website permissions}
  {image=../assets/common/card-people.png}
* ../documentation/opportunities//website-vulnerabilities.md
  {title=Website vulnerabilities}
  {image=../assets/common/card-puzzle.png}

-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="CORS configuration">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/cors-configuration.md" title="CORS 設定" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="CORS 設定"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/cors-configuration.md" target="_blank" rel="referrer" title="CORS 設定">CORS 設定</a>
                    </p>
                    <p class="is-size-6">CORS 設定の機会について、およびサイトのセキュリティの脆弱性を特定して修正する方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities/cors-configuration.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Cross-site scripting">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/cross-site-scripting.md" title="クロスサイトスクリプティング" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-gear.png" alt="クロスサイトスクリプティング"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/cross-site-scripting.md" target="_blank" rel="referrer" title="クロスサイトスクリプティング"> クロスサイトスクリプティング </a>
                    </p>
                    <p class="is-size-6">クロスサイトスクリプティングの機会について説明し、サイトセキュリティの脆弱性を特定して修正します。</p>
                </div>
                <a href="../documentation/opportunities/cross-site-scripting.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Website permissions">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/website-permissions.md" title="Web サイト権限" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-people.png" alt="Web サイト権限"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/website-permissions.md" target="_blank" rel="referrer" title="Web サイト権限">Web サイトの権限 </a>
                    </p>
                    <p class="is-size-6">Web サイトの権限の機会と、それを使用して Web サイト上ののセキュリティを強化する方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities/website-permissions.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Website vulnerabilities">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities//website-vulnerabilities.md" title="Web サイトの脆弱性" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-puzzle.png" alt="Web サイトの脆弱性"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities//website-vulnerabilities.md" target="_blank" rel="referrer" title="Web サイトの脆弱性">Web サイトの脆弱性 </a>
                    </p>
                    <p class="is-size-6">Web サイトの脆弱性の機会と、それを使用して Web サイト上ののセキュリティを強化する方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities//website-vulnerabilities.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


