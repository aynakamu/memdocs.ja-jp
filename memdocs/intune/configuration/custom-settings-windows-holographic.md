---
title: カスタム設定 - Windows Holographic for Business デバイス- Microsoft Intune | Microsoft Docs
description: カスタム プロファイルを追加または作成して、Microsoft Hololens など、Microsoft Intune で Windows Holographic for Business を実行しているデバイスに対して OMA-URI 設定を使用します。 AllowFastReconnect、AllowVPN、AllowUpdateService、UpdateServiceURL、RequireUpdatesApproval、ApprovedUpdates、および ApplicationLaunchRestrictions ポリシー構成サービス プロバイダー (CSP) の設定を行うことができます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.article: article
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43199009740f259c6a6484e455b0205da76492ba
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084044"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>Intune で Windows Holographic for Business デバイス用のカスタム設定を使用する

Microsoft Intune では、"カスタム プロファイル" を使用して Windows Holographic for Business デバイス用のカスタム設定を追加または作成できます。 カスタム プロファイルは Intune の機能です。 Intune に組み込まれていないデバイスの設定と機能を追加するように設計されています。

Windows Holographic for Business のカスタム プロファイルでは、Open Mobile Alliance Uniform Resource Identifier (OMA-URI) 設定を使って、さまざまな機能を構成します。 通常、これらの設定は、デバイスの機能を制御するためにモバイル デバイスの製造元によって使われます。

Windows Holographic for Business では、構成サービス プロバイダー (CSP) の多くの設定を利用できます。 CSP の概要については、「[構成サービス プロバイダー (CSP) の概要 (IT 担当者向け)](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers)」をご覧ください。 Windows Holographic で特定の CSP がサポートされているかどうかについては、「[CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens)」(Windows Holographic でサポートされている CSP) をご覧ください。

特定の設定を探している場合、[Windows Holographic for Business デバイス制限プロファイル](device-restrictions-windows-holographic.md)には多くの組み込み設定が含まれることに留意してください。 そのため、カスタム値の入力は必要ない場合があります。

この記事では、Windows Holographic for Business デバイス用のカスタム プロファイルを作成する方法を示します。 推奨される OMA-URI 設定の一覧も含まれます。

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次の設定を入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、適切なプロファイル名は **Hololens カスタム プロファイル**です。
    - **説明**:設定の概要および他の重要な詳細がわかる説明を入力します。
    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイルの種類]** : **[カスタム]** を選択します。

4. **[OMA-URI のカスタム設定]** で、 **[追加]** を選択します。 次の設定を入力します。

    - **名前**:OMA-URI 設定の一意の名前を入力すると、設定リスト内で容易に識別できます。
    - **説明**:設定の概要および他の重要な詳細がわかる説明を入力します。
    - **[OMA-URI]** (大文字と小文字を区別):設定として使用する OMA-URI を入力します。
    - **[データ型]** :この OMA-URI の設定に使用するデータ型を選択します。 次のようなオプションがあります。

        - 文字列型
        - 文字列 (XML ファイル)
        - 日付と時刻
        - 整数型
        - 浮動小数点
        - ブール型
        - Base64 (ファイル)

    - **[値]** :入力した OMA-URI に関連付けるデータ値を入力します。 値は、選択したデータ型に依存します。 たとえば、 **[日付と時刻]** を選択した場合は、日付の選択から値を選択します。

    設定を何か追加した後は、 **[エクスポート]** を選択できます。 **[エクスポート]** では、追加した値の一覧がコンマ区切り値 (.csv) ファイルで作成されます。

5. **[OK]** を選択して変更を保存します。 必要に応じて他の設定の追加を続けます。
6. 終わったら、 **[OK]**  >  **[作成]** の順に選択して Intune プロファイルを作成します。 完了すると、プロファイルが **[デバイス - 構成プロファイル]** の一覧に表示されます。

## <a name="recommended-custom-settings"></a>推奨されるカスタム設定

次の設定は、Windows Holographic for Business を実行しているデバイスにも役立ちます。

### <a name="allowfastreconnect"></a>[AllowFastReconnect](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|整数型<br/>0: 許可しません<br/>1: 許可します (既定)|

### <a name="allowupdateservice"></a>[AllowUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|整数型<br/>0: 更新サービスは許可されません <br/>1: 更新サービスは許可されます (既定)。|

### <a name="allowvpn"></a>[AllowVPN](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|整数型<br/>0: 許可しません<br/>1: 許可します (既定)|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|この設定は、RS5 (ビルド 17763) 以前で使用できます。 19H1 (ビルド 18362) 以降では、[Windows Update for Business](../protect/windows-update-for-business-configure.md) を使用します。<br/><br/>整数型<br/>0: 構成されていません デバイスは、適用可能なすべての更新プログラムをインストールします。<br/>1: デバイスは、適用可能で、[承認された更新プログラム] リストに表示される更新プログラムのみをインストールします。 展開前にテストが必要な場合など、IT 部門がデバイス上の更新プログラムの展開を制御する場合は、このポリシーを 1 に設定します。|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Integer 0-23、ここで 0=12AM および 23=11PM<br/>既定値は 3 です。|

### <a name="updateserviceurl"></a>[UpdateServiceURL](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|この設定は、RS5 (ビルド 17763) 以前で使用できます。 19H1 (ビルド 18362) 以降では、[Windows Update for Business](../protect/windows-update-for-business-configure.md) を使用します。<br/><br/>文字列型<br/>URL: デバイスは、指定された URL にある WSUS サーバーから更新プログラムを確認します。<br/>未構成: デバイスは、Microsoft Update から更新プログラムを確認します。|

### <a name="approvedupdates"></a>[ApprovedUpdates](https://docs.microsoft.com/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**重要**<br/>管理者は、エンド ユーザーの代わりに更新プログラムの EULA を読み、同意する必要があります。 この手順を怠ると、法律または契約上の義務に違反することになります。|エンド ユーザーの代理で行う更新プログラムの承認および EULA 同意のためのノード。<br/><br/>詳細については、「[Update CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp)」(CSP の更新) を参照してください。|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**重要**<br/>AppLocker CSP の記事では、エスケープされた XML の例を使用しています。 Intune カスタム プロファイルを含む設定を構成するには、プレーン XML を使用する必要があります。|文字列型<br/>詳細については、「[AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)」を参照してください。|

### <a name="deletionpolicy"></a>[DeletionPolicy](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|整数型<br/>0 - デバイスが現在アクティブなユーザーがいない状態に戻るとすぐに削除します<br/>1 - ストレージ容量のしきい値に達したときに削除します (既定)<br/>2 - ストレージ容量のしきい値とプロファイルの非アクティブな時間のしきい値の両方に達したときに削除します|

### <a name="enableprofilemanager"></a>[EnableProfileManager](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|ブール型<br/>True - 有効<br/>False - 無効 (既定)|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|整数型<br/>既定値は 30 です。|


### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|整数型<br/>既定値は 25 です。|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|データ型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|整数型<br/>既定値は 50 です。|

## <a name="find-the-policies-you-can-configure"></a>構成できるポリシーを見つける

「[CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens)」(Windows Holographic でサポートされている CSP) で、Windows Holographic によってサポートされているすべての構成サービス プロバイダー (CSP) の完全な一覧がわかります。 Windows Holographic のバージョンによっては、一部の設定に互換性がありません。 「[CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens)」 (Windows Holographic でサポートされている CSP) の表に、各 CSP でサポートされているバージョンが一覧表示されます。

また、「[CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens)」(Windows Holographic でサポートされている CSP) に一覧表示されているすべての設定が Intune でサポートされているわけではありません。 Intune で必要な設定がサポートされているかどうかを確認するには、その設定の記事を開きます。 各設定ページには、サポートされている操作が示されます。 Intune で利用するには、その設定で**追加**操作または**置換**操作がサポートされている必要があります。

## <a name="next-steps"></a>次のステップ

プロファイルは作成されましたが、まだ何も行われていません。 次に、[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Windows 10 デバイスでカスタム プロファイル](custom-settings-windows-10.md)を作成します。
