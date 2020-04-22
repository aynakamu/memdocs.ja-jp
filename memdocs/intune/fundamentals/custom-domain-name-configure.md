---
title: カスタムのドメイン名を構成する
titleSuffix: Microsoft Intune
description: Microsoft Intune サブスクリプションのカスタム ドメイン名を追加します
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 2382f36f-13d8-4a32-81ad-6cfa604889c3
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e9cf01f9ddf7d9d984a99a2d74e0d3294d05e95
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79363084"
---
# <a name="configure-a-custom-domain-name"></a>カスタムのドメイン名を構成する

このトピックでは、管理者が Microsoft Intune を使用して、DNS CNAME を作成し、ログオン エクスペリエンスの簡略化とカスタマイズを行う方法について説明します。

組織が Intune などの Microsoft クラウド ベース サービスにサインアップすると、**your-domain.onmicrosoft.com** のように Azure Active Directory (AD) でホストされる最初のドメイン名が付与されます。 この例では、**your-domain** はサインアップ時に選択したドメイン名です。 **onmicrosoft.com** はサブスクリプションに追加するアカウントに割り当てられるサフィックスです。 サブスクリプションで提供されるドメイン名ではなく、組織のカスタム ドメインを構成して Intune にアクセスできます。

ユーザー アカウントを作成する、またはオンプレミスの Active Directory を同期する前に、.onmicrosoft.com ドメインのみを使用するか、1 つ以上のカスタム ドメイン名を追加するかを決定することを強くお勧めします。 ユーザー管理を簡単にするために、ユーザーを追加する前にカスタム ドメインを設定します。 カスタム ドメインを設定すると、ユーザーは他のドメイン リソースへのアクセスに使う資格情報でサインインできます。

Microsoft のクラウドベースのサービスにサブスクライブすると、そのサービスのインスタンスが Microsoft [Azure AD テナント](https://technet.microsoft.com/library/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)になり、Azure AD によって、クラウドベースのサービスの ID サービスとディレクトリ サービスが提供されます。 Intune で組織のカスタム ドメイン名の使用を構成するタスクは、他の Azure AD テナントの場合と同じため、[ドメインの追加](https://azure.microsoft.com/documentation/articles/active-directory-add-domain/)に関する記事の情報と手順を利用できます。

> [!TIP]
> カスタム ドメインについて詳しくは、「[Azure Active Directory でのカスタム ドメイン名の概念の概要](https://azure.microsoft.com/documentation/articles/active-directory-add-domain-concepts/)」をご覧ください。

最初のドメイン名 onmicrosoft.com を変更または削除することはできません。 ビジネス ID をクリアにするために、Intune で使われるカスタム ドメイン名を追加、確認、削除することはできます。

## <a name="to-add-and-verify-your-custom-domain"></a>カスタム ドメインを追加して確認するには

1. [Microsoft 365 管理センター](https://admin.microsoft.com/)を開き、管理者アカウントにサインインします。

2. ナビゲーション ウィンドウで、 **[セットアップ]** &gt; **[ドメイン]** を選択します。

3. **[ドメインの追加]** を選択し、カスタム ドメイン名を入力します。 **[次へ]** を選択します。
   ![[設定] > [ドメイン] を選択して新しいドメイン名を追加した Microsoft 365 管理センターのスクリーンショット](./media/custom-domain-name-configure/domain-custom-add.png)
4. **[ドメインの確認]** ダイアログ ボックスが開き、DNS ホスティング プロバイダーに TXT レコードを作成する値が表示されます。
    - **GoDaddy ユーザー**:Microsoft 365 管理センターから GoDaddy のログイン ページにリダイレクトされます。 資格情報を入力し、ドメインの変更アクセス許可に同意すると、TXT レコードが自動的に作成されます。 または [TXT レコードを作成](https://support.office.com/article/Create-DNS-records-at-GoDaddy-for-Office-365-f40a9185-b6d5-4a80-bb31-aa3bb0cab48a)できます。
    - **Register.com ユーザー**:この[ステップ バイ ステップの指示](https://support.office.com/article/Create-DNS-records-at-Register-com-for-Office-365-55bd8c38-3316-48ae-a368-4959b2c1684e#BKMK_verify)に従って、TXT レコードを作成します。
5. [Intune の登録用に追加の DNS レコードを作成することが必要な場合があります](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium)。

カスタム ドメインを追加し、確認する手順は、[Azure Active Directory でも実行](https://azure.microsoft.com/documentation/articles/active-directory-add-domain/)できます。

詳しくは、「[Office 365 の最初の onmicrosoft.com ドメインの概要](https://support.office.com/article/About-your-initial-onmicrosoft-com-domain-in-Office-365-B9FC3018-8844-43F3-8DB1-1B3A8E9CFD5A)」をご覧ください

Intune サーバーに登録をリダイレクトする DNS CNAME を作成することにより、[Azure AD Premium を使用せずに Windows の登録を簡略化する](../enrollment/windows-enroll.md#simplify-windows-enrollment-without-azure-ad-premium)方法について、詳しく知ることができます。
