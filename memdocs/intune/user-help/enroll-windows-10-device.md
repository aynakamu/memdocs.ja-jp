---
title: Intune ポータル サイトで Windows 10 デバイスを登録する | Microsoft Docs
description: Intune ポータル サイトで Windows 10 デバイスを登録する手順
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 812e82df-76df-402b-bfe9-29302838f40e
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 46f8d7d46e376d2fb8f1cab1b3d0b3bc583bdeed
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643480"
---
# <a name="enroll-windows-10-devices-with-intune-company-portal"></a>Intune ポータル サイトで Windows 10 デバイスを登録する

Intune ポータル サイトを使用して、自分の Windows 10 デバイスを組織で管理されるように登録します。 この記事では、Windows 10 バージョン 1607 以降および Windows 10 バージョン 1511 以前のデバイスを登録する方法について説明します。 始める前に、[自分のデバイスのバージョンを確認](windows-enrollment-company-portal.md#find-windows-10-version-number)し、正しい手順を利用できるようにしてください。  

Windows 10 は、デスクトップ、スマートフォン、タブレットなど、さまざまなデバイスの種類でサポートされています。 登録の手順は、使用しているデバイスにかかわらず同じです。 ただし、画面は、この記事で示す画像と少し異なる可能性があります。  
</br>
> [!VIDEO https://www.youtube.com/embed/TKQxEckBHiE?rel=0]

## <a name="enroll-windows-10-version-1607-and-later-device"></a>Windows 10 バージョン 1607 以降のデバイスを登録する 
以下の手順では、Windows 10 バージョン 1607 以降が実行されているデバイスを登録する方法について説明します。  

1. **[スタート]** メニューに移動します。 

2. **[設定]** アプリを開きます。 アプリの一覧でアプリをすぐに使用できない場合は、検索バーに移動して「設定」と入力します。

3. **[アカウント]**  >  **[職場または学校にアクセスする]**  >  **[接続]** の順に選択します。  


    ![[職場または学校にアクセスする] アカウントの選択](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

4. 組織の Intune サインイン ページにアクセスするには、職場または学校のメール アドレスを入力します。 その後、 **[次へ]** を選択します。  


   ![職場または学校のアカウントを入力します。](./media/w10-enroll-rs1-set-up-work-or-school-account.png)  

5. 職場または学校のアカウントで Intune にサインインします。  


    ![職場または学校のアカウントを追加する](./media/w10-enroll-rs1-enter-your-credentials.png)  

    最終的に、会社または学校がデバイスを登録しているというメッセージが表示されます。

6. Windows Hello 用に PIN を設定する必要がある組織の場合は、確認コードの入力を求められます。 コードを入力し、画面の手順に従って PIN を作成します。  

7. **[準備が完了しました]** 画面で、 **[完了]** を選択します。 これでデバイスが登録されました。  

8. 接続を再確認するには、 **[設定]**  >  **[アカウント]**  >  **[職場または学校にアクセスする]** に戻ります。  自分のアカウントが表示されるようになっているはずです。  


## <a name="enroll-windows-10-version-1511-and-earlier-device"></a>Windows 10 バージョン 1511 以前のデバイスを登録する  
以下の手順では、Windows 10 バージョン 1511 以前が実行されているデバイスを登録する方法について説明します。  

1. **[スタート]** メニューに移動します。 

2. **[設定]** アプリを開きます。 アプリの一覧でアプリをすぐに使用できない場合は、検索バーに移動して「設定」と入力します。

3. **[アカウント]** を選択して、 >  **[Your accounts]\(自分のアカウント\)** を選択します。  


    ![[お使いのアカウント] を選択する](./media/W10-enroll-2-accounts-your-account.png)  

5. **[職場または学校アカウントを追加]** を選択します。  


    ![[職場または学校アカウントを追加] を選択する](./media/w10-enroll-3-add-work-school-acct.png)  

6. 職場または学校の資格情報でサインインします。  


    ![サインイン](./media/W10-enroll-4-sign-in.png)  


## <a name="troubleshooting"></a>トラブルシューティング 
エラー メッセージとその他の接続問題の解決方法を抜粋した一覧については、[Windows 10 デバイスでのアクセスのトラブルシューティング](troubleshoot-your-windows-10-device-windows.md)に関する記事を参照してください。  


## <a name="it-administrator-support"></a>IT 管理者のサポート   

デバイス登録中に問題に遭遇した IT 管理者は、「[Microsoft Intune の Windows デバイスの登録に関する問題のトラブルシューティング](https://support.microsoft.com/help/4469913)」を参照してください。 この記事では、一般的なエラー、その原因、解決する手順の一覧が示されています。 

## <a name="next-steps"></a>次のステップ  
Intune ポータル サイトまたは登録に関するヘルプが必要な場合は、組織の IT サポート チームにお問い合わせください。 連絡先の情報は、[Intune ポータル サイトの Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)でわかります。 職場または学校のアカウントでサイトにサインインします。  

 

