---
title: Windows デバイスを手動で同期する | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ba2f9d2e3f9e89d37b1dc8361cd80451155a6869
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820682"
---
# <a name="sync-your-windows-device-manually"></a>Windows デバイスを手動で同期する

アプリのインストールの速度が理想より遅いときは、手動によるデバイスの同期を開始します。手動同期を行うと、最新の更新プログラムと通信のためにデバイスが Intune と強制的に接続されます。 デバイスの同期が完了した後、インストールの速度が向上する可能性があります。

Intune では、ポータル サイト アプリから、デスクトップ タスク バーまたはスタート メニューから、あるいはデバイス設定アプリから手動同期できます。 Intune ポータル サイト アプリの機能は、Creators Update (1703) 以降を実行する Windows 10 デバイスでサポートされます。 

次のようなすべての Windows デバイスをデバイス設定アプリから同期できます。

* [Windows 10 デスクトップ](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Windows 用 Intune ポータル サイト アプリから直接同期する
Creators Update (バージョン 1709) 以降を実行する Windows 10 デバイスを手動で同期するには、次の手順のようにします。

1. デバイス上でポータル サイト アプリを開きます。

2. **[設定]**  >  **[同期]** を選びます。

    ![[設定] が強調表示された Intune ポータル サイト アプリのホーム ページのスクリーンショット](./media/RS1_homePage_settings_04.png)  
    
    ![[同期] ボタンが強調表示された Intune ポータル サイト アプリの設定ページのスクリーンショット](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>デバイス タスク バーまたはスタート メニューから同期する   

デバイスのデスクトップから、アプリの外部にある同期コントロールにアクセスすることもできます。 タスク バーまたはスタート メニューにアプリが直接ピン留めされているとき、簡単に同期する場合、この方法が便利です。  

1. タスク バーまたはスタート メニューでポータル サイトのアプリ アイコンを見つけます。  
2. アプリ アイコンを右クリックし、メニュー (ジャンプ リストとも呼ばれています) を表示します。  

    ![デバイスのデスクトップ上の Windows タスク バーのスクリーンショット。 ポータル サイトのアプリ アイコンが選択されると、メニューにオプションの [タスク バーにピン留め]、[ウィンドウを閉じる]、[このデバイスを同期] アクションが表示されます。](./media/sync-device-from-start-menu-1807.png)  

3. **[このデバイスを同期]** を選択します。 ポータル サイト アプリが開き、 **[設定]** ページが表示され、同期が開始されます。  

## <a name="sync-from-settings-app"></a>設定アプリから同期する 
設定アプリから Microsoft HoloLens と Windows 10 デスクトップ デバイスを手動で同期するには、次の手順を実行します。  

### <a name="windows-10-desktop"></a>Windows 10 Desktop
1. お使いのデバイスで、 **[スタート]**  >  **[設定]** を選びます。

2. **[アカウント]** を選択します。

    ![[設定] ページの [アカウント] の選択](./media/win10pc-sync-2-settings-accounts.png)  

3. デスクトップ用 Windows 10 には複数のバージョンが存在します。 実際の画面を以下のスクリーンショットと比較し、使用する手順を決定してください。 

    * 画面に **[職場または学校にアクセスする]** と表示される場合は、「[[職場または学校にアクセスする] の手順](#access-work-or-school-steps)」に進みます。

    ![設定アプリの [職場または学校にアクセスする] オプション](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * 画面に **[職場のアクセス]** と表示される場合は、「[[職場のアクセス] の手順](#work-access-steps)」に進みます。  

    ![アカウントの種類として職場のアクセスを選択する](./media/win10pc-sync-3-work-access.png)

### <a name="microsoft-hololens"></a>Microsoft HoloLens  
以下の手順は、Windows 10 Anniversary Update (RS1 とも呼ばれます) を実行する HoloLens デバイスに適用されます。  

1. デバイスで設定アプリを開きます。  

2. **[アカウント]**  >  **[職場のアクセス]** を選びます。  

    ![アカウント リンクが強調表示された HoloLens 設定アプリのスクリーンショット](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. 接続されたアカウントの **[同期]** を選びます。  

    ![[同期] ボタンが強調表示された HoloLens 設定アプリのスクリーンショット](./media/RS1_holoLens_SyncRS1_Sync_08.png)   

#### <a name="access-work-or-school-steps"></a>[職場または学校にアクセスする] の手順  

1. **[職場または学校にアクセスする]** を選択します。

    ![[職場または学校にアクセスする] オプションを示すスクリーンショット](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. 横にブリーフケース アイコンが表示されたアカウントを選びます。 このアカウントがまったく表示されない場合は、会社での設定の構成方法が異なる可能性があります。 代わりに、横に Microsoft ロゴが表示されたアカウントを選択します。

     ![ブリーフケースまたは Microsoft のロゴの横にあるアカウント名を選択する](./media/win10pc-rs1-sync-info-button.png)

3. **[情報]** を選択します。 

4. **[同期]** を選択します。 

#### <a name="work-access-steps"></a>[職場のアクセス] の手順

1. **[職場のアクセス]** を選びます。

    ![アカウントの種類として職場のアクセスを選択する](./media/win10pc-sync-3-work-access.png)

2. **[デバイス管理に登録する]** で、会社の名前を選びます。

    ![デバイス管理の会社名の選択](./media/win10pc-sync-4-tap-com-name.png)

3. **[同期]** を選択します。同期が完了するまで、ボタンは無効のままです。

    ![[同期] ボタンの選択](./media/win10pc-sync-5-tap-sync.png)  
    
## <a name="next-steps"></a>次のステップ  

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
