---
title: Microsoft Intune で Windows 10 デバイスをリセットする - Azure | Microsoft Docs
description: Microsoft Intune を使用して、Windows 10 PC 上のアプリを削除またはアンインストールするには、[新たに開始] を使用します。
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
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6d409f3ba1dc91815ce3dc67a2d65e5703c7268
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80322548"
---
# <a name="use-fresh-start-to-reset-windows-10-devices-with-intune"></a>[新たに開始] を使用して Intune が稼働する Windows 10 デバイスをリセットする


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**[新たに開始]** デバイス操作は、Windows 10 バージョン 1703 以降を実行している PC にインストールされているすべてのアプリを削除します。 [新たに開始] は、一般的に新しい PC にプレインストールされている (OEM) アプリケーションを削除するために役立ちます。 

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[デバイス]**  >  **[すべてのデバイス]** を選択します。
2. 管理するデバイスの一覧から Windows 10 デスクトップ デバイスを選択します。
3. **[新たに開始]** をクリックします。 
4. 以下の目的で **[このデバイスにあるユーザー データを保持する]** を選択します。
   * Azure AD に参加したデバイスを保持します。
   * Azure Active Directory が有効なユーザーがデバイスにサインインすると、デバイスはモバイル デバイス管理に再び登録されます。
   * デバイス ユーザーのホーム フォルダーの内容を保持し、アプリと設定を削除します。

  > [!IMPORTANT]
 > ユーザー データを保持していない場合、デバイスでは、組み込みの管理者アカウントを保持したまま、既定の OOBE (Out-Of-Box Experience) の完了状態に復元されます。
 > BYOD デバイスは、Azure AD とモバイル デバイス管理から登録解除されます。
 > Azure Active Directory が有効なユーザーがデバイスにサインインすると、Azure AD 参加済みデバイスはモバイル デバイス管理に再び登録されます。
 
5. **[OK]** をクリックします。   
6. この操作の状態を確認するには、 **[デバイス]** に戻り、 **[デバイス アクション]** をクリックします。  
7. デバイスは、初期のサインイン画面に復元されます。
