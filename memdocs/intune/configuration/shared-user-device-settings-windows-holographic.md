---
title: Windows Holographic Business 共有デバイスの設定 - Microsoft Intune - Azure | Microsoft Docs
description: Windows Holographic for Business を追加および使用して、Microsoft Intune で共有されるか複数のユーザーによって使用されるデバイスを構成します。 アカウント管理設定と、Microsoft HoloLens などのデバイスでのその動作の一覧を参照してください。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88b7f41b873697a7ec34bd1fc2f1098384ab1c18
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915723"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>Intune を使用して共有デバイスを管理するための Windows Holographic for Business の設定

Microsoft HoloLens などの Windows Holographic for Business デバイスは、複数のユーザーによって使用される可能性があります。 複数のユーザーを持つデバイスは共有デバイスと呼ばれ、モバイル デバイス管理 (MDM) ソリューションの一部です。

ユーザーは Microsoft Intune を使用して、これらの共有デバイスにゲスト アカウントでサインインできます。 これらのユーザーは、デバイスを使用する際、管理者が許可する機能にのみアクセスできます。

この記事では、管理者が Windows Holographic for Business デバイス構成プロファイルで使用する設定の一覧を示して説明します。 Intune でプロファイルが作成されると、そのプロファイルを組織内のデバイス グループにデプロイするか割り当てます。 このプロファイルは、さまざまな種類のデバイスやさまざまなバージョンの OS から成るデバイス グループに割り当てることもできます。

Intune でのこの機能の詳細については、[共有 PC またはマルチユーザー デバイスでのアクセス、アカウント、および電源機能の制御](shared-user-device-settings.md)に関するページを参照してください。 Windows CSP の詳細については、「[AccountManagement CSP](/windows/client-management/mdm/accountmanagement-csp)」を参照してください。

## <a name="before-your-begin"></a>作業を開始する前に

[Windows 10 共有マルチ ユーザー デバイス構成プロファイル](shared-user-device-settings.md)を作成します。

Windows 10 共有ユーザー デバイス構成プロファイルを作成する場合、この記事に記載されているものよりも多くの設定があります。 この記事の設定は、Windows Holographic for Business デバイスでサポートされています。

## <a name="shared-multi-user-device-settings"></a>共有のマルチユーザー デバイスの設定

> [!NOTE]
> Microsoft HoloLens など、Windows Holographic for Business を実行するデバイスは、 **[アカウント管理]** 設定のみをサポートしています。 **[共有 PC モード]** など、Intune に表示されるその他の設定を構成しても、これらのデバイスには影響を与えません。

- **アカウント管理**:アカウントを自動的に削除するかどうかを選択します。 次のようなオプションがあります。
  - **[未構成]** (既定値):ゲストによって作成されたローカル アカウント、および AD と Azure AD のアカウントが自動的に削除されます。 ユーザーがデバイスからサインオフするか、またはシステム メンテナンスが実行されると、これらのアカウントは削除されます。

    次の項目も入力します。

    - **アカウントの削除**:次のように、アカウントを削除するタイミングを選択します:
      - **記憶域スペースのしきい値で**
      - **記憶域スペースのしきい値と非アクティブなしきい値で**
      - **ログアウトの直後に**

    次の項目も入力します。

    - **削除開始のしきい値 (%)** :ディスク領域のパーセンテージ (0-100) を入力します。 合計ディスク領域/記憶域が入力した値を下回ると、キャッシュされているアカウントが削除されます。 継続的にアカウントが削除されて、ディスク領域が再利用されます。 最も長時間非アクティブになっているアカウントが最初に削除されます。
    - **[Stop delete threshold(%)]\(削除停止のしきい値 (%)\)** :ディスク領域のパーセンテージ (0-100) を入力します。 合計ディスク領域/記憶域が入力した値を満たすと、削除が停止されます。

  - **無効**:ゲストによって作成されたローカル、AD、および Azure AD のアカウントはデバイス上で保持され、削除されません。

## <a name="next-steps"></a>次のステップ

- [プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。
- [Windows 10 以降](shared-user-device-settings-windows.md)の共有ユーザーデバイス設定を参照してください。