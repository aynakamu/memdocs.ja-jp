---
title: Microsoft Intune を使用した Symantec コネクタ
titleSuffix: Microsoft Intune
description: モバイル デバイスから会社のリソースへのアクセスを制御するための Intune と Symantec Endpoint Protection Mobile の統合について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: df4ce3f6-a093-432c-ab86-7a83865e389e
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6f8f3cf9ced5b613323093ed2baafcf65667997
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80275086"
---
# <a name="symantec-endpoint-protection-mobile-connector"></a>Symantec Endpoint Protection Mobile コネクタ

Microsoft Intune に統合された Mobile Threat Defense ソリューションである Symantec Endpoint Protection Mobile (SEP Mobile) によって実行されるリスク評価に基づき、条件付きアクセスを利用し、モバイル デバイスから会社のリソースへのアクセスを制御できます。 リスクは、SEP Mobile を実行するデバイスから収集される次のような製品利用統計情報に基づいて評価されます。

- 物理的防御

- ネットワーク防御

- アプリケーション防御

- 脆弱性防御

Intune デバイス コンプライアンス ポリシーで SEP Mobile のリスク評価を有効にした後、条件付きアクセスのポリシーを使って、検出された脅威に基づき、非準拠デバイスから企業リソースへのアクセスを許可または拒否できます。

> [!NOTE]
> この Mobile Threat Defense ベンダーは、未登録のデバイスではサポートされていません。

## <a name="supported-platforms"></a>[サポートされているプラットフォーム]

- **Android 4.1 以降**

- **iOS 8 以降**

## <a name="pre-requisites"></a>前提条件

- Azure Active Directory Premium

- Microsoft Intune サブスクリプション

- Symantec Endpoint Protection Mobile のサブスクリプション

詳しくは、[Symantec の Web サイト](https://help.symantec.com/cs/sep_mobile/SEPMOBILE/v131237277_v127904070/Integrating-Microsoft-Intune-with-Endpoint-Protection-Mobile?locale=EN_US)をご覧ください。

## <a name="how-do-intune-and-sep-mobile-help-protect-your-company-resources"></a>Intune と SEP Mobile が会社のリソースを保護する方法

Android、iOS/iPadOS 向け SEP Mobile モバイル アプリは、ファイル システム、ネットワーク スタック、デバイス、アプリケーション テレメトリを可能な限り記録し、SEP Mobile クラウド サービスに送信し、モバイル デバイスの脅威に対するリスクを評価します。

Intune デバイス コンプライアンス ポリシーには、SEP Mobile のリスク評価に基づく、SEP Mobile に関するルールが含まれています。 このルールを有効にすると、Intune は、有効にされたポリシーに基づいてデバイスの準拠状態を評価します。

デバイスが準拠していないことが判明した場合、Exchange Online や SharePoint Online などのリソースに対するアクセスがブロックされます。 デバイスがブロックされたユーザーには SEP Mobile アプリから手引きが届きます。それを見て問題を解決し、企業リソースへのアクセスを回復できます。

Intune では、SEP Mobile との統合に 2 つのモードがあります。

- **基本セットアップ**は読み取り専用モードであり、SEP Mobile は Intune のデバイスを表示できます。

- **完全統合**の場合、SEP Mobile から、デバイスのリスクとセキュリティ インシデントの詳細を Intune に報告できます。

## <a name="sample-scenarios"></a>サンプル事例

一般的なシナリオを次に示します。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいてアクセスを制御する

マルウェアなどの悪意のあるアプリがデバイスで検出されると、脅威が解決されるまで、デバイスで次の行為が禁止されます。

- 会社の電子メールに接続する

- OneDrive for Work アプリを使用して会社のファイルを同期する

- 会社のアプリにアクセスする

*悪意のあるアプリが検出されたときにブロックする:*

![検出された悪意のあるアプリの概念図](./media/skycure-mobile-threat-defense-connector/symantec-arch-1.png)

*修復時に付与されるアクセス権:*

![悪意のあるアプリが検出された後、修復時に付与されるアクセス権の画像](./media/skycure-mobile-threat-defense-connector/symantec-arch-2.png)

### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する

ネットワークで **Man-in-the-middle** のような脅威を検出し、デバイスのリスクに基づいて Wi-Fi ネットワークへのアクセスを保護します。

*Wi-Fi 経由のネットワーク アクセスをブロックする:*

![Wi-Fi 経由のネットワーク アクセスをブロックする](./media/skycure-mobile-threat-defense-connector/symantec-arch-3.png)

*修復時に付与されるアクセス権:*

![修復するとアクセス権が付与される](./media/skycure-mobile-threat-defense-connector/symantec-arch-4.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいて SharePoint Online へのアクセスを制御する

ネットワークで **Man-in-the-middle** のような脅威を検出し、デバイスのリスクに基づいて会社内のファイルの同期を阻止します。

*ネットワークの脅威が検出されたときに SharePoint Online をブロック:*

![ネットワークの脅威が検出されたときに SharePoint Online をブロック](./media/skycure-mobile-threat-defense-connector/symantec-arch-5.png)

*修復時に付与されるアクセス権:*

![SharePoint で修復時にアクセス権を付与する例](./media/skycure-mobile-threat-defense-connector/symantec-arch-6.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Symantec Endpoint Protection Mobile Threat Defense solution considers a device to be infected:
![App protection policy blocks due to detected malware](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-remediated.png)
-->

## <a name="next-steps"></a>次のステップ

Intune と SEP Mobile の統合は次の手順で行います。

- [SEP Mobile と Intune の統合をセットアップする](skycure-mtd-connector-integration.md)

- [SEP Mobile アプリ、Microsoft Authenticator、iOS/iPadOS アプリ構成ポリシーを追加して割り当てる](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Intune で SEP Mobile デバイスのコンプライアンス ポリシーを作成する](mtd-device-compliance-policy-create.md)

- [Intune で SEP Mobile MTD コネクタを有効にする](mtd-connector-enable.md)
