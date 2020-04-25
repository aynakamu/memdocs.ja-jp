---
title: Intune ポータル サイトで Mac を登録する | Microsoft Docs
description: Intune ポータル サイト アプリで Intune に Mac を登録する方法について説明します。
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/16/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2ef7951217b0b6df21a86ca29a8637385aa65715
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79337019"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Intune ポータル サイト アプリを使用して macOS デバイスを登録する  

職日または学校の電子メール、ファイル、およびアプリに安全にアクセスするために、Intune ポータル サイト アプリで macOS デバイスを登録します。

通常、組織はユーザーに、組織が所有するデータにアクセスできるよう、事前にデバイスを登録するよう要求します。 デバイスが登録されると、*マネージド*になります。 組織は、Intune などのモバイル デバイス管理 (MDM) プロバイダーを介してデバイスにポリシーとアプリを割り当てることができます。 ご利用のデバイスから職場または学校の情報に継続的にアクセスするには、組織のポリシーの設定と一致するようにデバイスを構成する必要があります。  

この記事では、macOS 用の Intune ポータル サイト アプリを使用して、組織の要件を満たすようにデバイスの登録、構成、管理を行う方法について説明します。  


## <a name="what-to-expect-from-the-company-portal-app"></a>ポータル サイト アプリでできること

初期セットアップ時に、ユーザーは、Intune ポータル サイト アプリから、組織にサインインして自分自身の認証を行うよう要求されます。 その後、ユーザーは Intune ポータル サイトから、組織の要件を満たすために構成する必要があるデバイス設定を通知されます。 たとえば、組織では多くの場合、満たす必要のあるパスワードの最小または最大文字数に関する要件が設定されます。    

ユーザーがデバイスを登録すると、ユーザーのデバイスが組織の要件に従って保護されていることが、Intune ポータル サイトによって常に確認されます。 たとえば、ユーザーが信頼されていないソースからアプリをインストールした場合、ユーザーは Intune ポータル サイトから警告を受け、組織のリソースへのアクセスを制限される場合があります。 このようなアプリ保護ポリシーは一般的です。 アクセスを回復するには、ユーザーはおそらく信頼されていないアプリをアンインストールする必要があります。 

登録後、組織で多要素認証などの新しいセキュリティ要件が適用された場合、ポータル サイト アプリによって通知されます。 デバイスから作業を続行できるように、設定を調整することができます。  

登録の詳細については、[ポータル サイト アプリをインストールして、デバイスを登録するとどうなるか](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md)についてのページを参照してください。  

## <a name="get-your-macos-device-managed"></a>macOS デバイスを管理対象にする  
macOS デバイスを組織に登録するには、次の手順を使用します。 デバイスでは macOS 10.12 以降が実行されている必要があります。   

> [!NOTE]
> このプロセス全体で、ユーザーのキーチェーンに格納されている機密情報の使用を Intune ポータル サイトに許可するように求められる場合があります。 これらのプロンプトは、Apple のセキュリティの一部です。 プロンプトが表示されたら、ログイン キーチェーン パスワードを入力し、 **[常に許可]** を選択します。 キーボードの **Enter** キーまたは **Return** キーを押すと、プロンプトで代わりに **[許可]** が選択されて、追加のプロンプトが表示されることがあります。  

### <a name="install-company-portal-app"></a>ポータル サイト アプリをインストールする  
1. [[Enroll My Mac]\(Mac の登録\)](https://go.microsoft.com/fwlink/?linkid=853070) に移動します。  
2. Intune ポータル サイト インストーラーの .pkg ファイルがダウンロードされます。 インストーラーを開き、手順を続けます。 
3. ソフトウェア使用許諾契約に同意します。 
4. デバイスのパスワードまたは登録されている指紋を入力して、ソフトウェアをインストールします。  
5. ポータル サイトを開きます。 

> [!IMPORTANT]
> Microsoft ソフトウェアを更新するために Microsoft AutoUpdate が開く場合があります。 すべての更新プログラムがインストールされたら、Intune ポータル サイト アプリを開きます。 最適なセットアップ エクスペリエンスのため、最新バージョンの Microsoft AutoUpdate と Intune ポータル サイトをインストールします。  


### <a name="enroll-your-mac"></a>Mac を登録する  


1. 職場または学校のアカウントでポータル サイトにサインインします。  
2. アプリが開いたら **[開始]** を選択します。  
3. 登録されたデバイスで組織が見ることのできるものと、できないものを確認します。 **[続行]** を選択します。
4.  メッセージが表示されたら、 **[管理プロファイルをインストールする]** 画面でデバイスのパスワードを入力します。

    ![Intune ポータル サイトの [管理プロファイルをインストールする] 画面でパスワード プロンプトが強調して示されているスクリーンショットの例。](./media/install-management-profile-macos-1912.PNG)   
5. **[デバイス管理の確認]** 画面で、 **[システム設定を開く]** を選択し ます。  

    ![[デバイス管理の確認] 画面の [システム設定を開く] ボタンが強調して示されているスクリーンショットの例。](./media/confirm-device-management-macos-1912.PNG)  
6. デバイスのシステム設定が開きます。 デバイス プロファイルの一覧から **[管理プロファイル]** を選択し、 **[承認]**  >  **[承認]** を選択します。  
    ![システム設定の [管理プロファイル] 画面で [承認] ボタンが強調して示されているスクリーンショットの例。](./media/management-profile-approve-macos-1912.PNG)   
1. Intune ポータル サイトに戻り、 **[続行]** を選択します。    
2. 組織によって、デバイス設定を更新するように求められる場合があります。 設定の更新が終わったら、 **[設定の確認]** を選択します。  

    ![Intune ポータル サイトの [デバイス設定の更新] 画面で [設定の確認] ボタンが強調して示されているスクリーンショットの例。](./media/update-settings-mac-1911.PNG)  
9. セットアップが終わったら、 **[完了]** を選択します。  


 ## <a name="troubleshooting-and-feedback"></a>トラブルシューティングとフィードバック   

登録中に問題が発生した場合は、 **[ヘルプ]**  >  **[診断レポートの送信]** に移動し、問題を Microsoft のアプリ開発者に報告します。 この情報は、アプリを改善するために使用されます。 また、お客様の IT サポート担当者が支援を求めて来られた場合も、この情報を参考にして問題を解決します。  

Microsoft に問題を報告した後は、お客様の IT サポート担当者にエクスペリエンスの詳細を送信できます。 **[電子メールの詳細]** を選択します。 メールの本文に経験したことを入力します。 お客様のサポート担当者のメール アドレスを調べるには、Intune ポータル サイト アプリの **[連絡先]** に移動します。 または、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)を確認します。  
 

さらに、Microsoft Intune ポータル サイト チームに、お客様のフィードバックをお寄せください。 **[ヘルプ]**  >  **[フィードバックの送信]** に移動して、ご意見やアイデアをお寄せください。  

## <a name="unverified-profiles"></a>未確認のプロファイル  
**[システム設定]**  >  **[プロファイル]** でモバイル デバイス管理 (MDM) のプロファイルを確認した場合に、一部のプロファイルの状態が [未確認] と表示される場合があります。 管理プロファイルの状態が [確認済み] と表示される場合は、心配する必要はありません。  

管理プロファイルでは、MDM のチャネル接続が定義されます。 管理プロファイルが確認済みである場合、そのチャネルを介して送信されるその他のすべてのプロファイルは、その管理プロファイルのセキュリティ特性を継承します。  

## <a name="updating-the-company-portal-app"></a>ポータル サイト アプリを更新する

ポータル サイト アプリの更新は、Microsoft AutoUpdate for macOS を使用して、他の Office アプリの場合と同じように行われます。 詳細については、[Microsoft apps for macOS アプリの更新](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1)に関する記事を参照してください。  

## <a name="next-steps"></a>次のステップ  
サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。  

