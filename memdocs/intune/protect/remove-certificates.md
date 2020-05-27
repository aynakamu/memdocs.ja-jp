---
title: Microsoft Intune で SCEP または PKCS 証明書を削除する - Azure | Microsoft Docs
titleSuffix: ''
description: 管理者は "ワイプ" アクションまたは "インベントリからの削除" アクションを利用し、Microsoft Intune から証明書を削除できます。 デバイスの登録解除やコンプライアンス ポリシーの削除など、一部のシナリオでは証明書が自動的に削除されます。 Intune ライセンスが失われたり、削除されたりしたときなど、証明書が自動的にデバイスに残るシナリオもあります。 Android、Android Enterprise、iOS/iPadOS、macOS、Windows の各デバイスに応じたさまざまな方法をご確認ください。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: lacranda
ms.openlocfilehash: 90f75420eeb19bf78f41190fa45ae5133e7746d9
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990048"
---
# <a name="remove-scep-and-pkcs-certificates-in-microsoft-intune"></a>Microsoft Intune で SCEP 証明書と PKCS 証明書を削除する

Microsoft Intune では、Simple Certificate Enrollment Protocol (SCEP) および Public Key Cryptography Standards (PKCS) 証明書プロファイルを使って、デバイスに証明書を追加できます。

これらの証明書は、デバイスを[ワイプ](../remote-actions/devices-wipe.md#wipe)したり、[インベントリから削除](../remote-actions/devices-wipe.md#retire)したりするときに削除できます。 また、証明書が自動的に削除されるシナリオや、証明書がデバイスに残るシナリオも存在します。 この記事では、一般的なシナリオと、PKCS 証明書と SCEP 証明書への影響を紹介します。

> [!NOTE]
> オンプレミスの Active Directory または Azure Active Directory (Azure AD) から削除されるユーザーの証明書を削除して取り消すには、次の手順を順番に実行します。
>
> 1. ユーザーのデバイスをワイプします (または、インベントリから削除します)。
> 2. オンプレミスの Active Directory または Azure AD からユーザーを削除します。

## <a name="manually-deleted-certificates"></a>手動で削除された証明書

証明書の手動での削除は、SCEP または PKCS 証明書プロファイルによってプロビジョニングされたプラットフォームと証明書全体に適用されるシナリオです。 たとえば、デバイスが証明書ポリシーのターゲットのままであるときに、ユーザーがそのデバイスから証明書を削除する可能性があります。

このようなシナリオでは、証明書の削除後、次回デバイスが Intune にチェックインしたときに、それが想定される証明書を持っていないためコンプライアンスに準拠していないことがわかります。 そこで、デバイスのコンプライアンスを復元するために、Intune により新しい証明書が発行されます。 証明書を復元するために追加のアクションは必要ありません。

## <a name="windows-devices"></a>Windows デバイス

### <a name="scep-certificates"></a>SCEP 証明書

SCEP 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。
- Azure AD グループからデバイスが削除される。
- 証明書プロファイルがグループ割り当てから削除される。

SCEP 証明書は次の場合に取り消されます。

- 管理者が SCEP プロファイルを変更または更新する。

ルート証明書は次の場合に削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

SCEP 証明書は次の場合にデバイスに*残ります* (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 管理者が Azure AD からユーザーまたはグループを削除する。

### <a name="pkcs-certificates"></a>PKCS 証明書

PKCS 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

ルート証明書は次の場合に削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

PKCS 証明書は次の場合にデバイスに*残ります* (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 管理者が Azure AD からユーザーまたはグループを削除する。
- 管理者が PKCS プロファイルを変更または更新する。
- 証明書プロファイルがグループ割り当てから削除される。

## <a name="ios-devices"></a>iOS デバイス

### <a name="scep-certificates"></a>SCEP 証明書

SCEP 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。
- Azure AD グループからデバイスが削除される。
- 証明書プロファイルがグループ割り当てから削除される。

SCEP 証明書は次の場合に取り消されます。

- 管理者が SCEP プロファイルを変更または更新する。

ルート証明書は次の場合に削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

SCEP 証明書は次の場合にデバイスに*残ります* (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 管理者が Azure AD からユーザーまたはグループを削除する。

### <a name="pkcs-certificates"></a>PKCS 証明書

PKCS 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

PKCS 証明書は次の場合に削除されます。

- 証明書プロファイルがグループ割り当てから削除される。

ルート証明書は次の場合に削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

PKCS 証明書は次の場合にデバイスに*残ります* (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 管理者が Azure AD からユーザーまたはグループを削除する。
- 管理者が PKCS プロファイルを変更または更新する。

## <a name="android-knox-devices"></a>Android KNOX デバイス

### <a name="scep-certificates"></a>SCEP 証明書

SCEP 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。

SCEP 証明書は次の場合に取り消されます。

- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。
- Azure AD グループからデバイスが削除される。
- 証明書プロファイルがグループ割り当てから削除される。
- 管理者が Azure AD からユーザーまたはグループを削除する。
- 管理者が SCEP プロファイルを変更または更新する。

ルート証明書は次の場合に削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

SCEP 証明書は次の場合にデバイスに*残ります* (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 管理者が Azure AD からユーザーまたはグループを削除する。

### <a name="pkcs-certificates"></a>PKCS 証明書

PKCS 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

ルート証明書は次の場合に削除されます。

- ユーザーの登録が解除される。
- 管理者が[ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを実行する。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

PKCS 証明書は次の場合にデバイスに*残ります* (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 管理者が Azure AD からユーザーまたはグループを削除する。
- 管理者が PKCS プロファイルを変更または更新する。
- 証明書プロファイルがグループ割り当てから削除される。


> [!NOTE]
> Android for Work デバイスは、上記のシナリオで検証されていません。
> Android の従来のデバイス (Samsung 以外のすべての、仕事用プロファイル以外のデバイス) では証明書の削除が無効です。

## <a name="macos-certificates"></a>macOS 証明書

### <a name="scep-certificates"></a>SCEP 証明書

SCEP 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。
- Azure AD グループからデバイスが削除される。
- 証明書プロファイルがグループ割り当てから削除される。

SCEP 証明書は次の場合に取り消されます。

- 管理者が SCEP プロファイルを変更または更新する。

SCEP 証明書は次の場合にデバイスに*残ります* (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 管理者が Azure AD からユーザーまたはグループを削除する。

> [!NOTE]
> [ワイプ](../remote-actions/devices-wipe.md#wipe) アクションを使用して macOS デバイスを工場出荷時の状態にリセットすることはできません。

### <a name="pkcs-certificates"></a>PKCS 証明書

PKCS 証明書は次の場合に取り消され、*その上*、削除されます。

- ユーザーの登録が解除される。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

ルート証明書は次の場合に削除されます。

- ユーザーの登録が解除される。
- 管理者が[インベントリからの削除](../remote-actions/devices-wipe.md#retire)アクションを実行する。

PKCS 証明書は次の場合にデバイスに残ります (証明書は取り消されず、削除されません)。

- エンドユーザーが Intune ライセンスを失う。
- 管理者が Intune ライセンスを取り消す。
- 証明書プロファイルがグループ割り当てから削除される。 (プロファイルは削除されます)。
- 管理者が Azure AD からユーザーまたはグループを削除する。
- 管理者が PKCS プロファイルを変更または更新する。

## <a name="next-steps"></a>次のステップ

[認証に証明書を使用する](certificates-configure.md)