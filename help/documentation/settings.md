---
title: Sites Optimizer の設定
description: Sites Optimizer を設定し、他のツールと統合する方法について説明します。
TQID: https://experienceleague.adobe.com/eznjSHZgAmCh-ek-XE-lLtuoGJxC0yY4UVrmPjc0KYo
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
source-git-commit: 37d90154e6868ee392bf1b779b2bf3697112b7ce
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 39%
---
# Sites Optimizer の設定

![Sites Optimizer の設定](./assets/settings/hero.png){align="center"}

Sites Optimizer の設定は、Sites Optimizer エクスペリエンスを設定する中心的なハブです。

## Google Search Console

![Google Search Console の Sites Optimizer 設定](./assets/settings/google-search-console.png){align="center"}

AEM Sites Optimizer の Google Search Console 設定コネクタを使用すると、検索ランキング、クリックスルー率、コア Web バイタルなどの主要な SEO 指標を分析できます。 Google Search Console を常時接続しておくことで、JSON 分析を活用して最適化の機会を明らかにし、サイトのパフォーマンスを向上させることができます。

このコネクタを設定するには、ドメインの Google Search Console への管理者アクセス権を持つ資格情報が必要です。

## AEM Sites に接続

次のガイドでは、既存の Edge Delivery Services（EDS）サイトを AEM Sites Optimizer に接続する方法について説明します。 開始する前に、EDS サイトが既に設定され、動作していることを確認してください。この接続は、AEM Sites Optimizer がコンテンツにアクセスする専用のものです。

接続には次の 2 つの手順が必要です。

1. コードリポジトリ URL とコンテンツソース URL を指定します。
2. AEM Sites Optimizer にコンテンツソースへのアクセス権を付与します。

### 手順 1：コードリポジトリとコンテンツソースのリンク

AEM Sites Optimizer で、**設定／AEM Sites に接続**&#x200B;に移動し、次を入力します。

- **コードリポジトリ URL** - EDS サイトの GitHub URL。例：
  `https://github.com/owner/repo`

- **コンテンツソース URL** - EDS サイトをバックアップする SharePoint フォルダーまたは Google Drive フォルダーの URL。例：
  `https://drive.google.com/drive/folders/...` か `https://myorg.sharepoint.com/...` のどちらかにする必要があります。

コンテンツソース URLを入力すると、AEM Sites Optimizer がコンテンツソースタイプを検出し、以下の関連するアクセス手順を表示します。

### 手順 2 - コンテンツソースへのアクセス権を付与

コンテンツソースに一致するセクションに従ってください。

#### SharePoint - Adobe ドメイン

![Adobe SharePoint ドメインに対してアクションが不要であることを示す AEM Sites に接続ダイアログ](./assets/settings/connect-content-and-drive.png){align="center"}

コンテンツソース URL で Adobe SharePoint ドメインを使用している場合、これ以上のアクションは必要ありません。 アクセス権は既に設定されています。 「**保存**」をクリックして、接続を完了します。

#### SharePoint - カスタムドメイン

コンテンツソース URL で組織独自の SharePoint ドメインを使用している場合、Azure アプリケーションを登録し、この資格情報を AEM Sites Optimizer に指定する必要があります。

##### 必要なもの

- Azure Portal にアプリケーションを登録する権限またはユーザーに代わってアプリケーションを登録できる連絡先。
- API 同意を付与するテナント管理者権限または API 同意を承認できる管理者。

##### 手順 2a - Azureでアプリケーションを登録

1. **Azure Portal／Microsoft Entra ID／アプリの登録／新規登録**&#x200B;に移動します。
2. 名前を付けます（例：`AEM Sites Optimizer`）。
3. その他のすべてをデフォルトのままにして、「**登録**」をクリックします。
4. **概要**&#x200B;ページで、次をメモします。
   - **アプリケーション（クライアント）ID**
   - **ディレクトリ（テナント）ID**

##### 手順 2b - API 権限を追加

1. **API のアクセス許可／アクセス許可の追加／Microsoft Graph／アプリケーションの許可**&#x200B;に移動します。
2. 次の両方を追加します。
   - `Sites.Selected` - 特定の SharePoint サイトコレクションへのスコープ付きアクセス権。
   - `Files.SelectedOperations.Selected` - ログインしていないユーザーによるファイルへのアクセス権。
3. 両方に「**管理者の同意を与えます**」をクリックします。

![Sites.Selected と Files.SelectedOperations.Selected が付与されていることを示す Azure API 権限](./assets/settings/app-permissions.png){align="center"}

>[!NOTE]
>
>管理者の同意を付与するには、テナント管理者権限が必要です。 これがない場合は、先に進む前に、IT 管理者または Azure 管理者にこの手順を完了するように依頼してください。

##### 手順 2c：クライアントシークレットの作成

![アプリ登録用の Azure 証明書と秘密鍵のページ](./assets/settings/create-credentials.png){align="center"}

1. **証明書とシークレット／新しいクライアントシークレット**&#x200B;に移動します。
2. 説明と有効期限を設定し、「**追加**」をクリックします。
3. 秘密鍵の値をすぐにコピーします。1 回のみ表示されます。

##### 手順 2d - SharePoint サイトへのアプリのアクセス権を付与

Microsoft Graph Explorer、PowerShell、Graph API の直接呼び出しを使用して、アプリへのアクセス権を付与できます。

[Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) に移動し、Microsoft アカウントでログインして、次のリクエストを実行します。

1. サイト ID を見つけます。

```
GET https://graph.microsoft.com/v1.0/sites/{tenant}.sharepoint.com:/sites/{site-name}
```

1. 応答から `id` をコピーし、サイトレベルのアクセス権を付与します。

```
POST https://graph.microsoft.com/v1.0/sites/{siteId}/permissions
```

本文：

```json
{
  "roles": ["write"],
  "grantedToIdentities": [{
    "application": {
      "id": "{your-client-id}",
      "displayName": "{Your app name}"
    }
  }]
}
```

##### 手順 2e - AEM Sites Optimizer に資格情報を入力

![SharePoint 資格情報フィールドを示す AEM Sites に接続ダイアログ](./assets/settings/add-sharepoint-credentials.png){align="center"}

**AEM Sites に接続**&#x200B;ダイアログに戻り、**SharePoint 経由のコンテンツリポジトリ接続**&#x200B;に次を入力します。

- **テナント ID（Azure AD）** - アプリ登録／概要。
- **クライアント ID（アプリ登録）** - アプリ登録／概要。
- **クライアント秘密鍵** - 手順 2c で作成済み。

「**接続を検証**」をクリックしてアクセス権を確認し、「**保存**」をクリックします。

#### Google Drive

![共有アクセス用の Google Drive サービスアカウントを示す AEM Sites に接続ダイアログ](./assets/settings/validate-eds-google.png){align="center"}

1. Google Drive で、EDS サイトをバックアップするフォルダーを右クリックし、「**共有**」を選択します。
2. 「**ユーザーやグループを追加**」フィールドに、**AEM Sites に接続** ダイアログに表示されるサービスアカウントのメールを入力します。
   `aem-sites-optimizer@adbe-gcp0843.iam.gserviceaccount.com`
3. 権限レベルを&#x200B;**編集者**&#x200B;に設定します。
4. 「**ユーザーに通知する**」をオフにし、「**共有**」をクリックします。

共有が完了したら、ダイアログで「**接続を検証**」をクリックし、「**保存**」をクリックします。

## ユーザー権限の管理

Sites Optimizer内のサイトにアクセスできるユーザーとそのサイトで何ができるかを制御します。 アクセスは、ユーザーごとに付与する、独立した&#x200B;*機能* （ユーザーの表示、編集、デプロイ、設定、管理）の小さなセットから構築されます。

アクセス権は&#x200B;**additive**&#x200B;です。ユーザーの権限は、付与されたすべての合計です。 「拒否」はないので、助成金は互いに競合したりキャンセルしたりすることはありません。 アクセス権を減らすには、付与を上書きしようとするのではなく、付与を削除します。

### アクセスを許可する方法

ユーザーがアクセスできる方法は2つあり、それらは一緒に動作します。

- **組織全体のアクセス** — [Adobe Admin Console](https://adminconsole.adobe.com/)でAdobe組織管理者によって割り当てられます。 組織内のあらゆるサイトに適用できます。 あらゆる場所で同じアクセス権を必要とするユーザーに使用します。
- **サイトレベルのアクセス** — Sites Optimizer内の&#x200B;**設定→権限** ページで割り当てられます。 この機能は、単一のサイトに適用され、必要に応じて幅を広げたり狭めたりすることができます。 Admin Consoleへのアクセスは必要ありません。

>[!NOTE]
>
>2つのレイヤーの合計。 組織全体の表示アクセス権を持ち、1つのサイトで編集も許可されているユーザーは、すべてのサイトを表示して、そのサイトを編集できます。 オーディエンスを単一のサイトに限定するには、それらのサイトが組織全体を網羅していないことを確認する必要があります。

#### 組織全体の役割（Admin Console）

組織全体のアクセス権は、[AEM Sites Optimizer](https://adminconsole.adobe.com/)で割り当てられた2つの&#x200B;**Adobe Admin Console**&#x200B;製品ロールのいずれかから取得されます。

- **ASO Manager** — **ユーザーの管理**&#x200B;を含む、すべてのサイトへの完全アクセス。 マネージャーは、任意のサイトの&#x200B;**権限** ページを開き、他のサイトにアクセス権を割り当てることができます。
- **ASO User** – すべてのサイトへの表示専用アクセス。 変更もユーザー管理もありません。

ロールを割り当てるには、組織の&#x200B;**システム管理者**&#x200B;またはAEM Sites Optimizerの&#x200B;**製品管理者**&#x200B;である必要があります。

1. [Adobe Admin Console](https://adminconsole.adobe.com/)にログインします。
1. **製品**&#x200B;に移動し、**AEM Sites Optimizer**&#x200B;を選択します。
1. 「**ユーザー**」タブを開き、電子メールでユーザーを追加するか、既存のユーザーを選択します。
1. 「**+** （追加）」アイコンをクリックして製品プロファイルを追加し、製品プロファイルを選択します。

   ![Adobe Admin Consoleでのユーザーの製品プロファイルの選択](./assets/settings/permissions-admin-console-product-profile.png){align="center"}

1. 「**次へ**」をクリックします。
1. 役割（**ASO Manager**）をフルアクセス用に、または&#x200B;**ASO User**&#x200B;を表示専用アクセス用に選択し、**適用**&#x200B;をクリックします。

   ![Adobe Admin ConsoleでのASO Manager ロールの選択](./assets/settings/permissions-admin-console-aso-manager-role.png){align="center"}

   ![Adobe Admin ConsoleでのASO ユーザーロールの選択](./assets/settings/permissions-admin-console-aso-user-role.png){align="center"}

ユーザーの追加について詳しくは、[&#x200B; ユーザーのオンボーディング &#x200B;](setup/onboard-users.md)を参照してください。

>[!IMPORTANT]
>
>組織全体の&#x200B;**ユーザーの管理**&#x200B;を許可できるのは、組織管理者のみです。 サイトに&#x200B;**ユーザーの管理**&#x200B;を持つメンバーは、そのサイトでアクセス権を割り当てることができますが、組織全体の&#x200B;**ASO マネージャー**&#x200B;を作成することはできません。

### 能力レベル

各機能は、1種類のアクションを制御します。 それらは独立しています。例えば、編集せずにデプロイを許可できます。

| 機能 | できること | 許可されていないもの |
|---|---|---|
| 表示 | 機会、提案、修正、レポート、設定など、サイトに関するデータを変更することなく確認できます。 | 変更点： |
| 編集 | 機会と提案を作成して変更する（何を変更すべきか）。 | 変更の公開、設定の変更、ユーザーの管理を行います。 |
| デプロイ | 修正をサイトに公開し、元に戻します。 | ユーザーの管理： |
| 設定 | サイトの設定と接続を変更します。 | 修正を公開したり、ユーザーを管理したりします。 |
| ユーザーの管理 | 他のメンバーのサイトへのアクセス権を付与または取り消します。 | まだアクセスできないサイトを管理する。 |

>[!NOTE]
>
>**ビューは常に含まれます。** すべての付与にはビューが自動的に含まれます。表示できないものを管理、設定、編集、またはデプロイすることはできません。 このため、ビューは単独では削除できません。 誰かのアクセス権を完全に削除するには、すべての機能のチェックを解除する代わりに、メンバーを削除します（以下の[&#x200B; メンバーの編集または削除](#edit-or-remove-a-member)を参照）。

### 機会タイプへの範囲アクセス

1つのサイトで、サイト全体ではなく、**特定の商談タイプ**&#x200B;に対して表示、編集、およびデプロイを付与できます（例：Core Web Vitalsまたは内部リンクの破損）。 これにより、1人のユーザーがCore Web Vitalsを編集しながら、他のすべてを表示できます。

- **表示**、**編集**、**デプロイ**&#x200B;は、1つ以上の商談タイプまたは&#x200B;**すべて**&#x200B;の商談タイプにスコープできます。
- **Configure**&#x200B;および&#x200B;**Manage users**&#x200B;は、常にサイト全体に適用されます。商談タイプに限定することはできません。

スコープ付きの各付与は、メンバーの独自の行として表示され、**適用先**&#x200B;列には、商談タイプ、**すべて**、または&#x200B;**サイト全体**&#x200B;が表示されます。

>[!CAUTION]
>
>スコープ設定では、付与する&#x200B;*個の*&#x200B;個の付与のみが制限されます。別の付与が提供するアクセスは削除されません。 ユーザーに組織全体のアクセス権または&#x200B;**すべて** タイプの付与がある場合、その広範なアクセス権は引き続き適用されます。 そのため、特定のオポチュニティ タイプに本当に限定するには、より大きな役割や&#x200B;**All** タイプの付与も保持していないことを確認してください。

### メンバーの追加

1. **設定→権限**&#x200B;に移動し、サイトを選択します。
1. 「**メンバーを追加**」をクリックします。
1. 名前または電子メールで検索し、1人以上の人物を選択します。
1. アクセスが適用される&#x200B;**商談タイプ** （または&#x200B;**すべて**）を選択し、付与する機能を選択します。
1. 「**追加**」をクリックします。

<!-- MEDIA PENDING: Site Manager / Site User walkthrough videos are being re-recorded with demo data to remove PII, then re-uploaded to video.tv.adobe.com and embedded here with >[!VIDEO]. The earlier uploads v/3503767 and v/3503768 (KT-22672 / KT-22673) contain PII and must not be used. -->

### メンバーの編集または削除

**メンバー** テーブルの場合：

- メンバーの行の&#x200B;**機能を編集**&#x200B;をクリックして、メンバーの機能を変更します。 既存の付与を編集しても、その機会タイプは固定されたままになります。機能のみを変更し、少なくとも1つの機能を選択したままにする必要があります。
- 「**削除**」をクリックして、そのメンバーのサイトへのアクセス権を完全に取り消します。

>[!NOTE]
>
>機能の変更とメンバーの削除は異なるアクションです。 すべてのアクセス権を削除するには、**削除**&#x200B;を使用します。権限は少なくとも1つの機能を保持する必要があるため、機能のチェックを外すことはできません（表示は常に維持されます）。

### 権限を管理できるユーザー

サイトの&#x200B;**権限** ページは、次のユーザーが利用できます。

- そのサイトの&#x200B;**ユーザーの管理**&#x200B;機能を持つメンバー、および
- 組織の管理者（ASO マネージャー）。

**ユーザーを管理**&#x200B;していないメンバーには、そのサイトへのアクセスを管理する権限がないというメッセージが表示されます。

### ユーザーとアクセスの管理を有効にする

ユーザーとアクセスの管理は、組織の設定によって制御されます。 アクセス権は有効になる前に割り当てることができますが、設定が有効になると&#x200B;**強制**&#x200B;になります。

まだ有効になっていない場合は、**権限** ページに、アカウントチームに連絡するように求めるバナーが表示されます。 Sites Optimizerのアカウントチームに連絡して有効にしましょう。

>[!NOTE]
>
>ユーザーとアクセスの管理がオンになるまで、割り当てた権限は保存されますが、適用されません。

### よくある質問

**サイトレベルのメンバーにはAdmin Console ロールが必要ですか？**

いいえ。 サイトレベルのアクセス権は、**権限** ページのSites Optimizer内で完全に付与されます。 Admin Consoleでは、組織全体の役割のみが割り当てられます。

**組織全体およびサイトレベルの両方のアクセス権を持っているユーザーの場合はどうなりますか？**

両方が適用されます。 効果的なアクセスは、この2つを組み合わせることです。 付与が競合することはありません。付与がアクセスを拒否することはできないからです。

**管理ユーザーを持つメンバーが組織全体のマネージャーを作成できないのはなぜですか？**

組織全体での役割の作成は、Admin Consoleのアクションです。 **ユーザーの管理**&#x200B;を持つメンバーは、自分のサイトでアクセス権を割り当てることができますが、組織全体の役割を付与できるのは組織管理者だけです。

**サイトへのユーザーのアクセス権を取り消すにはどうすればよいですか？**

**権限** ページで付与を削除します。 これは、常に少なくとも1つの機能を残す必要がある編集機能とは異なります。

**特定の商談タイプに限定できますか？**

はい – **All**&#x200B;ではなく、特定の商談タイプにスコープを設定した表示、編集、またはデプロイを付与します。 アクセスは追加的であるため、そのユーザーが組織全体のアクセス権または&#x200B;**すべて** タイプの付与を持っていない場合にのみ有効になります。
