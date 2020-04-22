---
title: Windows Holographic for Business へのアップグレード
titleSuffix: Microsoft Intune
description: Windows Holographic を実行するデバイスを Windows Holographic for Business にアップグレードする方法について説明します
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e809a888fc2696e54540ee6baa2271d7340579
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79361056"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Windows Holographic を実行するデバイスを Windows Holographic for Business にアップグレードする

Microsoft Intune には、デバイスの管理と保護に役立つ多くの設定が含まれています。 この記事では、Windows Holographic デバイスを Windows Holographic for Business にアップグレードするための設定の一覧を示して説明します。 このような設定は、デバイスにプッシュまたは展開される Intune のアップグレード構成プロファイルに作成されます。

モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使用して Windows Holographic デバイスをアップグレードします。 Microsoft HoloLens の場合、Commercial Suite を購入してアップグレードに必要なライセンスを入手できます。 詳細については、「[Windows Holographic for Business 機能のロック解除](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise)」を参照してください。

この機能の詳細については、[Windows 10 エディションのアップグレードまたは S モードの有効化](edition-upgrade-configure-windows-10.md)に関するページを参照してください。

## <a name="before-you-begin"></a>始める前に

[デバイス構成プロファイルを作成します](edition-upgrade-configure-windows-10.md#create-the-profile)。

## <a name="edition-upgrade"></a>エディションのアップグレード

- **[アップグレード後のエディション]** : **[Windows 10 Holographic for Business]** を選択します。
- **[ライセンス ファイル]** : 提供された XML ライセンス ファイルを参照して選びます。

  ![Holographic for Business のライセンス情報を含む XML ファイル名を入力します](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## <a name="next-steps"></a>次のステップ

プロファイルは作成されましたが、まだ何も実行できない可能性があります。 必ず[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)してください。

[Windows 10 以降](edition-upgrade-windows-settings.md)のデバイス用にエディションのアップグレード プロファイルを作成することもできます。
