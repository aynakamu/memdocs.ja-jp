---
title: Check Point SandBlast MTD の統合
titleSuffix: Microsoft Intune
description: Intune で CheckPoint SandBlast Mobile Threat Defense (MTD) をセットアップし、モバイル デバイスから会社のリソースへのアクセスを制御する方法。
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
ms.assetid: 1e9b1576-b239-48cc-a672-da6b5fb7be0a
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71dc3eed84f2f1a5a267740b5c1539b29f4c63bb
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079860"
---
# <a name="integrate-check-point-sandblast-mobile-with-intune"></a>Check Point SandBlast Mobile と Intune を統合します

次の手順を行って、Check Point SandBlast Mobile Threat Defense ソリューションを Intune と統合します。

> [!NOTE]
> この Mobile Threat Defense ベンダーは、未登録のデバイスではサポートされていません。

## <a name="before-you-begin"></a>始める前に

この記事に記載の手順は、[Check Point SandBlast Mobile コンソール](https://intune-4.eu1.locsec.net/)で行います。 

Check Point SandBlast Mobile と Intune の統合を始める前に、次のものがあることを確認します。

- Microsoft Intune サブスクリプション

- 次のアクセス許可を付与する Azure Active Directory 管理者資格情報:

  - サインインしてユーザー プロファイルを読み取る

  - サインインしたユーザーとしてディレクトリにアクセスする

  - ディレクトリ データの読み込み

  - Intune にデバイス情報を送信する

- Check Point SandBlast Mobile MTD コンソールにアクセスするための管理者資格情報

### <a name="check-point-sandblast-app-authorization"></a>Check Point SandBlast アプリの承認

Check Point SandBlast アプリ承認プロセスは以下で構成されます。

- Check Point SandBlast Mobile サービスがデバイスの正常性状態に関する情報を Intune に通知できるようにします。

- Check Point SandBlast Mobile が Azure AD 登録グループ メンバーシップと同期され、そのデバイスのデータベースに入力が行われます。

- Check Point SandBlast 管理者コンソールが Azure AD シングル サインオン (SSO) を使用できるようにします。

- Check Point SandBlast Mobile アプリが Azure AD SSO を使ってサインインできるようにします。

## <a name="to-set-up-check-point-sandblast-mobile-integration"></a>Check Point SandBlast Mobile の統合をセットアップするには

1. [Check Point SandBlast Mobile MTD コンソール](https://intune-4.eu1.locsec.net/)に移動し、資格情報でサインインします。

2. **[設定]** タブをクリックします。

3. **[Device management\(デバイス管理\)]** 、 **[設定]** の順に選択します。

4. **[MDM Service\(MDM サービス\)]** ドロップダウン リストから **[Microsoft Intune]** を選択します。

5. Microsoft Intune を MDM サービスとして設定すると、**Microsoft Intune 構成** ウィンドウがポップアップ表示され、各デバイス プラットフォーム (iOS/iPadOS、Android、Windows) に対して **[Add to my organization]\(自分の組織に追加する\)** を選択して、Check Point SandBlast Mobile が Intune および Azure AD と通信することを承認します。

    ![Check Point MTD Intune の構成を示す画像](./media/checkpoint-sandblast-mobile-mtd-connector-integration/checkpoint-MTD-1.PNG)

    > [!IMPORTANT]
    > 次の手順に進むには、すべてのデバイス プラットフォームを追加する必要があります。

6. **[Accept\(承認\)]** を選択して、Check Point SandBlast Mobile アプリが Intune および Azure Active Directory と通信することを承認します。

7. すべてのデバイス プラットフォームを有効にした後、Azure AD セキュリティ グループを入力する必要があります。

8. **[Verify\(確認\)]** を選択し、Azure AD セキュリティ グループが正常に検証された後、 **[保存]** を選択します。

## <a name="next-steps"></a>次のステップ

- [Check Point SandBlast Mobile アプリをセットアップする](mtd-apps-ios-app-configuration-policy-add-assign.md)
