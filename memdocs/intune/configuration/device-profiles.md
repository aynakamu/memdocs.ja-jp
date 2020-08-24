---
title: Microsoft Intune のデバイスの機能と設定 - Azure | Microsoft Docs
description: さまざまな Microsoft Intune デバイス プロファイルの概要。 機能、制限事項、電子メール、WiFi、VPN、教育、証明書、Windows 10 のアップグレード、BitLocker と Microsoft Defender、Windows Information Protection、管理用テンプレート、および Microsoft Endpoint Manager admin center のカスタム デバイス構成設定に関する情報が得られます。 これらのプロファイルを使用して、社内のデータとデバイスを管理および保護します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43101602defab75c15c542ec922cba6f2bf96cf0
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146322"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Microsoft Intune でデバイス プロファイルを使用してデバイスに機能と設定を適用する

Microsoft Intune には、組織内のさまざまなデバイスで有効または無効にできる設定と機能が含まれています。 これらの設定と機能は "構成プロファイル" に追加されます。 さまざまなデバイス、および iOS/iPadOS、Androidデバイス管理者、Android エンタープライズ、Windows などのさまざまなプラットフォームに対するプロファイルを作成することができます。 次に、Intune を使用して、デバイスへのプロファイルの適用 ("割り当て") を行います。

モバイル デバイス管理 (MDM) ソリューションの一部として、これらの構成プロファイルを使用してさまざまなタスクを実行します。 プロファイルの例には、次のようなものがあります。

- Windows 10 デバイスでは、Internet Explorer で ActiveX コントロールをブロックするプロファイル テンプレートを使用します。
- iOS/iPadOS および macOS デバイスでは、ユーザーが組織内の AirPrint プリンターを使用できるようにします。
- デバイス上の Bluetooth へのアクセスを許可または禁止します。
- さまざまなデバイスに企業ネットワークへのアクセスを提供する WiFi または VPN プロファイルを作成します。
- インストールのタイミングを含め、ソフトウェア更新プログラムを管理します。
- 1 つのアプリ、または多くのアプリを実行できる専用のキオスク デバイスとして、Android デバイスを実行します。

この記事では、作成できるさまざまな種類のプロファイルの概要を示します。 これらのプロファイルを使用して、デバイスで一部の機能を許可または禁止します。

## <a name="administrative-templates"></a>管理用テンプレート

[管理用テンプレート](administrative-templates-windows.md)には数百の設定が含まれており、これらを Internet Explorer、Microsoft Edge、OneDrive、リモート デスクトップ、Word、Excel、その他の Office プログラム用に構成することができます。

これらのテンプレートでは、管理者にグループ ポリシーと同様の設定の簡易ビューが提供されますが、それらは 100% クラウドベースです。

この機能では以下をサポートします。

- Windows 10 以降

## <a name="certificates"></a>証明書

[証明書](../protect/certificates-configure.md)では、デバイスに割り当てられる、信頼された証明書、SCEP 証明書、および PKCS 証明書を構成します。 これらの証明書により、WiFi プロファイル、VPN プロファイル、および電子メール プロファイルが認証されます。

この機能では以下をサポートします。

- Android デバイス管理者
- Android エンタープライズ
- iOS/iPadOS
- macOS
- Windows 8.1
- Windows 10 以降

## <a name="custom-profile"></a>カスタム プロファイル

管理者は[カスタム設定](custom-settings-configure.md)を使用して、Intune に組み込まれていないデバイス設定を割り当てることができます。 Android デバイスでは、OMA-URI 値を入力できます。 iOS/iPadOS デバイスの場合は、Apple Configurator で作成した構成ファイルをインポートできます。

この機能では以下をサポートします。

- Android デバイス管理者
- Android エンタープライズ
- iOS/iPadOS
- macOS

## <a name="delivery-optimization"></a>配信の最適化

[配信の最適化](delivery-optimization-windows.md)では、ソフトウェア更新プログラムの配信に関するエクスペリエンスを向上させることができます。 これらの設定は、 **[ソフトウェア更新プログラム]**  >  **[Windows 10 更新プログラムのリング]** 設定に置き換わるものです。

これらの設定は、ソフトウェア更新プログラムを組織内のデバイスにダウンロードする方法を制御するために使用します。 たとえば、デバイス プロファイル内で、ユーザーが自分で更新プログラムを取得できるように設定することも、配信の最適化クラウド サービスを通じて更新プログラムを取得できるように設定することもできます。

この機能では以下をサポートします。

- Windows 10 以降

## <a name="derived-credential"></a>派生資格情報

[派生資格情報](../protect/derived-credentials.md)は、認証、署名、暗号化が可能なスマート カード上の証明書です。 Intune では、これらの資格情報を使用して、アプリ、電子メール プロファイル、VPN、S/MIME、Wi-Fi への接続に使用するためのプロファイルを作成できます。

この機能では以下をサポートします。

- Android エンタープライズ
- iOS/iPadOS

## <a name="device-features"></a>デバイスの機能

[デバイスの機能](device-features-configure.md)では、AirPrint、通知、ロック画面メッセージなど、iOS/iPadOS および macOS デバイスの機能を制御します。

この機能では以下をサポートします。

- iOS/iPadOS
- macOS

## <a name="device-firmware-configuration-interface"></a>デバイス ファームウェア構成インターフェイス

[デバイス ファームウェア構成インターフェイス](device-firmware-configuration-interface-windows.md) (DFCI) を使用すると、管理者は Intune を使用して UEFI (BIOS) の設定を有効または無効にすることができます。 これらの設定を使用して、ファームウェア レベルでセキュリティを強化します。通常は、悪意のある攻撃に対する回復力が高くなります。

この機能では以下をサポートします。

- サポートされているファームウェアでの Windows 10 1809 以降

## <a name="device-restrictions"></a>デバイスの制限

[デバイスの制限](device-restrictions-configure.md)は、セキュリティ、ハードウェア、データの共有など、デバイス上の設定を制御します。 たとえば、iOS/iPadOS デバイス ユーザーにデバイスのカメラの使用を禁じるデバイスの制限プロファイルを作成できます。 

この機能では以下をサポートします。

- Android デバイス管理者
- Android エンタープライズ
- iOS/iPadOS
- macOS
- Windows 10 以降
- Windows 10 Team

## <a name="domain-join"></a>ドメイン参加

[ドメイン参加](domain-join-configure.md)では、オンプレミスの Active Directory ドメインの情報が構成されます。 この情報は、Windows Autopilot と Intune を使用してプロビジョニングされるときにハイブリッド Azure AD 参加済みデバイスに展開されます。 このプロファイルでは、参加するドメインと OU がデバイスに通知されます。

この機能では以下をサポートします。

- Windows 10 以降

## <a name="edition-upgrade-and-mode-switch"></a>エディションのアップグレードとモードの切り替え

[Windows 10 エディションのアップグレード](edition-upgrade-configure-windows-10.md)は、Windows 10 のいずれかのバージョンを実行するデバイスを自動的に新しいエディションにアップグレードします。

この機能では以下をサポートします。

- Windows 10 以降

## <a name="education"></a>Education

[教育設定 - Windows 10](education-settings-configure.md) では、[Windows テスト アプリ](https://docs.microsoft.com/education/windows/take-tests-in-windows-10)のオプションを構成します。 これらのオプションを構成するとき、テストが完了するまで他のアプリをデバイスで実行できません。

[教育設定 - iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) では、iOS/iPadOS Classroom アプリを使用し、教室で学習を指導し、生徒のデバイスを操作します。 多数の学生が 1 台のデバイスを共有できるように iPad デバイスを構成できます。

## <a name="email"></a>電子メール

[電子メールの設定](email-settings-configure.md)では、デバイス上の Exchange ActiveSync 電子メール設定の作成、割り当て、監視を行います。 電子メール プロファイルにより、一貫性の確保とサポート負荷の軽減が可能になり、エンド ユーザーは自分では何の設定もせずに個人デバイスで会社の電子メールにアクセスできるようになります。 

この機能では以下をサポートします。

- Android デバイス管理者
- Android エンタープライズ
- iOS/iPadOS
- Windows 10 以降

## <a name="endpoint-protection"></a>エンドポイント保護

[Endpoint Protection](../protect/endpoint-protection-configure.md) では、Windows 10 デバイス用の BitLocker および Microsoft Defender の設定が構成されます。 また、macOS デバイスでファイアウォール、ゲートウェイ、その他のリソースを構成します。

Microsoft Defender Advanced Threat Protection (WDATP) と Microsoft Intune をオンボードするには、[モバイル デバイス管理ツール (MDM) を使用したエンドポイントの構成](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm)に関する記事を参照してください。

この機能では以下をサポートします。

- macOS
- Windows 10 以降

## <a name="esim-cellular---public-preview"></a>eSIM 携帯ネットワーク - パブリック プレビュー

管理者は [eSIM 携帯電話プロファイル](esim-device-configuration.md)を使用して、インターネットおよびデータ アクセスに関する、マネージド デバイスの携帯データ通信プランを構成できます。 携帯電話会社からアクティブ化コードを取得した後、Intune を使用して、このアクティブ化コードをインポートし、eSIM 対応デバイスに割り当てます。

この機能では以下をサポートします。

- Windows 10 Fall Creators Update 以降

## <a name="extensions"></a>の拡張

[macOS のシステム拡張機能とカーネル拡張機能](kernel-extensions-overview-macos.md)を使用することで、管理者はオペレーティング システムのネイティブ機能を拡張する機能やプログラムを追加できます。 これらの設定を、特定の開発者またはパートナーからのすべての拡張機能を信頼するように構成するか、あるいは特定の拡張機能を許可するように構成します。

この機能では以下をサポートします。

- macOS

## <a name="identity-protection"></a>ID 保護

Windows 10 デバイス上の Windows Hello for Business エクスペリエンスは、[ID 保護](../protect/identity-protection-configure.md)により制御されます。 この設定を構成し、Windows Hello for Business をユーザーやデバイスが利用できるようにし、デバイスの PIN とジェスチャの要件を指定します。  

この機能では以下をサポートします。  

- Windows 10 以降
- Windows Holographic for Business  

## <a name="kiosk"></a>キオスク

[キオスク設定](kiosk-settings.md)プロファイルでは、1 つのアプリを実行するようにデバイスを構成することも、多数のアプリを実行するようにデバイスを構成することもできます。 スタート メニューや Web ブラウザーなど、その他の機能もキオスクでカスタマイズできます。

この機能では以下をサポートします。

- Windows 10 以降

キオスク設定は、[Android](device-restrictions-android.md#kiosk)、[Android エンタープライズ](device-restrictions-android-for-work.md#device-experience)、および [iOS/iPadOS](device-restrictions-ios.md#kiosk) 用のデバイス制限としても使用できます。

## <a name="mx-profile-zebra"></a>MX プロファイル (Zebra)

[モビリティ拡張機能 (MX)](android-zebra-mx-overview.md) は、Zebra デバイスに固有の設定をカスタマイズしたり、追加したりする目的で、組み込みの Intune 設定で拡張されます。 Zebra デバイスは通常、工場の生産現場や小売環境で使用されます。 Zebra デバイスが大量にある場合、Intune を利用し、デバイスを構成し、管理できます。

この機能では以下をサポートします。

- Android デバイス管理者

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

[Microsoft Defender Advanced Threat Protection (ATP)](../protect/advanced-threat-protection.md) は、デバイスを監視し、保護できるように Intune と統合されています。 リスク レベルを設定し、デバイスがそのレベルを超えた場合の動作を決定します。 条件付きアクセスと組み合わせると、組織内の悪意のあるアクティビティを防ぐことができます。

この機能では以下をサポートします。

- Windows 10 以降

## <a name="oemconfig"></a>OEMConfig

Android Enterprise デバイスでは、[OEMConfig](android-oem-configuration-overview.md) は、OEM (相手先ブランド供給) と EMM (エンタープライズ モビリティ管理) で、OEM 固有の機能を標準化された方法で構築してサポートできるようにする標準です。 OEMConfig を使用して、OEM で固有の管理機能を定義するスキーマを作成し、それを Google Play にアップロードされるアプリに埋め込みます。 Intune でアプリからスキーマが読み取られ、Intune 管理者がスキーマの設定を構成できます。

この機能では以下をサポートします。

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>Powershell スクリプト

[PowerShell スクリプト](../apps/intune-management-extension.md)では、Intune 管理拡張機能を使用して PowerShell スクリプトが Intune にアップロードされた後、それらのスクリプトがデバイス上で実行されます。 この拡張機能を使用するために必要なもの、それらを Intune に追加する方法、およびその他の重要な情報も確認してください。

この機能では以下をサポートします。

- Windows 10 以降
- Windows Holographic for Business

## <a name="preference-file"></a>設定ファイル

macOS デバイスの[設定ファイル](preference-file-settings-macos.md)には、アプリに関する情報が含まれます。 たとえば、設定ファイルを使用して、Web ブラウザーの設定の制御、アプリのカスタマイズなどを行うことができます。

この機能では以下をサポートします。

- macOS

## <a name="shared-multi-user-device"></a>共有のマルチ ユーザー デバイス

[Windows 10](shared-user-device-settings-windows.md) および [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) には、複数のユーザーが使用するデバイス (共有デバイスや共有 PC ともいう) を管理するための設定が含まれます。 ユーザーがデバイスにサインインするときに、そのユーザーがスリープ オプションを変更できるようにするか、デバイス上にファイルを保存できるようにするかを選択します。 また、領域を節約するために、Windows HoloLens デバイスから非アクティブな資格情報を削除するプロファイルを作成することもできます。

これらの共有のマルチ ユーザー デバイス設定では、管理者はデバイスの一部の機能を制御し、Intune を使用してその共有デバイスを管理することができます。

この機能では以下をサポートします。

- Windows 10 以降
- Windows Holographic for Business

## <a name="update-policies"></a>更新ポリシー

[iOS/iPadOS 更新ポリシー](../protect/software-updates-ios.md)には、iOS/iPadOS デバイスにソフトウェア更新プログラムをインストールするための iOS/iPadOS ポリシーを作成し、割り当てる方法が示されます。 インストールの状態を確認することもできます。

Windows デバイスの更新プログラム ポリシーについては、[配信の最適化](delivery-optimization-windows.md)に関するページを参照してください。 

この機能では以下をサポートします。

- iOS/iPadOS

## <a name="vpn"></a>VPN

[VPN 設定](vpn-settings-configure.md)は、VPN プロファイルを組織内のユーザーとデバイスに割り当て、社内ネットワークに簡単かつ安全に接続できるようにします。 

仮想プライベート ネットワーク (VPN) を使用すると、会社のユーザーが社内ネットワークにリモート アクセスする際にセキュリティで保護することができます。 デバイスは VPN 接続プロファイルを使用して VPN サーバーとの接続を開始します。 

この機能では以下をサポートします。 

- Android デバイス管理者
- Android エンタープライズ
- iOS/iPadOS
- macOS
- Windows 8.1
- Windows 10 以降

## <a name="wi-fi"></a>Wi-Fi

[Wi-Fi 設定](wi-fi-settings-configure.md)は、ユーザーとデバイスにワイヤレス ネットワーク設定を割り当てます。 Wi-Fi プロファイルを割り当てると、ユーザーは自分でプロファイルを構成することなく、会社の Wi-Fi にアクセスできます。 

この機能では以下をサポートします。

- Android デバイス管理者
- Android エンタープライズ
- iOS/iPadOS
- macOS
- Windows 8.1 (インポートのみ)
- Windows 10 以降

## <a name="wired-networks"></a>有線ネットワーク

[有線ネットワーク](wired-networks-configure.md)では、macOS デスクトップ コンピューター用に 802.1x の有線接続を作成し、管理できます。 自分のプロファイルでネットワーク インターフェイスを選択し、承認された EAP タイプを選択し、PKCS 証明書や SCEP 証明書など、サーバー信頼設定を入力します。

プロファイルを割り当てると、macOS デスクトップ ユーザーは自分でプロファイルを構成することなく、会社の有線ネットワークにアクセスできます。

この機能では以下をサポートします。

- macOS

## <a name="zebra-mobility-extensions-mx"></a>Zebra モビリティ拡張 (MX)

管理者は [Zebra モビリティ拡張 (MX)](android-zebra-mx-overview.md) を使用して、Intune で Zebra デバイスを使用および管理できます。 設定で StageNow プロファイルを作成してから、Intune を使用して Zebra デバイスにこれらのプロファイルを割り当ておよび展開することができます。 [StageNow ログと一般的な問題](android-zebra-mx-logs-troubleshoot.md)に関する説明は、プロファイルのトラブルシューティング用の優れたリソースなので、StageNow を使用する際にはいくつかの潜在的な問題を参照してください。

この機能では以下をサポートします。

- Android デバイス管理者 (モビリティ拡張機能)

## <a name="manage-and-troubleshoot"></a>管理とトラブルシューティング

[プロファイルの管理](device-profile-monitor.md)に関する説明では、デバイスの状態や割り当てられているプロファイルの確認方法を説明しています。 競合を起こした設定と、これらの設定を含むプロファイルを確認することによって、競合も解決できます。 [一般的な問題と解決策](device-profile-troubleshoot.md)に関する説明は、管理者がプロファイルを操作するのに役立ちます。 プロファイルを削除した場合の動作や、デバイスに通知が送信される原因などについて説明しています。

## <a name="next-steps"></a>次のステップ

プラットフォームを選択し、操作を開始します。
