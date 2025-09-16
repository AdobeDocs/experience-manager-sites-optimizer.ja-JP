---
title: AEM Sites Optimizerによるプリフライトの最適化
description: AEM Sites Optimizerによるプリフライトの機会について説明します。
source-git-commit: 214a9d7d4c7e498a8c2f39009e93c4c1f8f772b1
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 23%

---


# プリフライトの機会

![プリフライトの機会](./assets/preflight/hero.png){align="center"}

AEM Sites Optimizerのプリフライトの機会は、運用開始前に、web ページがパフォーマンス、SEO、ユーザーエクスペリエンスに最適化されていることを確認するのに役立ちます。 リンクの破損、メタタグの欠落、アクセシビリティの問題などの潜在的な問題を特定することで、プリフライトチェックを使用して、コンテンツ作成者やマーケターが公開プロセスの早い段階でこれらの問題に対処できます。 このプロアクティブなアプローチにより、最適でないコンテンツを公開するリスクを最小限に抑え、サイト品質を向上させ、全体的なデジタルプレゼンスを向上させます。 プリフライトの機会を利用すると、ワークフローがスムーズになり、公開後の修正が減り、検索エンジンのランキングとユーザー満足度が向上します。

## 機会

<!-- CARDS

* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=Canonical}
  {image=../assets/common/card-link.png}
* ../documentation/opportunities/broken-internal-links.md
  {title=Broken Internal Links}
  {image=../assets/common/card-link.png}
* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=Metatags}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/invalid-or-missing-metadata.md
  {title=H1 count}
  {image=../assets/common/card-code.png}
* ../documentation/opportunities/accessibility-issues.md
  {title=Accessibility}
  {image=../assets/common/card-puzzle.png}

-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Canonical">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="正規" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-link.png" alt="正規"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="正規">正規</a>
                    </p>
                    <p class="is-size-6">正規化の機会と、これを使用して SEO を向上させ、重複コンテンツの問題を防ぐ方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Broken Internal Links">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/broken-internal-links.md" title="壊れた内部リンク" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-link.png" alt="壊れた内部リンク"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/broken-internal-links.md" target="_blank" rel="referrer" title="壊れた内部リンク">壊れた内部リンク</a>
                    </p>
                    <p class="is-size-6">壊れた内部リンクを使用する機会と、これを使用して web サイト上の壊れたリンクや問題のあるリンクを特定および修正する方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities/broken-internal-links.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Metatags">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="メタタグ" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="メタタグ"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="メタタグ">メタタグ</a>
                    </p>
                    <p class="is-size-6">メタタグの機会と、これを使用してページのメタデータを最適化し、SEO パフォーマンスを向上させる方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="H1 count">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/invalid-or-missing-metadata.md" title="H1 カウント" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-code.png" alt="H1 カウント"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" title="H1 カウント">H1 カウント</a>
                    </p>
                    <p class="is-size-6">H1 カウントの機会と、これを使用して適切な見出し構造と SEO 最適化を確保する方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities/invalid-or-missing-metadata.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Accessibility">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../documentation/opportunities/accessibility-issues.md" title="アクセシビリティ" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-puzzle.png" alt="アクセシビリティ"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../documentation/opportunities/accessibility-issues.md" target="_blank" rel="referrer" title="アクセシビリティ">アクセシビリティ</a>
                    </p>
                    <p class="is-size-6">アクセシビリティの機会と、これを使用してすべてのユーザーが web サイトにアクセスできるようにする方法について説明します。</p>
                </div>
                <a href="../documentation/opportunities/accessibility-issues.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>

</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## 設定

AEM Sites Optimizerのプリフライトのオポチュニティを特定するには、ページが公開される前にプリフライト監査を実行するために、ユニバーサルエディター、ドキュメントベースのプレビュー、AEM Cloud Service のいずれかでプリフライト拡張機能を設定する必要があります。

## ユーザーアクセスを有効にする

Preflight 拡張機能を使用するには、[Adobe Admin Console](https://adminconsole.adobe.com) でユーザーが次のAEM Sites Optimizer製品プロファイルの少なくとも 1 つに割り当てられていることを確認します。

* AEM Sites Optimizer - ユーザーの自動候補
* AEM Sites Optimizer - ユーザーを自動最適化

## Preflight 拡張機能の有効化

>[!BEGINTABS]

>[!TAB ユニバーサルエディター]

ユニバーサルエディターでプリフライトを設定するには、次の手順に従います。

1. 次の場所で **Extension Manager** を開きます。
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor)
1. **AEM Sites Optimizer Preflight 拡張機能を見つけて** 有効にするリクエストを送信します。
1. **Adobe AEM チーム** が拡張機能を確認し、組織に対して有効にします。
1. 拡張機能を有効にした後で、**ユニバーサルエディター** でページを開きます。例：
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. **Preflight 拡張機能** が **サイドパネル** に表示されます。
1. サイドパネルから **プリフライト拡張** を選択して、現在のページの **プリフライト監査** を開始します。

>[!TAB ドキュメントベースのオーサリング]

ドキュメントベースのオーサリング用にプリフライトを設定するには、次の手順に従います。

1. 次の設定をEdge Delivery Services プロジェクトの GitHub リポジトリの `/tools/sidekick/config.json` に追加します。

   ```json
   {
     "plugins": [
       {
         "id": "preflight",
         "titleI18n": {
           "en": "Preflight"
         },
         "environments": ["preview"],
         "event": "preflight"
       }
     ]
   }
   ```

1. `/tools/sidekick/aem-sites-optimizer-preflight.js` に新しいファイルを作成し、次の内容を追加します。

   ```javascript
   (function () {
     let isAEMSitesOptimizerPreflightAppLoaded = false;
     function loadAEMSitesOptimizerPreflightApp() {
       const script = document.createElement('script');
       script.src = 'https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=plugin';
       script.onload = function () {
         isAEMSitesOptimizerPreflightAppLoaded = true;
       };
       script.onerror = function () {
         console.error('Error loading AEMSitesOptimizerPreflightApp.');
       };
       document.head.appendChild(script);
     }
   
     function handlePluginButtonClick() {
       if (!isAEMSitesOptimizerPreflightAppLoaded) {
         loadAEMSitesOptimizerPreflightApp();
       }
     }
   
     // Sidekick V1 extension support
     const sidekick = document.querySelector('helix-sidekick');
     if (sidekick) {
       sidekick.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('helix-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   
     // Sidekick V2 extension support
     const sidekickV2 = document.querySelector('aem-sidekick');
     if (sidekickV2) {
       sidekickV2.addEventListener('custom:preflight', handlePluginButtonClick);
     } else {
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('aem-sidekick')
           .addEventListener('custom:preflight', handlePluginButtonClick);
       }, { once: true });
     }
   }());
   ```

1. プレビュー URL 用の Preflight スクリプトを読み込む `loadLazy()` は、`/scripts/scripts.js` 関数を更新します。

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. 監査するページのプレビュー URL （`*.aem.page`）を開きます。
1. **Sidekick** で「**Preflight**」ボタンをクリックして、現在のページの監査を開始します。

>[!TAB AEM Sitesページエディター ]

AEM Sitesページエディターで Preflight を使用するには、web ブラウザーでブックマークレットを作成します。 次の手順に従います。

1. Web ブラウザーに **ブックマークバー** を表示します。

   * **Ctrl + Shift + B** （Windows）または **Cmd + Shift + B** （Mac）を押します。

!. ブラウザーに新しいブックマークを作成します。

* ブックマークバーを右クリックし、**新規ページ** または **ブックマークを追加** を選択します。
* **アドレス（URL）** フィールドに、次のコードをペーストします。

```javascript
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

1. ブックマークに **Preflight** という名前（または任意の名前）を付けます。
1. `*.aem.page`AEM Sites ページエディター **で、監査するページのプレビュー URL （**）を開きます。
1. ブックマークバーの **Preflight** ブックマークをクリックして、現在のページの監査を開始します。

>[!ENDTABS]

## ベストプラクティス

プリフライト監査を実行する場合は、次のガイドラインに留意してください。

* 実稼動環境に公開する前に、必ず **ステージングページまたはプレビューページ** で監査を実行します。
* リンクの破損、H1 タグの欠落、安全でないリンクなど **影響の大きい問題** の解決を優先順位付けします。
* 監査を実行する前に、保護されたステージング環境で **認証が有効** になっていることを確認してください。
* SEO のパフォーマンスを向上させるために、**メタタグのレコメンデーション** を確認して適用します。
