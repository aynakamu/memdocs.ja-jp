---
title: 会社のデータへの無許可のアクセスを防止する
titleSuffix: Microsoft Intune
description: Microsoft Intune を使用して、企業ネットワーク外での共有時に、会社のデータへの無許可のアクセスを防止します。
keywords: Microsoft 365 M365 Azure Information Protection データ保護 ネットワークの外部 会社のデータ
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6a88573a-aa60-455c-858c-74562798246b
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24d0ed7b9111e54c4912cf23cd5b52072253c931
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996148"
---
# <a name="prevent-unauthorized-access-to-company-data-using-microsoft-intune"></a>Microsoft Intune を使用して、会社のデータへの無許可のアクセスを防止する

Microsoft 365 のドキュメントと電子メールを分類し、ラベル付けし、保護すると、許可されたユーザーだけがデータにアクセスできるようになります。 設定は、IT 管理者またはユーザーが規則と条件を設定すると自動的に管理されます。 または、IT チームからユーザーに推奨される設定を提供することもできます。 管理者とユーザーは、別の機関からの指示なく他のユーザーと既に共有されているデータへのアクセスを取り消すこともできます。 この作業により、データが企業ネットワークから離れた後も、保護されているデータを開いたり更新したりするユーザーを制御できるようになります。 

## <a name="before-you-begin"></a>始める前に

次の行動計画は、次の要件を満たすことで使用できます。
* 会社が、クラウドに安全に移行する準備ができている。
* 会社が Microsoft 365 Exchange Online、SharePoint Online、OneDrive for Business、または Yammer を使用している。
* 会社が Microsoft 365、Enterprise Mobility + Security (EMS)、または Azure Information Protection のライセンスを持っている。
* 会社が Windows 7 Service Pack 1 またはそれ以降が実行されているデバイスを使用している。
* 会社が Microsoft 365 アプリと 2016 アプリまたは 2013 アプリ、Office Professional Plus 2016、Office Professional Plus 2013 Service Pack 1 または Office Professional Plus 2010 を使用している。

## <a name="action-plan"></a>行動計画

[Azure Information Protection のクイック スタート チュートリアル](/information-protection/get-started/infoprotect-quick-start-tutorial)を完了します。  

## <a name="what-to-tell-employees-and-students"></a>社員や学生に伝えること

[機密情報が含まれるドキュメントおよび電子メールを保護する方法とタイミング](/information-protection/deploy-use/help-users)について詳細を共有できます。

## <a name="next-steps"></a>次のステップ

次の手順として、会社データの保護機能を上げる他の方法について学習できます。次のようなものがあります。 

* [iOS/iPadOS デバイスおよび Android デバイスで Azure Information Protection](/information-protection/rms-client/mobile-app-faq) を使用する方法を学習します。
* Mac コンピューターの場合は、[Microsoft Rights Management 共有アプリケーション](/previous-versions/msdn10/dn451248(v=msdn.10))について確認してください。
