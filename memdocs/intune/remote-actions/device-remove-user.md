---
title: Microsoft Intune を使用して iOS/iPadOS デバイスからユーザーを削除する
titleSuffix: ''
description: Intune を使用して共有の iOS/iPadOS デバイスからユーザーを削除する方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed91d31a7085d023ef012e1dd30d86c833819ecc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983067"
---
# <a name="remove-a-user-from-a-shared-iosipados-device"></a>共有の iOS/iPadOS デバイスからユーザーを削除する


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**ユーザーの削除**アクションでは、共有の iPad デバイス上のローカル キャッシュから選択したユーザーを削除します。 iPad デバイスは、[iOS/iPadOS 教育プロファイル](../fundamentals/education-settings-configure-ios.md)を使用して iOS/iPadOS Classroom アプリを管理するように設定する必要があります。 

## <a name="supported-platforms"></a>[サポートされているプラットフォーム]

- Windows - サポートされていません
- Windows Phone - サポートされていません
- iOS/iPadOS - iOS/iPadOS 9.3 以降 (共有 iPad デバイスのみ) でサポートされています
- macOS - サポートされていません
- Android - サポートされていません

## <a name="remove-a-user"></a>ユーザーを削除する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[すべてのデバイス]** の順に選択します。
3. 管理対象のデバイスのリストで、iOS/iPadOS デバイスを選択します。
4. デバイスのウィンドウで、 **[ユーザー]** を選択します。
5. リストで、削除するユーザーを右クリックして、 **[ユーザーの削除]** を選択します。

## <a name="next-steps"></a>次のステップ

- **ユーザーの削除**アクションの状態を表示するには、 **[デバイス]**  >  **[デバイス アクション]** の順に選択します。
