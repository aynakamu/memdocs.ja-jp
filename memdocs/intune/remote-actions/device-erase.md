---
title: MacOS デバイスを消去する
titleSuffix: Microsoft Intune
description: macOS デバイスからオペレーティング システムを含むすべてのデータを消去する方法を説明します。
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
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 650ba81c9e92ce03b67e90cf188435b7dc0800fb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338215"
---
# <a name="erase-all-data-from-a-macos-device"></a>MacOS デバイスからすべてのデータを消去する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

macOS デバイスから、オペレーティング システムを含むすべてのデータを消去することができます。 デバイスは Intune の管理からも削除されます。 エンド ユーザーに警告は表示されません。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]** 、 **[すべてのデバイス]** の順に選択し、消去するデバイスを選択します。
2. **[その他]**  >  **[消去]** の順にクリックし、 **[Recovery Pin]\(回復用 PIN\)** に 6 桁の数字を入力します。 これは、ユーザーが自分のデバイスにオペレーティング システムを再インストールできるようにユーザーに与える必要がある PIN です。 この PIN は、消去操作が完了した後では表示できないので、必ず書き留めておいてください。
![スクリーンショット](./media/device-erase/providepin.png)
3. **[OK]** をクリックしてデバイスを消去します。
