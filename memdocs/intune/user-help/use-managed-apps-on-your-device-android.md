---
title: Android デバイスで管理対象アプリを使用する | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/03/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ed10a62c-b026-4ad3-ac41-641933522df2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: chrisbal
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f891d88f929a8e4e297ec8bc58f5fe6d37228cf4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79347081"
---
# <a name="use-managed-apps-on-your-android-device"></a>Android デバイスで管理対象アプリを使用する
マネージド アプリは、組織のセキュリティ要件を満たすように構成されて、職場や学校のデータを保護します。 これらのアプリは、お使いのデバイスに自動的にインストールして使用できます。 

ユーザーがマネージド アプリを受け取ってインストールする前に、ユーザーの組織によってアプリのアクセス許可が構成されます。 アプリのデータが不正ユーザーによって共有または表示されないように、アプリの機能またはユーザーの操作が制限されることがあります。 たとえば、アプリ内でのコピーと貼り付けの使用が組織によってブロックされる場合があります。 または、ユーザーのデバイスのローカル ストレージへのデータの保存が制限されることがあります。

データ保護を最強にするため、組織は複数のマネージド アプリが連携して動作するように構成する可能性があります。 次に例を示します。
1. ユーザーは、Microsoft Edge などのマネージド ブラウザー アプリで、組織のネットワークに接続します。
2. リンクをクリックして、同僚のプレゼンテーション ファイルを開きます。
3. Microsoft PowerPoint などの適切なマネージド アプリでファイルが開かれます。

組織はユーザーに対し、作業ファイルを開いたり Web リンクにアクセスするといったことを、マネージド アプリを使用して行うよう要求することができます。 ユーザーは、アプリを持っていない場合、タスクを続行できない可能性があります。 マネージド アプリの中にはインストールできますが必要のないものもあります。

## <a name="how-do-i-know-im-using-a-managed-app"></a>マネージド アプリを使用していることを確認する方法
マネージド アプリで職場または学校のデータにアクセスしようとすると、アプリが組織によって保護されていることを示すメッセージが画面に表示されます。 

## <a name="commonly-managed-apps"></a>一般的なマネージド アプリ  
学校および職場で一般に必要とされる、または使用できるマネージド アプリの例は次のとおりです。

- Microsoft Edge

- Microsoft Outlook

- Microsoft Word、Excel、PowerPoint

## <a name="how-do-i-get-managed-apps"></a>管理対象アプリを取得する方法
マネージド アプリを入手するには次の 3 つの方法があります。  
* 組織によって自動的に、登録時にアプリにデバイスがインストールされます。  
* ユーザーが Google Play ストアからアプリをインストールした後、職場または学校アカウントでアプリにサインインします。    
* 組織が、ポータル サイトでマネージド アプリを使用できるようにします。 ポータル サイト アプリまたは Web サイトに移動し、使用可能なアプリを検索、表示、およびインストールします。 これらのアプリについて詳しくは、次の「[使用可能なアプリ](#available-apps)」セクションをご覧ください。  

### <a name="available-apps"></a>Available apps   
 組織では、職場または学校のユーザーにとって適切で便利なアプリを選択して、Intune ポータル サイトで利用できるようにすることができます。  

 アプリは、デバイスの種類に基づいて使用が許可されます。 たとえば、Android 用ポータル サイト アプリを使用している場合、Android アプリにはアクセスできますが、iOS アプリにはアクセスできません。   

## <a name="request-an-app-for-work-or-school"></a>職場または学校用のアプリを要求する   
 必要なアプリがあるが、ポータル サイト内に存在しない場合は、そのアプリを要求できます。 アプリの **[IT に連絡]** タブで、**ヘルプデスク**の連絡先の詳細を確認します。同じ連絡先情報は、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)でも確認できます。   

## <a name="what-can-my-company-support-manage-in-an-app"></a>会社のサポートがアプリで管理できるもの  
次の一覧に、会社のサポートがアプリ内で管理できる設定を示します。 これらの設定は、デバイスでの職場または学校のデータの表示方法、アクセス方法、それ以外の使用方法に影響します。

* 特定の web サイトへのアクセス  

* Microsoft Edge と Azure Active Directory プロキシを使用した社内 Web サイトへのアクセス  

* アプリの最小バージョン、OS のバージョン

* アプリ間でデータを共有および転送する機能  

* ユーザーがファイルを保存する方法と場所  

* コピーと貼り付けの機能  

* 暗証番号 (pin) のアクセスの要件  

* ユーザーが会社の資格情報を使用してサインインする方法  

* データをクラウドにバックアップする機能  

* スクリーン ショットを撮る機能  

* データの暗号化の要件  

デバイスの管理対象アプリの詳細については、会社のサポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
