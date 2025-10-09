---
title: プリフライト設定
description: AEM Sites Optimizer のプリフライト拡張機能を設定する方法について説明します。
source-git-commit: 6e177ef6b9d121ac7484ae118037c7e542f981d8
workflow-type: ht
source-wordcount: '424'
ht-degree: 100%

---


# プリフライト設定

AEM Sites Optimizer のプリフライトの機会を特定するには、ユニバーサルエディター、ドキュメントベースのプレビュー、または AEM Cloud Service のいずれかでプリフライト拡張機能を設定する必要があります。これにより、ページを公開する前にプリフライト監査を実行できます。

## ユーザーアクセスの有効化

プリフライト拡張機能を使用するには、[Adobe Admin Console](https://adminconsole.adobe.com) でユーザーが次の AEM Sites Optimizer 製品プロファイルの少なくとも 1 つに割り当てられていることを確認します。

* AEM Sites Optimizer - ユーザーの自動提案
* AEM Sites Optimizer - ユーザーの自動最適化

## プリフライト拡張機能の有効化

>[!BEGINTABS]

>[!TAB ユニバーサルエディター]

ユニバーサルエディターでプリフライトを設定するには、次の手順に従います。

1. 次の場所で **Extension Manager** を開きます。
   [https://experience.adobe.com/ja_JP/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/ja_JP/#/@org/aem/extension-manager/universal-editor)
1. **AEM Sites Optimizer プリフライト拡張機能**&#x200B;を見つけて、有効にするリクエストを送信します。
1. **Adobe AEM チーム**&#x200B;が組織の拡張機能を確認し、有効にします。
1. 拡張機能を有効にした後で、**ユニバーサルエディター**でページを開きます。例：
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. **プリフライト拡張機能**&#x200B;が&#x200B;**サイドパネル**&#x200B;に表示されます。
1. 現在のページの&#x200B;**プリフライト監査**&#x200B;を開始するには、サイドパネルから&#x200B;**プリフライト拡張機能**&#x200B;を選択します。

>[!TAB ドキュメントベースのオーサリング]

ドキュメントベースのオーサリング用にプリフライトを設定するには、次の手順に従います。

1. 次の設定を Edge Delivery Services プロジェクトの GitHub リポジトリの `/tools/sidekick/config.json` に追加します。

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

1. 以下の内容で、`/tools/sidekick/aem-sites-optimizer-preflight.js` という新しいファイルを作成します。

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

1. プレビュー URL 用のプリフライトスクリプトを読み込むには、`/scripts/scripts.js` の `loadLazy()` 関数を更新します。

   ```javascript
   if (window.location.href.includes('.aem.page')) {
      import('../tools/sidekick/aem-sites-optimizer-preflight.js');
   }
   ```

1. 監査するページのプレビュー URL（`*.aem.page`）を開きます。
1. **Sidekick** で「**プリフライト**」ボタンをクリックして、現在のページの監査を開始します。

>[!TAB AEM Sites ページエディター]

AEM Sites ページエディターでプリフライトを使用するには、web ブラウザーでブックマークレットを作成します。次の手順に従います。

1. Web ブラウザーに&#x200B;**ブックマークバー**&#x200B;を表示します。

   * **Ctrl + Shift + B** キー（Windows）または **Cmd + Shift + B** キー（Mac）を押します。

!. ブラウザーに新しいブックマークを作成します。

* ブックマークバーを右クリックし、「**新規ページ**」または「**ブックマークを追加**」を選択します。
* 「**アドレス（URL）**」フィールドに次のコードを貼り付けます。

```javascript
javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
```

1. ブックマークに「**プリフライト**」という名前（または任意の名前）を付けます。
1. **AEM Sites ページエディター**&#x200B;で、監査するページのプレビュー URL（`*.aem.page`）を開きます。
1. ブックマークバーの&#x200B;**プリフライト**&#x200B;ブックマークをクリックして、現在のページの監査を開始します。

>[!ENDTABS]

## ベストプラクティス

プリフライト監査を実行する際は、次のガイドラインに留意してください。

* 実稼動環境に公開する前に、必ず&#x200B;**ステージングページまたはプレビューページ**&#x200B;で監査を実行します。
* リンクの破損、H1 タグの欠落、安全でないリンクなど&#x200B;**影響の大きい問題**&#x200B;の解決を優先します。
* 監査を実行する前に、保護されたステージング環境で&#x200B;**認証が有効になっている**&#x200B;ことを確認してください。
* SEO パフォーマンスを向上させるには、**メタタグのレコメンデーション**&#x200B;を確認して適用します。
