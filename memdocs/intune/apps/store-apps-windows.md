---
title: Microsoft Store アプリを Microsoft Intune に追加する
titleSuffix: ''
description: Microsoft Store (Windows ストア) アプリを Microsoft Intune に追加する方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 07241b6d-86d8-4abb-83a2-3fc5feae5788
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 42be4df74093f90360d2968a7c0b6fe4597eedec
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987806"
---
# <a name="add-microsoft-store-apps-to-microsoft-intune"></a>Microsoft Store アプリを Microsoft Intune に追加する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

アプリの割り当て、監視、構成、または保護を行うには、対象のアプリを事前に Intune に追加しておく必要があります。 

## <a name="add-an-app-to-intune"></a>Intune にアプリを追加する
次の操作を行うことで、Intune に Microsoft Store アプリを追加できます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[すべてのアプリ]**  >  **[追加]** の順に選択します。
3. **[アプリの種類の選択]** ペインの使用できる **[ストア アプリ]** の種類で、 **[Windows ストア アプリ]** を選択します。
4. **[選択]** をクリックします。 **[アプリの追加]** 手順が表示されます。
5. Windows ストア アプリの **[アプリ情報]** を構成するには、[[Microsoft ストア]](https://www.microsoft.com/store/apps) に移動し、展開するアプリを検索します。 アプリのページを表示し、アプリの詳細をメモしておきます。 
6. **[アプリ情報 ]** ページで、アプリの詳細を追加します。
    - **名前**:アプリの名前を入力します。この名前は会社のポータルに表示されます。 使用するアプリ名が一意であることを確認してください。 アプリ名が重複している場合、会社のポータルでは 1 つの名前のみがユーザーに表示されます。
    - **説明**:アプリの説明を入力します。 この説明は会社のポータルでユーザーに表示されます。
    - **[発行元]** : アプリの発行元の名前を入力します。
    - **[アプリ ストアの URL]** : 作成するアプリのアプリ ストア URL を入力します。 URL は、目的のアプリの [Microsoft Store](https://www.microsoft.com/store/apps) を検索することで見つけることができます。 ブラウザーのアドレス バーから URL を使用します。
    - **[カテゴリ]** : (省略可能) 1 つ以上の組み込みアプリ カテゴリ、または作成したカテゴリを選択します。 そうすると、会社のポータルを閲覧するときに、ユーザーがアプリを探しやすくなります。
    - **[会社のポータルでおすすめアプリとして表示します]** : ユーザーがアプリを参照するとき、会社のポータルのメイン ページにアプリ スイートが目立つように表示するには、このオプションを選びます。
    - **[情報 URL]** : このアプリに関する情報が含まれる Web サイトの URL を入力することもできます。 この URL は会社のポータルでユーザーに表示されます。
    - **[プライバシー URL]** : このアプリのプライバシー情報が含まれる Web サイトの URL を入力することもできます。 この URL は会社のポータルでユーザーに表示されます。
    - **[開発者]** : (省略可能) アプリ開発者の名前を入力します。
    - **[所有者]** : (省略可能) このアプリの所有者の名前 ("*人事部*" など) を入力します。
    - **[メモ]** : (省略可能) このアプリに関連付けるメモを入力します。
    - **[ロゴ]** : (省略可能) アプリに関連付けるアイコンをアップロードします。 ユーザーが会社のポータルを参照するとき、アプリにこのアイコンが表示されます。
7. **[次 へ]** をクリックして **[スコープ タグ]** ページを表示します。
8. **[スコープ タグを選択]** をクリックして、必要に応じてアプリのスコープ タグを追加します。 詳細については、「[分散 IT にロールベースのアクセス制御 (RBAC) とスコープのタグを使用する](../fundamentals/scope-tags.md)」を参照してください。
9. **[次へ]** をクリックして、 **[割り当て]** ページを表示します。
10. アプリのグループ割り当てを選択します。 詳細については、「[ユーザーとデバイスを整理するためのグループを追加する](../fundamentals/groups-add.md)」を参照してください。 
11. **[次へ]** をクリックして、 **[確認と作成]** ページを表示します。 アプリに入力した値と設定を確認します。
12. 完了したら、 **[作成]** をクリックしてアプリを Intune に追加します。

作成したアプリの **[概要]** ブレードが表示されます。

作成したアプリはアプリの一覧に表示され、選択したグループに割り当てることができるようになります。

> [!IMPORTANT]
> Microsoft Store アプリは、割り当ての種類が **[登録済みデバイスで使用可能]** であるグループにのみ割り当てることができます (ユーザーは、Intune ポータル サイトまたは Web サイトからアプリをインストールします)。

## <a name="next-steps"></a>次のステップ

- [アプリをグループに割り当てる](apps-deploy.md)
