---
title: Microsoft Intune での Windows 10 用のデバイスの制限設定 - Azure | Microsoft Docs
description: Windows 10 およびそれ以降のデバイスに対するデバイス制限を作成するには、すべての設定とその説明の一覧を参照してください。 これらの設定を構成プロファイル内で使用すると、スクリーン ショット、パスワード要件、キオスク設定、ストア内アプリ、Microsoft Edge ブラウザー、Microsoft Defender、クラウドへのアクセス、[スタート] メニューなどを Microsoft Intune で制御できます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 237e281b88492ff7b7e1b5614600662e15761935
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407834"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune を使用して機能を許可または制限するように Windows 10 (以降) のデバイスを設定する

この記事では、Windows 10 以降のデバイスで制御できるさまざまな設定の一覧を示して説明します。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使って、機能の許可または無効化、パスワード規則の設定、ロック画面のカスタマイズ、Microsoft Defender の使用などを行います。

これらの設定は、Intune でデバイスの構成プロファイルに追加した後、ご使用の Windows 10 デバイスに割り当てたり展開したりします。

> [!Note]
> Windows のすべてのエディションですべてのオプションを利用できるわけではありません。 サポートされているエディションについては、[ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) に関するページを参照してください (別の Microsoft Web サイトが開きます)。

## <a name="before-you-begin"></a>始める前に

[デバイス構成プロファイルを作成します](device-restrictions-configure.md#create-the-profile)。

## <a name="app-store"></a>アプリ ストア

これらの設定では、[ApplicationManagement ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[アプリ ストア** (モバイルのみ)]: **[ブロック]** を選択すると、エンド ユーザーはモバイル デバイスでアプリ ストアにアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、OS によりエンド ユーザーがアプリ ストアにアクセスできるようにされている場合があります。
- **[ストア アプリの自動更新]** : **[ブロック]** を選択すると、更新プログラムが Microsoft Store から自動的にインストールされなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、Microsoft Store からインストールされたアプリの自動更新が OS で許可されている可能性があります。

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **[信頼できるアプリのインストール]** :Microsoft Store 以外のアプリをインストールできる場合に選択します。これはサイドローディングとも呼ばれます。 サイドローディングでは、Microsoft Store によって認定されていないアプリのインストール後に、アプリが実行されるかテストされます。 たとえば、社内でのみ使用されるアプリです。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[ブロック]** :サイドローディングを禁止します。 Microsoft Store 以外のアプリをインストールすることはできません。
  - **[許可]** :サイドローディングを許可します。 Microsoft Store 以外のアプリをインストールできます。
- **[開発者によるロック解除]** :エンド ユーザーによるサイドロードされたアプリの変更を許可するなど、Windows の開発者向け設定を許可します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[ブロック]** :開発者モードとアプリのサイドローディングを禁止します。
  - **[許可]** :開発者モードとアプリのサイドローディングを許可します。

  この機能の詳細については、「[Enable your device for development (デバイスを開発用に有効にする)](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)」を参照してください。
  
  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **[共有ユーザー アプリ データ]** :アプリケーション データを、同じデバイスの異なるユーザー間で共有する場合、およびそのアプリの他のインスタンスと共有する場合は、 **[許可]** を選択します。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、OS は同じアプリの他のユーザーや他のインスタンスとデータを共有できない場合があります。

  [ApplicationManagement/AllowSharedUserAppData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **[プライベート ストアのみを使用する]** : **[許可]** に設定すると、アプリはプライベート ストアからのみダウンロードでき、小売りカタログを含むパブリック ストアからはダウンロードできません。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、アプリをプライベート ストアおよびパブリック ストアからダウンロードすることが OS で許可されている可能性があります。

  [ApplicationManagement/RequirePrivateStoreOnly CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **[ストアから配信されたアプリの起動]** : **[ブロック]** に設定すると、デバイスにプレインストールされたアプリ、または Microsoft Store からダウンロードされたアプリがすべて無効になります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、これらのアプリを開くことが OS によって許可されている可能性があります。

  [ApplicationManagement/DisableStoreOriginatedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **[システム ボリューム上でアプリ データをインストールします]** : **[ブロック]** に設定すると、アプリでデータをデバイスのシステム ボリュームに格納できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、アプリによるシステム ディスク ボリュームへのデータの格納が OS によって許可されている可能性があります。

  [ApplicationManagement/RestrictAppDataToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **[システム ドライブ上でアプリをインストールします]** : **[ブロック]** に設定すると、アプリはデバイスのシステム ドライブにインストールされなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、アプリによるシステム ドライブへのインストールが OS によって許可されている可能性があります。

  [ApplicationManagement/RestrictAppToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **[ゲーム録画** (デスクトップのみ)]: **[ブロック]** に設定すると、Windows ゲームの録画とブロードキャストが無効になります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、ゲームの記録とブロードキャストが OS によって許可されている可能性があります。

  [ApplicationManagement/AllowGameDVR CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **[ストアのアプリのみ]** :この設定により、ユーザーが Microsoft Store 以外の場所からアプリをインストールするときのユーザー エクスペリエンスが決まります。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。 既定では、他のポリシー設定で定義されているアプリを含め、エンド ユーザーが Microsoft Store 以外の場所からアプリをインストールすることが OS によって許可されている可能性があります。  
  - **[どこでも]** :アプリの推奨設定がオフになり、ユーザーは任意の場所からアプリをインストールできます。  
  - **[Microsoft Store のみ]** :エンド ユーザーに対して、Microsoft Store からのみアプリをインストールするように強制します。
  - **[推奨事項]** :ユーザーが Microsoft Store から入手できるアプリを Web からインストールすると、ストアからダウンロードすることを推奨するメッセージが表示されます。  
  - **[Microsoft Store を優先する]** :ユーザーが Microsoft Store 以外の場所からアプリをインストールすると、警告が表示されます。

  [SmartScreen/EnableAppInstallControl CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **[インストールに対するユーザー コントロール]** : **[ブロック]** を選択すると、通常はシステム管理者用に予約されているインストール オプションをユーザーが変更できなくなります。たとえば、ファイルをインストールするディレクトリの入力などです。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、Windows インストーラーによって、ユーザーがこれらのインストール オプションを変更できなくなり、一部の Windows インストーラー セキュリティ機能がバイパスされる場合があります。

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **[昇格された特権を持つアプリをインストールします]** : **[ブロック]** にすると、システムにプログラムをインストールするときに引き上げられたアクセス許可を使用することが Windows インストーラーに指示されます。 これらの特権はすべてのプログラムに拡張されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、システム管理者が展開または提供していないプログラムをインストールするときに、システムが現在のユーザーのアクセス許可を適用する場合があります。 

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **[スタートアップ アプリ]** : ユーザーがデバイスにサインインした後で開くアプリの一覧を入力します。 セミコロンで区切られた Windows アプリケーションのパッケージ ファミリ名 (PFN) の一覧を必ず使用してください。 このポリシーが動作するには、Windows アプリのマニフェストでスタートアップ タスクを使用する必要があります。

  [ApplicationManagement/LaunchAppAfterLogOn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>携帯ネットワークと接続性

これらの設定では、[接続ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) CSP と[Wi-Fi ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi) CSP が使用されます。それには、サポートされる Windows のエディションも示されています。

- [Wi-Fi ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi)

- **[携帯データ ネットワーク チャネル]** :移動体通信ネットワークに接続しているときに、Web を閲覧するなど、エンド ユーザーがデータを使用できる場合に選択します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。 エンド ユーザーはこれをオフにできます。
  - **[ブロック]** :携帯データ ネットワーク チャネルを許可しません。 エンド ユーザーはこれをオンにすることはできません。
  - **[許可 (編集不可)]** : 携帯データ ネットワーク チャネルを許可します。 エンド ユーザーはこれをオフにすることはできません。

- **[データ ローミング]** : **[ブロック]** に設定すると、デバイスでの携帯データ ネットワークのローミングが禁止されます。 **[未構成]** : (既定値) データへのアクセス時にネットワーク間のローミングを許可します。
- **[移動体通信ネットワーク経由の VPN]** : **[ブロック]** に設定すると、移動体通信ネットワークに接続している間、デバイスは VPN 接続にアクセスできなくなります。 **[未構成]** (既定値) にすると、移動体通信を含むすべての接続での VPN の使用が許可されます。
- **[移動体通信ネットワーク経由の VPN ローミング]** : **[ブロック]** に設定すると、移動体通信ネットワークでローミングしている間、デバイスは VPN 接続にアクセスできなくなります。 **[未構成]** (既定値) にすると、ローミング時の VPN 接続が許可されます。
- **[接続されているデバイスのサービス]** : **[ブロック]** に設定すると、Connected Devices Platform (CDP) コンポーネントが無効になります。 CDP では、(Bluetooth/LAN またはクラウドを通した) リモート アプリの起動、リモート メッセージ、リモート アプリ セッション、およびその他のデバイス間エクスペリエンスをサポートするために、他のデバイスを検出して接続できます。 **[未構成]** (既定値) にすると、接続されているデバイスのサービスが許可され、他の Bluetooth デバイスを検出して接続できます。
- **[NFC]** : **[ブロック]** に設定すると、近距離無線通信 (NFC) 機能の使用が禁止されます。 **[未構成]** (既定値) にすると、ユーザーがデバイス上の NFC 機能を有効にして構成することが許可されます。
- **[Wi-Fi]** : **[ブロック]** に設定すると、ユーザーがデバイスで Wi-Fi 接続の有効化と構成を行うことが禁止され、Wi-Fi 接続を使用することができなくなります。 **[未構成]** (既定値) にすると、Wi-Fi 接続が許可されます。
- **[Automatically connect to Wi-Fi hotspot]\(自動的に Wi-Fi ホットスポットに接続します\)** : **[ブロック]** に設定すると、Wi-Fi ホットスポットへのデバイスの自動接続が禁止されます。 **[未接続]** (既定値) にすると、デバイスは無料の Wi-Fi ホットスポットに自動的に接続され、接続の使用条件に自動的に同意します。
- **[Wi-Fi の手動設定]** : **[ブロック]** に設定すると、MDM サーバーにインストールされたネットワーク以外の Wi-Fi へのデバイス接続が禁止されます。 **[未構成]** (既定値) にすると、エンド ユーザーが自分の Wi-Fi 接続ネットワーク SSID を追加して構成することが許可されます。
- **[Wi-Fi スキャンの間隔]** :デバイスで Wi-Fi ネットワークをスキャンする頻度を入力します。 1 (頻度が最も多い) から 500 (頻度が最も少ない) までの値を入力します。 既定値は `0` (ゼロ) です。

### <a name="bluetooth"></a>Bluetooth

これらの設定では、[Bluetooth ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[Bluetooth]** : **[ブロック]** に設定すると、ユーザーは Bluetooth を有効にできなくなります。 **[未構成]** にすると、デバイスでの Bluetooth の使用が許可されます。
- **[Bluetooth の検出可能性]** : **[ブロック]** に設定すると、このデバイスは他の Bluetooth 対応デバイスで検出されなくなります。 **[未構成]** (既定値) にすると、ヘッドセットなどの他の Bluetooth 対応デバイスからのこのデバイスの検出が許可されます。
- **[Bluetooth の事前ペアリング]** : **[ブロック]** に設定すると、特定の Bluetooth デバイスをホスト デバイスと自動的にペアリングできなくなります。 **[未構成]** (既定値) にすると、ホスト デバイスとの自動的なペアリングが許可されます。
- **[Bluetooth 広告]** : **[ブロック]** に設定すると、デバイスは Bluetooth 広告を送信できなくなります。 **[未構成]** (既定値) にすると、デバイスによる Bluetooth 広告の送信が許可されます。
- **[Bluetooth を使用できるサービス]** :許可される Bluetooth のサービスとプロファイルの一覧を 16 進数文字列 (例: `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`) で入力し、 **[追加]** を選択します。

  サービスの一覧の詳細については、[ServicesAllowedList 使用ガイド](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide)を参照してください。

## <a name="cloud-and-storage"></a>クラウドとストレージ

これらの設定では、[アカウント ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[Microsoft アカウント]** : **[ブロック]** に設定すると、エンド ユーザーは Microsoft アカウントをデバイスに関連付けることができなくなります。 **[未構成]** (既定値) にすると、Microsoft アカウントの追加と使用が許可されます。
- **[Microsoft 以外のアカウント]** : **[ブロック]** に設定すると、エンドユーザーはユーザー インターフェイスを使用して Microsoft 以外のアカウントを追加できなくなります。 **[未構成]** (既定値) にすると、Microsoft アカウントに関連付けられていない電子メール アカウントのユーザーによる追加が許可されます。
- **[Microsoft アカウントの設定の同期]** : **[未構成]** (既定値) に設定すると、Microsoft アカウントに関連付けられたデバイスとアプリの設定をデバイス間で同期できるようになります。 **[ブロック]** にすると、この同期が行われなくなります。
- **[Microsoft アカウント サインイン アシスタント]** : **[未構成]** (既定値) に設定すると、エンドユーザーは、**Microsoft アカウント サインイン アシスタント** (wlidsvc) サービスの開始と停止を実行できます。 このオペレーティング システム サービスでは、ユーザーが自分の Microsoft アカウントにサインインすることが許可されます。 **[無効にする]** にすると、エンド ユーザーが Microsoft サインイン アシスタント サービス (wlidsvc) を制御できなくなります。

## <a name="cloud-printer"></a>クラウド プリンター

これらの設定では、[EnterpriseCloudPrint ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[プリンターの検出 URL]** :クラウド プリンターを検出するための URL を入力します。 たとえば、「`https://cloudprinterdiscovery.contoso.com`」と入力します。
- **[プリンター アクセスの権限 URL]** :OAuth トークンを取得するための認証エンドポイント URL を入力します。 たとえば、「`https://azuretenant.contoso.com/adfs`」と入力します。
- **[Azure ネイティブ クライアント アプリの GUID]** :OAuthAuthority から OAuth トークンを取得する権限を持つクライアント アプリケーションの GUID を入力します。 たとえば、「`E1CF1107-FF90-4228-93BF-26052DD2C714`」と入力します。
- **[印刷サービスのリソース URI]** :Azure portal で構成された印刷サービスの OAuth リソース URI を入力します。 たとえば、「`http://MicrosoftEnterpriseCloudPrint/CloudPrint`」と入力します。
- **[照会するプリンターの最大数]** : 照会されるプリンターの最大数を入力します。 既定値は `20` です。
- **[プリンター検出サービスのリソース URI]** :Azure portal で構成されたプリンター検出サービスの OAuth リソース URI を入力します。 たとえば、「`http://MopriaDiscoveryService/CloudPrint`」と入力します。

> [!TIP]
> [Windows Server のハイブリッド クラウド印刷](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview)を設定した後、これらの設定を構成して、Windows デバイスに展開することができます。

## <a name="control-panel-and-settings"></a>コントロール パネルと設定

- **[[設定] アプリ]** : **[ブロック]** に設定すると、エンド ユーザーは Windows の [設定] アプリにアクセスできなくなります。 **[未構成]** (既定値) にすると、ユーザーはデバイス上で設定アプリを開くことができます。
  - **[システム]** : **[ブロック]** に設定すると、[設定] アプリの [システム] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
    - **[電源とスリープの設定の変更** (デスクトップのみ)]: **[ブロック]** に設定すると、エンド ユーザーはデバイスの電源とスリープの設定を変更できなくなります。 **[未構成]** (既定値) にすると、ユーザーによる電源とスリープの設定の変更が許可されます。
  - **[デバイス]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [デバイス] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[ネットワークとインターネット]** : **[ブロック]** にすると、デバイスで [設定] アプリの [ネットワークとインターネット] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[個人用設定]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [個人用設定] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[アプリ]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [アプリ] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[アカウント]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [アカウント] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[時刻と言語]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [時刻と言語] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
    - **[システム時刻の変更]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスで日付と時刻の設定を変更できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 ユーザーはこれらの設定を変更できます。
    - **[地域設定の変更** (デスクトップのみ)]: **[ブロック]** に設定すると、エンド ユーザーはデバイスで地域設定を変更できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 ユーザーはこれらの設定を変更できます。
    - **[言語設定の変更 (デスクトップのみ)]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスで言語設定を変更できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 ユーザーはこれらの設定を変更できます。

      [設定ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **[ゲーム]** : **[ブロック]** にすると、デバイスで [設定] アプリの [ゲーム] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[簡単操作]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [簡単操作] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[プライバシー]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [プライバシー] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[更新とセキュリティ]** : **[ブロック]** に設定すると、デバイスで [設定] アプリの [更新とセキュリティ] 領域にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

## <a name="display"></a>ディスプレイ

これらの設定では、[ディスプレイ ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display) が使用されます。それには、サポートされる Windows のエディションも示されています。

GDI DPI スケールでは、DPI 対応でないアプリケーションをモニターごとの DPI 対応にすることができます。

- **[アプリの GDI DPI スケールをオンにする]** : GDI DPI スケールをオンにするレガシ アプリを入力し、 **[追加]** を選択します。 たとえば、「`filename.exe`」や「`%ProgramFiles%\Path\Filename.exe`」と入力します。

  一覧に含まれるすべてのレガシ アプリケーションで、GDI DPI スケールがオンになります。

- **[アプリの GDI DPI スケールをオフにする]** : GDI DPI スケールをオフにするレガシ アプリを入力し、 **[追加]** を選択します。 たとえば、「`filename.exe`」や「`%ProgramFiles%\Path\Filename.exe`」と入力します。

  一覧に含まれるすべてのレガシ アプリケーションで、GDI DPI スケールがオフになります。

アプリの一覧を使用して .csv ファイルを**インポート**することもできます。

## <a name="general"></a>全般

これらの設定では、[エクスペリエンス ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience) が使用されます。それには、サポートされる Windows のエディションも示されています。 

- **[画面キャプチャ** (モバイルのみ)]: **[ブロック]** に設定すると、エンドユーザーはデバイスでスクリーンショットを取得できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[コピー/貼り付け (モバイルのみ)]** : **[ブロック]** に設定すると、エンドユーザーはデバイスでアプリ間でのコピー アンド ペーストを使用できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[手動での登録解除]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスでワークプレース コントロール パネルを使用して会社アカウントを削除できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

  コンピューターが Azure AD に参加していて、自動登録が有効になっている場合、このポリシー設定は適用されません。

- **[ルート証明書の手動インストール** (モバイルのみ)]: **[ブロック]** に設定すると、エンド ユーザーは、ルート証明書と中間 CAP 証明書を手動でインストールできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[カメラ]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスでカメラを使用できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 既定では、OS により、デバイスのカメラへのアクセスが許可される場合があります。

  Intune では、デバイス カメラへのアクセスのみが管理されます。 画像やビデオにアクセスすることはできません。

  [カメラ CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **[OneDrive のファイル同期]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスから OneDrive にファイルを同期できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[リムーバブル記憶域]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスで SD カードなどの外部記憶装置を使用できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[位置情報]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスで位置情報サービスをオンにできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[インターネット共有]** : **[ブロック]** に設定すると、デバイスでのインターネット接続の共有が禁止されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[電話のリセット]** : **[ブロック]** に設定すると、エンド ユーザーはデバイスをワイプまたは出荷時の設定にリセットできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[USB 接続]** : **[ブロック]** に設定すると、デバイスで USB 接続を介して外部記憶域装置にアクセスできなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 USB 充電はこの設定の影響を受けません。
- **[盗難防止モード**(モバイルのみ)]: **[ブロック]** に設定すると、エンド ユーザーはデバイスで盗難防止モードの設定を選択できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[Cortana]** : **[ブロック]** に設定すると、デバイスで Cortana 音声アシスタントが無効になります。 Cortana がオフの場合でも、ユーザーはデバイス上の項目を検索できます。 **[未構成]** (既定値) にすると、Cortana の使用が許可されます。
- **[音声録音** (モバイルのみ)]: **[ブロック]** に設定すると、エンド ユーザーはデバイスでデバイスのボイス レコーダーを使用できなくなります。 **[未構成]** (既定値) にすると、アプリの音声録音が許可されます。
- **[デバイス名の変更** (モバイルのみ)]: **[ブロック]** に設定すると、エンド ユーザーはデバイスの名前を変更できなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[プロビジョニング パッケージを追加する]** : **[ブロック]** に設定すると、デバイスにプロビジョニング パッケージをインストールするランタイム構成エージェントの使用が禁止されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[プロビジョニング パッケージを削除する]** : **[ブロック]** に設定すると、デバイスからプロビジョニング パッケージを削除するランタイム構成エージェントの使用が禁止されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[デバイスの検出]** : **[ブロック]** に設定すると、このデバイスは他のデバイスで検出されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[タスク スイッチャー** (モバイルのみ)]: **[ブロック]** に設定すると、デバイスでのタスクの切り替えが禁止されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[SIM カードのエラー ダイアログ** (モバイルのみ)]: **[ブロック]** に設定すると、SIM カードが検出されない場合のエラー メッセージが、デバイスに表示されなくなります。 **[未構成]** (既定値) にすると、エラー メッセージが表示されます。
- **[Ink Workspace]\(Ink ワークスペース\)** :ユーザーが Ink ワークスペースにアクセスするかどうか、アクセスする場合はその方法を選択します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Ink ワークスペースはオンになり、ユーザーはロック画面上でこれを使用できます。
  - **[ロック画面では無効]** : Ink ワークスペースが有効になり、機能がオンになります。 ただし、ユーザーは、ロック画面ではそれにアクセスできません。
  - **Disabled**:Ink ワークスペースへのアクセスを無効にします。 機能はオフになります。

  [WindowsInkWorkspace ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **[自動再展開]** : **[許可]** を選択すると、管理権限を持つユーザーは、デバイス ロック画面で **CTRL + Win + R** を使用してすべてのユーザー データとユーザー設定を削除できます。 デバイスは自動的に再構成され、管理対象に再登録されます。 **[未構成]** (既定値) では、この機能は使用できなくなります。
- **[デバイスのセットアップ中、ユーザーにネットワークへの接続を求める]** : **[必須]** を選択すると、Windows 10 のセットアップ中、[ネットワーク] ページから先に進む前にデバイスがネットワークに接続されます。 **[未構成]** (既定値) にすると、ネットワークに接続されていない場合でも、ユーザーが [ネットワーク] ページを通過することが許可されます。

  次回デバイスがワイプまたはリセットされたときに、この設定が有効になります。 その他の Intune の構成のように、構成設定を受信するには、デバイスを Intune で登録して管理する必要があります。 ただし、一度登録され、ポリシーを受信すると、デバイスをリセットにより、次の Windows のセットアップ中に設定が適用されます。

  [TenantLockdown CSP](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **[DMA]** : **[ブロック]** では、ユーザーが Windows にサインインするまで、ホット プラグ可能なすべての PCI ダウンストリーム ポートへの直接メモリ アクセス (DMA) が禁止されます。 **[有効]** (既定値) にすると、ユーザーがサインインしていない場合でも、DMA へのアクセスが許可されます。

  [DataProtection/AllowDirectMemoryAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **[タスク マネージャーからのプロセスを終了する]** :この設定により、管理者以外がタスク マネージャーを使用してタスクを終了できるかどうかが決まります。 **[ブロック]** は、標準ユーザー (管理者以外) がタスク マネージャーを使用してデバイス上でプロセスまたはタスクを終了するのを防ぎます。 **[未構成]** (既定値) は、標準ユーザーがタスク マネージャーを使用してプロセスまたはタスクを終了するのを許可します。

## <a name="locked-screen-experience"></a>ロック画面

- **[アクション センターの通知 (モバイルのみ)]** : **[ブロック]** に設定すると、デバイスのロック画面にアクション センターの通知が表示されなくなります。 **[未構成]** (既定値) にすると、ユーザーがロック画面に通知を表示するアプリを選択することが許可されます。

  [AboveLock/AllowActionCenterNotifications CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- **[ロック画面の画像の URL (デスクトップのみ)]** : Windows のロック画面の壁紙として使用する、JPG、JPEG、または PNG 形式の画像への URL を入力します。 たとえば、「`https://contoso.com/image.png`」と入力します。 この設定によって画像が固定され、後で変更することはできません。

  [Personalization/LockScreenImageUrl CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- **[ユーザーが構成可能なスクリーン タイムアウト (モバイルのみ)]** : **[許可]** を設定すると、ユーザーはスクリーン タイムアウトを構成できます。 **[未構成]** (既定値) にすると、ユーザーにこのオプションは提供されません。

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **[ロック画面での Cortana** (デスクトップのみ)]: **[ブロック]** に設定すると、デバイスがロック画面になっているときに、ユーザーは Cortana と対話できなくなります。 **[未構成]** (既定値) にすると、Cortana との対話が許可されます。

  [AboveLock/AllowCortanaAboveLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **[ロック画面でのトースト通知]** : **[ブロック]** に設定すると、デバイスのロック画面にトースト通知が表示されなくなります。 **[未構成]** (既定値) にすると、これらの通知が許可されます。

  [AboveLock/AllowToasts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **[スクリーン タイムアウト (モバイルのみ)]** :画面がロックされてから画面がオフになるまでの期間 (秒単位) を設定します。 サポートされる値は 11 から 1800 です。 たとえば、このタイムアウトを 5 分に設定するには、`300` と入力します。

  [DeviceLock/ScreenTimeoutWhileLocked CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>メッセージング

これらの設定では、[メッセージング ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[メッセージ同期 (モバイルのみ)]** : **[ブロック]** に設定すると、テキスト メッセージのバックアップと復元を実行できなくなり、Windows デバイス間でメッセージが同期されなくなります。 無効にすると、組織の管理外にあるサーバーに情報が格納されるのを回避できます。 **[未構成]** (既定値) にすると、ユーザーがこれらの設定を変更でき、メッセージの同期が許可されます。
- **[MMS (モバイルのみ]** : **[ブロック]** に設定すると、デバイスでの MMS の送受信機能が無効になります。 企業では、このポリシーを使用して、監査または管理要件の一部として、デバイスでの MMS を無効にします。 **[未構成]** (既定値) にすると、MMS の送受信が許可されます。
- **[RCS (モバイルのみ)]** : **[ブロック]** に設定すると、デバイスでのリッチ通信サービス (RCS) の送受信機能が無効になります。 企業では、このポリシーを使用して、監査または管理要件の一部として、デバイスでの RCS を無効にします。 **[未構成]** (既定値) にすると、RCS の送受信が許可されます。

## <a name="microsoft-edge-browser"></a>Microsoft Edge ブラウザー

これらの設定では、[ブラウザー ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser) が使用されます。それには、サポートされる Windows のエディションも示されています。

### <a name="use-microsoft-edge-kiosk-mode"></a>Microsoft Edge キオスク モードを使用する

利用できる設定は、選択した内容によって変化します。 次のようなオプションがあります。

- **[いいえ]** (既定値): Microsoft Edge はキオスク モードで実行されていません。 Microsoft Edge の設定はすべて、変更および構成することができます。
- **[デジタル/インタラクティブ サイネージ (シングル アプリ キオスク)]** : Windows 10 シングル アプリ キオスクのみに使用されるデジタル/インタラクティブ サイネージの Microsoft Edge キオスク モードに適用できる、Microsoft Edge 設定をフィルター処理します。 この設定を選択すると、URL の全画面表示が開き、その Web サイトのコンテンツのみが表示されます。 [デジタル署名の設定](https://docs.microsoft.com/windows/configuration/setup-digital-signage)に関するページでは、この機能に関する詳細情報を提供しています。
- **[InPrivate 公共閲覧用 (シングル アプリ キオスク)]** : Windows 10 シングル アプリ キオスクに使用される InPrivate 公共閲覧用の Microsoft Edge キオスク モードに適用できる Microsoft Edge 設定をフィルター処理します。 Microsoft Edge の複数のタブ バージョンを実行します。
- **[通常モード (マルチ アプリ キオスク)]** : 通常の Microsoft Edge キオスク モードに適用できる Microsoft Edge の設定をフィルター処理します。 すべての参照機能を使って完全版の Microsoft Edge を実行します。
- **[公共閲覧用 (マルチ アプリ キオスク)]** : Windows 10 マルチ アプリ キオスクの公共閲覧用に適用できる Microsoft Edge の設定をフィルター処理します。  Microsoft Edge InPrivate の複数のタブ バージョンを実行します。

> [!TIP]
> これらのオプションで行う内容の詳細については、[Microsoft Edge キオスク モードの構成の種類](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)に関するページを参照してください。

このデバイスの制限プロファイルは、[Windows のキオスク設定](kiosk-settings-windows.md)を使用して作成するキオスク プロファイルに直接関連付けられます。 まとめ

1. [Windows のキオスク設定](kiosk-settings-windows.md)プロファイルを作成して、キオスク モードでデバイスを実行します。 Microsoft Edge をアプリケーションとして選択し、キオスク プロファイルに Microsoft Edge キオスク モードを設定します。
2. この記事で説明されているデバイスの制限プロファイルを作成し、Microsoft Edge で許可された特定の機能と設定を構成します。 ご利用のキオスク プロファイル ([Windows のキオスク設定](kiosk-settings-windows.md)) で選択されているのと同じ Microsoft Edge キオスク モードの種類を選択してください。 

    [サポートされているキオスク モードの設定](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode)は、最適なリソースです。

> [!IMPORTANT] 
> この Microsoft Edge プロファイルをご利用のキオスク プロファイル ([Windows のキオスク設定](kiosk-settings-windows.md)) と同じデバイスに割り当ててください。

[ConfigureKioskMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>開始エクスペリエンス

- **[Microsoft Edge を開始するときに開く内容]** :Microsoft Edge を起動したときに開くページを選択します。 次のようなオプションがあります。
  - **[カスタム スタート ページ]** : スタート ページを入力します (例: `http://www.contoso.com`)。 Microsoft Edge では、入力されたスタート ページが読み込まれます。
  - **[新しいタブ ページ]** :Microsoft Edge では、 **[新しいタブの URL]** 設定に入力された URL が読み込まれます。
  - **[最後のセッションのページ]** :Microsoft Edge で最後のセッションのページが読み込まれます。
  - **[ローカル アプリのスタート ページの設定]** : Microsoft Edge の起動時に、OS で定義された既定のスタート ページが開きます。

- **[ユーザーにスタート ページの変更を許可する]** : **[はい]** (既定値) に設定すると、ユーザーはスタート ページを変更できます。 管理者は `EdgeHomepageUrls` を使用して、Microsoft Edge を開いたときに既定でユーザーに表示されるスタート ページを入力できます。 **[いいえ]** にすると、ユーザーはスタート ページを変更できなくなります。
- **[新しいタブ ページでの Web コンテンツを許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge で **[新しいタブの URL]** 設定に入力された URL が開きます。 **[新しいタブの URL]** 設定が空白の場合、Microsoft Edge で Microsoft Edge の設定に含まれている新しいタブ ページが開きます。 ユーザーはそれを変更できます。 **[いいえ]** を設定すると、Microsoft Edge で空白の新しいタブ ページが開きます。 ユーザーはそれを変更することはできません。
- **[新しいタブの URL]** : 新しいタブ ページ上で開く URL を入力します。 たとえば、「`https://www.bing.com`」や「`https://www.contoso.com`」と入力します。

- **[ホーム ボタン]** :[ホーム] ボタンを選択したときに実行される処理を選択します。 次のようなオプションがあります。
  - **[スタート ページ]** : **[Microsoft Edge を開始するときに開く内容]** 設定で選択されたオプションが開きます。
  - **[新しいタブ ページ]** : **[新しいタブの URL]** 設定に入力された URL が開きます。
  - **[[ホーム] ボタンの URL]** : 開く URL を入力します。 たとえば、「`https://www.bing.com`」や「`https://www.contoso.com`」と入力します。
  - **[[ホーム] ボタンを非表示にする]** :[ホーム] ボタンを非表示にします。
- **[ユーザーによるホーム ボタンの変更を許可する]** : **[はい]** に設定すると、ユーザーは [ホーム] ボタンを変更できます。 [ホーム] ボタンに対して管理者が行った設定は、ユーザーが行った変更でオーバーライドされます。 **[いいえ]** (既定値) にすると、管理者がホーム ボタンを構成した方法をユーザーが変更することはできなくなります。
- **[最初の実行エクスペリエンス ページの表示 (モバイルのみ)]** : **[はい]** (既定値) に設定すると、初めて使用する際の紹介ページが Microsoft Edge に表示されます。 **[いいえ]** にすると、Microsoft Edge の初回実行時に紹介ページが表示されなくなります。 この機能により、企業 (ゼロ エミッション コンフィギュレーションに登録している組織など) は、このページをブロックできます。
- **[最初の実行エクスペリエンス URL 一覧の場所** (Windows 10 Mobile のみ)]: 最初の実行ページの URL を含む XML ファイルをポイントする URL を入力します。 たとえば、「`https://www.contoso.com/sites.xml`」と入力します。

- **[アイドル時間が経過した後、ブラウザーを更新する]** :ブラウザーが更新されるまでのアイドル時間の分数を入力します (0 から 1440 分)。 既定値は `5` 分です。 `0` (ゼロ) に設定すると、ブラウザーはアイドル後も更新されません。

  この設定は、[[InPrivate 公共閲覧用 (シングル アプリ キオスク)]](#use-microsoft-edge-kiosk-mode) で実行されているときにのみ利用できます。

- **[ポップアップを許可する** (デスクトップのみ)]: **[はい]** (既定値) に設定すると、Web ブラウザーでポップアップが表示されます。 **[いいえ]** にすると、ブラウザーにポップアップ ウィンドウが表示されなくなります。
- **[Internet Explorer にイントラネット トラフィックを送信する** (デスクトップのみ)]: **[はい]** に設定すると、ユーザーは、Microsoft Edge ではなく、Internet Explorer でイントラネット Web サイトを開くことができます。 この設定は下位互換性を維持するためのものです。 **[いいえ]** (既定値) にすると、ユーザーによる Microsoft Edge の使用が許可されます。
- **[エンタープライズ モードのサイト一覧の場所** (デスクトップのみ)]: エンタープライズ モードで開く Web サイトの一覧を含む XML ファイルをポイントする URL を入力します。 この一覧はユーザーが変更できません。 たとえば、「`https://www.contoso.com/sites.xml`」と入力します。
- **[Message when opening sites in Internet Explorer]\(Internet Explorer でサイトを開くときにメッセージを表示する\)** :この設定を使用すると、Internet Explorer 11 でサイトを開く前に Microsoft Edge で通知を表示するように構成できます。 次のようなオプションがあります。
  - **[メッセージを表示しない]** : OS の既定の動作が使用され、メッセージが表示される場合も、表示されない場合もあります。
  - **[サイトが Internet Explorer 11 で開かれているというメッセージを表示する]** : IE でサイトを開くときにメッセージを表示します。 サイトが IE で開きます。 
  - **[Show message with option to open sites in Microsoft Edge]\(Microsoft Edge でサイトを開くオプションを含むメッセージを表示する\)** : Microsoft Edge でサイトを開くときにメッセージを表示します。 このメッセージには、 **[Keep going in Microsoft Edge]\(Microsoft Edge で続行する\)** リンクが含まれているため、ユーザーは IE の代わりに Microsoft Edge を選択できます。

  > [!IMPORTANT]
  > この設定では、 **[エンタープライズ モード サイト一覧の場所]** 設定と **[Internet Explorer にイントラネット トラフィックを送信する]** 設定のいずれか、または両方を使用する必要があります。

- **[Microsoft 互換性リストを許可する]** : **[はい]** (既定値) に設定すると、Microsoft 互換性リストの使用が許可されます。 **[いいえ]** にすると、Microsoft Edge で Microsoft 互換性リストは使用されなくなります。 Microsoft が提供するこのリストを使用すると、既知の互換性の問題があるサイトを Microsoft Edge で正しく表示できます。
- **[スタート ページと新しいタブ ページの事前読み込み]** : **[はい]** (既定値) に設定すると、OS の既定の動作が使用され、これらのページが事前読み込みされる可能性があります。 事前読み込みを行うと、Microsoft Edge の起動時間と新しいタブの読み込み時間が最小限に抑えられます。 **[いいえ]** にすると、Microsoft Edge でスタート ページと新しいタブ ページが事前読み込みされなくなります。
- **[Prelaunch Start pages and New Tab page]\(スタート ページと新しいタブ ページの事前起動\)** : **[はい]** (既定値) に設定すると、OS の既定の動作が使用され、これらのページが事前起動される可能性があります。 事前起動を行うと、Microsoft Edge のパフォーマンスが向上し、Microsoft Edge の起動時間が最小限に抑えられます。 **[いいえ]** にすると、Microsoft Edge でスタート ページと新しいタブ ページが事前起動されなくなります。

### <a name="favorites-and-search"></a>お気に入りおよび検索

- **[お気に入りバーを表示する]** : Microsoft Edge のページ上のお気に入りバーに対する処理を選択します。 次のようなオプションがあります。
  - **[スタート ページと新しいタブ ページ上]** : Microsoft Edge の起動時に、すべてのタブ ページにお気に入りバーが表示されます。 エンド ユーザーはこの設定を変更できます。
  - **[すべてのページ]** : すべてのページ上でお気に入りバーが表示されます。 エンド ユーザーはこの設定を変更できません。
  - **非表示**:すべてのページ上でお気に入りバーが非表示になります。 エンド ユーザーはこの設定を変更できません。
- **[お気に入りに対する変更を許可する]** : **[はい]** (既定値) に設定すると、OS の既定値が使用され、ユーザーによる一覧の変更が許可されます。 **[いいえ]** にすると、エンド ユーザーはお気に入りの一覧に対する追加、インポート、並べ替え、編集を実行できなくなります。
  - **[お気に入りの一覧]** :お気に入りのファイルの URL の一覧を追加します。 たとえば、`http://contoso.com/favorites.html` を追加します。
- **[Microsoft ブラウザー間でお気に入りを同期する** (デスクトップのみ)]: **[はい]** に設定すると、Internet Explorer と Microsoft Edge 間でお気に入りが強制的に同期されます。 お気に入りに対する追加、削除、変更、および順序変更がブラウザー間で共有されます。  **[いいえ]** (既定値) にすると、OS の既定値が使用され、ユーザーがブラウザー間でお気に入りを同期することを選択できる可能性があります。
- **[既定の検索エンジン]** :デバイス上の既定の検索エンジンを選択します。 エンド ユーザーはこの値をいつでも変更できます。 次のようなオプションがあります。
  - クライアントの Microsoft Edge の設定に指定された検索エンジン
  - Bing
  - Google
  - Yahoo
  - カスタム値: **[OpenSearch Xml URL]** に、検索エンジンの短い名前と URL が最小限含まれている XML ファイルの HTTPS URL を入力します。 たとえば、「`https://www.contoso.com/opensearch.xml`」と入力します。
- **[検索候補を表示する]** : **[はい]** (既定値) に設定すると、アドレス バーに検索語句を入力したときに、検索エンジンからサイトが提案されます。 **[いいえ]** にすると、この機能が停止されます。
- **[検索エンジンへの変更を許可する]** : **[はい]** (既定値) に設定すると、ユーザーは、Microsoft Edge で新しい検索エンジンを追加したり、既定の検索エンジンを変更したりすることができます。 **[いいえ]** を選択すると、ユーザーが検索エンジンをカスタマイズできないようにします。

  この設定は、[[通常モード (マルチ アプリ キオスク)]](#use-microsoft-edge-kiosk-mode) を実行しているときにのみ利用できます。

### <a name="privacy-and-security"></a>プライバシーとセキュリティ

- **[InPrivate ブラウズを許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge での InPrivate ブラウズが許可されます。 すべての InPrivate タブを閉じると、Microsoft Edge によってデバイスから閲覧データが削除されます。 **[いいえ]** にすると、エンド ユーザーが InPrivate 閲覧セッションを開けなくなります。
- **[閲覧履歴の保存]** : **[はい]** (既定値) に設定すると、Microsoft Edge での閲覧履歴の保存が許可されます。 **[いいえ]** にすると、閲覧履歴を保存できなくなります。
- **[終了時に閲覧データをクリアする** (デスクトップのみ)]: **[はい]** に設定すると、Microsoft Edge の終了時に履歴と閲覧データが消去されます。 **[未構成]** にすると、OS の既定値が使用され、閲覧データがキャッシュされる可能性があります。
- **[Sync browser settings between user's devices]\(ユーザーのデバイス間でブラウザーの設定を同期する\)** :デバイス間でブラウザーの設定を同期する方法を選択します。 次のようなオプションがあります。
  - **[許可]** :ユーザーのデバイス間で Microsoft Edge ブラウザーの設定を同期することを許可します
  - **[Block and enable user override]\(ブロックおよびユーザーのオーバーライドを許可\)** :ユーザーのデバイス間での Microsoft Edge ブラウザーの設定の同期をブロックします。 この設定はユーザーがオーバーライドできます。
  - **[ブロック]** :ユーザーのデバイス間で Microsoft Edge ブラウザーの設定が同期されなくなります。 この設定はユーザーがオーバーライドできません。

[Block and enable user override]\(ブロックしてユーザーによるオーバーライドを有効にする\) が選択されている場合、ユーザーが管理者による指定をオーバーライドできます。

- **[Password Manager を許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge は Password Manager を自動的に使用するようになり、ユーザーはデバイスにパスワードを保存して管理できます。 **[いいえ]** にすると、Microsoft Edge で Password Manager は使用できなくなります。
- **[Cookie]** :Web ブラウザーで Cookie を処理する方法を選択します。 次のようなオプションがあります。
  - **[許可]** :Cookie がデバイス上に保存されます。
  - **[すべての Cookie をブロックする]** :Cookie がデバイス上に保存されまません。
  - **[サード パーティの Cookie のみブロックする]** :サード パーティまたはパートナーの Cookie がデバイス上に保存されません。
- **[フォームでオートフィルを許可する]** : **[はい]** (既定値) に設定すると、ユーザーはブラウザーでオートコンプリート設定を変更でき、フォームのフィールドが自動的に設定されます。 **[いいえ]** にすると、Microsoft Edge でオートフィル機能が無効になります。
- **[トラッキング拒否ヘッダーを送信する]** : **[はい]** に設定すると、追跡情報を要求している Web サイトにトラッキング拒否ヘッダーが送信されます (推奨)。 **[いいえ]** (既定値) にすると、ヘッダーが送信されず、Web サイトによるユーザーの追跡が許可されます。 ユーザーが構成できます。
- **[WebRTC localhost IP アドレスを表示する]** : **[はい]** (既定値) に設定すると、このプロトコルを使用して電話をかけるときにユーザーの localhost IP アドレスが表示されます。 **[いいえ]** にすると、ユーザーの localhost IP アドレスが表示されなくなります。 
- **[ライブ タイル データの収集を許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge によって、[スタート] メニューにピン留めされたライブ タイルから情報が収集されます。 **[いいえ]** にすると、この情報の収集ができなくなり、それによってユーザーのエクスペリエンスが制限される場合があります。
- **[User can override certificate errors]\(ユーザーが証明書のエラーをオーバーライドできる\)** : **[はい]** (既定値) に設定すると、Secure Sockets Layer/transport Layer Security (SSL/TLS) エラーが発生している Web サイトへのユーザーのアクセスが許可されます。 **[いいえ]** にすると (セキュリティ強化のために推奨)、ユーザーが SSL または TLS エラーが発生している Web サイトにアクセスできなくなります。

### <a name="additional"></a>その他

- **[Microsoft Edge ブラウザーを許可する** (モバイルのみ)]: **[はい]** (既定値) に設定すると、モバイル デバイスで Microsoft Edge Web ブラウザーの使用が許可されます。 **[いいえ]** にすると、デバイスで Microsoft Edge を使用できなくなります。 **[いいえ]** を選択した場合、他の個々の設定はデスクトップにのみ適用されます。
- **[アドレス バーのドロップダウンを許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge のアドレス バーに候補の一覧のドロップダウンが表示されます。 **[いいえ]** にすると、Microsoft Edge で入力時にドロップダウン リスト内に候補の一覧が表示されなくなります。 **[いいえ]** を設定すると:
  - Microsoft Edge と Microsoft サービスの間のネットワーク帯域幅を最小に抑えるために役立ちます。
  - Microsoft Edge の [設定] で、 **[入力時に検索候補とおすすめサイトを表示する]** が無効になります。
- **[全画面表示モードを許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge で全画面表示モードを使用して、Web コンテンツのみを表示し、Microsoft Edge の UI を非表示にすることができます。 **[いいえ]** にすると、Microsoft Edge で全画面表示モードを使用できなくなります。
- **[About Flags ページを許可する]** : **[はい]** (既定値) に設定すると、OS の既定値が使用され、`about:flags` ページへのアクセスが許可される可能性があります。 `about:flags` ページで、ユーザーは、開発者向けの設定を変更し、試験的な機能を有効にできます。 **[いいえ]** にすると、エンド ユーザーは、Microsoft Edge で `about:flags` ページにアクセスできなくなります。
- **[開発者ツールを許可する]** : **[はい]** (既定値) に設定すると、ユーザーは、既定で、Web ページの作成とデバッグに F12 開発者ツールを使用できます。 **[いいえ]** にすると、エンドユーザーが F12 開発者ツールを使用できなくなります。
- **[JavaScript を許可する]** : **[はい]** (既定値) に設定すると、Microsoft Edge ブラウザーで、JavaScript などのスクリプトを実行できます。 **[いいえ]** にすると、ブラウザーで Java スクリプトを実行できなくなります。
- **[ユーザーは拡張機能をインストールできます]** : **[はい]** (既定値) に設定すると、エンド ユーザーは Microsoft Edge 拡張機能をデバイスにインストールできます。 **[いいえ]** にすると、このインストールを実行できなくなります。
- **[開発者用拡張機能のサイドローディングを許可する]** : **[はい]** (既定値) に設定すると、OS の既定値が使用され、サイドロードが許可される可能性があります。 サイドローディングでは、検証されていない拡張機能がインストールされて実行されます。 **[いいえ]** にすると、Microsoft Edge での**拡張機能の読み込み**機能を使用したサイドローディングは実行できなくなります。 PowerShell などの他の方法を使用した拡張機能のサイドローディングは禁止されません。
- **[必要な拡張機能]** :Microsoft Edge 内でエンド ユーザーがオフにできない拡張機能を選択します。 パッケージ ファミリ名を入力し、 **[追加]** を選択します。 ガイダンスについては、「[アプリごとの VPN のパッケージ ファミリ名 (PFN) の検索](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn)」を参照してください。

  パッケージ ファミリ名を含む CSV ファイルを**インポート**することもできます。 または、入力したパッケージ ファミリの名前を**エクスポート**します。

## <a name="network-proxy"></a>ネットワーク プロキシ

これらの設定では、[NetworkProxy ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[自動的にプロキシ設定を検出する]** : **[ブロック]** に設定すると、デバイスでのプロキシ自動構成 (PAC) スクリプトの自動検出が無効になります。 **[未構成]** (既定値) にすると、この機能が有効になります。 有効にすると、デバイスでは PAC スクリプトのパスが検索されます。
- **[プロキシ スクリプトを使う]** : **[許可]** を選択して、プロキシ サーバーを構成する PAC スクリプトへのパスを入力します。 **[未構成]** (既定値) にすると、PAC スクリプトへの URL を入力できなくなります。
  - **[セットアップ スクリプトのアドレスの URL]** :プロキシ サーバーの構成に使用する PAC スクリプトの URL を入力します。
- **[手動プロキシ サーバーを使う]** : **[許可]** を選択して、プロキシ サーバーの名前または IP アドレス、および TCP ポート番号を手動で入力します。 **[未構成]** (既定値) にすると、プロキシ サーバーの詳細を手動で入力できなくなります。
  - **[アドレス]** :プロキシ サーバーの名前または IP アドレスを入力します。
  - **[ポート番号]** :プロキシ サーバーのポート番号を入力します。
  - **[プロキシの例外]** :プロキシ サーバーを使用してはいけない URL を入力します。 各項目の区切りにはセミコロンを使用します。
  - **[ローカル アドレスにはプロキシ サーバーを使わない]** : **[未構成]** (既定値) に設定すると、イントラネットでローカル アドレスに対してプロキシ サーバーを使用できなくなります。 **[許可]** にすると、ローカル アドレスでプロキシ サーバーが使用されます。

## <a name="password"></a>パスワード

これらの設定では、[DeviceLock ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **パスワード**: エンド ユーザーがデバイスにアクセスする際に、パスワードの入力を**要求**します。 **[未構成]** (既定値) にすると、パスワードなしでのデバイスへのアクセスが許可されます。 ローカル アカウントのみに適用されます。 ドメイン アカウントのパスワードは、Active Directory (AD) および Azure AD によって構成されたままになります。

  - **[必要なパスワードの種類]** :パスワードの種類を選択します。 次のようなオプションがあります。
    - **[未構成]** :パスワードに数字と文字を含めることができます。
    - **[数字]** : パスワードを数値のみにする必要があります。
    - **[英数字]** : パスワードを数字と文字の組み合わせにする必要があります。
  - **[パスワードの最小文字数]** :最小限必要なパスワードの長さを入力します (4 から 16)。 たとえば、少なくとも 6 文字の長さのパスワードを要求するには、`6` と入力します。
  
    > [!IMPORTANT]
    > Windows デスクトップでパスワード要件が変更されると、デバイスがアイドルからアクティブに移行する次回のサインイン時にユーザーに影響します。 要件を満たすパスワードを持っているユーザーにも、パスワードの変更を求めるメッセージが表示されます。
    
  - **[デバイスがワイプされるまでのサインイン失敗回数]** :デバイスがワイプされるまでに許容される認証の失敗回数 (最大 11 回)。 入力する有効な回数は、エディションによって異なります。 [DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) は、サポートされる値の一覧を示します。 `0` (ゼロ) を使用すると、デバイスのワイプ機能が無効になる可能性があります。

    この設定も、エディションによって影響が異なります。 この設定の詳細については、[DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) に関するページをご覧ください。

  - **[画面がロックされるまでの非アクティブな最長時間 (分)]** :画面がロックされるまでのデバイスのアイドル時間の長さを入力します。
  - **[パスワードの有効期限 (日数)]** :デバイスのパスワードの変更が必要になるまでの日数を指定します (1 から 365)。 たとえば、パスワードを 90 日後に期限切れにするには、`90` と入力します。
  - **[以前のパスワードを再利用できないようにする]** :何回前までのパスワードを使用できないようにするかを入力します (1 から 24)。 たとえば、ユーザーが現在のパスワードとその前の 4 つのパスワードを新しいパスワードとして設定できないようにするには、`5` と入力します。
  - **[デバイスがアイドル状態から戻るときにパスワードを必須にする** (モバイルおよび Holographic)]: **[必須]** を選択すると、ユーザーは、アイドル状態だったデバイスのロックを解除するためにパスワードを入力する必要があります。 **[未構成]** (既定値) にすると、デバイスがアイドル状態から戻るときに、PIN もパスワードも必要ありません。
  - **[単純なパスワード]** : **[ブロック]** に設定すると、ユーザーは、`1234` や `1111` などの単純なパスワードを設定できません。 **[未構成]** にすると、ユーザーは `1234` や `1111` などのパスワードを作成できます。 この設定は、Windows ピクチャ パスワードの使用も許可またはブロックします。
- **[AADJ 中の自動暗号化]** : **[ブロック]** に設定すると、デバイスが Azure AD 参加済みの場合、使い始めるために必要なデバイスの準備ができたときに、BitLocker 自動デバイス暗号化は行われません。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 [BitLocker デバイスの暗号化](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption)を参照。

  [Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **[Federal Information Processing Standard (FIPS) ポリシー]** : **[許可]** を設定すると、Federal Information Processing Standard (FIPS) ポリシーが使用されます。これは、暗号化、ハッシュ、署名に関する米国政府標準です。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 オペレーティング システムの既定で、FIPS が使用されない可能性があります。

  [Cryptography/AllowFipsAlgorithmPolicy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **[Windows Hello デバイス認証]** : **[許可]** を設定すると、ユーザーは Windows Hello のコンパニオン デバイス (電話、フィットネス バンド、IoT デバイスなど) を使用して、Windows 10 コンピューターにサインインできます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 オペレーティング システムの既定で、Windows Hello コンパニオン デバイスが Windows で認証されない可能性があります。

  [Authentication/AllowSecondaryAuthenticationDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **[Web サインイン]** (非推奨): Windows サインインで、Security Assertion Markup Language (SAML) などの非 ADFS (Active Directory フェデレーション サービス) フェデレーション プロバイダーのサポートを有効にします。 SAML では、シングル サインオン (SSO) の操作性を提供するセキュリティで保護されたトークンを使用します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **有効**: サインインに Web 資格情報プロバイダーを使用できます。
  - **Disabled**:サインインに Web 資格情報プロバイダーを使用できません。

  この設定は、今後のリリースで削除されます。 この設定を使用しないでください。

  [Authentication/EnableWebSignIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-enablewebsignin)

- **[Azure AD テナントの優先ドメイン]** : 自分の Azure AD 組織に既存のドメイン名を入力します。 このドメイン内のユーザーがサインインする場合、ドメイン名を入力する必要はありません。 たとえば、「`contoso.com`」と入力します。 `contoso.com` ドメインのユーザーは、`abby@contoso.com` の代わりに、ユーザー名 (`abby` など) を使用してサインインできます。

  [Authentication/PreferredAadTenantDomainName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>アプリごとのプライバシー例外

"既定のプライバシー" で定義したものと異なるプライバシー動作をするアプリを追加できます。

- **[パッケージ名]** :アプリのパッケージ ファミリ名。
- **[アプリ名]** :アプリの名前。

### <a name="exceptions"></a>例外

- **[アカウント情報]** :このアプリがユーザー名、画像、およびその他の連絡先情報にアクセスできるかどうかを定義します。
- **[バックグラウンド アプリ]** :このアプリをバックグラウンドで実行できるかどうかを定義します。
- **[カレンダー]** :このアプリがカレンダーにアクセスできるかどうかを定義します。
- **[通話履歴]** :このアプリが通話履歴にアクセスできるかどうかを定義します。
- **[カメラ]** :このアプリがカメラにアクセスできるかどうかを定義します。
- **[連絡先]** :このアプリが連絡先にアクセスできるかどうかを定義します。
- **[電子メール]** :このアプリが電子メールにアクセスし、電子メールを送信できるかどうかを定義します。
- **場所**: このアプリが場所情報にアクセスできるかどうかを定義します。
- **[メッセージング]** :このアプリがテキストや MMS メッセージを読み取りまたは送信できるかどうかを定義します。
- **[マイク]** :このアプリがマイクを使用できるかどうかを定義します。
- **[モーション]** :このアプリがデバイス モーション情報にアクセスできるかどうかを定義します。
- **[通知]** :このアプリが通知にアクセスできるかどうかを定義します。
- **[電話]** :このアプリが電話にアクセスできるかどうかを定義します。
- **[無線]** :一部のアプリはデバイスで無線 (Bluetooth など) を使用してデータ送受信するため、無線をオンまたはオフにする必要があります。 このアプリが無線を制御できるかどうかを定義します。
- **[タスク]** :このアプリがタスクにアクセスできるかどうかを定義します。
- **[信頼済みデバイス]** :このアプリが、信頼済みデバイスを使用できるかどうかを選択します。 信頼済みデバイスは、既に接続済みのハードウェア、またはデバイスに付属するハードウェアです。 たとえば、テレビやプロジェクターなどを信頼済みデバイスとして使用します。
- **[Feedback and diagnostics]\(フィードバックと診断\)** :このアプリが診断情報にアクセスできるかどうかを選択します。
- **[Sync with devices]\(デバイスとの同期\)** :このアプリが、このデバイスと明示的にペアリングされていないワイヤレス デバイスと自動的に情報を共有し、同期できるかどうかを選択します。

## <a name="personalization"></a>個人設定

これらの設定では、[個人設定ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[デスクトップの背景画像の URL (デスクトップのみ)]** :Windows デスクトップの壁紙として使用する jpg、jpeg、または .png 形式の画像への URL を入力します。 ユーザーはこの画像を変更できません。 たとえば、「`https://contoso.com/logo.png`」と入力します。

## <a name="printer"></a>プリンター

- **[プリンター]** :追加されたローカル プリンターの一覧。
- **[既定のプリンター]** :既定のプリンターを設定します。
- **[User access to add new printers]\(新しいプリンターを追加するためのユーザー アクセス権\)** :ローカル プリンターの使用を許可またはブロックします。

## <a name="privacy"></a>プライバシー

これらの設定では、[プライバシー ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[入力個人設定]** : **[ブロック]** に設定すると、ディクテーション、Cortana への呼びかけ、Microsoft クラウドベースの音声認識を使用するその他のアプリで、音声を使用できなくなります。 設定が無効になり、ユーザーが設定を使用してオンライン音声認識を有効にすることはできなくなります。 **[未構成]** (既定値) にすると、ユーザーが設定を選択できます。 これらのサービスを許可した場合、サービス向上のために Microsoft によって音声データが収集される場合があります。
- **[ペアリングとプライバシーに関するユーザーの同意プロンプトの自動受け入れ]** : **[許可]** を選択すると、Windows は、アプリの実行時にペアリングとプライバシーに関する同意メッセージを自動的に受け入れることができます。 **[未構成]** (既定値) にすると、アプリの実行時にペアリングとプライバシーに関するユーザーの同意ウィンドウの自動的に受け入れることはできなくなります。
- **ユーザー アクティビティの公開**: **[ブロック]** に設定すると、アクティビティ フィードでの共有エクスペリエンスおよび最近使われたリソースの検出が禁止されます。 **[未構成]** にすると、この機能が有効になり、アプリでエンド ユーザー アクティビティを公開できます。
- **ローカル アクティビティの場合のみ**: **[ブロック]** を選択すると、ローカル アクティビティのみに基づいて、タスク スイッチャーでの共有エクスペリエンスおよび最近使われたリソースの検出が行われなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

デバイス上のすべてのアプリがアクセス可能な情報を構成できます。 また、**アプリごとのプライバシー例外**を使用して、アプリごとに例外を定義します。

### <a name="exceptions"></a>例外

- **[アカウント情報]** :このアプリがユーザー名、画像、およびその他の連絡先情報にアクセスできるかどうかを定義します。
- **[バックグラウンド アプリ]** :このアプリをバックグラウンドで実行できるかどうかを定義します。
- **[カレンダー]** :このアプリがカレンダーにアクセスできるかどうかを定義します。
- **[通話履歴]** :このアプリが通話履歴にアクセスできるかどうかを定義します。
- **[カメラ]** :このアプリがカメラにアクセスできるかどうかを定義します。
- **[連絡先]** :このアプリが連絡先にアクセスできるかどうかを定義します。
- **[電子メール]** :このアプリが電子メールにアクセスし、電子メールを送信できるかどうかを定義します。
- **場所**: このアプリが場所情報にアクセスできるかどうかを定義します。
- **[メッセージング]** :このアプリがテキストや MMS メッセージを読み取りまたは送信できるかどうかを定義します。
- **[マイク]** :このアプリがマイクを使用できるかどうかを定義します。
- **[モーション]** :このアプリがデバイス モーション情報にアクセスできるかどうかを定義します。
- **[通知]** :このアプリが通知にアクセスできるかどうかを定義します。
- **[電話]** :このアプリが電話にアクセスできるかどうかを定義します。
- **[無線]** :一部のアプリはデバイスで無線 (Bluetooth など) を使用してデータ送受信するため、無線をオンまたはオフにする必要があります。 このアプリが無線を制御できるかどうかを定義します。
- **[タスク]** :このアプリがタスクにアクセスできるかどうかを定義します。
- **[信頼済みデバイス]** :このアプリが、信頼済みデバイスを使用できるかどうかを選択します。 信頼済みデバイスは、既に接続済みのハードウェア、またはデバイスに付属するハードウェアです。 たとえば、テレビやプロジェクターなどを信頼済みデバイスとして使用します。
- **[Feedback and diagnostics]\(フィードバックと診断\)** :このアプリが診断情報にアクセスできるかどうかを選択します。
- **[デバイスとの同期]** - このアプリが、この PC、タブレット、または電話と明示的にペアリングされていないワイヤレス デバイスと自動的に情報を共有し、同期できるかどうかを定義します。

## <a name="projection"></a>プロジェクション

これらの設定では、[WirelessDisplay ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[ワイヤレス ディスプレイ受信者によるユーザー入力]** : **[ブロック]** に設定すると、ワイヤレス ディスプレイ受信者によるユーザー入力が禁止されます。 **[未構成]** (既定値) にすると、ワイヤレス ディスプレイによるキーボード、マウス、ペン、およびタッチ入力のソース デバイスへの送信が許可されます。
- **[この PC へのプロジェクション]** : **[ブロック]** に設定すると、このデバイスは他のデバイスでプロジェクション用として検出されません。 **[未構成]** (既定値) にすると、デバイスが検出可能になることが許可され、デバイスのロック画面にプロジェクションできます。
- **[ペアリングには PIN が必要]** : **[必須]** を選択すると、プロジェクション デバイスに接続するときに常に PIN の入力を要求します。 **[未構成]** (既定値) にすると、デバイスとプロジェクション デバイスのペアリングで PIN は不要になります。

## <a name="reporting-and-telemetry"></a>レポートと遠隔測定

- **[使用状況データの共有]** :送信される診断データのレベルを選択します。 次のようなオプションがあります。
  - **[未構成]** :データは共有されません。
  - **[セキュリティ]** :Windows のより強力なセキュリティ保護を維持するために必要な情報。接続されたユーザー エクスペリエンスとテレメトリ コンポーネントの設定、悪意のあるソフトウェアの削除ツール、Microsoft Defender に関するデータなどが含まれます。
  - **[基本]** : 基本的なデバイス情報。品質に関連するデータ、アプリの互換性、アプリの使用状況データ、およびセキュリティ レベルのデータが含まれます。
  - **[拡張]** : 追加の分析情報。Windows、Windows Server、System Center、およびアプリの利用状況、それらのパフォーマンス、詳細な信頼性データ、基本レベルとセキュリティ レベルの両方の情報が含まれます。
  - **[完全]** : 問題の特定に必要で、問題の修正にも役立つすべてのデータと、セキュリティ、基本、および拡張レベルのデータ。

  [システム/AllowTelemetry CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **[Send Microsoft Edge browsing data to Microsoft 365 Analytics]\(Microsoft Edge 閲覧データを Microsoft 365 Analytics に送信する\)** :この機能を使用するには、 **[使用状況データの共有]** 設定を **[拡張]** または **[Full]\(フル\)** に設定します。 この機能では、商用 ID が構成されたエンタープライズ デバイスについて、Microsoft Edge から Microsoft 365 Analytics に送信されるデータを制御します。 次のようなオプションがあります。
  - **[未構成]** :Intune では、この設定は変更または更新されません。 オペレーティング システムの既定で、閲覧履歴データが送信されない可能性があります。
  - **[Only send intranet data]\(イントラネット データのみを送信\)** :管理者がイントラネット データの履歴を送信できます。
  - **[Only send internet data]\(インターネット データのみを送信\)** :管理者がインターネット データの履歴を送信できます。
  - **[Send intranet and internet data]\(イントラネットおよびインターネット データを送信\)** :管理者がイントラネットおよびインターネット データの履歴を送信できます。

  [ブラウザー/ConfigureTelemetryForMicrosoft365Analytics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **[テレメトリ プロキシ サーバー]** :Secure Sockets Layer (SSL) 接続を使用して、接続ユーザー エクスペリエンスとテレメトリ要求を転送するプロキシ サーバーの完全修飾ドメイン名 (FQDN) または IP アドレスを入力します。 この設定の形式は、*サーバー*:*ポート*です。 指定されたプロキシが失敗した場合、またはこのポリシーを有効にするときにプロキシが入力されなかった場合は、接続ユーザー エクスペリエンスとテレメトリ データが送信されず、ローカル デバイス上に残ります。

  形式の例:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [システム/TelemetryProxy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

**[OK]** を選択して変更を保存します。

## <a name="search"></a>検索

これらの設定では、[検索ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search) が使用されます。それには、サポートされる Windows のエディションも示されています。 

- **[セーフ サーチ (モバイルのみ)]** :Cortana が検索結果でアダルト コンテンツをフィルター処理する方法を制御します。 次のようなオプションがあります。
  - **[ユーザー定義]** : エンドユーザーが自分専用の設定を選択することを許可します。
  - **[厳格]** : 成人向けコンテンツに対する最高レベルのフィルタリング。
  - **[中程度]** : 成人向けコンテンツに対する中程度のフィルタリング。 有効な検索結果はフィルター処理されません。
- **[Search で Web 結果を表示する]** : **[ブロック]** に設定すると、ユーザーは検索を実行できず、[検索] に Web 検索の結果は表示されません。 **[未構成]** (既定値) にすると、ユーザーによる Web の検索が許可され、結果がデバイスに表示されます。

## <a name="start"></a>開始

これらの設定では、[開始ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start) が使用されます。それには、サポートされる Windows のエディションも示されています。  

- **[スタート メニューのレイアウト]** :デスクトップ デバイスの [スタート] の既定レイアウトをオーバーライドし、[スタート] メニューをカスタマイズします。 アプリが一覧される順序などの使用するカスタマイズが含まれる XML ファイルをアップロードします。 入力された [スタート] メニューのレイアウトをユーザーが変更することはできません。
- **[Pin websites to tiles in Start menu]\(Web サイトを [スタート] メニューにタイルとしてピン留めする\)** :デスクトップ デバイスで Windows の [スタート] メニューにリンクとして表示される Microsoft Edge から画像をインポートします。
- **[Unpin apps from task bar]\(タスク バーからアプリをピン解除する\)** : **[ブロック]** に設定すると、ユーザーはタスク バーからアプリのピン留めを外すことができなくなります。 **[未構成]** (既定値) にすると、ユーザーがタスクバーからアプリのピン留めを外すことが許可されます。
- **[高速なユーザーの切り替え]** : **[ブロック]** に設定すると、同時にログオンしているユーザーをログオフしないで切り替えることができなくなります。 **[未構成]** (既定値) にすると、ユーザー タイルに **[ユーザーの切り替え]** が表示されます。
- **[Most used apps]\(最もよく使用されたアプリ\)** : **[ブロック]** に設定すると、最もよく使用されているアプリが [スタート] メニューに表示されなくなります。 [設定] アプリ内の対応するトグルも無効にされます。 **[未構成]** (既定値) にすると、最もよく使用されたアプリが表示されます。
- **[最近追加したアプリ]** : **[ブロック]** に設定すると、最近追加されたアプリが [スタート] メニューに表示されなくなります。 [設定] アプリ内の対応するトグルも無効にされます。 **[未構成]** (既定値) にすると、最近追加したアプリが [スタート] メニューに表示されます。
- **[スタート画面モード]** :スタート画面の表示方法を選択します。 次のようなオプションがあります。
  - **[ユーザー定義]** : 開始サイズの指定はありません。 ユーザーがサイズを設定できます。
  - **[全画面表示]** :スタート画面を全画面表示します。
  - **[非全画面表示]** : スタート画面を非全画面表示します。
- **[Recently opened items in Jump Lists]\(ジャンプ リストで最近開いたアイテム\)** : **[ブロック]** に設定すると、最近使用したジャンプ リストが [スタート] メニューおよびタスク バーに表示されなくなります。 [設定] アプリ内の対応するトグルも無効にされます。 **[未構成]** (既定値) にすると、最近開いた項目がジャンプ リストに表示されます。
- **[アプリ リスト]** :すべてのアプリ リストの表示方法を選択します。 次のようなオプションがあります。
  - **[ユーザー定義]** : 強制される設定はありません。 デバイス上にアプリの一覧を表示する方法は、ユーザーが選択します。
  - **[折りたたみ]** : すべてのアプリ リストを非表示にします。
  - **[Collapse and disable the Settings app]\(折りたたんで設定アプリを無効にする\)** : すべてのアプリ リストを非表示にして、[設定] アプリの **[スタート メニューにアプリ リストを表示する]** を無効にします。
  - **[Removes and disables the Settings app]\(削除して設定アプリを無効にする\)** : すべてのアプリ リストを非表示にして、[すべてのアプリ] ボタンを削除し、[設定] アプリの **[スタート メニューにアプリの一覧を表示する]** を無効にします。
- **[電源ボタン]** : **[ブロック]** に設定すると、[スタート] メニューに電源ボタンが表示されなくなります。 **[未構成]** (既定値) にすると、電源ボタンが表示されます。
- **[ユーザー タイル]** : **[ブロック]** に設定すると、[スタート] メニューにユーザー タイルが表示されなくなります。 **[未構成]** (既定値) にすると、ユーザー タイルが表示され、次の設定も設定されます。
  - **[ロック]** : **[ブロック]** に設定すると、[スタート] メニューのユーザー タイルに **[ロック]** オプションが表示されなくなります。 **[未構成]** (既定値) にすると、 **[ロック]** オプションが表示されます。
  - **[サインアウト]** : **[ブロック]** に設定すると、[スタート] メニューのユーザー タイルに **[サインアウト]** オプションが表示されなくなります。 **[未構成]** (既定値) にすると、 **[サインアウト]** オプションが表示されます。
- **[シャットダウン]** : **[ブロック]** に設定すると、[スタート] メニューの電源オプションに **[更新してシャットダウン]** オプションと **[シャットダウン]** オプションが表示されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[スリープ]** : **[ブロック]** に設定すると、[スタート] メニューの電源オプションに **[スリープ]** オプションが表示されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[休止状態]** : **[ブロック]** に設定すると、[スタート] メニューの電源オプションに **[休止状態]** オプションが表示されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[アカウントの切り替え]** : **[ブロック]** に設定すると、[スタート] メニューのユーザー タイルに **[アカウントの切り替え]** が表示されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[再起動オプション]** : **[ブロック]** に設定すると、[スタート] メニューの電源ボタンに **[更新して再起動]** オプションと **[再起動]** オプションが表示されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
- **[[スタート] の [ドキュメント]]** :Windows の [スタート] メニュー内にある [ドキュメント] フォルダーを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [ダウンロード]]** :Windows の [スタート] メニュー内にある [ダウンロード] フォルダーを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [エクスプローラー]]** :Windows の [スタート] メニュー内にある [エクスプローラー] を表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [ホームグループ]]** :Windows の [スタート] メニュー内にある [ホームグループ] ショートカットを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [ミュージック]]** :Windows の [スタート] メニューにある [ミュージック] フォルダーを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [ネットワーク]]** :Windows の [スタート] メニュー内にある [ネットワーク] を表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [個人用フォルダー]]** :Windows の [スタート] メニュー内にある個人用フォルダーを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [ピクチャ]]** :Windows の [スタート] メニュー内にあるピクチャ用のフォルダーを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [設定]]** :Windows の [スタート] メニュー内にある [設定] ショートカットを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。
- **[[スタート] の [ビデオ]]** :Windows の [スタート] メニュー内にあるビデオ用のフォルダーを表示または非表示にします。 次のようなオプションがあります。
  - **[未構成]** (既定値):強制される設定はありません。 ショートカットを表示するか非表示にするかは、ユーザーが選択します。
  - **[非表示にする]** :ショートカットが非表示になり、[設定] アプリの設定が無効になります。
  - **[表示]** :ショートカットが表示され、[設定] アプリの設定が無効になります。

## <a name="microsoft-defender-smart-screen"></a>Microsoft Defender SmartScreen

- **[SmartScreen for Microsoft Edge]** : **[必須]** に設定すると、Microsoft Defender SmartScreen がオフになり、ユーザーはそれをオンにすることができなくなります。 **[未構成]** (既定値) にすると、SmartScreen がオンになります。 潜在的な脅威からユーザーを保護するために役立ち、ユーザーがそれをオフにすることはできなくなります。

  Microsoft Edge では、(オンになった) Microsoft Defender SmartScreen を使用して、フィッシング詐欺にあう可能性や悪意のあるソフトウェアからユーザーを保護しています。

  [ブラウザー/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **[悪意のあるサイトへのアクセス]** : **[ブロック]** に設定すると、ユーザーは、Microsoft Defender SmartScreen フィルターの警告を無視してサイトに移動することができなくなります。 **[未構成]** (既定値) にすると、ユーザーは警告を無視してサイトに進むことができます。

  [ブラウザー/PreventSmartScreenPromptOverride CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **[確認されていないファイルのダウンロード]** : **[ブロック]** に設定すると、ユーザーは、Microsoft Defender SmartScreen フィルターの警告を無視して、確認されていないファイルをダウンロードすることができなくなります。 **[未構成]** (既定値) にすると、ユーザーは警告を無視して、確認されていないファイルのダウンロードに進むことができます。

  [ブラウザー/PreventSmartScreenPromptOverrideForFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows スポットライト

これらの設定では、[エクスペリエンス ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[Windows スポットライト]** : **[ブロック]** に設定すると、ロック画面上の Windows スポットライト、Windows のヒント、Microsoft のコンシューマー向け機能、その他の関連機能がオフになります。 デバイスからのネットワーク トラフィックを最小限に抑えることを目標とする場合は、これを **[ブロック]** に設定します。 **[未構成]** (既定値) にすると、Windows スポット ライト機能が許可され、エンド ユーザーによる制御が可能になります。 有効にすると、次の設定も、許可またはブロックできます。

  - **[ロック画面の Windows スポットライト]** : **[ブロック]** に設定すると、デバイス ロック画面上で Windows スポットライトに情報が表示されなくなります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[Windows スポットライトでのサード パーティのおすすめ]** : **[ブロック]** に設定すると、Windows スポットライトで、Microsoft が発行していないコンテンツは提案されなくなります。 **[未構成]** (既定値) にすると、Windows スポットライト機能 (ロック画面上のスポットライト、[スタート] メニューでのおすすめのアプリ、Windows のヒントなど) でのパートナーのソフトウェア発行元からのアプリとコンテンツのおすすめが許可されます。
  - **[コンシューマー向けの機能]** : **[ブロック]** に設定すると、通常はコンシューマー専用のエクスペリエンス (提案の開始、メンバーシップ通知、Out Of Box Experience 後のアプリのインストール、タイルのリダイレクトなど) がオフになります。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。
  - **[Windows のヒント]** : **[ブロック]** に設定すると、Windows のヒントのポップアップが無効になります。 **[未構成]** (既定値) にすると、Windows のヒントが表示されます。
  - **[アクション センターの Windows スポットライト]** : **[ブロック]** に設定すると、Windows スポットライト通知がアクション センターに表示されなくなります。 **[未構成]** (既定値) にすると、Windows でユーザーの生産性を向上させるために役立つアプリまたは機能を提案する通知をアクション センターに表示される可能性があります。
  - **[Windows スポットライトのパーソナル化]** : **[ブロック]** に設定すると、Windows で診断データを使用して、カスタマイズされたエクスペリエンスをユーザーに提供することができなくなります。 **[未構成]** (既定値) にすると、Microsoft が診断データを使用して、ユーザーのニーズに対応する パーソナライズされた提案、ヒント、およびWindows 製品を提供することが許可されます。
  - **[Windows へようこそのエクスペリエンス]** : **[ブロック]** に設定すると、Windows スポットライトの Windows へようこそエクスペリエンス機能がオフになります。 Windows とそのアプリに対する更新や変更があるときに、Windows へようこそエクスペリエンスが表示されることはありません。 **[未構成]** (既定値) では、新機能や更新機能に関する情報をユーザーに表示する Windows へようこそエクスペリエンスが許可されます。

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender ウイルス対策

これらの設定では、[Defender ポリシー CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender) が使用されます。それには、サポートされる Windows のエディションも示されています。

- **[リアルタイム監視]** : **[有効]** に設定すると、マルウェアやスパイウェア、その他の望ましくないソフトウェアのリアルタイム スキャンがオンになります。 ユーザーはこれをオフにすることはできません。 

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、この機能がオンになり、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowRealtimeMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **[動作の監視]** : **[有効]** に設定すると、動作の監視がオンになり、デバイス上で特定の既知のパターンで行われる疑わしい動作がチェックされます。 ユーザーは動作の監視を無効にすることはできません。 

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、動作の監視がオンになり、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowBehaviorMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **[Network Inspection System (NIS)]** :NIS は、ネットワークベースのエクスプロイトからデバイスを守るために役立ちます。 Microsoft Endpoint Protection Center にある既知の脆弱性の署名を使用して、悪意のあるトラフィックを検出してブロックします。

  **[有効]** に設定すると、ネットワークの保護とネットワークのブロックがオンになります。 ユーザーはこれをオフにすることはできません。 有効にすると、ユーザーは既知の脆弱性に接続できなくなります。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、NIS がオンになり、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/EnableNetworkProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **[Scan all downloads]\(すべてのダウンロードをスキャンする\)** : **[有効]** に設定すると、この設定がオンになり、Defender はインターネットからダウンロードされたすべてのファイルをスキャンします。 ユーザーは、この設定をオフにすることはできません。 

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、この設定がオンになり、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowIOAVProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **[Microsoft Web ブラウザーに読み込まれたスクリプトをスキャンする]** : **[有効]** に設定すると、Internet Explorer で使用されるスクリプトを Defender でスキャンできます。 ユーザーは、この設定をオフにすることはできません。 

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、この設定がオンになり、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowScriptScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **[End user access to Defender]\(Defender へのエンド ユーザー アクセス\)** : **[ブロック]** に設定すると、Microsoft Defender ユーザー インターフェイスがエンド ユーザーに対して表示されなくなります。 Microsoft Defender のすべての通知も表示されなくなります。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 設定をブロックした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、Microsoft Defender UI へのユーザー アクセスが許可され、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  この設定の変更は、エンド ユーザーの PC が次に再起動されたときに有効になります。

  [Defender/AllowUserUIAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **[セキュリティ インテリジェンスの更新間隔 (時間)]** :Defender で新しいセキュリティ インテリジェンスがチェックされる間隔を入力します (0 から 24)。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。 オペレーティング システムの既定で、8 時間ごとに更新がチェックされる可能性があります。
  - **[チェックしない]** :Defender で新しいセキュリティ インテリジェンスの更新はチェックされません。
  - **[1 - 24]** : `1` は 1 時間ごとにチェックし、 `2` は 2 時間ごとにチェックし、`24` は毎日チェックします。以下同様です。
  
  [Defender/SignatureUpdateInterval CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **[ファイルとプログラムのアクティビティを監視する]** :デバイス上のファイルとプログラムのアクティビティの監視を Defender に許可します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。 オペレーティング システムの既定で、すべてのファイルが監視される可能性があります。
  - **監視無効**
  - **すべてのファイルを監視**
  - **受信ファイルのみを監視**
  - **送信ファイルのみを監視**

  [Defender/RealTimeScanDirection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **[検疫済みマルウェアを削除するまでの日数]** :入力した日数の間、解決済みマルウェアの追跡を続けて、以前に影響を受けたデバイスを手動でチェックできるようにします。 日数を `0` に設定すると、マルウェアは検疫フォルダーに残り、自動的に削除されなくなります。 `90` に設定すると、検疫項目がシステム上に 90 日間保存された後で削除されます。

  [Defender/DaysToRetainCleanedMalware CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **[スキャン中の CPU 使用率の制限]** :スキャンに使用できる CPU の使用率を制限します (`0` から `100`)。
- **[アーカイブ ファイルをスキャンする]** : **[有効]** に設定すると、Defender が有効になり、Zip ファイルや Cab ファイルなどのアーカイブ ファイルがスキャンされます。 ユーザーは、この設定をオフにすることはできません。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、このスキャンがオンになり、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowArchiveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **[受信メール メッセージをスキャンする]** : **[有効]** に設定すると、デバイスが電子メール メッセージを受信した際に Defender が電子メール メッセージをスキャンできるようにします。 有効にすると、エンジンはメールボックスとメール ファイルを解析して、メールの本文と添付ファイルを分析します。 .Pst (Outlook)、.dbx、.mbx、MIME (Outlook Express)、BinHex (Mac) 形式をスキャンできます。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、このスキャンがオフになり、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowEmailScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **[フル スキャン中に、リムーバブル ドライブをスキャンする]** : **[有効]** に設定すると、フル スキャン中の Defender リムーバブル ドライブのスキャンがオンになります。 ユーザーは、この設定をオフにすることはできません。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、Defender は USB スティックなどのリムーバブル ドライブをスキャンできるようになり、ユーザーはこの設定を変更できます。

  クイック スキャン中でも、リムーバブル ドライブがスキャンされる場合があります。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowFullScanRemovableDriveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **[フル スキャン中に、マップされたネットワーク ドライブをスキャンする]** : **[有効]** に設定すると、マップされたネットワーク ドライブ上のファイルを Defender がスキャンできるようにします。 ドライブ上のファイルが読み取り専用である場合、Defender では、検出したマルウェアを一切削除できません。 ユーザーは、この設定をオフにすることはできません。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、この機能がオンになり、ユーザーはこれを変更できます。

  クイック スキャン中でも、マップされたネットワーク ドライブがスキャンされる場合があります。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **[ネットワーク フォルダーから開いたファイルをスキャンする]** : **[有効]** に設定すると、Defender で、ネットワーク フォルダーまたは共有ネットワーク ドライブから開かれたファイル (UNC パスからアクセスされるファイルなど) がスキャンされます。 ユーザーは、この設定をオフにすることはできません。 ドライブ上のファイルが読み取り専用である場合、Defender では、検出したマルウェアを一切削除できません。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では、OS はネットワーク フォルダーから開かれたファイルをスキャンし、ユーザーはこれを変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowScanningNetworkFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **[クラウド保護]** : **[有効]** に設定すると、Microsoft Active Protection Service で、管理対象のデバイスからマルウェア アクティビティに関する情報を受信できるようになります。 この設定はユーザーが変更できません。 

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 この設定を有効にした後、 **[未構成]** に戻した場合、Intune では、以前に構成した状態の設定が保持されます。 既定では OS により、Microsoft Active Protection Service で情報を受信できるようになり、ユーザーはこの設定を変更できます。

  Intune では、この機能はオフにされません。 無効にするには、カスタム URI を使用します。

  [Defender/AllowCloudProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **[サンプルを送信する前にユーザーに確認メッセージを表示する]** :悪意の有無を判断するために詳しい分析が必要なファイルを Microsoft に自動的に送信するかどうかを制御します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。 オペレーティング システムの既定で、安全なサンプルが自動的に送信される可能性があります。
  - **[常に確認する]**
  - **[個人データを送信する前に確認メッセージを表示する]**
  - **[データを送信しない]**
  - **[確認メッセージを表示せずにすべてのデータを送信する]** : データは自動的に送信されます。

  [Defender/SubmitSamplesConsent CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **[毎日のクイック スキャンを実行する時刻]** :毎日のクイック スキャンを実行する時刻を選択します。 **[未構成]** では毎日のスキャンは実行されません。 さらにカスタマイズが必要な場合は、 **[実行するシステム スキャンの種類]** の設定を構成します。

  [Defender/ScheduleQuickScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **[実行するシステム スキャンの種類]** :スキャンのレベルやスキャンを実行する日時など、システム スキャンをスケジュールします。 次のようなオプションがあります。
  - **[未構成]** :デバイス上でシステム スキャンをスケジュールしません。 エンド ユーザーは、デバイス上で必要なスキャンを手動で実行することができます。
  - **無効**:デバイス上で任意のシステム スキャンを無効にします。 デバイスをスキャンするパートナーのウイルス対策ソリューションを使用している場合は、このオプションを選びます。
  - **クイック スキャン**: レジストリ キーや既知の Windows スタートアップ フォルダーなど、マルウェアが登録されている可能性がある一般的な場所を調べます。
    - **[ススケジュールされた日]** : スキャンを実行する日を選びます。
    - **[スケジュールされた時刻]** : スキャンを実行する時刻を選びます。
  - **フル スキャン**:マルウェアが登録されている可能性がある一般的な場所を探し、デバイス上のすべてのファイルとフォルダーもスキャンします。
    - **[ススケジュールされた日]** : スキャンを実行する日を選びます。
    - **[スケジュールされた時刻]** : スキャンを実行する時刻を選びます。

  > [!TIP]
  > この設定は、 **[毎日のクイック スキャンを実行する時刻]** の設定と競合する可能性があります。 いくつかの推奨設定:  
  >
  > - 毎日のクイック スキャンと毎週のフル スキャンをスケジュールするには、次の操作を行います。
  >   1. **[毎日のクイック スキャンを実行する時刻]** 設定を構成します。
  >   2. フル スキャンを実行するには、 **[実行するシステム スキャンの種類]** を構成します。
  > 
  > - 1 日に 1 回だけクイック スキャンを実行する (フル スキャンなし) 場合は、次のいずれかの設定を使用します: **[毎日のクイック スキャンを実行する時刻]** 、または **[実行するシステム スキャンの種類]** 。 たとえば、毎週火曜日の午前 6 時にクイック スキャンを実行するには、 **[実行するシステム スキャンの種類]** の設定を構成します。
  > 
  > - **[実行するシステム スキャンの種類]** を **[クイック スキャン]** に設定して、同時に **[毎日のクイック スキャンを実行する時刻]** の設定を構成しないでください。 これらの設定は競合する場合があり、スキャンが実行されない可能性があります。

  [Defender/ScanParameter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/ScheduleScanDay CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/ScheduleScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **[望ましくない可能性のあるアプリケーションの検出]** :望ましくない可能性のあるアプリケーションが Windows で検出されたときの保護レベルを選択します。 次のようなオプションがあります。
  - **[未構成]** (既定値):Microsoft Defender による望ましくない可能性のあるアプリケーションの保護が無効になります。
  - **[ブロック]** :Microsoft Defender で、望ましくない可能性のあるアプリケーションが検出され、検出された項目がブロックされます。 これらの項目は、その他の脅威と共に履歴に表示されます。
  - **[監査]** : Microsoft Defender で、望ましくない可能性のあるアプリケーションが検出されますが、対策は何も行われません。 Microsoft Defender でアクションが実行されるアプリケーションに関する情報を確認できます。 たとえば、Microsoft Defender によって作成されたイベントをイベント ビューアーで検索します。

  望ましくない可能性のあるアプリの詳細については、「[Detect and block potentially unwanted applications (望ましくない可能性があるアプリケーションの検出とブロック)](https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/detect-block-potentially-unwanted-apps-windows-defender-antivirus)」をご覧ください。

  [Defender/PUAProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **[サンプル送信の同意]** :現在、この設定は影響を与えません。 この設定を使用しないでください。 今後のリリースで削除される可能性があります。

- **[On Access Protection]\(アクセス保護\)** : **[ブロック]** を選択すると、アクセスまたはダウンロードされたファイルがスキャンされなくなります。 ユーザーはこれをオンにすることはできません。

  **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。 設定をブロックした後、 **[未構成]** に戻した場合、Intune では、以前に OS で構成された状態の設定が保持されます。 既定では OS により、この機能が有効になり、ユーザーはこれを変更できます。

  Intune では、この機能はオンにされません。 有効にするには、カスタム URI を使用します。

  [Defender/AllowOnAccessProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **[検出されたマルウェアの脅威に対するアクション]** :マルウェアのスレッドの処理方法を選択します。 **[未構成]** (既定) を設定すると、Microsoft Defender により、最適なオプションが選択されます。 **[有効]** に設定した場合は、検出された脅威レベルごとに Defender によって実行されるアクションを選択します: 低、中、高、重大。 次のようなオプションがあります。
  
  - **消去**
  - **検疫**
  - **削除**
  - **許可**
  - **ユーザー定義**
  - **ブロック**

  アクションが不可能な場合は、Microsoft Defender により、脅威を確実に修復できる最適なオプションが選択されます。 

  [Defender/ThreatSeverityDefaultAction CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Windows Defender ウイルス対策の除外

除外リストを変更することで、特定のファイルを Microsoft Defender ウイルス対策のスキャンから除外できます。 **通常は、除外を適用する必要はありません**。 Microsoft Defender ウイルス対策には、既知の OS の動作と一般的な管理ファイルに基づき、自動的な除外が多数含まれています。これには、エンタープライズ管理、データベース管理、およびその他のエンタープライズのシナリオや状況に使用されるファイルなどが含まれます。

> [!WARNING]
> **除外を定義すると、Microsoft Defender ウイルス対策によって提供される保護機能が低下します**。 除外を実装することに関連するリスクを、常に評価してください。 悪意がないとわかっているファイルのみを除外してください。

- **[スキャンおよびリアルタイム保護から除外するファイルとフォルダー]** :**C:\Path** や **%ProgramFiles%\Path\filename.exe** などのファイルやフォルダーを、除外リストに 1 つ以上追加します。 これらのファイルとフォルダーは、リアルタイムまたはスケジュールされたスキャンの対象外となります。
- **[スキャンおよびリアルタイム保護から除外するファイル拡張子]** :**jpg** や **txt** などのファイル拡張子を、除外リストに 1 つ以上追加します。 これらの拡張子が付いたファイルは、リアルタイム スキャンやスケジュールされたスキャンの対象外です。
- **[スキャンとリアルタイム保護から除外するプロセス]** : **.exe**、 **.com**、 **.scr** などの種類のプロセスを、除外リストに 1 つ以上追加します。 これらのプロセスは、リアルタイム スキャンやスケジュールされたスキャンの対象外です。

## <a name="power-settings"></a>電源設定

### <a name="battery"></a>バッテリ

- **[省電力設定を有効にするバッテリ レベル]** :デバイスがバッテリ電源を使用している場合に、省電力設定を有効にするバッテリ充電レベルを入力します (0 から 100)。 バッテリ充電レベルを示すパーセント値を入力します。 既定値は 70% です。 70% に設定すると、バッテリの残量が 70% 以下になると省電力設定が有効になります。

  [Power/EnergySaverBatteryThresholdOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **[Lid close (mobile only)]\(カバーを閉じたとき (モバイルのみ)\)** :デバイスがバッテリ電源を使用している場合にカバーが閉じられたときの動作を選択します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[何もしない]** :デバイスはそのままで、バッテリ電源を使用し続けます。
  - **[スリープ]** :デバイスはスリープ モードになり、消費されるバッテリ残量は少量です。 コンピューターの電源は入っており、開かれているアプリとファイルはランダム アクセス メモリ (RAM) に格納されています。
  - **[休止状態]** :デバイスは休止モードになります。 開かれているアプリとファイルはハード ディスクに保存され、デバイスの電源が切られます。
  - **[シャットダウン]** :デバイスをシャットダウンします。 開かれているアプリとファイルは保存されずに閉じられます。

  [Power/SelectLidCloseActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **[電源ボタン]** :デバイスがバッテリ電源を使用している場合に [電源] ボタンが選択されたときの動作を選択します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[何もしない]** :デバイスはそのままで、バッテリ電源を使用し続けます。
  - **[スリープ]** :デバイスはスリープ モードになり、消費されるバッテリ残量は少量です。 コンピューターの電源は入っており、開かれているアプリとファイルはランダム アクセス メモリ (RAM) に格納されています。
  - **[休止状態]** :デバイスは休止モードになります。 開かれているアプリとファイルはハード ディスクに保存され、デバイスの電源が切られます。
  - **[シャットダウン]** :デバイスをシャットダウンします。 開かれているアプリとファイルは保存されずに閉じられます。

  [Power/SelectPowerButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **[スリープ ボタン]** :デバイスがバッテリ電源を使用している場合にスリープ ボタンが選択されたときの動作を選択します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[何もしない]** :デバイスはそのままで、バッテリ電源を使用し続けます。
  - **[スリープ]** :デバイスはスリープ モードになり、消費されるバッテリ残量は少量です。 コンピューターの電源は入っており、開かれているアプリとファイルはランダム アクセス メモリ (RAM) に格納されています。
  - **[休止状態]** :デバイスは休止モードになります。 開かれているアプリとファイルはハード ディスクに保存され、デバイスの電源が切られます。
  - **[シャットダウン]** :デバイスをシャットダウンします。 開かれているアプリとファイルは保存されずに閉じられます。

  [Power/SelectSleepButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **[ハイブリッド スリープ]** : **[無効]** に設定すると、デバイスは、バッテリ電源を使用している場合にハイブリッド スリープ モードになりません。 ハイブリッド スリープ モードでは、開かれているアプリとファイルはランダム アクセス メモリ (RAM) とハード ディスクに格納されます。 消費されるバッテリ残量は少量です。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

  [Power/TurnOffHybridSleepOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **[省電力設定を有効にするバッテリ レベル]** :デバイスが電源に接続されている場合に、省電力設定を有効にするバッテリ充電レベルを入力します (0 から 100)。 バッテリ充電レベルを示すパーセント値を入力します。 既定値は 70% です。 70% に設定すると、バッテリの残量が 70% 以下になると省電力設定が有効になります。

  [Power/EnergySaverBatteryThresholdPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **[Lid close (mobile only)]\(カバーを閉じたとき (モバイルのみ)\)** :デバイスが電源に接続されている場合にカバーが閉じられたときの動作を選択します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[何もしない]** :デバイスはそのままです。
  - **[スリープ]** :デバイスがスリープ モードになります。 コンピューターの電源は入っており、開かれているアプリとファイルはランダム アクセス メモリ (RAM) に格納されています。
  - **[休止状態]** :デバイスは休止モードになります。 開かれているアプリとファイルはハード ディスクに保存され、デバイスの電源が切られます。
  - **[シャットダウン]** :デバイスをシャットダウンします。 開かれているアプリとファイルは保存されずに閉じられます。
  
    [Power/SelectLidCloseActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **[電源ボタン]** :デバイスが電源に接続されている場合に [電源] ボタンが選択されたときの動作を選択します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[何もしない]** :デバイスはそのままです。
  - **[スリープ]** :デバイスがスリープ モードになります。 コンピューターの電源は入っており、開かれているアプリとファイルはランダム アクセス メモリ (RAM) に格納されています。
  - **[休止状態]** :デバイスは休止モードになります。 開かれているアプリとファイルはハード ディスクに保存され、デバイスの電源が切られます。
  - **[シャットダウン]** :デバイスをシャットダウンします。 開かれているアプリとファイルは保存されずに閉じられます。

  [Power/SelectPowerButtonActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **[スリープ ボタン]** :デバイスが電源に接続されている場合にスリープ ボタンが選択されたときの動作を選択します。 次のようなオプションがあります。

  - **[未構成]** (既定値):Intune では、この設定は変更または更新されません。
  - **[何もしない]** :デバイスはそのままです。
  - **[スリープ]** :デバイスがスリープ モードになります。 コンピューターの電源は入っており、開かれているアプリとファイルはランダム アクセス メモリ (RAM) に格納されています。
  - **[休止状態]** :デバイスは休止モードになります。 開かれているアプリとファイルはハード ディスクに保存され、デバイスの電源が切られます。
  - **[シャットダウン]** :デバイスをシャットダウンします。 開かれているアプリとファイルは保存されずに閉じられます。

  [Power/SelectSleepButtonActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **[ハイブリッド スリープ]** : **[無効]** に設定すると、デバイスは電源に接続されている場合にハイブリッド スリープ モードになりません。 ハイブリッド スリープ モードでは、開かれているアプリとファイルはランダム アクセス メモリ (RAM) とハード ディスクに格納されます。 **[未構成]** (既定) に設定すると、Intune では、この設定は変更または更新されません。

  [Power/TurnOffHybridSleepPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>次のステップ

各設定に関する技術的な詳細と、サポートされている Windows のエディションについては、[Windows 10 のポリシー CSP のリファレンス](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider)に関する記事をご覧ください
