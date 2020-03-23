---
title: Intune を使用して iOS および Android 用の Microsoft Edge を管理する
titleSuffix: ''
description: Microsoft Edge で Intune アプリ保護ポリシーを使用して、企業の Web サイトが確実に保護機能付きでアクセスされるようにすることができます。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/02/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cf77349508144498b847236598abda6bced52b0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361225"
---
# <a name="manage-web-access-by-using-microsoft-edge-with-microsoft-intune"></a>Microsoft Edge と Microsoft Intune を使用して Web アクセスを管理する

Microsoft Edge で Intune アプリ保護ポリシーを使うと、企業の Web サイトへのアクセスに常にセーフガードが適用されるようにするのに役立ちます。 Intune ポリシーで有効になっている次の Microsoft Edge エンタープライズ機能を使用できます。

- **デュアル ID。** ユーザーは、閲覧用に、職場アカウントだけでなく個人アカウントも追加できます。 2 つの ID の間は完全に分離されており、Office 365 と Outlook のアーキテクチャとエクスペリエンスに似ています。 Intune 管理者は、職場アカウント内での保護された閲覧エクスペリエンス用に必要なポリシーを設定できます。
- **Intune アプリ保護ポリシーの統合。** Microsoft Edge は Intune SDK と統合されているため、データ損失から保護するためのアプリ保護ポリシーを対象にすることができます。 これらの機能には、切り取り、コピー、貼り付けの制御、画面キャプチャの禁止、ユーザーが選択したリンクが他のマネージド アプリでのみ開かれることの保証が含まれます。
- **Azure アプリケーション プロキシの統合。** サービスとしてのソフトウェア (SaaS) アプリおよび Web アプリへのアクセスを制御できます。 これは、エンド ユーザーが企業ネットワークまたはインターネットのどちらから接続した場合でも、ブラウザー ベースのアプリがセキュリティで保護された Microsoft Edge ブラウザーでのみ実行されることを保証するのに役立ちます。
- **アプリケーションの構成。** アプリケーション構成の設定を使って、組織のセキュリティ体制を強化し、エンド ユーザーが使いやすい機能を構成することができます。 たとえば、ブックマーク、ホーム ページのショートカット、許可またはブロックされるサイト、Azure Active Directory (Azure AD) アプリケーション プロキシなどを定義できます。

Microsoft Edge の Microsoft Intune 保護ポリシーは、組織のデータとリソースを保護するのに役立ちます。 Microsoft Edge でこれらのポリシーを使用することで、会社のリソースが、ネイティブにインストールされたアプリ内だけでなく、Web ブラウザーを介してアクセスしたときにも確実に保護されます。

## <a name="getting-started"></a>はじめに

ご自身とエンド ユーザーは、組織で使用するためにパブリック アプリ ストアから Microsoft Edge をダウンロードすることができます。 ブラウザー ポリシーに対するオペレーティング システムの要件は、次のいずれかです。
- Android 4 以降
- iOS 8.0 以降

## <a name="application-protection-policies-for-microsoft-edge"></a>Microsoft Edge のアプリケーション保護ポリシー

Microsoft Edge は Intune SDK と統合されているため、アプリケーション保護ポリシーを適用することができます。

これらの設定は以下のものに適用できます。
- Intune に登録されたデバイス。
- 別のモバイル デバイス管理製品に登録されたるデバイス。
- アンマネージド デバイス。

Microsoft Edge が Intune ポリシーの対象ではない場合、ユーザーはそれを使用して、Office アプリなどの他の Intune で管理されているアプリケーションからデータにアクセスすることはできません。 

## <a name="conditional-access-for-microsoft-edge"></a>Microsoft Edge の条件付きアクセス

Azure AD の条件付きアクセスを使って、Microsoft Edge を介してのみ、会社のコンテンツにアクセスするようにユーザーをリダイレクトすることができます。 これにより、Azure AD に接続されている Web アプリへのモバイル ブラウザーからのアクセスは、ポリシーで保護された Microsoft Edge に制限されます。 これにより、Safari や Chrome などの他の保護されていないブラウザーからのアクセスはブロックされます。 条件付きアクセスは、Exchange Online や SharePoint Online のような Azure リソース、Microsoft 365 管理センター、および [Azure AD アプリケーション プロキシ](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)を介して外部ユーザーに公開されているオンプレミス サイトにも適用できます。

Azure AD に接続された Web アプリで iOS および Android 上の Microsoft Edge が使われるように制限するには:
1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. Intune ノードで、 **[条件付きアクセス]**  >  **[新しいポリシー]** の順に選択します。
3. ウィンドウの **[アクセス制御]** セクションから **[許可]** を選択します。
4. **[承認されたクライアント アプリが必要です]** を選択します。
5. **[許可]** ウィンドウで **[選択]** を選択します。 このポリシーは、Intune Managed Browser アプリにのみアクセス可能にするクラウド アプリに割り当てる必要があります。

    ![条件付きアクセス ポリシー - 許可のスクリーンショット](./media/manage-microsoft-edge/manage-microsoft-edge-01.png)

6. [割り当て] セクションで、 **[条件]**  >  **[アプリ]** を選択します。 **[アプリ]** ウィンドウが表示されます。
7. **[構成]** で **[はい]** を選択して、特定のクライアント アプリにポリシーを適用します。
8. **[ブラウザー]** がクライアント アプリとして選択されていることを確認します。

    ![条件付きアクセス ポリシー - クライアント アプリの選択のスクリーンショット](./media/manage-microsoft-edge/manage-microsoft-edge-02.png)

    > [!NOTE]
    > これらのクラウド アプリケーションにアクセスできるネイティブ アプリ (ブラウザー ベースではないアプリ) を制限する場合は、 **[モバイル アプリとデスクトップ クライアント]** を選択することもできます。

9. **[割り当て]** セクションで、 **[ユーザーとグループ]** を選択し、このポリシーを割り当てるユーザーまたはグループを選択します。

10. **[割り当て]** セクションで、 **[クラウド アプリ]** を選択して、このポリシーで保護するアプリを選択します。

上記のポリシーが構成された後、ユーザーは、このポリシーで保護されている Azure AD に接続された Web アプリにアクセスする場合、Microsoft Edge の使用を強制されるようになります。 ユーザーがこのシナリオで管理されていないブラウザーを使おうとすると、Microsoft Edge を使う必要があることを示すメッセージが表示されます。

> [!TIP]
> 条件付きアクセスは、Azure AD のテクノロジです。 Intune からアクセスされる条件付きアクセス ノードは、Azure AD からアクセスされるものと同じノードです。

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>ポリシーで保護されたブラウザーでの Azure AD に接続されている Web アプリへのシングル サインオン

iOS および Android 上の Microsoft Edge では、Azure AD に接続されているすべての Web アプリ (SaaS およびオンプレミス) へのシングル サインオン (SSO) を利用できます。 SSO では、ユーザーは資格情報を再入力しなくても、Microsoft Edge を介して Azure AD に接続されている Web アプリにアクセスできます。

SSO では、iOS デバイス用の Microsoft Authenticator アプリ、または Android 上の Intune ポータル サイトで、ご利用のデバイスを登録する必要があります。 これらのいずれかを使っているユーザーは、ポリシーで保護されているブラウザーで Azure AD に接続された Web アプリにアクセスすると、デバイスの登録を求められます。 (これは、デバイスがまだ登録されていない場合にのみ当てはまります。)Intune で管理されているユーザーのアカウントでデバイスが登録されると、そのアカウントでは Azure AD に接続されている Web アプリに対する SSO が有効になります。

> [!NOTE]
> デバイスの登録は、Azure AD サービスによる単純なチェックインです。 デバイスを完全に登録する必要はなく、デバイスに対する追加の権限が IT に与えられることもありません。

## <a name="create-a-protected-browser-app-configuration"></a>保護ブラウザー アプリの構成を作成する

Microsoft Edge 用のアプリの構成を作成するには:

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]** を選択します。
3. **[構成ポリシーの追加]** ウィンドウで **[名前]** を入力し、必要に応じてアプリ構成設定の **[説明]** を入力します。
4. **[デバイス登録の種類]** には、 **[管理対象アプリ]** を選択します。
5. **[必要なアプリの選択]** を選択します。 その後、 **[対象アプリ]** ウィンドウで、iOS/iPadOS に対して、または Android に対して、あるいはその両方に対して、 **[Managed Browser]** または **[Edge]** を選択します。
6. **[OK]** を選択して、 **[構成ポリシーの追加]** ウィンドウに戻ります。
7. **[構成設定]** を選択します。 **[構成]** ウィンドウで、Microsoft Edge の構成を指定するためのキーと値のペアを定義します。 定義できる別のキーと値のペアについては、この記事の後半のセクションで説明します。

    > [!NOTE]
    > Microsoft Edge は、Managed Browser と同じキーと値のペアを使用します。 Android では、アプリ構成ポリシーを有効にするには、Microsoft Edge がアプリ保護ポリシーの対象になっている必要があります。

8. 終了したら、 **[OK]** を選択します。
9. **[構成ポリシーの追加]** ウィンドウで、 **[追加]** を選択します。<br>
    新しい構成が作成され、 **[アプリの構成]** ウィンドウに表示されます。

## <a name="assign-the-configuration-settings-you-created"></a>作成した構成設定を割り当てる 

Azure AD のユーザーのグループに設定を割り当てます。 ユーザーが対象の保護ブラウザー アプリをインストールしている場合、そのアプリは指定された設定で管理されます。

1. Intune モバイル アプリケーション管理ダッシュボードの **[アプリ]** ウィンドウで、 **[アプリ構成ポリシー]** を選択します。
2. アプリの構成の一覧から、割り当てる構成を選択します。
3. 次のウィンドウで、 **[割り当て]** を選択します。
4. **[割り当て]** ウィンドウで、アプリの構成を割り当てる Azure AD グループを選択し、 **[OK]** を選択します。

## <a name="direct-users-to-microsoft-edge-instead-of-the-intune-managed-browser"></a>ユーザーに Intune Managed Browser ではなく Microsoft Edge を指示する 

Intune Managed Browser と Microsoft Edge のどちらも、ポリシーで保護されたブラウザーとして使用できます。 ユーザーが確実に適切なブラウザー アプリの使用を指示されるようにするには、以下の構成設定で、すべての Intune で管理されたアプリ (Outlook、OneDrive、SharePoint など) を対象にします。

|    キー    |    値    |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.useEdge`    |    値が `true` の場合、ユーザーは Microsoft Edge をダウンロードして使用するように指示されます。<br>値が `false` の場合、ユーザーは Intune Managed Browser を使用することができます。    |

このアプリ構成の値が設定されて**いない**場合、次のロジックで、企業のリンクを開くために使用されるブラウザーが定義されます。

Android 上の場合:
- ユーザーが Intune Managed Browser と Microsoft Edge の両方をデバイスにダウンロードしている場合は、Intune Managed Browser が起動されます。 
- Microsoft Edge のみがデバイスにダウンロードされていて、Intune ポリシーの対象になっている場合は、Microsoft Edge が起動されます。
- Managed Browser のみがデバイス上にあり、Intune ポリシーの対象になっている場合は、Managed Browser が起動されます。

iOS/iPadOS 上で、iOS バージョン 9.0.9+ 用の Intune SDK を統合したアプリ向けの場合:
- Managed Browser と Microsoft Edge の両方がデバイス上にある場合は、Intune Managed Browser が起動されます。  
- Microsoft Edge のみがデバイス上にあり、Intune ポリシーの対象になっている場合は、Microsoft Edge が起動されます。
- Managed Browser のみがデバイス上にあり、Intune ポリシーの対象になっている場合は、Managed Browser が起動されます。

## <a name="configure-application-proxy-settings-for-microsoft-edge"></a>Microsoft Edge 用にアプリケーション プロキシの設定を構成する

Microsoft Edge と [Azure AD アプリケーション プロキシ](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)を一緒に使用して、ユーザーが自分のモバイル デバイスでイントラネット サイトにアクセスできるようにすることができます。 

以下に示すのは、Azure AD アプリケーション プロキシを有効にするいくつかのシナリオ例です。 

- ユーザーは、Intune で保護されている、Outlook モバイル アプリを使用しています。 その後、メールでイントラネット サイトへのリンクをクリックすると、Microsoft Edge によって、このイントラネット サイトがアプリケーション プロキシを介してユーザーに公開されていることが認識されます。 ユーザーは、イントラネット サイトに到達する前に、適用される多要素認証と条件付きアクセスによる認証を行うため、アプリケーション プロキシを経由するよう自動的にルーティングされます。 これにより、ユーザーはモバイル デバイス上でも内部サイトにアクセスできるようになり、Outlook のリンクが意図したとおりに機能するようになります。
- ユーザーは自分の iOS または Android デバイスで Microsoft Edge を開きます。 Microsoft Edge が Intune で保護されており、アプリケーション プロキシが有効になっている場合、ユーザーは、内部 URL を使用してイントラネット サイトに移動できます。 Microsoft Edge では、このイントラネット サイトがアプリケーション プロキシを使ってユーザーに公開されていることが認識されます。 ユーザーは、イントラネット サイトに到達する前に認証を行うため、アプリケーション プロキシを経由するよう自動的にルーティングされます。 

### <a name="before-you-start"></a>開始する前に

- Azure AD アプリケーション プロキシを経由するように内部アプリケーションを設定します。
  - アプリケーション プロキシを構成し、アプリケーションを公開するには、[セットアップに関するドキュメント](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)を参照してください。
- Microsoft Edge アプリには、[Intune アプリ保護ポリシー](app-protection-policy.md)を割り当てる必要があります。

> [!NOTE]
> 更新されたアプリケーション プロキシのリダイレクト データが、Managed Browser や Microsoft Edge で有効になるまでには、最大で 24 時間かかる場合があります。

#### <a name="step-1-enable-automatic-redirection-to-microsoft-edge-from-outlook"></a>手順 1:Outlook から Microsoft Edge への自動リダイレクトを有効にする
設定 **[ポリシーで管理されているブラウザーで Web コンテンツを共有する]** を有効にするアプリ保護ポリシーで、Outlook を構成します。

![[アプリ保護ポリシー] - [ポリシーで管理されているブラウザーで Web コンテンツを共有する] のスクリーンショット](./media/manage-microsoft-edge/manage-microsoft-edge-03.png)

#### <a name="step-2-set-the-app-configuration-setting-to-enable-app-proxy"></a>手順 2:アプリ プロキシを有効にするためにアプリ構成を設定する
次のキー/値ペアで Microsoft Edge を対象とし、Microsoft Edge に対してアプリケーション プロキシを有効にします。

|    キー    |    値    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    true    |

オンプレミスの Web アプリへのシームレスな (保護された) アクセスのために、Microsoft Edge と Azure AD アプリケーション プロキシを並行使用する方法について詳しくは、「[Better together: Intune and Azure Active Directory team up to improve user access (最適な組み合わせ: ユーザーのアクセスを向上するための Intune と Azure Active Directory の連携)](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254)」を参照してください。 このブログ記事では Intune Managed Browser を参照しますが、そのコンテンツは Microsoft Edge にも適用されます。

## <a name="configure-a-homepage-shortcut-for-microsoft-edge"></a>Microsoft Edge のホーム ページ ショートカットを構成する

この設定では、Microsoft Edge のホーム ページ ショートカットを構成することができます。 構成したホーム ページ ショートカットは、ユーザーが Microsoft Edge で新しいタブを開くと、検索バーの下に最初のアイコンとして表示されます。 ユーザーは、自分で管理しているコンテキストで、このショートカットを編集したり削除したりすることはできません。 ホーム ページ ショートカットには、区別のために組織の名前が表示されます。 

ホーム ページ ショートカットを構成するには、以下のキー/値のペアを使用します。

|    キー    |    値    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    有効な URL を指定します。 セキュリティ対策のため、誤った URL はブロックされます。<br>**例:**  <`https://www.bing.com`>     |

## <a name="configure-multiple-top-site-shortcuts-for-new-tab-pages-in-microsoft-edge"></a>Microsoft Edge の新しいタブ ページに対して複数のトップ サイト ショートカットを構成する 
ホームページのショートカットを構成するのと同様に、Microsoft Edge の新しいタブ ページで、複数のトップ サイト ショートカットを構成できます。 ユーザーは、管理しているコンテキストで、これらのショートカットを編集したり削除したりすることはできません。 注: ホームページのショートカットを含めて、全部で 8 個のショートカットを構成できます。 ホームページのショートカットを構成した場合、構成されている最初の最上位サイトがそれによってオーバーライドされます。 

|    キー    |    値    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    値の URL のセットを指定します。 各トップ サイト ショートカットは、タイトルと URL で構成されます。 タイトルと URL は、`|` 文字で区切ります。 次に例を示します。 <br> `GitHub | https://github.com/||LinkedIn|https://www.linkedin.com`    |

## <a name="configure-your-organizations-logo-and-brand-color-for-new-tab-pages-in-microsoft-edge"></a>Microsoft Edge 内の新しいタブ ページ用に組織のロゴとブランドの色を構成する

これらの設定を使用すると、Microsoft Edge の新しいタブ ページをカスタマイズして、組織のロゴとブランドの色をページの背景として表示することができます。

組織のロゴと色をアップロードするには、まず、次の手順を実行します。
- Azure portal 内で [[Microsoft Endpoint Manager admin center]](https://go.microsoft.com/fwlink/?linkid=2109431) ->  **[テナント管理]**  ->  **[ブランド化とカスタマイズ]**  ->  **[Company Identity Branding]\(会社 ID のブランド化\)** に移動します。
- ブランドのロゴを設定するために、[表示] の下にある [会社のロゴのみ] を選択します。 背景が透明なロゴをお勧めします。 
- ブランドの背景色を設定するには、[表示] の下にある [テーマの色] を選択します。 Microsoft Edge では、新しいタブ ページ上に明るい色の網掛けが適用され、ページの読みやすさが向上しています。 

次に、以下のキーと値のペアを使用して、組織のブランドを Microsoft Edge にプルします。

|    キー    |    値    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    True    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    True    |

## <a name="display-relevant-industry-news-on-new-tab-pages"></a>新しいタブ ページに関連する業界ニュースを表示する

Microsoft Edge モバイル内の新しい タブ ページ エクスペリエンスを構成して、組織に関連する業界のニュースを表示できます。 この機能を有効にすると、Microsoft Edge モバイルでは、組織のドメイン名を使用して、組織、組織の業界、および競合他社に関するニュースが Web から集約されるので、ユーザーは Microsoft Edge の新しいタブ ページだけですべての関連する外部ニュースを検索できます。 業界ニュースは既定ではオフになっており、組織に対して選択できます。 

|    キー    |    値    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **True** にすると、Microsoft Edge モバイルの新しいタブ ページに業界のニュースが表示されます。<p>**False** (既定値) にすると、新しいタブ ページの業界ニュースは非表示になります。    |

## <a name="configure-managed-bookmarks-for-microsoft-edge"></a>Microsoft Edge 用に管理対象ブックマークを構成する

アクセスしやすくするため、ユーザーが Microsoft Edge を使用するときに利用できるようにしたいブックマークを構成できます。 

詳細をいくつか以下に示します。

- これらのブックマークは、ユーザーが Microsoft Edge の[企業モード](https://docs.microsoft.com/intune/apps/app-configuration-managed-browser#how-to-configure-bookmarks-for-a-protected-browser)を使用している場合にのみ表示されます。 
- これらのブックマークを、ユーザーが削除したり、変更したりすることはできません。
- これらのブックマークは、リストの上部に表示されます。 ユーザーが作成したブックマークは、これらのブックマークの下に表示されます。
- アプリケーション プロキシのリダイレクトを有効にしてある場合は、内部 URL または外部 URL を使ってアプリケーション プロキシ Web アプリを追加できます。
- リストに入力するときは、すべての URL の先頭に必ず **http://** または **https://** を付けてください。

管理対象ブックマークを構成するには、次のキー/値のペアを使用します。

|    キー    |    値    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    この構成の値はブックマークのリストです。 各ブックマークは、ブックマークのタイトルとブックマークの URL で構成されます。 タイトルと URL は、`|` 文字で区切ります。      例:<br>`Microsoft Bing|https://www.bing.com`<br>複数のブックマークを構成するには、二重の `||` 文字で各ペアを区切ります。<p>例:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

## <a name="display-myapps-within-microsoft-edge-bookmarks"></a>Microsoft Edge ブックマーク内に MyApps を表示する

既定では、Microsoft Edge ブックマークの内部のフォルダー内でユーザーに対して構成されている MyApps サイトが、ユーザーに対して表示されます。 フォルダーには組織名でラベルが付けられます。

|    キー    |    値    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **True** の場合、Microsoft Edge ブックマーク内に MyApps が表示されます。<p>**False** の場合、Microsoft Edge 内で MyApps が非表示となります。    |
    
## <a name="use-https-protocol-as-default"></a>HTTPS プロトコルを既定として使用する

ユーザーが指定していない場合、既定で HTTPS プロトコルを使用するように Microsoft Edge モバイルを構成できます。 一般に、これはベスト プラクティスと考えられます。 既定のプロトコルとして HTTPS を有効にするには、次のキーと値のペアを使用します。

|    キー    |    値    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.defaultHTTPS`     |     **True** にすると、既定のプロトコルは HTTPS を使用するように設定されます     |


## <a name="specify-allowed-or-blocked-sites-list-for-microsoft-edge"></a>Microsoft Edge に対して許可またはブロックするサイトのリストを指定する
アプリ構成を使って、ユーザーが仕事用プロファイルを使用するときにアクセスできるサイトを定義できます。 許可リストを使用した場合、ユーザーは明示的にリストされているサイトにのみアクセスできます。 ブロック リストを使用した場合、ユーザーは明示的にブロックされているサイトを除く、すべてのサイトにアクセスできます。 両方ではなく、許可リストまたはブロック リストのみを適用する必要があります。 両方を適用した場合は、許可リストが受け付けられます。  

Microsoft Edge に対して許可またはブロックするサイトのリストを構成するには、次のキー/値ペアを使います。 

|    キー    |    値    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    次の中から選択します。<p>1.許可された URL を指定する場合 (これらの URL のみが許可され、その他のサイトにはアクセスできない):<br>`com.microsoft.intune.mam.managedbrowser.AllowListURLs`<p>2.ブロックされた URL を指定する場合 (その他のすべてのサイトにアクセスできる):<br>`com.microsoft.intune.mam.managedbrowser.BlockListURLs`    |    キーに対応する値は URL のリストです。 許可またはブロックするすべての URL をパイプ `|` 文字で区切り、単一の値として入力します。<br>**例:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`  |

### <a name="url-formats-for-allowed-and-blocked-site-list"></a>許可およびブロック サイト リストの URL 形式 
さまざまな URL 形式を使用して、許可/ブロック サイト リストを作成することができます。 次の表で、これらの許可されているパターンについて詳しく説明します。 開始する前に次のいくつかの点に注意してください。 
- リストに入力するときは、すべての URL の先頭に必ず **http://** または **https://** を付けてください。
- ワイルドカード記号 (\*) は、以下の許可されているパターン リストの規則に従って使用できます。
- ワイルドカードは、ホスト名のコンポーネント全体 (ピリオドで区切られた部分) またはパスの全体部分 (スラッシュで区切られた部分) にのみ一致します。 たとえば、`http://*contoso.com` はサポートされて**いません**。
- アドレスにはポート番号を指定できます。 ポート番号を指定しない場合は、次の値が使用されます。
  - http の場合はポート 80
  - https の場合はポート 443
- ポート番号でのワイルドカードの使用はサポートされて**いません**。 たとえば、 `http://www.contoso.com:*` と `http://www.contoso.com:*/` はサポートされていません。 

    |    [URL]    |    説明    |    ［一致する］    |    ［次の値に一致しない］    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    単一のページと一致する    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    単一のページと一致する    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    `www.contoso.com` で始まるすべての URL と一致する    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    `contoso.com` の下のすべてのサブドメインと一致する    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    `contoso.com/` で終わるすべてのサブドメインと一致する    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    単一のフォルダーと一致する    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    ポート番号を使用し、単一のページと一致する    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    セキュリティで保護された単一のページと一致する    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    1 つのフォルダーおよびすべてのサブフォルダーと一致する    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- 指定することができない入力例を次に示します。
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP アドレス
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

## <a name="transition-users-to-their-personal-context-when-trying-to-access-a-blocked-site"></a>ブロックされたサイトにアクセスしようとしたユーザーを個人用コンテキストに移行させる

Microsoft Edge に組み込まれているデュアル ID モデルでは、Intune Managed Browser で可能であったものより柔軟なエクスペリエンスを、エンド ユーザーに対して有効にできます。 ユーザーが Microsoft Edge でブロックされているサイトにアクセスしたら、職場コンテキストではなく、個人用コンテキストでリンクを開くよう求めることができます。 これにより、企業リソースを安全な状態に保ちながら、ユーザーを保護された状態に維持できます。 たとえば、Outlook でニュース記事へのリンクがユーザーに送信された場合、ユーザーは個人コンテキストまたは [InPrivate] タブで、リンクを開くことができます。職場のコンテキストでは、ニュースの Web サイトは許可されません。 既定では、これらの移行が許可されます。

以下のキー/値のペアを使用して、これらのソフト移行を許可するかどうかを構成します。

|    キー    |    値    |
|-------------------------------------------------------------------|-------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock`    |    **True** (既定) の場合、Microsoft Edge で、ブロックされたサイトを開くために個人用コンテキストにユーザーを移行させることができます。<p>**False** では、Microsoft Edge でユーザーを移行させることはできません。 ユーザーには、アクセスしようとしているサイトがブロックされていることを示すメッセージが単に表示されます。    |

## <a name="disable-inprivate-and-microsoft-accounts-msa-to-restrict-personal-browsing"></a>InPrivate および Microsoft アカウント (MSA) を無効にして、個人の閲覧を制限する
高度に規制された業界で、Microsoft Edge を使用している一部のお客様は、AAD コンテキスト内でのみ閲覧できるようにユーザーのスコープを指定することができます。 次のアプリ構成設定を使用して、Microsoft アカウントまたは InPrivate ブラウズを無効にすることができます。

|    キー    |    値    |
|-------------------------------------------------------------------|-------------------------------------------------------|
|     `com.microsoft.intune.mam.managedbrowser.disabledFeatures`    |    **inprivate** を使用して、InPrivate ブラウザーを無効にします。 <br> **msa** を使用して、ユーザーが個人の MSA アカウントを Microsoft Edge に追加する機能を無効にします。<br> InPrivate と MSA の両方のアカウントを無効にするには、`inprivate| msa` を使用します    |  


アプリ保護ポリシーを展開していない場合は、ユーザーが Microsoft アカウントを使用できないように制限し、登録されているデバイスでの職場または学校アカウントからの閲覧のみを許可することもできます。 Microsoft Edge の組織アカウント専用モードを構成するためのキーの詳細については、以下を参照してください。
- [Android 組織アカウント専用](https://docs.microsoft.com/intune/apps/app-configuration-policies-use-android#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS 組織アカウント専用](https://docs.microsoft.com/intune/apps/app-configuration-policies-use-ios#allow-only-configured-organization-accounts-in-multi-identity-apps)

## <a name="open-restricted-links-directly-in-inprivate-tab-pages"></a>制限されたリンクを InPrivate タブ ページで直接開く

制限されたリンクを InPrivate ブラウズで直接開く必要があるかどうかを構成できます。InPrivate ブラウズでは、よりシームレスな閲覧エクスペリエンスがユーザーに提供されます。 これにより、ユーザーはサイトを表示するために個人用コンテキストを経由する手間がなくなります。 InPrivate ブラウズはアンマネージドと見なされるため、InPrivate ブラウズ モードの使用中は、ユーザーはアクセスできません。  注:この設定を有効にするには、上記の設定 `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock` を **true** に構成しておく必要もあります。

|    キー    |    値    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked`    |    **True** の場合、個人用アカウントへの切り替えをユーザーに求めることなく、自動的に InPrivate タブでサイトを直接開きます。 <p> **False** (既定) の場合、Microsoft Edge 内でサイトがブロックされ、ユーザーは自分の個人用アカウントに切り替えて表示するように求められます。    |


## <a name="disable-microsoft-edge-features-to-customize-the-end-user-experience-for-your-organizations-needs"></a>Microsoft Edge の機能を無効にしてエンド ユーザー エクスペリエンスを組織のニーズに応じてカスタマイズする

### <a name="disable-prompts-to-share-usage-data-for-personalization"></a>個人用設定のために使用状況データを共有する確認を無効にする 

Microsoft Edge の既定では、閲覧エクスペリエンスをカスタマイズするために、使用状況データの収集についてユーザーに確認します。 この確認がエンド ユーザーに表示されないようにすることで、このデータの共有を無効にすることができます。 

|    キー    |    値    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableShareUsageData`    |     **true** にすると、この確認はエンド ユーザーに表示されなくなります。    |

### <a name="disable-prompts-to-share-browsing-history"></a>閲覧の履歴を共有する確認を無効にする 

Microsoft Edge の既定では、閲覧エクスペリエンスをカスタマイズするために、履歴データの収集についてユーザーに確認します。 この確認がエンド ユーザーに表示されないようにすることで、このデータの共有を無効にすることができます。

|    キー    |    値    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     `com.microsoft.intune.man.managedbrowser.disableShareBrowsingHistory`    |     **true** にすると、この確認はエンド ユーザーに表示されなくなります。     |

### <a name="disable-prompts-that-offer-to-save-passwords"></a>パスワードを保存するための確認を無効にする

iOS の Microsoft Edge の既定では、ユーザーのパスワードがキーチェーンに保存されます。 組織に対してこのプロンプトを無効にする場合は、次の設定を構成します。

|    キー    |    値    |
|-----------------------|-----------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **password** にすると、エンド ユーザーのパスワードを保存するための確認が無効になります。    |

### <a name="disable-inprivate-browsing-and-microsoft-accounts-to-restrict-browsing-to-work-only-contexts"></a>InPrivate ブラウズと Microsoft アカウントを無効にして閲覧を職場のみのコンテキストに制限する

組織が規制の厳しい業界で運営されている場合、またはアプリごとの VPN を使用して、ユーザーが Microsoft Edge を使用して職場のリソースにアクセスできるようにする場合は、Microsoft Edge の使用を MAM で保護されたコンテキストのみに限定することができます。 この機能は、MDM に登録されたデバイスに対してのみ提供されます。

|    キー    |    値    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **inprivate** にすると、InPrivate ブラウズが無効になります。 <br> **msa** にすると、個人の Microsoft アカウント (MSA) をユーザーが Microsoft Edge アプリに追加できなくなります。 <br> 複数の機能を無効にするには、`|` で値を区切ります。 たとえば、`inprivate|msa` とすると、InPrivate アカウントと個人用アカウントの両方がブロックされます。   |

### <a name="restrict-microsoft-edge-use-to-allowed-accounts-only"></a>Microsoft Edge の使用を許可されたアカウントのみに制限する

InPrivate および MSA ブラウズをブロックするだけでなく、ユーザーが AAD アカウントでログインしている場合に限って Microsoft Edge の使用を許可できます。 この機能は、MDM に登録されたユーザーのみが使用できます。 この設定の構成に関する詳細については、次を参照してください。

- [Android の設定](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS の設定](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

## <a name="use-microsoft-edge-on-ios-to-access-managed-app-logs"></a>iOS で Microsoft Edge を使用してマネージド アプリのログにアクセスする

iOS デバイスに Microsoft Edge をインストールしているユーザーは、Microsoft で公開されたすべてのアプリの管理状態を表示できます。 管理対象 iOS アプリの問題を解決するためにログを送信できます。 次に手順を示します。

1. iOS デバイスで Microsoft Edge を開きます。
2. アドレス バーに「`about:intunehelp`」と入力します。
3. Microsoft Edge がトラブルシューティング モードで起動されます。

アプリ ログに格納されている設定の一覧については、「[Managed Browser 内のアプリの保護ログのレビュー](app-protection-policy-settings-log.md)」を参照してください。

Android デバイスでログを表示する方法については、[メールによる IT 管理者へのログの送信](https://docs.microsoft.com/user-help/send-logs-to-your-it-admin-by-email-android)に関するページを参照してください。

## <a name="security-and-privacy-for-microsoft-edge"></a>Microsoft Edge のセキュリティとプライバシー

Microsoft Edge のセキュリティとプライバシーに関するその他の考慮事項を次に示します。

- Microsoft Edge では、ユーザーが自分のデバイス上でネイティブ ブラウザーに対して行った設定は使用されません (https://docs.microsoft.com/en-us/intune/apps/app-configuration-policies-use-android#allow-only-configured-organization-accounts-in-multi-identity-apps )。これは、Microsoft Edge でこれらの設定にアクセスできないためです。
- Microsoft Edge に関連付けられているアプリ保護ポリシーで、オプション **[アクセスの際にシンプルな PIN を要求する]** または **[アクセスの際に会社の資格情報を要求する]** を構成できます。 ユーザーは、認証ページでヘルプのリンクを選択した場合、ポリシーのブロック リストに追加されているかどうかにかかわらず、インターネット サイトを参照できます。
- Microsoft Edge では、直接アクセスされたときにのみ、サイトへのアクセスをブロックできます。 ユーザーがサイトへのアクセスに中間サービス (翻訳サービスなど) を使っている場合、アクセスはブロックされません。
- 認証を許可し、Intune ドキュメントにアクセスするために、* **.microsoft.com** は許可またはブロック リスト設定の対象から除外されます。 常に許可されます。
- ユーザーはデータ収集を無効にできます。 Microsoft は、Microsoft の製品やサービスを改善するために、Managed Browser のパフォーマンスおよび使用に関する匿名データを自動的に収集します。 ただし、ユーザーはデバイスの **[使用状況データ]** 設定を使用して、データの収集を無効にすることができます。 このデータの収集方法は制御できません。 iOS デバイスでは、証明書の有効期限が切れている Web サイトや証明書が信頼されていない Web サイトにユーザーがアクセスしても、開くことができません。

## <a name="next-steps"></a>次のステップ

- [アプリ保護ポリシーとは?](app-protection-policy.md) 
