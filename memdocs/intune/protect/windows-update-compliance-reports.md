---
title: Microsoft Intune で Windows 更新プログラムの Update Compliance レポートを使用する
titleSuffix: Microsoft Intune
description: OMS Update Compliance を使用して、Intune で展開する Windows Updates のレポート データを表示します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4ef3a4c2ba539cc507ef413a4648b42e246b11d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990907"
---
# <a name="intune-compliance-reports-for-updates"></a>更新プログラムに関する Intune コンプライアンス レポート

Intune を使用して Windows 10 デバイスに Windows の更新プログラムを展開する場合は、Intune を使用するか、*Update Compliance* と呼ばれる無料のソリューションを使用して、更新プログラムのコンプライアンスについて詳細を表示できます。 Update Compliance は Microsoft Operations Management Suite (OMS) の一部です。

## <a name="use-intune"></a>Intune を使用する

構成済みの Windows 10 更新プログラム リングの展開状態に関するポリシー レポートを確認するには、次の操作を行います。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[概要]**  >  **[ソフトウェアの更新状態]** を選択します。 割り当てたすべての更新プログラム リングの状態に関する一般的な情報を表示することができます。

3. 追加の詳細を表示するには、 **[モニター]** を選択します。 次に、 **[ソフトウェア更新プログラム]** の下にある **[更新プログラムごとのリングの展開の状態]** を選択し、確認する展開リングを選択します。

   **[監視]** セクションで、更新プログラム リングの詳細情報を表示するレポートを以下から選択します。

   - **[デバイスの状態]** - デバイスの構成の状態が表示されます。詳しくは、「[deviceConfigurationDeviceStatus の更新]( https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0)」をご覧ください。

   - **[ユーザーの状態]** - ユーザー名、状態、最終レポート日が表示されます。詳しくは、「[deviceConfigurationUserStatuses のリスト](https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0)」をご覧ください。

   - **[End-user update status] (エンドユーザーの更新状態)** - Windows デバイスの更新状態が表示されます。詳しくは、[windowsUpdateState](https://docs.microsoft.com/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta) に関するページをご覧ください。

## <a name="use-update-compliance"></a>Update Compliance を使用する

Windows 10 更新プログラム ロールアウトを監視するには、[Update Compliance](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor) を使用します。 Update Compliance は、Azure portal を介して提供され、[前提条件](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites)を満たすデバイスでは無料で使用できます。  

このソリューションを使用する場合は、更新プログラムのコンプライアンス対応を報告する任意の Intune マネージド Windows 10 デバイスに商用 ID を展開します。  

Intune で、カスタム ポリシーの OMA-URI 設定を使用して、商用 ID を構成します。 「[Intune で Windows 10 デバイス用のカスタム設定を使用する](../configuration/custom-settings-windows-10.md)」を参照してください。

商用 ID を構成するための OMA-URI (大文字と小文字を区別する) パスは、 *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID* です。

たとえば、 **[OMA-URI 設定の追加または編集]** で次の値を使用できます。

- **設定名**:Windows Analytics の商用 ID
- **設定の説明**:Windows Analytics ソリューションの商用 ID を構成
- **OMA-URI** (大文字と小文字を区別): . *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*
- **データ型**:文字列型
- **値**:\<OMS ワークスペースの Windows 利用統計情報に示された GUID を使用>

> [!NOTE]
> MS DM サーバーに関する詳細については、「[DMClient 構成サービス プロバイダー (CSP)]( https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp)」を参照してください。

## <a name="next-steps"></a>次のステップ

[Intune でのソフトウェア更新プログラムの管理](windows-update-for-business-configure.md)
