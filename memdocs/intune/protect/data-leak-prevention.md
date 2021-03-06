---
title: 管理されていないデバイスでのデータ漏洩の防止
titleSuffix: Microsoft Intune
description: Microsoft Intune を使用して、デバイス上での企業データへのアクセスを許可し、データ漏洩を防ぎます。
keywords: データ保護 漏洩の防止 デバイス M365 Microsoft 365
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: b1512c3a-3bbd-4111-a0df-c874a0a335df
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c979d6cf35611a419c4e27605b696c6ad3d85cd9
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996182"
---
# <a name="prevent-data-leaks-on-non-managed-devices-using-microsoft-intune"></a>Microsoft Intune を使用して、管理されていないデバイスでのデータ漏洩を防止する

Microsoft 365 でホストされている会社のデータへのアクセスを許可すると、意図的または偶発的なデータ漏洩のリスクなしでユーザーがデータを共有したり保存したりする方法を制御できます。 Microsoft Intune は、ユーザーが所有するデバイス上の会社データの保護のために設定するアプリの保護ポリシーを提供します。 デバイスを Intune サービスに登録する必要はありません。 

Intune で設定されたアプリの保護ポリシーは、Microsoft 以外のデバイス管理ソリューションで管理されるデバイスでも動作します。 IT 部門によって管理されるのは会社のデータのみで、デバイス上の個人データは管理されません。 

Windows、iOS、iPadOS、Android が実行されているデバイスの Office モバイル アプリにアプリの保護ポリシーを設定して会社のデータを保護することができます。 これらのポリシーにより、アプリベースの PIN や会社のデータの暗号化などのポリシー設定だけでなく、ユーザーが管理対象/管理対象外のアプリ間で切り取り、コピー、貼り付け、名前を付けて保存の機能を使用する方法を制限するための詳細な設定もできるようになります。 ユーザーがデバイスを登録していなくても、会社のデータをリモートでワイプすることもできます。

Intune アプリの保護ポリシーは、デバイスの管理に依存しません。 アプリの保護ポリシーにより、Intune で管理されるデバイスでも管理されないデバイスでも、さらには Microsoft 以外の MDM ソリューションで管理されるデバイスでも、Office モバイル アプリを管理できるようになります。

## <a name="before-you-begin"></a>始める前に

次の行動計画は、次の要件を満たすことで使用できます。

* 会社が、クラウドに安全に移行する準備ができている。
* 会社が Microsoft 365 Exchange Online、SharePoint Online、OneDrive for Business、または Yammer を使用している。
* 会社が Microsoft 365、Enterprise Mobility + Security (EMS)、または Azure Information Protection のライセンスを持っている。
* 会社が会社所有の、または個人所有の Windows、iOS、iPadOS、Android デバイスから会社のデータへのアクセスをユーザーに許可している。
* 会社がデバイス管理サービスで個人所有のデバイスの登録を求めていない。

## <a name="action-plan"></a>行動計画

iOS/iPadOS および Android デバイスの場合:

1. [アプリ保護ポリシー](../apps/app-protection-policy.md)のしくみをご確認ください。
2. Office モバイル アプリで[アプリ保護ポリシーを作成して展開する](../apps/app-protection-policies.md)方法をご確認ください。
3. 作成して展開した[アプリ保護ポリシーを監視](../apps/app-protection-policies-monitor.md)します。

Windows 10 デバイスの場合:

1. [Windows 情報保護 (WIP) のしくみ](/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)をご確認ください。
2. [Windows 10 用のアプリ保護ポリシー](../apps/app-protection-policies-configure-windows-10.md)を構成する準備をします。
3. [Intune で WIP アプリ保護ポリシーを作成して展開します](../apps/windows-information-protection-policy-create.md)。

## <a name="what-to-tell-employees-and-students"></a>社員や学生に伝えること

必要に応じて、追加情報を提供する次のリンクを共有してください。

* [アプリ保護ポリシーを使用して iOS/iPadOS アプリを管理するときの注意点](../fundamentals/end-user-mam-apps-ios.md)
* [アプリ保護ポリシーを使用して Android アプリを管理するときの注意点](../fundamentals/end-user-mam-apps-android.md)

## <a name="next-steps"></a>次のステップ

EMS または Microsoft 365 のさまざまなシナリオを有効にする支援をご希望ですか? Microsoft 365、Enterprise Mobility + Security、または Azure Active Directory Premium のライセンスを 150 以上お持ちでしたら、[FastTrack の特典](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program)をご利用いただけます。
