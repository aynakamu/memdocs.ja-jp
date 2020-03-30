---
title: Hybrid Azure AD 参加済みデバイスの登録 - Windows Autopilot
titleSuffix: ''
description: Windows Autopilot を使用して Hybrid Azure AD 参加済みデバイスを Microsoft Intune に登録します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84d14943a37cf29a224c94364317d899b65ffef0
ms.sourcegitcommit: bbb63f69ff8a755a2f2d86f2ea0c5984ffda4970
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79526328"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>Intune と Windows Autopilot を使用して Hybrid Azure AD 参加済みデバイスをデプロイする
Intune と Windows Autopilot を使用して、Hybrid Azure Active Directory (Azure AD) 参加済みデバイスを設定できます。 そのためには、この記事の手順のようにします。

## <a name="prerequisites"></a>[前提条件]

[Hybrid Azure AD 参加済みデバイス](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)を正しく構成します。 Get-MsolDevice コマンドレットを使用して、[デバイスの登録を確認](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration)します。

登録するデバイスでは次のことも必要です。
- Windows 10 v1809 以降を実行している。
- [文書化されている Windows Autopilot のネットワーク要件に従って](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements)インターネットにアクセスできる。
- Active Directory ドメイン コントローラーにアクセスできる。したがって、組織のネットワークに接続されている必要があります (そこで、AD ドメインと AD ドメイン コントローラーの DNS レコードを解決し、ドメイン コントローラーと通信してユーザーの認証を行うことができます。 現時点では、VPN 接続はサポートされていません)。
- 参加を試みるドメインのドメイン コントローラーを ping できる。
- プロキシを使用する場合は、WPAD プロキシ設定オプションを有効にして構成する必要がある。
- OOBE (Out-of-Box Experience) を使用している。
- Azure Active Directory が OOBE でサポートしている認証の種類を使用する。


## <a name="set-up-windows-10-automatic-enrollment"></a>Windows 10 の自動登録を設定する

1. Azure にサインインし、左側のウィンドウで **[Azure Active Directory]** を選択します。

   ![Azure portal](./media/windows-autopilot-hybrid/auto-enroll-azure-main.png)

1. **[モビリティ (MDM および MAM)]** を選択します。

   ![[Azure Active Directory] ウィンドウ](./media/windows-autopilot-hybrid/auto-enroll-mdm.png)

1. **[Microsoft Intune]** を選択します。

   ![[モビリティ (MDM および MAM)] ウィンドウ](./media/windows-autopilot-hybrid/auto-enroll-intune.png)

1. Intune と Windows を使用して Azure AD 参加済みデバイスをデプロイするユーザーが、**MDM ユーザー スコープ**に含まれるグループのメンバーであることを確認します。

   ![[モビリティ (MDM および MAM)] の [構成] ウィンドウ](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

1. **[MDM 利用規約 URL]** 、 **[MDM 探索 URL]** 、 **[MDM 準拠 URL]** の各ボックスには既定値を使用して、 **[保存]** を選択します。

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>組織単位でコンピューター アカウントの上限を増やす

Active Directory 用の Intune コネクタでは、オンプレミスの Active directory ドメインに Autopilot 登録済みコンピューターが作成されます。 Intune コネクタをホストするコンピューターには、ドメイン内にコンピューター オブジェクトを作成する権限が必要です。 

一部のドメインでは、コンピューターにはコンピューターを作成する権限が付与されません。 また、ドメインには組み込みの制限 (既定値は 10) があり、コンピューター オブジェクトの作成権限を委任されていないすべてのユーザーとコンピューターに適用されます。 そのため、Intune コネクタをホストし、Hybrid Azure AD 参加済みデバイスを作成する組織単位のコンピューターに、この権限を委任する必要があります。

コンピューター作成権限を付与される組織単位は、次のどちらかと一致している必要があります。
- ドメイン参加プロファイルで入力された組織単位。
- プロファイルが選択されていない場合は、お使いのドメインに対するコンピューターのドメイン名。

1. **[Active Directory ユーザーとコンピューター]** (DSA.msc) を開きます。

1. Hybrid Azure AD 参加済みコンピューターの作成に使用する組織単位を右クリックして、 **[制御の委任]** を選択します。

    ![[制御の委任] コマンド](./media/windows-autopilot-hybrid/delegate-control.png)

1. **制御の委任**ウィザードで、 **[次へ]**  >  **[追加]**  >  **[オブジェクトの種類]** を選択します。

1. **[オブジェクトの種類]** ウィンドウで、 **[コンピューター]** チェック ボックスをオンにして、 **[OK]** を選択します。

    ![[オブジェクトの種類] ウィンドウ](./media/windows-autopilot-hybrid/object-types-computers.png)

1. **[ユーザー、コンピューター、またはグループの選択]** ウィンドウの **[選択するオブジェクト名を入力してください]** ボックスに、コネクタをインストールするコンピューターの名前を入力します。

    ![[ユーザー、コンピューター、またはグループの選択] ウィンドウ](./media/windows-autopilot-hybrid/enter-object-names.png)

1. **[名前の確認]** を選択して入力を検証し、 **[OK]** を選択してから、 **[次へ]** を選択します。

1. **[委任するカスタム タスクを作成する]**  >  **[次へ]** を選択します。

1. **[フォルダー内の次のオブジェクトのみ]** チェック ボックスをオンにし、 **[コンピューター オブジェクト]** 、 **[選択されたオブジェクトをこのフォルダーに作成する]** 、および **[選択されたオブジェクトをこのフォルダーから削除する]** チェック ボックスをオンにします。

    ![[Active Directory オブジェクトの種類] ウィンドウ](./media/windows-autopilot-hybrid/only-following-objects.png)
    
1. **[次へ]** を選択します。

1. **[アクセス許可]** で、 **[フル コントロール]** チェック ボックスをオンにします。  
    この操作で、他のすべてのオプションが選択されます。

    ![[アクセス許可] ウィンドウ](./media/windows-autopilot-hybrid/full-control.png)

1. **[次へ]** を選択し、 **[完了]** を選択します。

## <a name="install-the-intune-connector"></a>Intune コネクタをインストールする

Active Directory 用の Intune コネクタは、Windows Server 2016 以降を実行しているコンピューターにインストールする必要があります。 コンピューターは、インターネットとお使いの Active Directory にもアクセスできる必要があります。 スケールと可用性を高めたり、複数の Active Directory ドメインをサポートしたりするため、環境内に複数のコネクタをインストールできます。 コネクタは、他の Intune コネクタが実行されていないサーバーにインストールすることをお勧めします。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[Windows]**  >  **[Windows の登録]**  >  **[Active Directory の Intune コネクタ]**  >  **[追加]** を選択します。 
2. 手順に従ってコネクタをダウンロードします。
3. ダウンロードしたコネクタのセットアップ ファイル *ODJConnectorBootstrapper.exe* を開いて、コネクタをインストールします。
4. セットアップの最後に、 **[構成]** を選択します。
5. **[サインイン]** を選択します。
6. ユーザーのグローバル管理者ロールまたは Intune 管理者ロールの資格情報を入力します。  
   ユーザー アカウントに Intune ライセンスが割り当てられている必要があります。
7. **[デバイス]**  >  **[Windows ]**  >  **[Windows の登録]**  >  **[Active Directory の Intune コネクタ]** に移動し、接続の状態が **[アクティブ]** であることを確認します。

> [!NOTE]
> コネクタにサインインした後、それが [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)に表示されるまでに数分かかる場合があります。 Intune サービスと正常に通信できる場合にのみ表示されます。

### <a name="turn-off-ie-enhanced-security-configuration"></a>[IE セキュリティ強化の構成] をオフにする
Windows Server では既定で、Internet Explorer セキュリティ強化の構成がオンになっています。 Intune Connector for Active Directory にサインインできない場合、管理者向けの [IE セキュリティ強化の構成] をオフにします。 「[How To Turn Off Internet Explorer Enhanced Security Configuration (Internet Explorer セキュリティ強化の構成をオフにする方法)](https://blogs.technet.microsoft.com/chenley/2011/03/10/how-to-turn-off-internet-explorer-enhanced-security-configuration)」

### <a name="configure-web-proxy-settings"></a>Web プロキシ設定の構成

ネットワーク環境に Web プロキシがある場合は、「[既存のオンプレミス プロキシ サーバーと連携する](autopilot-hybrid-connector-proxy.md)」を参照して、Active Directory 用の Intune コネクタが正しく動作することを確認します。


## <a name="create-a-device-group"></a>デバイス グループを作成する
1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[グループ]** を選択し、 **[新しいグループ]** を選択します。

1. **[グループ]** ウィンドウで、次のようにします。

    a. **[グループの種類]** で、 **[セキュリティ]** を選択します。

    b. **[グループ名]** と **[グループの説明]** を入力します。

    c. **[メンバーシップの種類]** を選択します。

1. メンバーシップの種類で **[動的デバイス]** を選択した場合は、 **[グループ]** ウィンドウで **[動的なデバイス メンバー]** を選択し、 **[高度なルール]** ボックスで次のいずれかのようにします。
    - すべての Autopilot デバイスを含むグループを作成するには、「`(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`」と入力します。
    - Intune のグループ タグ フィールドは、Azure AD デバイス上の OrderID 属性にマップされます。 特定のグループ タグ (OrderID) を使って Autopilot デバイスをすべて含むグループを作成する場合は、「`(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`」と入力する必要があります
    - 特定の注文書 ID のすべての Autopilot デバイスを含むグループを作成するには、「`(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`」と入力します。
    
1. **[保存]** を選択します。

1. **[作成]** を選択します。  

## <a name="register-your-autopilot-devices"></a>Autopilot デバイスを登録する

次の方法のいずれかを選択して Autopilot デバイスを登録します。

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>既に登録されている Autopilot デバイスを登録する

1. **[すべての対象デバイスを Autopilot に変換する]** を **[はい]** に設定して、Autopilot Deployment プロファイルを作成します。 
2. Autopilot で自動的に登録するメンバーが含まれるグループにプロファイルを割り当てます。

詳しくは、「[Autopilot Deployment プロファイルを作成する](enrollment-autopilot.md#create-an-autopilot-deployment-profile)」をご覧ください。

### <a name="register-autopilot-devices-that-arent-enrolled"></a>登録されていない Autopilot デバイスを登録する

デバイスがまだ登録されていない場合は、自分で登録できます。 詳しくは、「[デバイスを追加する](enrollment-autopilot.md#add-devices)」をご覧ください。

### <a name="register-devices-from-an-oem"></a>OEM からデバイスを登録する

新しいデバイスを購入する場合、OEM によってはデバイスを登録できます。 詳しくは、[Windows Autopilot のページ](https://aka.ms/WindowsAutopilot)をご覧ください。

"*登録*" が済んだ Autopilot デバイスは、Intune に登録される前に、次の 3 つの場所に表示されます (名前はシリアル番号に設定されます)。
- Azure portal の Intune の **[Autopilot デバイス]** ウィンドウ。 **[デバイスの登録]**  >  **[Windows の登録]**  >  **[デバイス]** を選択します。
- Azure portal の Intune の **[Azure AD デバイス]** ウィンドウ。 **[デバイス]**  >  **[Azure AD デバイス]** を選択します。
- Azure portal の Azure Active Directory の **[Azure AD All Devices]\(Azure AD のすべてのデバイス\)** ウィンドウ ( **[デバイス]**  >  **[すべてのデバイス]** )。

Autopilot デバイスが "*登録*" された後は、次の 4 つの場所に表示されます。
- Azure portal の Intune の **[Autopilot デバイス]** ウィンドウ。 **[デバイスの登録]**  >  **[Windows の登録]**  >  **[デバイス]** を選択します。
- Azure portal の Intune の **[Azure AD デバイス]** ウィンドウ。 **[デバイス]**  >  **[Azure AD デバイス]** を選択します。
- Azure portal の Azure Active Directory の **[Azure AD All Devices]\(Azure AD のすべてのデバイス\)** ウィンドウ。 **[デバイス]**  >  **[すべてのデバイス]** を選択します。
- Azure portal の Intune の **[すべてのデバイス]** ウィンドウ。 **[デバイス]**  >  **[すべてのデバイス]** を選択します。

登録後の Autopilot デバイスの名前は、デバイスのホスト名になります。 既定では、ホスト名は *DESKTOP-* で始まります。


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>AutoPilot Deployment プロファイルを作成して割り当てる
Autopilot Deployment プロファイルは、Autopilot デバイスを構成する場合に使用されます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[Windows]**  >  **[Windows の登録]**  >  **[デプロイ プロファイル]**  >  **[プロファイルの作成]** を選択します。
2. **[基本]** ページ上で、 **[名前]** と省略可能な **[説明]** に入力します。
3. 割り当てられたグループ内のデバイスのすべてが自動的に Autopilot に変換されるようにする場合は、 **[すべての対象デバイスを Autopilot に変換する]** を **[はい]** に設定します。 割り当てられたグループ内にある会社所有の Autopilot 以外のデバイスは、すべて Autopilot デプロイ サービスに登録されます。 個人所有のデバイスは、Autopilot に変換されません。 登録が処理されるまで 48 時間待ちます。 デバイスが登録解除されリセットされると、Autopilot によってそのデバイスが登録されます。 この方法でデバイスを登録すると、このオプションを無効にしてもプロファイルの割り当てを削除しても、Autopilot 展開サービスからデバイスは削除されません。 [デバイスを直接削除](enrollment-autopilot.md#delete-autopilot-devices)する必要があります。
4. **[次へ]** を選択します。
5. **[Out-of-box experience (OOBE)]** ページの **[配置モード]** で、 **[ユーザー ドリブン]** を選択します。
6. **[Azure AD への参加の種類]** ボックスで、 **[ハイブリッド Azure AD 参加済み]** を選択します。
7. 必要に応じて、 **[Out-of-box experience (OOBE)]** ページで残りのオプションを構成します。
8. **[次へ]** を選択します。
9. **[スコープ タグ]** ページで、このプロファイルの[スコープ タグ](../fundamentals/scope-tags.md)を選択します。
10. **[次へ]** を選択します。
11. **[割り当て]** ページで、 **[含めるグループを選択]** を選択し、デバイス グループを検索して選択し、 **[選択]** を選択します。
12. **[次へ]**  >  **[作成]** を選択します。

デバイス プロファイルの状態が *[未割り当て]* から *[割り当て中]* を経て最後に *[割り当て済み]* に変わるまでに、約 15 分かかります。

## <a name="optional-turn-on-the-enrollment-status-page"></a>(省略可能) 登録状態ページを有効にする

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[Windows]**  >  **[Windows の登録]**  >  **[登録状態ページ]** を選択します。
1. **[登録ステータス ページ]** ウィンドウで、 **[既定]**  >  **[設定]** の順に選択します。
1. **[アプリとプロファイルのインストール進行状況を表示する]** ボックスで、 **[はい]** を選択します。
1. 必要に応じて、他のオプションを構成します。
1. **[保存]** を選択します。

## <a name="create-and-assign-a-domain-join-profile"></a>ドメイン参加プロファイルを作成して割り当てる

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
2. 次のプロパティを入力します。
   - **名前**:新しいプロファイルのわかりやすい名前を入力します。
   - **説明**:プロファイルの説明を入力します。
   - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
   - **[プロファイルの種類]** : **[ドメイン参加 (プレビュー)]** を選択します。
3. **[設定]** を選択し、**コンピューター名のプレフィックス**と**ドメイン名**を指定します。
4. (省略可能) [DN 形式](https://docs.microsoft.com/windows/desktop/ad/object-names-and-identities#distinguished-name)で**組織単位** (OU) を指定します。 次のような方法があります。
   - Intune コネクタを実行している Windows 2016 デバイスに制御を委任した OU を指定します。
   - オンプレミスの Active Directory でルート コンピューターに制御を委任した OU を指定します。
   - この値を空白のままにすると、コンピューター オブジェクトが Active Directory の既定のコンテナー ([変更しないかぎり](https://support.microsoft.com/en-us/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom) CN=Computers) に作成されます。
   
   有効な例を示します。
   - OU=Level 1、OU=Level2、DC=contoso、DC=com
   - OU=Mine、DC=contoso、DC=com
   
   有効ではない例を示します。
   - CN=Computers、DC=contoso、DC=com (コンテナーを指定することはできません。ドメインの既定値を使用する場合は、代わりに値を空白のままにします)
   - OU=Mine (DC=attributes を使用してドメインを指定する必要があります)
     
   > [!NOTE]
   > **[組織単位]** の値の周りで引用符を使用しないでください。
5. **[OK]**  >  **[作成]** を選択します。  
    プロファイルが作成されて、一覧に表示されます。
6. プロファイルを割り当てるには、「[デバイス プロファイルを割り当てる](../configuration/device-profile-assign.md#assign-a-device-profile)」の手順に従って、この「[デバイス グループを作成する](windows-autopilot-hybrid.md#create-a-device-group)」の手順で使用したのと同じグループにプロファイルを割り当てます。 または、別のドメインまたは OU にデバイスを参加させる必要がある場合は、異なるグループを使用できます。

> [!NOTE]
> Hybrid Azure AD Join 用の Windows Autopilot の名前付け機能では、%SERIAL% などの変数はサポートされません。サポートされるのは、コンピューター名のプレフィックスのみです。

## <a name="next-steps"></a>次のステップ

Windows Autopilot を構成した後は、これらのデバイスを管理する方法を学習します。 詳細については、「[Microsoft Intune デバイスの管理とは](../remote-actions/device-management.md)」を参照してください。
