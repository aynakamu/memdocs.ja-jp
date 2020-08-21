---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: d887f842b789b41260a49b149b61f28741937613
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703838"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> コレクションを削除できない

<!--6245446-->
このバージョンの Technical Preview Branch では、コレクションを削除することはできません。

この問題を回避するには、次の Configuration Manager の PowerShell コマンドレットを使用してコレクションを削除します。

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)