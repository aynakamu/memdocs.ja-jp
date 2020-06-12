---
title: Check Point SandBlast MTD コネクタと Intune の設定
titleSuffix: Microsoft Intune
description: モバイル デバイスから会社のリソースへのアクセスを制御するための Intune と Check Point SandBlast Mobile Threat Defense の統合について説明します。
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
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0645c771b304bfb4930f5cd365b9291366499b1
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330918"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Intune との Check Point SandBlast Mobile Threat Defense コネクタ

Microsoft Intune に統合された Mobile Threat Defense ソリューションであるチェック ポイントの SandBlast Mobile によって実行されるリスク評価に基づき、条件付きアクセスを利用し、モバイル デバイスから会社のリソースへのアクセスを制御できます。 リスクは、チェック ポイントの SandBlast Mobile アプリを実行するデバイスから収集される製品利用統計情報に基づいて評価されます。

Intune デバイス コンプライアンス ポリシーで有効にした Check Point SandBlast Mobile リスク評価に基づき、条件付きアクセスのポリシーを構成できます。Intune デバイス コンプライアンス ポリシーは、検出された脅威に基づき、非準拠デバイスから企業リソースへのアクセスを許可したり、拒否したりするために利用できます。

> [!NOTE]
> この Mobile Threat Defense ベンダーは、未登録のデバイスではサポートされていません。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

- **Android 4.1 以降**

- **iOS 8 以降**

## <a name="pre-requisites"></a>前提条件

- Azure Active Directory Premium

- Microsoft Intune サブスクリプション

- Check Point SandBlast Mobile Threat Defense サブスクリプション
  - 詳細については、[Check Point SandBlast の Web サイト](https://www.checkpoint.com/)を参照してください。

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>Intune と Check Point SandBlast Mobile を利用し、会社のリソースをどのように保護しますか?

Android、iOS/iPadOS 向け Check Point Sandblast Mobile アプリは、ファイル システム、ネットワーク スタック、デバイス、アプリケーション テレメトリを可能な限り記録し、Check Point SandBlast クラウド サービスにテレメトリ データを送信し、モバイル デバイスの脅威に対するリスクを評価します。

Intune デバイス コンプライアンス ポリシーには、Check Point SandBlast リスク評価に基づく、Check Point SandBlast Mobile Threat Defense のルールが含まれています。 このルールを有効にすると、Intune は、有効にされたポリシーに基づいてデバイスの準拠状態を評価します。 デバイスが準拠していないことが判明した場合、ユーザーは Exchange Online や SharePoint Online などの会社リソースへのアクセスをブロックされます。 また、ユーザーは、デバイスにインストールされている Check Point SandBlast Mobile アプリから、問題を解決して会社リソースへのアクセスを回復するための案内を受け取ります。

一般的なシナリオを次に示します。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>悪意のあるアプリの脅威に基づいてアクセスを制御する

マルウェアなどの悪意のあるアプリがデバイスで検出されると、脅威が解決されるまで、デバイスで次の行為が禁止されます。

- 会社の電子メールに接続する

- OneDrive for Work アプリを使用して会社のファイルを同期する

- 会社のアプリにアクセスする

*悪意のあるアプリが検出されたときにブロックする:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD - 悪意のあるアプリが検出されたときにブロック](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*修復後、アクセスが与えられる:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD - アクセスを許可](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>ネットワークに対する脅威に基づいてアクセスを制御する

ネットワークで **Man-in-the-middle** のような脅威を検出し、デバイスのリスクに基づいて Wi-Fi ネットワークへのアクセスを保護します。

*Wi-Fi 経由のネットワーク アクセスをブロックする:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD - Wi-Fi 経由のネットワーク アクセスをブロック](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*修復後、アクセスが与えられる:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD - Wi-Fi アクセスを許可](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークへの脅威に基づいて SharePoint Online へのアクセスを制御する

ネットワークで **Man-in-the-middle** のような脅威を検出し、デバイスのリスクに基づいて会社内のファイルの同期を阻止します。

*ネットワークの脅威が検出されたときに SharePoint Online をブロック:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD - SharePoint Online アクセスをブロック](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*修復後、アクセスが与えられる:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD - SharePoint Online アクセスを許可](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>次のステップ

- [Check Point SandBlast Mobile と Intune を統合する](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [Check Point SandBlast Mobile アプリをセットアップする](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Check Point SandBlast Mobile のデバイス コンプライアンス ポリシーを作成する](mtd-device-compliance-policy-create.md)

- [Check Point SandBlast Mobile MTD コネクタを有効にする](mtd-connector-enable.md)
