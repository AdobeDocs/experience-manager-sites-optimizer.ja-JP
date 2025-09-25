---
title: プリフライト設定
description: AEM Sites Optimizer用に Preflight 拡張機能をセットアップする方法を説明します。
source-git-commit: 6e177ef6b9d121ac7484ae118037c7e542f981d8
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 2%

---


# プリフライト設定

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
