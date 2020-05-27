---
title: Intune に iOS/iPadOS デバイスを登録する
titleSuffix: Microsoft Intune
description: Microsoft Intune で iOS/iPadOS デバイスの登録を設定します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/23/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 439c33a6-e80c-4da9-ba09-a51fc36f62ad
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf413dc551d8be8fd646a03826fb3e5507f4d272
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988939"
---
# <a name="enroll-iosipados-devices-in-intune"></a>Intune に iOS/iPadOS デバイスを登録する

Intune では、iPad および iPhone のモバイル デバイス管理 (MDM) が有効になり、会社のメール、データ、およびアプリへのセキュリティで保護されたアクセス権がユーザーに付与されます。

Intune 管理者は、会社のリソースにアクセスする iOS/iPadOS および iPadOS デバイスの登録を設定することができます。 "Bring Your Own Device" (BYOD) の登録と呼ばれる、個人所有のデバイスをユーザーが登録することを許可できます。 会社所有のデバイスの登録を設定することもできます。

## <a name="prerequisites-for-iosipados-enrollment"></a>iOS/iPadOS の登録の前提条件

iOS/iPadOS デバイスを有効にする前に、次の手順を完了する必要があります。

- [デバイスがサポートされていることを確認します](../fundamentals/supported-devices-browsers.md)。
- [Intune のセットアップ](../fundamentals/setup-steps.md) - この手順で、Intune インフラストラクチャをセットアップします。 特に、デバイスの登録には [MDM 機関を設定する](../fundamentals/mdm-authority-set.md)必要があります。
- [Apple MDM プッシュ通知証明書の取得](apple-mdm-push-certificate-get.md) - Apple では、iOS/iPadOS および macOS デバイスの管理を有効にするために証明書が必要です。

## <a name="user-owned-iosipados-and-ipados-devices-byod"></a>ユーザー所有の iOS/iPadOS および iPadOS デバイス (BYOD)

Intune 管理のために、ユーザーに個人用デバイスを登録させることができます。これは "Bring Your Own Device" (BYOD) と呼ばれます。 ユーザーを登録するには、次の 3 つの選択肢があります。
- アプリ保護ポリシーを使用すると、アプリ レベルでのみ管理できる最も軽量な BYOD エクスペリエンスを実現できます。 ただし、6 桁の複雑な PIN を使用してデバイスをセキュリティで保護する場合は、これらのポリシーをユーザー登録と共に使用することもできます。
- デバイスの登録は、一般的な BYOD の登録と考えることができます。 これにより、管理者は幅広い管理オプションを使用できるようになります。
- ユーザー登録は、管理者にデバイス管理オプションの一部を提供する、より簡素化された登録プロセスです。 現在のところ、この機能はプレビュー段階です。 

前提条件を満たし、ユーザーのライセンスを割り当てると、ユーザーはアプリ ストアから Intune ポータル サイト アプリをダウンロードし、アプリの登録手順を実行できるようになります。 「[Intune ポータル サイト アプリ、ポータル サイト Web サイト、および Intune アプリをカスタマイズする方法](../apps/company-portal-app.md#configuration)」で説明されているように、iOS/iPadOS デバイスでポータル サイトのプライバシーに関する声明をカスタマイズできます。

## <a name="company-owned-iosipados-devices"></a>会社所有の iOS/iPadOS デバイス

Intune では、ユーザーのデバイスを購入する組織のために、次の会社所有の iOS/iPadOS デバイスの登録方法がサポートされています。

- Apple の自動デバイス登録 (ADE)
- Apple School Manager
- Apple Configurator セットアップ アシスタントでの登録
- Apple Configurator の直接登録

[デバイス登録マネージャー](device-enrollment-manager-enroll.md)のアカウントで会社所有の iOS/iPadOS デバイスを登録することもできます。

## <a name="automated-device-enrollment"></a>デバイスの自動登録

組織は、Apple の自動デバイス登録 (ADE) を通して iOS または iPadOS デバイスを購入できます。 ADE では、登録プロファイルを "無線で" 展開して、デバイスを管理対象にすることができます。 詳細については、[Device Enrollment Program](device-enrollment-program-enroll-ios.md) に関する記事を参照してください。

## <a name="user-enrollment"></a>ユーザー登録
ユーザー登録により、管理者は他の登録方法と比較して少ない数の管理オプションを使用できるようになります。 詳細については、[ユーザー登録でサポートされるアクション、パスワード、およびその他のオプション](ios-user-enrollment-supported-actions.md)と [iOS/iPadOS と iPadOS のユーザー登録の設定](ios-user-enrollment.md)に関する記事を参照してください。

## <a name="apple-school-manager"></a>Apple School Manager

Apple School Manager は、学校向けのデバイス購入と登録プログラムです。 ADE と同様に、プロファイルを展開して管理にデバイスを登録できます。 詳細については、[Apple School Manager](apple-school-manager-set-up-ios.md) に関するページを参照してください。

## <a name="apple-configurator"></a>Apple Configurator

Mac コンピューターで実行している Apple Configurator を使って、iOS/iPadOS デバイスを登録することができます。 デバイスを準備するには、デバイスを USB 接続して、登録プロファイルをインストールします。 Apple Configurator では、次の 2 つの方法でデバイスを登録することができます。

- セットアップ アシスタントの登録 - デバイスをワイプし、セットアップ アシスタントを実行する準備を行い、デバイスの新しいユーザー用に会社のポリシーをインストールします。
- 直接登録 - デバイスをワイプせず、定義済みのポリシーでデバイスを登録します。 この方法は、ユーザー アフィニティなしのデバイス向けです。

詳細については、[Apple Configurator の登録](apple-configurator-enroll-ios.md)に関するページを参照してください。

## <a name="use-the-company-portal-on-ade-enrolled-or-apple-configurator-enrolled-devices"></a>ADE または Apple Configurator で登録されたデバイスでのポータル サイトの使用

ユーザー アフィニティが構成されているデバイスは、会社のポータル アプリをインストールして実行することにより、アプリをダウンロードしてデバイスを管理できるようになります。 ユーザーは、デバイスを受け取った後、セットアップ アシスタントを完了してポータル サイト アプリをインストールするために、いくつもの追加の手順を完了する必要があります。

以下をサポートするには、ユーザー アフィニティが必要です。

- モバイル アプリケーション管理 (MAM) アプリ
- 電子メールと会社データへの条件付きアクセス
- ポータル サイト アプリ

### <a name="how-users-enroll-corporate-owned-iosipados-devices-with-user-affinity"></a>ユーザー アフィニティありで企業所有 iOS/iPadOS デバイスを登録する方法

1. ユーザーは、デバイスの電源をオンにすると、セットアップ アシスタントを完了するように求められます。
2. セットアップが完了すると、ユーザーは Apple ID を要求されます。 デバイスでポータル サイトをインストールできるように、Apple ID を入力する必要があります。
3. iOS/iPadOS デバイスは、App Store からポータル サイト アプリを自動的にインストールします。
4. ユーザーは、ポータル サイト アプリを起動し、Intune のサブスクリプションに関連付けられている資格情報 (一意の個人名や UPN など) を使用してサインインする必要があります。
5. ログインしたら、登録は完了です。 このデバイスのすべての機能を使用できるようになります。

### <a name="about-corporate-owned-managed-devices-with-no-user-affinity"></a>ユーザー アフィニティなしの企業所有のマネージド デバイスについて

ユーザー アフィニティなしで構成されているデバイスではポータル サイトはサポートされません。そのようなデバイスにはポータル サイト アプリをインストールしないでください。 ポータル サイトは、会社の資格情報を持ち、カスタマイズされた企業リソース (電子メールなど) へのアクセスを必要とするユーザー向けです。 ユーザー アフィニティなしで登録されたデバイスは、専用ユーザー サインインのためのデバイスではありません。 ユーザー アフィニティなしで登録されているデバイスの一般的な使用例としては、キオスクや販売時点管理 (POS)、共有ユーティリティのデバイスがあります。

ユーザー アフィニティが必要な場合は、デバイスを登録する前に、デバイスの登録プロファイルで **[ユーザー アフィニティ]** が選択されていることを確認してください。 デバイスのアフィニティの状態を変更するには、デバイスをインベントリから削除してから再登録する必要があります。

## <a name="see-also"></a>関連項目

[Microsoft Intune での iOS/iPadOS デバイスの登録に関する問題のトラブルシューティング](https://support.microsoft.com/help/4039809)
