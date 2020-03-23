---
title: クイック スタート - クライアント アプリを追加および割り当てる
titleSuffix: Microsoft Intune
description: このクイック スタートでは、Microsoft Intune を使用して、クライアント アプリを追加および割り当てます。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dab6f5c8-1ebb-42c4-a7a7-7af001f94e15
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5b6762669e4d816010982c63a119bffdec2f055
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79334276"
---
# <a name="quickstart-add-and-assign-a-client-app"></a>クイック スタート:クライアント アプリの追加および割り当て

このクイック スタートでは、Intune を使用して、会社の従業員にクライアント アプリを追加して割り当てます。 管理者の優先事項の 1 つは、エンド ユーザーが仕事を行う上で必要なアプリに確実にアクセスできるようにすることです。

Intune サブスクリプションがない場合は、[無料試用版アカウントにサインアップ](../fundamentals/free-trial-sign-up.md)します。

## <a name="prerequisites"></a>[前提条件]

- このクイック スタートを完了するには、[ユーザーの作成](../fundamentals/quickstart-create-user.md)、[グループの作成](../fundamentals/quickstart-create-group.md)、[デバイスの登録](../enrollment/quickstart-setup-auto-enrollment.md)を行う必要があります。

## <a name="sign-in-to-intune"></a>Intune にサインインする

[グローバル管理者または Intune サービス管理者](../fundamentals/users-add.md#types-of-administrators)として [Intune](https://aka.ms/intuneportal) にサインインします。 Intune の試用版サブスクリプションを作成した場合、サブスクリプションを作成したアカウントがグローバル管理者になります。

## <a name="add-the-client-app-to-intune"></a>Intune にクライアント アプリを追加する

Intune でそのアプリの側面を管理できるように、アプリを追加することができます。 

Intune にアプリを追加するには、次の手順に従います。

1. [Intune](https://aka.ms/intuneportal) で、 **[アプリ]**  >  **[すべてのアプリ]**  >  **[追加]** を選択します。 
2. **[アプリケーションの種類の選択]** ペインの **[Office 365 スイート]** セクションで **[Windows 10]** を選択します。
3. **[選択]** をクリックします。 **[アプリの追加]** 手順が表示されます。
4. **[アプリ スイートの情報]** ページで、既定の詳細を確認します。
5. **[次へ]** をクリックして、 **[アプリ スイートの構成]** ページを表示します。
6. **[更新プログラム チャネル]** の横にあるドロップダウン ボックスから **[毎月]** を選択しします。
7. * **[アプリ スイートの構成]** ページで、その他の既定の詳細を確認します。
8. **[次 へ]** をクリックして **[スコープ タグ]** ページを表示します。
9. **[スコープ タグを選択]** をクリックして、必要に応じてアプリのスコープ タグを追加します。 詳細については、「[分散 IT にロールベースのアクセス制御 (RBAC) とスコープのタグを使用する](../fundamentals/scope-tags.md)」を参照してください。
10. **[次へ]** をクリックして、 **[割り当て]** ページを表示します。
11. アプリのグループ割り当てを選択します。 詳細については、「[ユーザーとデバイスを整理するためのグループを追加する](../fundamentals/groups-add.md)」を参照してください。
12. **[次へ]** をクリックして、 **[確認と作成]** ページを表示します。 アプリに入力した値と設定を確認します。
13. 完了したら、 **[作成]** をクリックしてアプリを Intune に追加します。

## <a name="assign-the-app-to-a-group"></a>アプリをグループに割り当てる

アプリを Microsoft Intune に追加した後は、そのアプリをユーザー グループとデバイスに割り当てることができます。

> [!NOTE]
> このクイック スタートは、このシリーズの前のクイック スタートに基づいています。 詳細については、このクイック スタートの「[Prerequisites](quickstart-add-assign-app.md#prerequisites)」(前提条件) を参照してください。

グループにアプリを割り当てるには、次の手順に従います。

1. [Intune](https://aka.ms/intuneportal) で、 **[アプリ]**  >  **[すべてのアプリ]** を選択します。 
2. グループに割り当てるアプリを選びます。
3. **[割り当て]**  >  **[グループの追加]** をクリックして、 **[グループの追加]** ウィンドウを表示します。
4. **[割り当ての種類]** ドロップダウン ボックスで **[Available for enrolled devices]** \(登録済みデバイスで利用可能\) を選択します。 
5. **[組み込まれたグループ]**  >  **[含めるグループを選択]**  >  **[Contoso テスト担当者]** の順に選択します。
6. **[選択]**  >  **[OK]**  >  **[OK]**  >  **[保存]** をクリックして、グループを割り当てます。

これでアプリを **[Contoso テスト担当者]** グループに割り当てることができました。

## <a name="install-the-app-on-the-enrolled-device"></a>登録済みデバイスにアプリをインストールする

ポータル サイト アプリをインストールおよび使用し、Intune で提供されている **Contoso 社の To-Do** アプリをインストールする必要があります。 登録済みのデバイスのユーザーがアプリを使用できるかどうかを確認するには、次の手順を使用します。

1. 登録済みの Windows 10 Desktop デバイスにログインします。

    > [!IMPORTANT]
    > このデバイスは [Intune に登録されている](../enrollment/quickstart-enroll-windows-device.md)必要があります。 また、アプリに割り当てたグループに含まれるアカウントを使用してデバイスにサインインする必要があります。

2. **[スタート]** メニューから **[Microsoft Store]** を開きます。 次いで **[ポータル サイト]** アプリを探しインストールします。
3. **ポータル サイト** アプリを起動します。
4. Intune を使用して追加したアプリをクリックします。 このクイック スタートでは、**Microsoft Office 365 アプリ スイート** アプリを追加しました。

    > [!NOTE]
    > Intune ユーザーに何らかのアプリを正しく割り当てることができなかった場合、「*IT 管理者が用意した利用可能なアプリはありません*」というメッセージが表示されます。

5. **[インストール]** をクリックします。

ただし、ビジネス上のニーズにより従業員にポータル サイト アプリを割り当てる必要がある場合は、Intune から直接 Windows 10 ポータル サイト アプリを手動で割り当てることができます。 詳細については、「[Microsoft Intune を使用して Windows 10 ポータル サイト アプリを手動で追加する](company-portal-app.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

このクイック スタートでは、Intune にアプリを追加し、そのアプリをグループに割り当て、登録済みの Windows 10 デスクトップ デバイスにそのアプリをインストールしました。 Intune でのアプリの管理に関する詳細については、「[Microsoft Intune でのアプリの管理とは](app-management.md)」を参照してください。

この一連の Intune のクイック スタートに従うには、次のクイック スタートに進んでください。

> [!div class="nextstepaction"]
> [クイック スタート: アプリ保護ポリシーの作成および割り当て](quickstart-create-assign-app-policy.md)
