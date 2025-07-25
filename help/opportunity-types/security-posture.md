---
title: Sites Optimizer を使用したセキュリティ態勢の最適化
description: Sites Optimizer を使用してサイトのセキュリティ態勢を向上させる方法について説明します。
source-git-commit: cb64a34b758de8f5dcea298014ddd0ba79a24c17
workflow-type: ht
source-wordcount: '212'
ht-degree: 100%

---


# セキュリティ態勢の機会

![セキュリティ態勢の機会](./assets/security-posture/hero.png){align="center"}

AEM Sites Optimizer で強力なセキュリティ態勢を維持することは、デジタルエクスペリエンスとユーザーデータを保護する上で重要です。CORS 設定、クロスサイトスクリプティング、web サイト権限、web サイトの脆弱性などの改善の機会を特定することで、チームは潜在的なセキュリティリスクに積極的に対処し、ベストプラクティスへの準拠を確保できます。セキュリティ対策を強化すると、機密情報が保護されるだけでなく、ユーザーの信頼とサイトの信頼性も向上します。AEM Sites Optimizer のインサイトを使用することで、組織はセキュリティ態勢を継続的に監視および改善し、リスクを軽減して安全なデジタル環境を維持できます。

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
                    <p class="is-size-6">CORS 設定の機会と、サイトのセキュリティの脆弱性を特定して修正する方法について説明します。</p>
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
                        <a href="../documentation/opportunities/cross-site-scripting.md" target="_blank" rel="referrer" title="クロスサイトスクリプティング">クロスサイトスクリプティング</a>
                    </p>
                    <p class="is-size-6">クロスサイトスクリプティングの機会と、サイトのセキュリティの脆弱性を特定して修正する方法について説明します。</p>
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
                        <a href="../documentation/opportunities/website-permissions.md" target="_blank" rel="referrer" title="Web サイト権限">Web サイト権限</a>
                    </p>
                    <p class="is-size-6">Web サイト権限の機会と、これを使用して web サイトのセキュリティを強化する方法について説明します。</p>
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
                        <a href="../documentation/opportunities//website-vulnerabilities.md" target="_blank" rel="referrer" title="Web サイトの脆弱性">Web サイトの脆弱性</a>
                    </p>
                    <p class="is-size-6">Web サイトの脆弱性の機会と、これを使用して web サイトのセキュリティを強化する方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities//website-vulnerabilities.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


