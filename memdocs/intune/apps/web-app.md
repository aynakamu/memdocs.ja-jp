---
title: Web アプリを Microsoft Intune に追加する
titleSuffix: ''
description: Web アプリ (クライアント/サーバー アプリケーション) を Microsoft Intune に追加する方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f08752f-0e87-4ad9-a34c-4991b3150775
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6dde51e28872585f251b72320c17b89bf0edece9
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988503"
---
# <a name="add-web-apps-to-microsoft-intune"></a>Web アプリを Microsoft Intune に追加する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune では、Web アプリなど、さまざまなアプリの種類がサポートされています。 Web アプリはクライアント/サーバー アプリケーションです。 サーバーから Web アプリが提供されます。これには UI、コンテンツ、および機能が含まれます。 さらに、最新の Web ホスティング プラットフォームでは一般的にセキュリティや負荷分散などの利点が提供されます。 Web アプリは Web 上で個別に維持されます。 Microsoft Intune を使って、このアプリの種類を参照します。 また、このアプリへのアクセスを許可するユーザー グループを割り当てます。 

ユーザー用アプリを管理して割り当てるには、そのアプリを Intune に追加します。 

Intune によって、ユーザーのデバイスに Web アプリへのショートカットが作成されます。 iOS/iPadOS デバイスの場合、Web アプリへのショートカットがホーム画面に追加されます。 Android デバイス管理デバイスの場合、Web アプリへのショートカットが Intune ポータル サイト ウィジェットに追加されます。ウィジェットはユーザーが手動でピン留めする必要があります。 Windows デバイスの場合、Web アプリへのショートカットが [スタート] メニューに配置されます。

> [!Note]
> Web アプリを起動するには、ユーザーのデバイスにブラウザーがインストールされている必要があります。 
> 
> Android Enterprise デバイスについては、[マネージド Google Play の Web リンク](apps-add-android-for-work.md#managed-google-play-web-links)を参照してください。
> 
> iOS デバイスの場合、新しい web クリップ (ピン留めされた web アプリ) は、保護されたブラウザーで開く必要があるときに、Intune Managed Browser ではなく Microsoft Edge で開きます。 以前の iOS Web クリップの場合は、これらの Web クリップのターゲットを再設定して、Managed Browser ではなく Microsoft Edge で開くようにする必要があります。
>
> レガシ デバイスを管理する Android デバイスの場合、ポータル サイト ウィジェットで固定された Web リンクは、ユーザーのポータル サイト バージョンが 5.0.4737.0 より古い場合にのみ、Intune Managed Browser で開くことができます。 

## <a name="add-a-web-app-to-intune"></a>Web アプリを Intune に追加する
Web 上のアプリへのショートカットとしてアプリを Intune に追加するには、次の操作を行います。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[すべてのアプリ]**  >  **[追加]** の順に選択します。
3. **[アプリケーションの種類の選択]** ペインの使用できる **[その他]** の種類で、 **[Web リンク]** を選択しします。
4. **[選択]** をクリックします。 **[アプリの追加]** 手順が表示されます。
5. **[アプリ情報]** ページで、以下の情報を追加します。
    - **名前**:アプリの名前を入力します。この名前は会社のポータルに表示されます。 

        > [!NOTE]
        > アプリをデプロイしてインストールした後で、Intune Azure Portal からアプリの名前を変更すると、そのアプリを対象としてコマンドを使用できなくなります。

    - **説明**:アプリの説明を入力します。 この説明は会社のポータルでユーザーに表示されます。
    - **[発行元]** : このアプリの発行元の名前を入力します。
    - **[アプリ URL]** : 割り当てるアプリをホストする Web サイトの URL を入力します。
    - **[カテゴリ]** : (省略可能) 1 つ以上の組み込みアプリ カテゴリ、または作成したカテゴリを選択します。 そうすると、会社のポータルを閲覧するときに、ユーザーがアプリを探しやすくなります。
    - **[会社のポータルでおすすめアプリとして表示します]** : ユーザーがアプリを参照するとき、会社のポータルのメイン ページにアプリ スイートが目立つように表示するには、このオプションを選びます。
    - **[このリンクを開くには Managed Browser が必要です]** : Web サイトまたは Web アプリへのリンクをユーザーに割り当てて、ユーザーが Intune Managed Browser で開けるようにするには、このオプションを選びます。 このブラウザーをデバイスにインストールする必要があります。
    - **[ロゴ]** : アプリに関連付けるアイコンをアップロードします。 ユーザーが会社のポータルを参照するとき、アプリにこのアイコンが表示されます。
6. **[次 へ]** をクリックして **[スコープ タグ]** ページを表示します。
7. **[スコープ タグを選択]** をクリックして、必要に応じてアプリのスコープ タグを追加します。 詳細については、「[分散 IT にロールベースのアクセス制御 (RBAC) とスコープのタグを使用する](../fundamentals/scope-tags.md)」を参照してください。
8. **[次へ]** をクリックして、 **[割り当て]** ページを表示します。
9. アプリのグループ割り当てを選択します。 詳細については、「[ユーザーとデバイスを整理するためのグループを追加する](../fundamentals/groups-add.md)」を参照してください。 
10. **[次へ]** をクリックして、 **[確認と作成]** ページを表示します。 アプリに入力した値と設定を確認します。
11. 完了したら、 **[作成]** をクリックしてアプリを Intune に追加します。

    作成したアプリの **[概要]** ブレードが表示されます。

> [!Note]
> 現在、iOS/iPadOS デバイスへの Intune Web アプリの展開は管理プロファイルに関連付けられ、手動で削除することはできません。 Intune ポータルで展開の種類を**アンインストール**に変更することができ、そうすると Web アプリを自動的に削除することができます。 ただし、アプリ割り当て意図を**アンインストール**に変更する前に展開を削除すると、デバイスが Intune から登録解除されるまで、Web アプリは永続的にデバイス上に残っています。

エンドユーザーは、Windows ポータル サイト アプリから直接 Web アプリを起動できます。それには、Web アプリを選択してから、 **[ブラウザーで開く]** オプションを選択します。 発行された Web URL は、Web ブラウザー内で直接開かれます。 

## <a name="next-steps"></a>次のステップ

作成したアプリはアプリの一覧に表示され、選択したグループに割り当てることができるようになります。 詳細については、[アプリをグループに割り当てる方法](apps-deploy.md)に関するページを参照してください。 
