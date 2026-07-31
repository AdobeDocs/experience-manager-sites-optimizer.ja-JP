---
title: プリフライト設定
description: AEM Sites Optimizerにプリフライトを設定する方法を説明します。
TQID: https://experienceleague.adobe.com/GfLmEEBoSP2481ZZUjRyyfMjExGgI0l9yMAqTF8ObcY
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
source-git-commit: 14f10c231373992c49a8bb93c043556305b6280d
workflow-type: tm+mt
source-wordcount: 785
ht-degree: 52%

---

# プリフライト設定

プリフライトを実行するには、オーサリング環境で設定する必要があります。 ユニバーサルエディター、ドキュメントベースのオーサリング、AEM Sites ページエディター、Adobe Managed Services用にプリフライトを設定することで、ページが公開される前にプリフライト監査を実行できます。

## ユーザーアクセスの有効化

プリフライトを使用するには、[Adobe Admin Console](https://adminconsole.adobe.com)で次のAEM Sites Optimizer製品プロファイルの少なくとも1つにユーザーが割り当てられていることを確認します。

* AEM Sites Optimizer - ユーザーの自動提案
* AEM Sites Optimizer - ユーザーの自動最適化

## プリフライトを有効にする

>[!BEGINTABS]

>[!TAB ユニバーサルエディター]

ユニバーサルエディターでプリフライトを設定するには、次の手順に従います。

1. 次の場所で **Extension Manager** を開きます。
   [https://experience.adobe.com/#/@org/aem/extension-manager/universal-editor](https://experience.adobe.com/ja_JP/#/@org/aem/extension-manager/universal-editor)
1. **AEM Sites Optimizer プリフライト**&#x200B;拡張機能を見つけます。
1. 組織のシステム管理者は、この拡張機能を有効にする必要があります。
1. 拡張機能を有効にした後で、**ユニバーサルエディター**&#x200B;でページを開きます。例：
   `https://author-p12345-e123456.adobeaemcloud.com/ui#/@org/aem/universal-editor/canvas/author-p12345-e123456.adobeaemcloud.com/content/en/example/home.html`
1. **プリフライト拡張機能**&#x200B;が&#x200B;**サイドパネル**&#x200B;に表示されます。
1. サイドレールから&#x200B;**プリフライト拡張機能**&#x200B;を選択し、現在のページのプリフライトを開きます。

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
1. **Sidekick**&#x200B;で、**プリフライト** ボタンをクリックして、現在のページのプリフライトを開きます。

>[!TAB AEM Sites ページエディター]

オーサー環境で[AEM 2026.7.0 （リリース 27083） &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/release-notes/maintenance/2026/2026-7-0#release-27083)以降を実行している場合、プリフライトはAEM Sites ページエディターに組み込まれており、ブックマークレットは必要ありません。 次の手順に従います。

1. **AEM Sites ページエディター**&#x200B;で、監査するページを開きます。
1. エディターツールバーで、**プリフライト** アイコン（下に強調表示された再生ボタン）を選択して、現在のページのプリフライトパネルを開きます。

   ![AEM Sites ページエディターのツールバーのプリフライトアイコン &#x200B;](./assets/setup/toolbar-preflight-button.png){align="center"}

>[!NOTE]
>
>ツールバーに&#x200B;**プリフライト** アイコンが表示されませんか？ 次の項目を確認します。
>
>* **サポートされているリリース** – 統合ボタンには、AEM 2026.7.0 （リリース 27083）以降が必要です。 以前のリリースでは、以下のbookmarklet メソッドを使用します。
>* **ロールアウト** – 統合ボタンは段階的に組織に対して有効になっているので、サポートされているリリースであっても、組織にまだ到達していない可能性があります。 それまでは、以下のブックマークレット方式を使用するか、Adobeまたは管理者に連絡してください。
>* **ページアクセス** — ボタンは、ページへの編集アクセス権がある場合にのみ表示されます。
>* **ユーザーアクセス** — ユーザーに&#x200B;**AEM Sites Optimizer - Auto-Suggest User**&#x200B;または&#x200B;**AEM Sites Optimizer - Auto-Optimize User** プロファイルが割り当てられていることを確認します。 [&#x200B; ユーザーアクセスの有効化](#enable-user-access)を参照してください。

以前のAEM リリースのAEM Sites ページエディターでプリフライトを使用するには、web ブラウザーでブックマークレットを作成します。 次の手順に従います。

1. Web ブラウザーに&#x200B;**ブックマークバー**&#x200B;を表示します。

   * **Ctrl + Shift + B** キー（Windows）または **Cmd + Shift + B** キー（Mac）を押します。

1. ブラウザーに新しいブックマークを作成します。

   * ブックマークバーを右クリックし、「**新規ページ**」または「**ブックマークを追加**」を選択します。
   * 「**アドレス（URL）**」フィールドに次のコードを貼り付けます。

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=aem-cloud-service';document.head.appendChild(script);})();
   ```

1. ブックマークに「**プリフライト**」という名前（または任意の名前）を付けます。
1. **AEM Sites ページエディター**&#x200B;で、監査するページのプレビュー URL（`*.aem.page`）を開きます。
1. ブックマークバーの&#x200B;**プリフライト** ブックマークをクリックして、現在のページのプリフライトを開きます。

>[!TAB Adobe Managed Services]

>[!IMPORTANT]
>
>AEM オーサーでの認証にアドビの ID プロバイダー（IMS）を使用する Adobe Managed Services（AMS）環境のみがサポートされます。 組織が AMS 認証に他の ID プロバイダーを使用している場合、プリフライトは機能しません。

AMS環境のAEM Sites ページエディターでプリフライトを使用するには、次の手順に従ってweb ブラウザーでブックマークレットを作成します。

1. Web ブラウザーに&#x200B;**ブックマークバー**&#x200B;を表示します。

   * **Ctrl + Shift + B** キー（Windows）または **Cmd + Shift + B** キー（Mac）を押します。

1. ブラウザーに新しいブックマークを作成します。

   * ブックマークバーを右クリックし、「**新規ページ**」または「**ブックマークを追加**」を選択します。
   * 「**アドレス（URL）**」フィールドに次のコードを貼り付けます。

   ```javascript
   javascript:(function(){const script=document.createElement('script');script.src='https://experience.adobe.com/solutions/OneAdobe-aem-sites-optimizer-preflight-mfe/static-assets/resources/sidekick/client.js?source=bookmarklet&target-source=ams';document.head.appendChild(script);})();
   ```

1. ブックマークに「**プリフライト**」という名前（または任意の名前）を付けます。
1. **AEM Sites ページエディター**&#x200B;で、監査するページを開きます。
1. ブックマークバーの&#x200B;**プリフライト** ブックマークをクリックして、現在のページのプリフライトを開きます。

>[!ENDTABS]

## ベストプラクティス

プリフライト監査を実行する際は、次のガイドラインに留意してください。

* 実稼動環境に公開する前に、必ず&#x200B;**ステージングページまたはプレビューページ**&#x200B;で監査を実行します。
* リンクの破損、H1 タグの欠落、安全でないリンクなど&#x200B;**影響の大きい問題**&#x200B;の解決を優先します。
* 監査を実行する前に、保護されたステージング環境で&#x200B;**認証が有効になっている**&#x200B;ことを確認してください。
* SEO パフォーマンスを向上させるには、**メタタグのレコメンデーション**&#x200B;を確認して適用します。
