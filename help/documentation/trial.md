---
title: Sites Optimizer 体験版
description: 既存の AEM Sites のお客様向けの AEM Sites Optimizer 体験版を開始します。
source-git-commit: 052faac621530a5b9e74bd8e4790a604887515f7
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 45%
---

# Sites Optimizer 体験版

既存の&#x200B;**AEM Sitesのお客様（Edge Delivery Services、Cloud Services、Managed Services）**&#x200B;向けに、この体験版を使用してSites Optimizerを開始します。 ドメインデータは既にオンボードされているので、すぐに最適化を開始できます。 以下のビデオでは、体験版エクスペリエンスと開始方法を順を追って説明します。

>[!IMPORTANT]
>
>まず、自社サイトが次の要件を満たしていることを確認しましょう。
>
>* AEM Sites（Edge Delivery Services、Cloud Service、Managed Services）上に構築されています。
>* 本番サイトであり、開発、QA、ステージング、オーサー、プレビュー環境ではありません。
>* これは一般にアクセス可能であり、ログインの背後にはありません。
>* AEM Sitesのフロントエンド配信を使用します。 ヘッドレス配信は現在サポートされていません。

>[!VIDEO](https://video.tv.adobe.com/v/3483253/?learn=on&enablevpops)

>[!TIP]
>
> ご質問やご要望がある場合は、[siteoptimizer-now@adobe.com](mailto:siteoptimizer-now@adobe.com) にお問い合わせください。

## 今すぐ体験版を開始しましょう

体験版を開始するには、次の手順に従います。

1. AEM Sites IMS 組織 ID を使用して、[www.sitesoptimizer.live](http://www.sitesoptimizer.live/) にログインします。
2. ページビュー数、読み込み時間、エンゲージメント率などの主要指標を、影響ごとに優先順位が付けられた上位の最適化の機会と共に表示します。
3. 使用可能な 3 つの機会タイプ（[破損したバックリンク](./opportunities/broken-backlinks.md)、[コア web バイタル](./opportunities/core-web-vitals.md)、[欠落している代替テキスト](./opportunities/missing-alt-text.md)）を探索します。
4. 各機会について、特定された最大 3 つの問題を確認します。 AI が生成した提案を使用し、準備が整い次第、最適化を AEM 環境に直接デプロイします。
5. いつでもフルライセンスにアップグレードすることで、より多くの機会を獲得できます。

## 体験版で使用できる内容

体験版には、以下が含まれます。

* 3 つの機会タイプ：[破損したバックリンク](./opportunities/broken-backlinks.md)、[コア web バイタル](./opportunities/core-web-vitals.md)、[欠落している代替テキスト](./opportunities/missing-alt-text.md)。
* 機会ごとに毎月最大 3 つの問題。
* 問題ごとに完全なワークフロー：自動特定、自動提案、自動最適化。
  * **自動特定** - 複数のデータソースを使用して、サイト全体で問題を検出します。
  * **自動提案** - 各問題に対して、AI が生成した規範的なレコメンデーションを提供します。
  * **自動最適化** - 承認後、修正をオーサリング環境に直接デプロイします。 アップデートは既存のワークフローに従って行われるので、チームは AEM を通じてレビューおよび公開できます。

## Sites Optimizerによるサイトへのアクセスを許可

Sites Optimizerがサイトをスキャンし、最適化の機会を特定します。 サイトがファイアウォール、コンテンツ配信ネットワーク（CDN）、または未認識のクライアントをブロックするその他のセキュリティ設定の背後にある場合、スキャナーはページに到達できません。 このような場合、オンボーディングでは、Sites Optimizerがweb サイトにアクセスできないことを示す&#x200B;**アクションが必要**&#x200B;というメッセージが表示され、アクセスを許可するまでスキャンは一時停止されます。

![&#x200B; オンボーディングダイアログで、Sites OptimizerがWeb サイトにアクセスできないこと、User-AgentとスキャナーのIP アドレスがYoutubeに一覧表示され、それぞれに「コピー」ボタンと、アクセスを再確認するための「更新」ボタンが表示されている](./assets/trial/ip-allowlist-action-required.png){align="center"}

スキャナーを通過させるには、ファイアウォール、ホスティングプロバイダー、またはセキュリティ設定で次の両方を許可リストに加えるします。 AEM Cloud Service サイトの場合は、Cloud Managerの[CDN トラフィックフィルタールール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf)にスキャナーの許可ルールを追加します。このルールは、User-Agent アドレスとIP アドレスの両方で一致します。 [Cloud Manager IP 許可リスト](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/introduction)を使用してアクセスを制限する場合は、適用された許可リストにもスキャナーのIP アドレスを追加します。

* **User-Agent** — スキャナーは、トークン `Spacecat/1.0`を含むUser-Agentで自分自身を識別します。 このトークンを許可リストに加えるします。理想的には「contains」の一致として指定するので、完全なUser-Agent文字列が変更されても機能し続けます。
* **スキャナーのIP アドレス** — スキャナーの送信IP アドレスを許可リストに加えるします。

オンボーディング画面には、**Copy** ボタンが付いたUser-AgentとIP アドレスが正確に表示され、現在の値を設定に直接コピーできます。

スキャナーを許可リストしたら、オンボーディング画面で「**更新**」を選択します。 アクセスが許可されると、スキャンは自動的に再開され、最適化の機会が表示されます。

>[!NOTE]
>
>これらのIP アドレスは、サイトの分析にのみ使用されます。 それらを許可リストに加えるしても、他のアクセス権は付与されません。

## Edge Delivery体験版サイトの自動修正を有効にする

トライアル版のお客様が、Google DriveまたはSharePointで作成されたEdge Delivery Services（EDS）サイトに対する自動修正の提案を行うために、**作成者にデプロイ** アクションを有効にする方法について説明します。

>[!NOTE]
>
>この要件は、Google DriveまたはSharePointでサイトを作成している体験版の組織にのみ適用されます。 有料のお客様、およびCrosswalkまたはDark Alleyで作成されたサイトは、影響を受けません。

体験版のお客様は、**ASO-EDS-Autofix-Users** IMS グループに属している必要があります。 グループが存在しない場合は、組織の管理者がグループを作成して追加できます。

1. [Adobe Admin Console](https://adminconsole.adobe.com/)にログインします。
1. **ユーザー**/**ユーザーグループ**&#x200B;を選択します。
1. 「**ユーザーグループを追加**」を選択します。
1. **ユーザーグループ名**&#x200B;に対して、次のように正確に入力します。

   ```
   ASO-EDS-Autofix-Users
   ```

   >[!IMPORTANT]
   >
   > グループ名は、大文字と小文字を含めて正確に一致する必要があります。 大文字と小文字を区別して一致するので、異なるスペルや大文字と小文字の区別（例：`ASO-EDS-Autofix-users`）は機能しません。 作成後にグループの名前を変更しないでください。

1. 「**保存**」を選択します。

   ![Adobe Admin Consoleで新しいユーザーグループダイアログを作成し、「ユーザーグループ名」フィールドをASO-EDS-Autofix-Users](./assets/trial/create-user-group.png){align="center"}に設定します

1. 新しいグループを開き、**ユーザーを追加**&#x200B;を選択します。
1. 自動修正をデプロイできるユーザーの電子メールアドレスまたはユーザー名を入力し、**保存**&#x200B;を選択します。

   ![Adobe Admin Console](./assets/trial/add-users-to-group.png){align="center"}でこのユーザーグループにユーザーを追加ダイアログ

グループのメンバーの場合、「**作成者にデプロイ**」ボタンが有効になります。 まだメンバーでない場合は、**作成者へのデプロイ**&#x200B;は無効になり、管理者に連絡してグループに追加するように求めるツールチップが表示されます。 管理者がグループにユーザーを追加したら、ログアウトしてSites Optimizerに再度ログインし、セッションで新しいグループメンバーシップを選択します。

## よくある質問

AEM Sites Optimizer 体験版に関するよくある質問とその回答については、以下を参照してください。

+++AEM Sites Optimizer とは何ですか？

[AEM Sites Optimizer](/help/home.md) は、web サイト全体の問題を特定し、規範的なレコメンデーションを提供し、トラフィックの獲得、エンゲージメント、コンバージョンを向上させるための修正を支援する AI ファーストのアプリケーションです。

+++
+++この体験版に参加できるのは誰ですか？

既存の AEM Sites のお客様（Edge Delivery Services、Cloud Services、Managed Services）。

+++
+++体験版にアクセスするにはどうすればよいですか？

[www.sitesoptimizer.live](http://www.sitesoptimizer.live/) に移動し、AEM Sites IMS 組織 ID を使用してログインします。

+++
+++体験版にはコストがかかりますか？

いいえ。 この体験版は、既存の AEM Sites のお客様は無料でご利用いただけます。

+++
+++有効期限はありますか？

いいえ。 体験版は時間ベースではありません。 使用可能な機会タイプと問題の数を通じて使用状況により制限されます。
+++
+++すべての問題が修正された後はどうなりますか？

Sites Optimizer は、パフォーマンスに影響を与える問題を継続的に特定します。 無料体験版では、問題は毎月のみ追加されます。 継続的な監査と最適化のためにアップグレードします。

+++
+++より多くの機会にアクセスするにはどうすればよいですか？

製品エクスペリエンスを通じて利用可能なアップグレード CTA またはセールスにお問い合わせ CTA を使用するか、[siteoptimizer-now@adobe.com](mailto:siteoptimizer-now@adobe.com) までメールでお問い合わせください。

+++
+++ASO-EDS-Autofix-Users グループに属していますが、オーサーへのデプロイはまだ無効です。 何を確認すればよいですか？

ログアウトして再度ログインすると、グループメンバーシップはログイン時に読み取られます。 また、グループ名のスペルと大文字が正確に`ASO-EDS-Autofix-Users`であること、およびサイトが属するのと同じ組織で作成されていることを確認します。

+++
+++ASO-EDS-Autofix-Users グループ要件は、すべてのEdge Delivery Services サイトに適用されますか？

いいえ。 これは、**SharePoint ドライブ**&#x200B;または&#x200B;**Google**&#x200B;で作成された体験版サイトにのみ適用されます。 **Crosswalk**&#x200B;または&#x200B;**Dark Alley**&#x200B;で作成されたサイト、およびすべての&#x200B;**有料** サイトは影響を受けません。

+++
+++Sites Optimizerが私のサイトにアクセスできないと言います。 どうすればいいですか？」

スキャナーをブロックするファイアウォール、CDN、セキュリティ設定が存在する可能性があります。 スキャナーのUser-Agent （`Spacecat/1.0` トークン）とIP アドレスをセキュリティ設定に許可リストに加えるするか、AEM Cloud Service サイトの場合はCloud Manager CDN 許可リストに設定します。 次に、**更新**&#x200B;を選択します。 [Sites Optimizerによるサイトへのアクセスの許可](#allow-sites-optimizer-to-access-your-site)を参照してください。

+++

<!--
CARDS
* ./opportunities/core-web-vitals.md
  {title=Core web vitals}
  {image=../assets/common/card-performance.png}
* ./opportunities/missing-alt-text.md
  {title=Missing alt text}
  {image=../assets/common/card-arrows.png}
* ./opportunities/broken-backlinks.md
  {title=Broken backlinks}
  {image=../assets/common/card-arrows.png}
-->

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Core web vitals">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/core-web-vitals.md" title="コア web バイタル" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-performance.png" alt="コア web バイタル"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/core-web-vitals.md" target="_blank" rel="referrer" title="コア web バイタル">コア web バイタル</a>
                    </p>
                    <p class="is-size-6">Core Web Vitals に関する最適化の機会と、これを使用してトラフィック獲得を向上させる方法について説明します。</p>
                </div>
                <a href="./opportunities/core-web-vitals.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Missing alt text">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/missing-alt-text.md" title="欠落している代替テキスト" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-arrows.png" alt="欠落している代替テキスト"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/missing-alt-text.md" target="_blank" rel="referrer" title="欠落している代替テキスト">欠落している代替テキスト</a>
                    </p>
                    <p class="is-size-6">代替テキストの欠落に関する最適化の機会と、これを使用して web サイトのエンゲージメントを向上させる方法について説明します。</p>
                </div>
                <a href="./opportunities/missing-alt-text.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Broken backlinks">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./opportunities/broken-backlinks.md" title="破損したバックリンク" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/common/card-arrows.png" alt="破損したバックリンク"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./opportunities/broken-backlinks.md" target="_blank" rel="referrer" title="破損したバックリンク">破損したバックリンク</a>
                    </p>
                    <p class="is-size-6">破損したバックリンクの機会と、これを使用してトラフィックの獲得を向上させる方法について説明します。</p>
                </div>
                <a href="./opportunities/broken-backlinks.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
