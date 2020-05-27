---
title: Intune で Sophos Mobile を使用する
titleSuffix: Intune on Azure
description: Microsoft Intune で Sophos Mobile ソリューションを使用し、モバイル デバイスから会社のリソースへのアクセスを制御する方法。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: be5cf3d0ba83fe1027dcec9dcde50257e30b7c47
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988213"
---
# <a name="sophos-mobile-threat-defense-connector-with-intune"></a>Sophos Mobile Threat Defense コネクタと Intune
モバイル デバイスからの会社のリソースへのアクセスは、Microsoft Intune に統合する Mobile Threat Defense (MTD) ソリューションである Sophos Mobile が実行するリスク評価に基づく条件付きアクセスを利用して制御できます。 リスクは、Sophos Mobile アプリを実行するデバイスが収集した製品利用統計情報に基づいて評価されます。
条件付きアクセス ポリシーは、Intune のデバイス コンプライアンス ポリシーを使用して有効にする Sophos Mobile でのリスクの評価に基づいて構成できます。これを使用すると、検出された脅威に基づき、準拠していないデバイスが企業リソースにアクセスするのを許可または拒否できます。

> [!NOTE]
> この Mobile Threat Defense ベンダーは、未登録のデバイスではサポートされていません。

## <a name="supported-platforms"></a>[サポートされているプラットフォーム]

- Android 5.0 以降
- iOS 11.0 以降

## <a name="prerequisites"></a>[前提条件]

- Azure Active Directory Premium
- Microsoft Intune サブスクリプション
- Sophos Mobile Threat Defense サブスクリプション

詳細については、[Sophos の Web サイト](https://www.sophos.com/products/mobile-control.aspx)を参照してください。

## <a name="how-do-intune-and-sophos-mobile-help-protect-your-company-resources"></a>Intune と Sophos Mobile が会社のリソースを保護する方法

Android、iOS/iPadOS 用の Sophos Mobile アプリは、ファイル システム、ネットワーク スタック、デバイス、アプリケーション テレメトリを可能な限り記録し、Sophos Mobile クラウド サービスにテレメトリ データを送信し、モバイル デバイスの脅威に対するリスクを評価します。

Intune デバイス コンプライアンス ポリシーには、Sophos Mobile でのリスクの評価に基づく、Sophos Mobile Threat Defense のルールが含まれています。 このルールを有効にすると、Intune は、有効にされたポリシーに基づいてデバイスの準拠状態を評価します。 デバイスが準拠していないことが判明した場合、ユーザーは Exchange Online や SharePoint Online などの会社リソースへのアクセスをブロックされます。 また、ユーザーは、デバイスにインストールされている Sophos Mobile アプリから、問題を解決して会社のリソースへのアクセスを回復するための案内を受け取ります。  

## <a name="sample-scenarios"></a>サンプル事例

一般的なシナリオを次に示します。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいてアクセスを制御する

マルウェアなどの悪意のあるアプリがデバイスで検出されると、脅威が解決されるまで、デバイスで次の行為が禁止されます。

- 会社の電子メールに接続する
- OneDrive for Work アプリを使用して会社のファイルを同期する
- 会社のアプリにアクセスする

*悪意のあるアプリが検出されたときにブロックする*:

![検出された悪意のあるアプリの概念図](./media/sophos-mtd-connector/sophos-malicious-apps-blocked.png)  

*修復するとアクセス権が付与される*:  
![修復後に付与されたアクセス権の概念図](./media/sophos-mtd-connector/sophos-malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する

中間者攻撃など、ネットワークに対する脅威を検出し、デバイスのリスクに基づいて Wi-Fi ネットワークへのアクセスを保護します。  

*Wi-Fi 経由のネットワーク アクセスをブロックする*:  
![Wi-Fi 経由のネットワーク アクセスをブロックする](./media/sophos-mtd-connector/sophos-network-wifi-blocked.png)

*修復するとアクセス権が付与される*:   
![修復するとアクセス権が付与される](./media/sophos-mtd-connector/sophos-network-wifi-unblocked.png)  

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいて SharePoint Online へのアクセスを制御する

中間者攻撃攻撃など、ネットワークに対する脅威を検出し、デバイスのリスクに基づいて会社内のファイルの同期を阻止します。  

*ネットワークの脅威が検出されたときに SharePoint Online をブロック*:

![ネットワークの脅威が検出されたときに SharePoint Online をブロック](./media/sophos-mtd-connector/sophos-network-spo-blocked.png)  

*修復するとアクセス権が付与される*:

![SharePoint で修復時にアクセス権を付与する例](./media/sophos-mtd-connector/sophos-network-spo-unblocked.png)  

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Sophos Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/sophos-mtd-connector/sophos-mobile-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/sophos-mtd-connector/sophos-mobile-app-policy-remediated.png)
-->

## <a name="next-steps"></a>次のステップ

- [Sophos を Intune と統合する](sophos-mtd-connector-integration.md)
- [Sophos アプリを設定する](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Sophos デバイス コンプライアンス ポリシーを作成する](mtd-device-compliance-policy-create.md)
- [Sophos MTD コネクタを有効にする](mtd-connector-enable.md)
