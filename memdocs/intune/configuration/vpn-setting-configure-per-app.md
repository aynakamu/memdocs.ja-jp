---
title: Microsoft Intune での iOS/iPadOS デバイスに対するアプリごとの VPN の設定 - Azure | Microsoft Docs
description: 前提条件を参照し、仮想プライベート ネットワーク (VPN) ユーザーのグループを作成し、SCEP 証明書プロファイルを追加し、アプリごとの VPN プロファイルを構成し、iOS/iPadOS デバイスの Microsoft Intune でいくつかのアプリを VPN プロファイルに割り当てます。 デバイスの VPN 接続を確認する手順も一覧表示します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 97d3c4ee2e1ad173b8fff238f072b1b36c3ed1cb
ms.sourcegitcommit: 0907ee1137773f0482b1d2b9bb344e206d05aede
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2020
ms.locfileid: "80536874"
---
# <a name="set-up-per-app-virtual-private-network-vpn-for-iosipados-devices-in-intune"></a>Intune での iOS/iPadOS デバイスに対するアプリごとの仮想プライベート ネットワーク (VPN) の設定

Microsoft Intune では、アプリに割り当てられた仮想プライベート ネットワーク (VPN) を作成して使用することができます。 この機能は、"アプリごとの VPN" と呼ばれます。 Intune で管理されているデバイスで VPN を使用できるマネージド アプリを選択します。 アプリごとの VPN を使用すると、エンド ユーザーは VPN 経由で自動的に接続し、ドキュメントなどの組織のリソースへのアクセスを取得します。

この機能は、以下に適用されます。

- iOS 9 以降
- iPadOS 13.0 以降

VPN プロバイダーのドキュメントで、お使いの VPN でアプリごとの VPN がサポートされているかどうかを確認します。

この記事では、アプリごとの VPN プロファイルを作成し、アプリにこのプロファイルを割り当てる方法を説明します。 これらの手順を使用すると、エンド ユーザーに対してシームレスなアプリごとの VPN エクスペリエンスを作成できます。 アプリごとの VPN をサポートするほとんどの VPN では、ユーザーがアプリを開くと、自動的に VPN に接続されます。

一部の VPN では、アプリごとの VPN でユーザー名とパスワードの認証を許可しています。 つまり、ユーザーは VPN に接続するためにユーザー名とパスワードを入力する必要があります。

> [!IMPORTANT]
> iOS/iPadOS 用の IKEv2 VPN プロファイルでは、アプリごとの VPN はサポートされていません。

## <a name="per-app-vpn-with-zscaler"></a>Zscaler でのアプリごとの VPN

Zscaler Private Access (ZPA) は、認証のために Azure Active Directory (Azure AD) と統合されています。 ZPA を使用する場合、(この記事で説明されている) [信頼された証明書](#create-a-trusted-certificate-profile)や [SCEP または PKCS 証明書](#create-a-scep-or-pkcs-certificate-profile)プロファイルは必要ありません。 Zscaler 用にアプリごとの VPN プロファイルを設定すると、関連付けられているいずれかのアプリを開いても、ZPA に自動的に接続されません。 代わりに、ユーザーは、まず Zscaler アプリにサインインする必要があります。 その結果、リモート アクセスは関連付けられているアプリに制限されます。

## <a name="prerequisites-for-per-app-vpn"></a>アプリごとの VPN の前提条件

> [!IMPORTANT]
> ご利用の VPN ベンダーによっては、特定のハードウェアやライセンスなど、アプリごとの VPN に関するその他の要件がある場合があります。 必ず、そのドキュメントを参照し、Intune でアプリごとの VPN を設定する前に前提条件を満たすようにしてください。

身元を証明するため、VPN サーバーはデバイスによってプロンプトなしに受け入れられる必要がある証明書を提示します。 証明書の自動承認を確認するには、証明機関 (CA) によって発行された VPN サーバーのルート証明書が含まれる、信頼済み証明書プロファイルを作成します。

### <a name="export-the-certificate-and-add-the-ca"></a>証明書をエクスポートし、CA を追加する

1. VPN サーバーで、管理コンソールを開きます。
2. VPN サーバーで証明書ベースの認証が使用されていることを確認します。 
3. 信頼されたルート証明書ファイルをエクスポートします。 拡張子は .cer で、信頼済み証明書プロファイルの作成時にこのファイルを追加します。
4. VPN サーバーへの認証用に証明書を発行した CA の名前を追加します。

    デバイスによって提示される CA が VPN サーバーの信頼された証明機関リストの CA と一致する場合、VPN サーバーによるデバイスの認証が成功します。

## <a name="create-a-group-for-your-vpn-users"></a>VPN ユーザーのグループを作成する

アプリごとの VPN を使用するユーザーまたはデバイス用に、Azure Active Directory (Azure AD) でグループを作成するか既存のグループを選択します。 新しいグループを作成するには、「[ユーザーとデバイスを整理するためのグループを追加する](../fundamentals/groups-add.md)」を参照してください。

## <a name="create-a-trusted-certificate-profile"></a>信頼済み証明書プロファイルを作成する

CA によって発行された VPN サーバーのルート証明書を、Intune で作成されたプロファイルにインポートします。 信頼済み証明書プロファイルから iOS/iPadOS デバイスに、VPN サーバーが提示する CA を自動的に信頼するように指示します。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[iOS/iPadOS]** を選択します。
    - **[プロファイルの種類]** : **[信頼された証明書]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、**会社全体の iOS/iPadOS 信頼済み証明書 VPN プロファイル**は適切なプロファイル名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** で、フォルダー アイコンを選択し、VPN 管理コンソールからエクスポートした VPN 証明書 (.cer ファイル) を参照します。
8. **[次へ]** を選択し、プロファイルの作成を続行します。 詳細については、「[VPN プロファイルの作成](vpn-settings-configure.md#create-the-profile)」を参照してください。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune で iOS/iPadOS デバイスの信頼された証明書プロファイルを作成する](./media/vpn-setting-configure-per-app/vpn-per-app-create-trusted-cert.png)

## <a name="create-a-scep-or-pkcs-certificate-profile"></a>SCEP または PKCS 証明書プロファイルを作成する

信頼されたルート証明書プロファイルにより、デバイスが VPN サーバーを自動的に信頼できるようになります。 SCEP または PKCS 証明書は、iOS/iPadOS の VPN クライアントから VPN サーバーに資格情報を提供します。 この証明書により、ユーザー名とパスワードを求めることなくデバイスがサイレント認証をすることができるようになります。 

クライアント認証証明書を構成して割り当てるには、次のいずれかの記事を参照してください。

- [Intune を使用して SCEP をサポートするようにインフラストラクチャを構成する](../protect/certificates-scep-configure.md)
- [Intune で PKCS 証明書を構成して管理する](../protect/certficates-pfx-configure.md)

クライアント認証用の証明書を必ず構成してください。 クライアント認証は、SCEP 証明書プロファイルで直接設定することができます ( **[拡張キー使用法]** リスト > **[クライアント認証]** )。 PKCS の場合は、証明書機関 (CA) の証明書テンプレートでクライアント認証を設定します。

> [!div class="mx-imgBorder"]
> ![Microsoft Intune で SCEP 証明書プロファイルを作成する (サブジェクト名の形式、キーの使用法、拡張キーの使用法などを含む)](./media/vpn-setting-configure-per-app/vpn-per-app-create-scep-cert.png)

## <a name="create-a-per-app-vpn-profile"></a>アプリごとの VPN プロファイルを作成する

VPN プロファイルには、クライアントの資格情報が含まれる SCEP または PKCS 証明書、VPN の接続情報、iOS/iPadOS アプリケーションでアプリごとの VPN を使用できるようにするアプリごとの VPN フラグが含まれています。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[iOS/iPadOS]** を選択します。
    - **[プロファイルの種類]** : **[VPN]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:カスタム プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、**会社全体の iOS/iPadOS アプリ別 VPN プロファイル**は適切なプロファイル名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[構成設定]** で、次の設定を構成します。

    - **接続の種類**:VPN クライアント アプリを選択します。
    - **[基本 VPN]** : 自分の設定を構成します。 [iOS/iPadOS の VPN 設定](vpn-settings-ios.md)に関するページでは、すべての設定が一覧表示され、説明されています。 アプリごとの VPN を使用する場合は、次のプロパティが記載されているとおりに設定されていることを確認します。

      - **[認証方法]** : **[証明書]** を選択します。 
      - **[認証証明書]** :既存の SCEP または PKCS 証明書を選択し、 **[OK]** を選択します。
      - **[分割トンネリング]** :VPN 接続がアクティブなときに、すべてのトラフィックで VPN トンネルの使用を強制するには、 **[無効]** を選択します。 

      > [!div class="mx-imgBorder"]
      > ![アプリごとの VPN プロファイルで、接続、IP アドレスまたは FQDN、認証方法、Microsoft Intune での分割トンネリングを入力する](./media/vpn-setting-configure-per-app/vpn-per-app-create-vpn-profile.png)

    その他の設定については、[iOS/iPadOS の VPN 設定](vpn-settings-ios.md)に関するページを参照してください。

    - **[自動 VPN]**  >  **[自動 VPN の種類]**  >  **[アプリごとの VPN]**

      > [!div class="mx-imgBorder"]
      > ![Intune で、iOS/iPadOS デバイスの [自動 VPN] を [アプリごとの VPN] に設定する](./media/vpn-setting-configure-per-app/vpn-per-app-automatic.png)

7. **[次へ]** を選択し、プロファイルの作成を続行します。 詳細については、「[VPN プロファイルの作成](vpn-settings-configure.md#create-the-profile)」を参照してください。

## <a name="associate-an-app-with-the-vpn-profile"></a>アプリと VPN プロファイルを関連付ける

VPN プロファイルを追加した後、アプリと Azure AD グループをプロファイルに関連付けます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[アプリ]**  >  **[すべてのアプリ]** の順に選択します。
2. 一覧からアプリを選択し、 **[プロパティ]**  >  **[割り当て]**  >  **[グループの追加]** を選択します。
3. **[割り当ての種類]** で、 **[必須]** または **[登録済みデバイスで使用可能]** を選択します。
4. **[組み込まれたグループ]**  >  **[含めるグループを選択]** > (この記事で) [作成した](#create-a-group-for-your-vpn-users)グループを選択 > **[選択]** の順に選択します。
5. **[VPN]** で、(この記事で) [作成した](#create-a-per-app-vpn-profile) VPN プロファイルを選択します。

    > [!div class="mx-imgBorder"]
    > ![Microsoft Intune でアプリごとの VPN プロファイルにアプリを割り当てる](./media/vpn-setting-configure-per-app/vpn-per-app-app-to-vpn.png)

6. **[OK]**  >  **[保存]** の順に選択します。

アプリとプロファイルの関連付けは、次のすべての条件が存在する場合、次回のデバイス チェックインの際に解除されます。

- アプリが必須インストール インテントのターゲットになった場合
- プロファイルとアプリの両方が同じグループをターゲットにしている場合
- アプリごとの VPN 構成をアプリ割り当てから削除する場合

次のすべての条件が存在する場合、アプリとプロファイルの関連付けは、ユーザーがポータル サイトからの再インストールを要求するまで存在します。

- アプリが利用可能インストール インテントのターゲットになった場合
- プロファイルとアプリの両方が同じグループをターゲットにしている場合
- エンド ユーザーがポータル サイトでアプリのインストールを要求したため、アプリとプロファイルがデバイスにインストールされる場合
- アプリごとの VPN 構成をアプリ割り当てから削除または変更する場合

## <a name="verify-the-connection-on-the-iosipados-device"></a>iOS/iPadOS デバイスでの接続を確認する

アプリと関連付けられたアプリごとの VPN 設定で、デバイスからの接続を確認します。

### <a name="before-you-attempt-to-connect"></a>接続を試行する前に

- 同じグループに、前述のすべてのポリシーを展開しておきます。 そうしないと、アプリごとの VPN のエクスペリエンスは機能しません。
- Pulse Secure VPN アプリまたはカスタムの VPN クライアント アプリを使用している場合、アプリ層またはパケット層でのトンネリングを使用することを選択できます。 **[ProviderType]** 値には、アプリ層トンネリングの場合は **[app-proxy]** を設定し、パケット層トンネリングの場合は **[packet-tunnel]** を設定します。 VPN プロバイダーのドキュメントで、適切な値を使用していることを確認します。

### <a name="connect-using-the-per-app-vpn"></a>アプリごとの VPN を使用して接続する

VPN を選択したり、資格情報を入力したりせずに接続されるゼロタッチ操作を確認します。 ゼロタッチ操作とは、次のような意味です。

- デバイスから VPN サーバーを信頼するように求められません。 つまり、ユーザーには **[Dynamic Trust]\(動的な信頼\)** ダイアログ ボックスが表示されません。
- ユーザーが資格情報を入力する必要はありません。
- ユーザーが関連付けられているアプリのいずれかを開くと、ユーザーのデバイスが VPN に接続されます。

## <a name="next-steps"></a>次のステップ

- iOS/iPadOS の設定を確認するには、[Microsoft Intune での iOS/iPadOS デバイス向けの VPN 設定](vpn-settings-ios.md)に関するページを参照してください。
- VPN の設定と Intune の詳細については、[Microsoft Intune での VPN の設定の構成](vpn-settings-configure.md)に関するページを参照してください。
