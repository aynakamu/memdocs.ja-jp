---
title: Microsoft Intune - Azure でデバイスの詳細を表示する | Microsoft Docs
description: デバイスの詳細を表示します。たとえば、オペレーティング システム、記憶域、製造元、モデルなどです。 Azure で Microsoft Intune を使用して、インストールされているアプリのリストを取得したり、コンプライアンス ポリシーを確認したり、TeamViewer をセットアップしたりします。 管理するデバイスのインベントリを表示する作業と似ています。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50c56cff5f6b58894ff1abb24dad397d7e6c2c1e
ms.sourcegitcommit: cd2cbc23b8909df3a000d8ad4140e87052d6de5a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508476"
---
# <a name="see-device-details-in-intune"></a>Intune でデバイスの詳細を確認する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**[デバイス]** 機能を使用すると、ハードウェアやインストールされているアプリなど、管理するデバイスの詳細を表示できます。

この記事では、Azure Portal ですべてのデバイスと、それらのプロパティを表示する方法を示します。

## <a name="view-the-device-details"></a>デバイスの詳細を表示する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
3. **[デバイス]**  >  **[すべてのデバイス]** を選択します。次に、一覧表示されているデバイスのいずれかを選択して、その詳細を開きます。

   - **[概要]** にはデバイス名が表示されます。また、個人用デバイスか会社用デバイスか、シリアル番号、プライマリ ユーザーなど、デバイスのいくつかの主要なプロパティが一覧表示されます。 デバイスでは、次のことを実行できます。
      - [削除](devices-wipe.md#retire)
      - [ワイプ](devices-wipe.md#wipe)
      - [削除](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [リモート ロック](device-remote-lock.md)
      - [同期](device-sync.md)
      - [パスコードのリセット](device-passcode-reset.md)
      - [再起動](device-restart.md) (Windows のみ)
      - [新たに開始](device-fresh-start.md) (Windows のみ)
      - [Autopilot リセット](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (Windows のみ)
      - [クイック スキャン](../configuration/device-restrictions-windows-10.md) (Windows 10 のみ)
      - [フル スキャン](../configuration/device-restrictions-windows-10.md) (Windows 10 のみ)
       - [デバイス名の変更](device-rename.md)
      - リモート アシスタンス セッションの開始
   - **[プロパティ]** を使用して、[作成するデバイス カテゴリ](../enrollment/device-group-mapping.md)を割り当て、デバイスの所有権を個人のデバイス、または会社のデバイスに変更します。
   - **[ハードウェア]** には、デバイス ID、オペレーティング システムおよびバージョン、記憶域などの詳細に関して、多くの詳しい情報が含まれます。
   - **[検出されたアプリ]** には、Intune でデバイスにインストールされていると判断されたすべてのアプリと、アプリのバージョンが一覧表示されます。 詳細については、「[Intune discovered apps (Intune で検出されたアプリ)](../apps/app-discovered-apps.md)」を参照してください。
   - **[デバイスのポリシー準拠]** には、割り当てられているコンプライアンス ポリシーがすべて一覧表示され、デバイスがポリシーに準拠しているかどうかが示されます。
   - **[デバイス構成]** には、デバイスに割り当てられているデバイス構成ポリシーがすべて表示され、ポリシーが成功したか失敗したかが示されます。

## <a name="hardware-device-details"></a>ハードウェア デバイスの詳細
デバイスで使用される通信事業者によっては、一部の詳細が収集されない場合があります

> [!Note]  
> Intune サービスでは、ハードウェアとソフトウェアのインベントリが 7 日ごとに更新されます。

|項目|[説明]|プラットフォーム| 
|--------------|----------------------|----|  
|名前|デバイスの名前。|Windows、iOS|
|管理名|コンソールでのみ使用されるデバイス名。 この名前を変更しても、デバイス上の名前は変更されません。|Windows、iOS|
|UDID|デバイスの一意のデバイス識別子。|Windows、iOS|
|Intune デバイス ID|デバイスを一意に識別する GUID。|Windows、iOS|
|シリアル番号|製造元のデバイスのシリアル番号。|Windows、iOS|
|共有デバイス|**[はい]** の場合、デバイスが複数のユーザーで共有されます。|Windows、iOS|
|ユーザー承認済みの登録|**[はい]** の場合、デバイスには、管理者がデバイス上で特定のセキュリティ設定を管理できる、ユーザー承認済みの登録があります。|Windows、iOS|
|オペレーティング システム|デバイスで使用されるオペレーティング システム。|Windows、iOS|
|オペレーティング システムのバージョン|デバイス上のオペレーティング システムのバージョン。|Windows、iOS|
|オペレーティング システムの言語|デバイス上のオペレーティング システムに設定された言語。|Windows、iOS|
|ビルド番号|オペレーティング システムのビルド番号。|Android|
|セキュリティ パッチ レベル|デバイス用のセキュリティ パッチ レベル。|Android|
|記憶域の合計容量|デバイスの記憶域の合計容量 (ギガバイト)。|Windows、iOS|
|記憶域の空き容量|デバイスの記憶域で未使用の容量 (ギガバイト)。|Windows、iOS|
|IMEI|このデバイスの International Mobile Equipment Identity。|Windows、iOS/iPadOS、Android|
|MEID|デバイスの Mobile Equipment Identifier。|Windows、iOS/iPadOS、Android|
|製造元|デバイスの製造元。|Windows、iOS/iPadOS、Android|
|モデル|デバイスのモデル。|Windows、iOS/iPadOS、Android|
|電話番号|このデバイスに割り当てられている電話番号。|Windows、iOS/iPadOS、Android*|
|通信事業者|デバイスの無線通信事業者。|Windows、iOS/iPadOS、Android|
|通信方式|デバイスで使用される無線システム。|Windows、iOS/iPadOS、Android|
|Wi-Fi MAC|デバイスの MAC アドレス。|Windows、iOS/iPadOS、Android|
|ICCID|SIM カードの一意の識別番号である IC カードの識別子。|Windows、iOS/iPadOS、Android|
|登録日|デバイスが Intune に登録された日時。|Windows、iOS/iPadOS、Android|
|最後接続日時|デバイスが最後に Intune に接続された日時。|Windows、iOS/iPadOS、Android|
|アクティベーション ロックのバイパス コード|アクティベーション ロックを無効にするために使用できるコード。|iOS|
|Azure AD に登録済み|**[はい]** の場合、デバイスが Azure Active Directory に登録されています。|Windows、iOS/iPadOS、Android|
|Intune 登録済み|**[はい]** の場合、デバイスが Intune に登録されます|Windows、iOS/iPadOS、Android|
|コンプライアンス|デバイスのコンプライアンスの状態。|Windows、iOS/iPadOS、Android|
|EAS アクティブ化|**[はい]** の場合、デバイスが Exchange のメールボックスと同期されています。|Windows、iOS/iPadOS、Android|
|EAS アクティブ化 ID|デバイスの Exchange ActiveSync の識別子。|Windows、iOS/iPadOS、Android|
|監督下|**[はい]** の場合、管理者がデバイスの制御を強化しています。|Windows、iOS/iPadOS、Android|
|暗号化|**[はい]** の場合、デバイスに格納されているデータが暗号化されます。|Windows、iOS/iPadOS、Android|

> [!Note]  
> Android Enterprise 専用デバイスまたはフル マネージド デバイスでは、電話番号はインベントリされません。

## <a name="next-steps"></a>次のステップ
Intune で[デバイスを管理](device-management.md)するために他に行えることを確認します。
