---
title: Sites Optimizer の設定
description: Sites Optimizer を設定し、他のツールと統合する方法について説明します。
source-git-commit: b71d5510162864ee76931cf754164ea637cadd92
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 12%

---


# Sites Optimizer の設定

![Sites Optimizer の設定](./assets/settings/hero.png){align="center"}

Sites Optimizerの設定は、Sites Optimizer エクスペリエンスを構成するための中心的なハブです。

## Google Search Console

![Google Search ConsoleのSites Optimizer設定](./assets/settings/google-search-console.png){align="center"}

AEM Sites Optimizer の Google Search Console 設定コネクタを使用すると、検索ランキング、クリックスルー率、コア Web バイタルなどの主要な SEO 指標を分析できます。 Google Search Console を常時接続しておくことで、JSON 分析を活用して最適化の機会を明らかにし、サイトのパフォーマンスを向上させることができます。

このコネクタを設定するには、ドメインの Google Search Console への管理者アクセス権を持つ資格情報が必要です。

## AEM Sitesに接続

このガイドでは、既存のEdge Delivery Services（EDS）サイトをAEM Sites Optimizerに接続する方法について説明します。 始める前に、EDS サイトが既に設定されていて動作していることを確認してください。この接続は、AEM Sites Optimizerがコンテンツにアクセスするために特別に使用されます。

接続には2つの手順が必要です。

1. コードリポジトリ URLとコンテンツソース URLを指定します。
2. AEM Sites Optimizerにコンテンツソースへのアクセス権を付与します。

### ステップ 1 - コードリポジトリとコンテンツソースをリンクする

AEM Sites Optimizerで、**Settings → Connect to AEM Sites**&#x200B;に移動し、以下を入力します。

- **Code Repository URL** — EDS サイトのGitHub URL。例：
  `https://github.com/owner/repo`

- **Content Source URL** — EDS サイトをバックアップするSharePoint フォルダーまたはGoogle Drive フォルダーのURL。例：
  `https://drive.google.com/drive/folders/...` か `https://myorg.sharepoint.com/...` のどちらかにする必要があります。

Content SourceのURLを入力すると、AEM Sites Optimizerがコンテンツソースの種類を検出し、以下の関連するアクセス手順を表示します。

### ステップ 2 - コンテンツソースへのアクセス権を付与する

コンテンツソースに一致するセクションに従います。

#### SharePoint — Adobe ドメイン

![AEM Sitesに接続ダイアログで、Adobe SharePoint ドメインに対する操作が不要であることが表示される](./assets/settings/connect-content-and-drive.png){align="center"}

Content SourceのURLでAdobe SharePoint ドメインを使用している場合、それ以上の操作は必要ありません。 アクセスは既に設定されています。 **保存**&#x200B;をクリックして接続を完了します。

#### SharePoint — カスタムドメイン

Content Source URLで組織独自のSharePoint ドメインを使用している場合は、Azure アプリケーションを登録し、その資格情報をAEM Sites Optimizerに提供する必要があります。

##### 必要なもの

- Azure ポータルにアプリケーションを登録する権限、またはユーザーに代わってアプリケーションを登録できる担当者。
- API同意を付与するテナント管理者権限、またはAPI同意を承認できる管理者。

##### ステップ 2a - Azureでアプリケーションを登録する

1. **Azure Portal → Microsoft Entra ID → App Registrations → New Registration**&#x200B;に移動します。
2. 名前を付けます（例：`AEM Sites Optimizer`）。
3. その他の既定値をすべて残し、**登録**&#x200B;をクリックします。
4. **概要** ページで、次の点に注意してください。
   - **アプリケーション （クライアント） ID**
   - **ディレクトリ （テナント） ID**

##### ステップ 2b - API権限の追加

1. **API権限に移動→ Microsoft Graph → アプリケーション権限**→権限を追加します。
2. 次の両方を追加します。
   - `Sites.Selected` – 特定のSharePoint サイトコレクションへのスコープ付きアクセス。
   - `Files.SelectedOperations.Selected` — ログイン ユーザーなしでファイルにアクセスできます。
3. 両方の場合は、**管理者の同意を付与**&#x200B;をクリックします。

![Sites.SelectedとFiles.SelectedOperations.Selected granted](./assets/settings/app-permissions.png){align="center"}を示すAzure API権限

>[!NOTE]
>
>管理者の同意を付与するには、テナント管理者権限が必要です。 この機能がない場合は、IT管理者またはAzure管理者に次の手順を実行する前に、この手順を完了するように依頼してください。

##### ステップ 2c - クライアントシークレットの作成

![ アプリ登録用のAzure証明書とシークレットのページ ](./assets/settings/create-credentials.png){align="center"}

1. **証明書と秘密鍵→新しいクライアント秘密鍵**&#x200B;に移動します。
2. 説明と有効期限を設定し、**追加**&#x200B;をクリックします。
3. 秘密値をすぐにコピーします。1回だけ表示されます。

##### ステップ 2d — SharePoint サイトへのアプリのアクセス権を付与する

Microsoft Graph Explorer、PowerShell、またはダイレクト Graph API呼び出しを使用して、アプリにアクセス権を付与できます。

[Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)に移動し、Microsoft アカウントでログインして、次のリクエストを実行します。

1. 自分のサイト IDを検索：

```
GET https://graph.microsoft.com/v1.0/sites/{tenant}.sharepoint.com:/sites/{site-name}
```

1. 応答から`id`をコピーし、サイトレベルのアクセス権を付与します。

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

##### ステップ 2e - AEM Sites Optimizerに資格情報を入力する

![SharePointに接続ダイアログに表示されたAEM Sitesの資格情報フィールド ](./assets/settings/add-sharepoint-credentials.png){align="center"}

**AEM Sitesに接続** ダイアログに戻り、**SharePoint経由のコンテンツリポジトリ接続**&#x200B;に次のように入力します。

- **テナント ID （Azure AD）** — アプリ登録→概要。
- **クライアント ID （アプリ登録）** — アプリ登録→概要から。
- **クライアントシークレット** – 手順2cで作成しました。

「**接続を検証**」をクリックしてアクセスを確認し、「**保存**」をクリックします。

#### Google Drive

![AEM Sitesに接続ダイアログに、アクセスを共有するためのGoogle Drive サービスアカウントが表示されている](./assets/settings/validate-eds-google.png){align="center"}

1. Google ドライブで、EDS サイトをバックアップするフォルダーを右クリックし、**Share**&#x200B;を選択します。
2. 「**ユーザーとグループを追加**」フィールドに、**AEM Sitesに接続** ダイアログに表示されるサービスアカウントの電子メールを入力します。
   `experience-success-studio@helix-225321.iam.gserviceaccount.com`
3. 権限レベルを&#x200B;**編集者**&#x200B;に設定します。
4. **ユーザーに通知**&#x200B;のチェックを外し、**共有**&#x200B;をクリックします。

共有が完了したら、ダイアログで「**接続を検証**」をクリックし、「**保存**」をクリックします。
