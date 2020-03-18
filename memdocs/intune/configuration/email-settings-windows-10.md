---
title: Microsoft Intune での Windows 10 デバイス向けの電子メール設定 - Azure | Microsoft Docs
description: Exchange サーバーを使用するデバイス構成電子メール プロファイルを作成し、Azure Active Directory から属性を取得します。 SSL を有効にして、Microsoft Intune を使用して Windows 10 で電子メールとスケジュールを同期することもできます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/29/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 86a792505a07a48d545ab0c5fd115f3aa8dae0eb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343636"
---
# <a name="email-profile-settings-for-devices-running-windows-10---intune"></a>Windows 10 を実行するデバイスの電子メールのプロファイル設定 - Intune

電子メールのプロファイル設定を使用して、Windows 10 を実行するデバイスで "メール" アプリを構成します。

- **[電子メール サーバー]** :Exchange サーバーのホスト名を入力します。
- **[アカウント名]** :電子メール アカウントの表示名を入力します。 この名前は、ユーザーのデバイス上に表示されます。
- **[AAD からのユーザー名の属性]** :これは、Intune が Azure Active Directory (AAD) から取得する名前です。 Intune はこのプロファイルで使用されるユーザー名を動的に生成します。 次のようなオプションがあります。
  - **[ユーザー プリンシパル名]** :`user1` や `user1@contoso.com` などの名前を取得します。
  - **[プライマリ SMTP アドレス]** :`user1@contoso.com` のような書式で電子メール アドレスを取得します。
  - **[sAM アカウント名]** :`domain\user1` などのドメインを要求します。

    次の項目も入力します。  
    - **[ユーザー ドメイン名のソース]** : **[AAD]** (Azure Active Directory) または **[カスタム]** を選択します。

      **[AAD]** から属性を取得する場合、次を入力します。
      - **[AAD からのユーザー ドメイン名属性]** :ユーザーの **[完全なドメイン名]** または **[NetBIOS 名]** 属性を取得する選択を行います。

      **[カスタム]** 属性を使用する選択を行っている場合、次を入力します。
      - **[使用するカスタム ドメイン名]** :Intune がドメイン名として使用する、`contoso.com` や `contoso` などの値を入力します。

- **[AAD からのメール アドレス属性]** :ユーザーの電子メール アドレスを生成する方法を選択します。 完全プリンシパル名を電子メール アドレスとして使用する場合は **[ユーザー プリンシパル名]** (`user1@contoso.com` または `user1`) を選択し、Exchange へのサインインにプライマリ SMTP アドレスを使用する場合は **[プライマリ SMTP アドレス]** (`user1@contoso.com`) を選択します。

## <a name="security-settings"></a>セキュリティ設定

- **[SSL]** :電子メールの送受信および Exchange サーバーとの通信に、SSL (Secure Sockets Layer) 通信を使用します。

## <a name="synchronization-settings"></a>同期設定

- **[同期する電子メールの日数]** :同期する電子メールの日数を選択します。 または、利用可能なすべての電子メールを同期する場合は **[無制限]** を選択します。
- **[同期スケジュール]** :Exchange サーバーからデータを同期するデバイスのスケジュールを選択します。 **[メッセージが到着したとき]** を選択して、電子メールが届いたらすぐにデータを同期することもできます。また、 **[手動]** を選択した場合は、デバイスのユーザーが同期を開始する必要があります。

## <a name="content-sync-settings"></a>コンテンツ同期設定

- **[同期するコンテンツの種類]** :デバイスに同期するコンテンツの種類を選択します。
  - **連絡先**
  - **カレンダー**
  - **タスク**

## <a name="next-steps"></a>次のステップ
[Intune で電子メールを設定する](email-settings-configure.md)
