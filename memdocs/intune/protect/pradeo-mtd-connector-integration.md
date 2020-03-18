---
title: Intune との Pradeo 統合を設定する
titleSuffix: Intune on Azure
description: Intune と Pradeo コネクタを統合する
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 82872ba6-80f8-4cc9-adf4-0ccd8ff26dd2
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8a38ad4cf8aa9186bfbd061c5463d36e93c116c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351462"
---
# <a name="integrate-pradeo-mobile-threat-defense-with-intune"></a>Pradeo Mobile Threat Defense を Intune と統合する

Pradeo Mobile Threat Defense ソリューションを Intune と統合するには、次の手順を実行します。

> [!NOTE]  
> この Mobile Threat Defense ベンダーは、未登録のデバイスではサポートされていません。

## <a name="before-you-begin"></a>始める前に

> [!NOTE]
> 次の手順は、[Pradeo のセキュリティ コンソール](https://www.apps-security.com)で完了する必要があります。

Pradeo と Intune の統合を始める前に、次のものがあることを確認します。

- Microsoft Intune サブスクリプション

- 次のアクセス許可を付与する Azure Active Directory 管理者資格情報:

  - サインインしてユーザー プロファイルを読み取る

  - サインインしたユーザーとしてディレクトリにアクセスする

  - ディレクトリ データの読み込み

  - Intune にデバイス情報を送信する

- Pradeo のセキュリティ コンソールにアクセスするための管理者資格情報。

### <a name="pradeo-app-authorization"></a>Pradeo アプリの承認

Pradeo アプリ承認プロセスは以下で構成されます。

- Pradeo サービスがデバイスの正常性状態に関する情報を Intune に通知できるようにします。

- Pradeo は、Azure AD 登録グループ メンバーシップと同期してデバイスのデータベースを設定します。

- Pradeo 管理者コンソールが Azure AD シングル サインオン (SSO) を使用できるようにします。

- Pradeo アプリが Azure AD SSO を使用してサインインできるようにします。

## <a name="to-set-up-pradeo-integration"></a>Pradeo の統合を設定するには

1. [Pradeo のセキュリティ コンソール](https://www.apps-security.com)に移動し、資格情報を使用してサインインします。

2. メニューから **[Administration - Enterprise Mobility Management]** (管理 - Enterprise Mobility Management) を選択します。

3. **Intune のロゴ**を選択します。

4. **[EMM (Enterprise Mobility Management - Intune)]** (EMM (Enterprise Mobility Management - Intune)) ウィンドウの **[手順 1]** で、 **[Pradeo Connector]** (Pradeo コネクタ) ボタンを選択します。 

    ![Pradeo EMM Intune ウィンドウのスクリーンショット](./media/pradeo-mtd-connector-integration/pradeo_setup.png)

5. Microsoft Intune の接続ウィンドウに Intune の資格情報を入力します。

5. Pradeo の Web ページが再度開きます。 **[手順 2]** の **[Pradeo Device Health]** (Pradeo デバイスの正常性) ボタンを選択します。

7. Pradeo-Intune Connector \(Pradeo-Intune コネクタ) ウィンドウで **Accept** \(同意する) を選択します。 

8. Pradeo device API connector \(Pradeo デバイス API コネクタ) ウィンドウで **Accept** \(同意する) を選択します。

9. Pradeo の Web ページが再度開きます。 **[手順 3]** の **[Connect to Microsoft]** (Microsoft に接続) ボタンを選択します。 

10. Microsoft Intune の認証ウィンドウで、Intune の資格情報を入力します。

11. **[Successful Integration]** (統合に成功しました) というメッセージが表示されると統合は完了です。

## <a name="next-steps"></a>次のステップ

- [登録されたデバイスに Pradeo アプリを設定する](mtd-apps-ios-app-configuration-policy-add-assign.md)
