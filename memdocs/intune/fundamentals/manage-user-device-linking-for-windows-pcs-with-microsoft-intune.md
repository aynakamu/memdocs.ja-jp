---
title: Windows PC に対するユーザー デバイスの関連付けを管理する
titleSuffix: Microsoft Intune
description: Intune で管理された Windows PC にユーザーを関連付ける方法を説明します。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 53c99d63-c312-442a-8a71-de1b10fcd39b
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 72b816938e803b28a06d3975f062f105d4c6a1cc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79358742"
---
# <a name="manage-user-device-linking-for-windows-pcs"></a>Windows PC に対するユーザー デバイスの関連付けを管理する

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

このトピックの情報は、Intune ソフトウェア クライアントを使用して PC として管理している Windows デスクトップにのみ適用されます。 

ユーザーにソフトウェアを展開する前に、ユーザーを PC に関連付ける必要があります。 1 人のユーザーを複数の PC に関連付けることができますが、1 台の PC に関連付けられるユーザーは 1 人だけです。 ユーザーは、ポータル サイトを使用して Intune で登録したすべての PC に自動的に関連付けられます。

デバイスのプライマリ ユーザーについて詳しくは、「[プライマリ ユーザーを見つける](../remote-actions/find-primary-user.md)」を参照してください。

PC にユーザーを関連付けるには:

1. [Microsoft Intune 管理コンソール](https://manage.microsoft.com/)で、 **[グループ]** &gt; **[すべてのデバイス]** (または、ユーザーに関連付ける PC が含まれる別のグループ) を選択します。

2. ユーザーを関連付ける PC を選択して、 **[ユーザーの関連付け]** を選択します。

   **[ユーザーの関連付け]** ダイアログ ボックスには、関連付けることができるユーザーの表示名とユーザー ID、および現在関連付けられている PC の台数が表示されます。 選択した PC に既にユーザーが関連付けられている場合は、そのユーザーの名前とユーザー ID が **[現在のユーザー]** の下に表示されます。 PC がどのユーザーにも関連付けられていない場合、 **[現在のユーザー]** の下に **[ユーザーなし]** と表示されます。

3. 以下のいずれかを実行します。

   - PC と現在のユーザーの関連付けをそのままにするには、 **[キャンセル]** を選択します。

   - 現在のユーザーとの関連付けを削除する (存在する場合) には、<strong>[リンクの削除] **&gt;** [OK]</strong> の順に選択します。

   - PC を新しいユーザーに関連付けるには、 **[すべてのユーザー]** の一覧からユーザーを選択します。 選択したユーザーのデータが正しいことを確認して、 **[OK]** を選択します。

> [!TIP]
> エンド ユーザーが各自の PC に関連付けをするのを抑制する場合は、 **[Microsoft Intune エージェントの設定]** ポリシーの **[ユーザーによる各自のコンピューターへの関連付けを制限する]** オプションを有効にします。

## <a name="see-also"></a>関連項目

[Intune ソフトウェア クライアントを使用した一般的な Windows PC 管理タスク](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
