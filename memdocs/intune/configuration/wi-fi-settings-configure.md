---
title: Microsoft Intune でデバイス用の Wi-Fi プロファイルを作成する - Azure | Microsoft Docs
description: Microsoft Intune で Wi-Fi デバイスの構成プロファイルを作成する手順を説明します。 Android、Android エンタープライズ、Android キオスク、iOS、iPadOS、macOS、Windows 10 以降、Windows Holographic for Business 用のプロファイルを作成します。 これらのプロファイルは、証明書を使用するための Wi-Fi 接続の作成、EAP の種類の選択、認証方法の選択、プロキシの有効化、その他に使用します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5297f87dd3aad6b88281b491ccb7c1f0878ffc1e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343129"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Microsoft Intune でデバイスに Wi-Fi 設定を追加して使用する

Wi-Fi は、多数のモバイル デバイスがネットワークにアクセスするために使用しているワイヤレス ネットワークです。 Microsoft Intune には、組織内のユーザーとデバイスに展開できる組み込みの Wi-Fi 設定が含まれています。 この設定のグループは "プロファイル" と呼ばれ、さまざまなユーザーとグループに割り当てることができます。 割り当てると、ユーザーは自分で構成しなくても組織の Wi-Fi ネットワークにアクセスできるようになります。

たとえば、Contoso Wi-Fi という新しい Wi-Fi ネットワークをインストールします。 そして、すべての iOS/iPadOS デバイスをこのネットワークに接続するように設定するものとします。 その手順は次のとおりです。

1. Contoso Wi-Fi ワイヤレス ネットワークに接続するための設定が含まれる Wi-Fi プロファイルを作成します。
2. iOS/iPadOS デバイスのすべてのユーザーを含むグループにそのプロファイルを割り当てます。
3. ユーザーは、自分のデバイスでワイヤレス ネットワークの一覧にある新しい Contoso Wi-Fi ネットワークを見つます。 ユーザーは、選択されている認証方法を使用して、ネットワークに接続できます。

この記事では、Wi-Fi プロファイルの作成手順を説明します。 また、各プラットフォームのさまざまな設定について説明されたリンクも含まれています。

## <a name="supported-device-platforms"></a>サポートされているデバイス プラットフォーム

Wi-Fi プロファイルでは次のデバイス プラットフォームをサポートしています。

- Android 4 以降
- Android エンタープライズ、キオスク
- iOS 8.0 以降
- iPadOS 13.0 以降
- macOS X 10.11 以降
- Windows 10 以降、Windows 10 Mobile、Windows Holographic for Business

> [!NOTE]
> Windows 8.1 を実行しているデバイスの場合は、以前に別のデバイスからエクスポートした Wi-Fi 構成をインポートできます。

## <a name="create-a-device-profile"></a>デバイス プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「**会社全体の WiFi プロファイル**」は適切なプロファイル名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **[プラットフォーム]** :デバイスのプラットフォームを選択します。 次のようなオプションがあります。

      - **Android**
      - **Android エンタープライズ**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 8.1 以降**
      - **Windows 10 以降**

    - **[プロファイルの種類]** : **[Wi-Fi]** を選択します。

      > [!TIP]
      >
      > - 専用デバイス (キオスク) として実行されている **Android エンタープライズ** デバイスの場合、 **[デバイスの所有者のみ]**  >  **[Wi-Fi]** の順に選択します。
      > - **Windows 8.1 以降**の場合は、 **[Wi-Fi インポート]** を選択できます。 このオプションを使用すると、以前に別のデバイスからエクスポートした Wi-Fi 設定を XML ファイルとしてインポートすることができます。

4. Wi-Fi 設定の一部は、プラットフォームごとに異なります。 特定のプラットフォーム向けの設定を確認するには、プラットフォームを選択します。

    - [Android](wi-fi-settings-android.md)
    - [Android エンタープライズ](wi-fi-settings-android-enterprise.md) (専用デバイスを含む)
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 以降](wi-fi-settings-windows.md)
    - [Windows 8.1 以降](wi-fi-settings-import-windows-8-1.md) (Windows Holographic for Business を含む)

5. 完了したら、 **[プロファイルの作成]**  >  **[作成]** の順に選択します。

プロファイルが作成され、プロファイル一覧に表示されます ( **[デバイス構成]**  >  **[プロファイル]** )。

## <a name="next-steps"></a>次のステップ

プロファイルは作成されますが、何も実行されません。 次に、[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。

[Intune での Wi-Fi プロファイルのトラブルシューティング](troubleshoot-wi-fi-profiles.md)。
