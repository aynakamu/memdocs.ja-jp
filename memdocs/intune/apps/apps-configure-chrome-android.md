---
title: Intune を使用して Android デバイス用 Google Chrome を構成する
titleSuffix: Microsoft Intune
description: Android デバイス用 Google Chrome で Intune 構成ポリシーを使用します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed8acbcbe550ffd0a3a3f94e07d5752489ae8be6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79340932"
---
# <a name="configure-google-chrome-for-android-devices-using-intune"></a>Intune を使用して Android デバイス用 Google Chrome を構成する 

Intune アプリ構成ポリシーを使用して、Android デバイス用 Google Chrome を構成できます。 アプリの設定を自動的に適用できます。 たとえば、ブロックまたは許可するブックマークと URL を具体的に設定できます。

## <a name="prerequisites"></a>[前提条件]

- ユーザーの Android Enterprise デバイスは、Intune に登録されている必要があります。 詳細については、「[Android Enterprise 仕事用プロファイル デバイスの登録を設定する](../enrollment/android-work-profile-enroll.md)」を参照してください。
- Google Chrome は managed Google Play アプリとして追加されます。 managed Google Play の詳細については、「[managed Google Play アカウントに Intune アカウントを接続する](../enrollment/connect-intune-android-enterprise.md)」を参照してください。

## <a name="add-the-google-chrome-app-to-intune"></a>Google Chrome アプリを Intune に追加する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[すべてのアプリ]**  >  **[追加]** を選択し、**マネージド Google Play** アプリを追加します。
3. managed Google Play に移動し、**Google Chrome** を検索して承認します。

    ![Google Chrome を検索して承認する](/media/apps-configure-chrome-android/search.png)

4. 必要なアプリの種類として Google Chrome をユーザー グループに割り当てます。 デバイスが Intune に登録されると、Google Chrome が自動的に展開されます。

managed Google Play アプリを Intune に追加する方法の詳細については、「[マネージド Google Play ストア アプリ](apps-add-android-for-work.md#managed-google-play-store-apps)」を参照してください。

## <a name="add-app-configuration-for-managed-ae-devices"></a>マネージド AE デバイスのアプリ構成を追加する

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) から、 **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド デバイス]** を選択します。
2. 次の詳細を設定します。
    - **名前**: Azure portal に表示されるプロファイルの名前。
    - **説明**: Azure portal に表示されるプロファイルの説明。
    - **[デバイス登録の種類]** - この設定は、 **[マネージド デバイス]** に設定されています。
    - **[プラットフォーム]** - **[Android]** を選択します。

    ![Google Chrome 構成ポリシーを追加する](/media/apps-configure-chrome-android/add-policy.png)

3. **[関連アプリ]** をクリックして、 **[関連アプリ]** ウィンドウを表示します。 **Google Chrome** を検索して選択します。 この一覧には、[承認して Intune に同期したマネージド Google Play アプリ](apps-add-android-for-work.md)が含まれます。

    ![[関連アプリ] で [Google Chrome] を選択する](/media/apps-configure-chrome-android/associated-app.png)

4. **[構成設定]** をクリックし、 **[構成デザイナーを使用する]** を選択し、 **[追加]** をクリックして構成キーを選択します。

    ![[構成デザイナーを使用する] の追加](/media/apps-configure-chrome-android/configuration.png)

    共通設定の例を次に示します。
    - **URL の一覧へのアクセスをブロックする**: `["*"]`
    - **URL の一覧へのアクセスを許可する**: `["baidu.com", "youtube.com", "chromium.org", "chrome://*"]`
    - **マネージド ブックマーク**: `[{"toplevel_name": "My managed bookmarks folder"  },  {"url": "baidu.com",   "name": "Baidu"},  {"url": "youtube.com", "name": "Youtube"},  {"name": "Chrome links",  "children": [{"url": "chromium.org", "name": "Chromium"},    {"url": "dev.chromium.org", "name": "Chromium Developers"}]}]`
    - **シークレット モードの可用性**: `Incognito mode disabled`

    構成デザイナーを使用して構成設定が追加されると、表に一覧表示されます。 

    ![共通設定](/media/apps-configure-chrome-android/common-settings.png)

    上記の設定によりブックマークが作成され、`baidu.com`、`yahoo.com`、`chromium.org`、`chrome://` を除くすべての URL へのアクセスがブロックされます。

5. **[OK]** と **[追加]** をクリックして、構成ポリシーを Intune に追加します。
6. この構成ポリシーをユーザー グループに割り当てます。 詳細については、「[Microsoft Intune を使用してアプリをグループに割り当てる方法](apps-deploy.md)」を参照してください。

## <a name="verify-the-device-settings"></a>デバイスの設定を確認する

Android デバイスが Android Enterprise に登録されると、ポートフォリオ アイコン付きのマネージド Google Chrome アプリが自動的に展開されます。

   <img alt="Managed Google Chrome with the portfolio icon" src="/media/apps-configure-chrome-android/chrome-icon.png" width="350">

Google Chrome を起動すると、設定が適用されていることがわかります。

   ブックマーク:<br>
   <img alt="Bookmarks" src="/media/apps-configure-chrome-android/bookmarks.png" width="350">

   ブロックされた URL:<br>
   <img alt="Blocked URL" src="/media/apps-configure-chrome-android/blocked-url.png" width="350">

   許可する URL:<br>
   <img alt="Allow URL" src="/media/apps-configure-chrome-android/allowed-url.png" width="350">

   シークレット タブ:<br>
   <img alt="Incognito tab" src="/media/apps-configure-chrome-android/incognito-tab.png" width="350">

## <a name="troubleshooting"></a>トラブルシューティング

1. Intune ポータルを確認してポリシーの展開状態を監視します。

    ![ポリシーの展開状態を監視する](/media/apps-configure-chrome-android/monitor-status.png)

2. Google Chrome を起動し、**chrome://policy** にアクセスします。 設定が正常に適用されたかどうかを確認できます。

    ![設定が正常に適用されたことを確認する](/media/apps-configure-chrome-android/confirm.png)

## <a name="additional-information"></a>追加情報

- [マネージド Android Enterprise デバイス用にアプリ構成ポリシーを追加する](app-configuration-policies-use-android.md)
- [Chrome Enterprise のポリシー リスト](https://cloud.google.com/docs/chrome-enterprise/policies/)

## <a name="next-steps"></a>次のステップ

- Android Enterprise フル マネージド デバイスの詳細については、「[Android Enterprise フル マネージド デバイスの Intune 登録を設定する](../enrollment/android-fully-managed-enroll.md)」を参照してください。
