---
title: Microsoft Intune によるボリューム購入アプリとブックの管理
titleSuffix: ''
description: Microsoft Intune を使用して、ストアからのボリューム購入アプリとブックの使用状況を管理および監視する方法について説明します。"
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 85b07f57-661a-4bc8-87d2-7b446d5cf4d6
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: db078b6c89b58b9b7acb897fa053899d1fdcdd33
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79334042"
---
# <a name="manage-volume-purchased-apps-and-books-with-microsoft-intune"></a>Microsoft Intune によるボリューム購入アプリとブックの管理

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

## <a name="introduction"></a>概要

一部のアプリ ストアでは、社内で使用するアプリやブックの複数のライセンスを購入できます。 ライセンスの一括購入は、購入したアプリとブックの複数コピーを追跡する管理オーバーヘッドを削減するのに役立ちます。

Microsoft Intune を使用することで、このようなプログラムを通じて購入したアプリとブックを管理できます。 ストアからライセンス情報をインポートし、使用したライセンスの数を追跡できます。 このプロセスにより、所有している数より多くのアプリまたはブックのコピーがインストールされないようにできます。

## <a name="which-types-of-apps-and-books-can-you-manage"></a>管理できるアプリとブックの種類

Intune では、iOS ストアからボリューム購入したアプリとブックを管理し、ビジネス向け Microsoft ストアからボリューム購入したアプリを管理できます。 各ストアからライセンスを購入したアプリを管理する方法については、次のトピックのいずれかをご覧ください。

- [iOS/iPadOS のボリューム購入アプリの管理](vpp-apps-ios.md)
- [ビジネス向け Microsoft ストアからボリューム購入したアプリの管理](windows-store-for-business.md)
- [iOS/iPadOS 電子ブックを Microsoft Intune で管理する方法](vpp-ebooks-ios.md)
