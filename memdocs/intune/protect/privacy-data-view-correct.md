---
title: 個人データの表示と修正
titleSuffix: Microsoft Intune
description: 個人データを表示および修正する方法について学習します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c2bacea3e1e87e6bd1a14c14b22bd6f4c2870fd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339034"
---
# <a name="view-and-correct-personal-data"></a>個人データの表示と修正

Intune 管理者は、自身のアクセス許可に基づいていくつかの個人データを表示することができますが、エンド ユーザーのデバイスの個人データを変更できるのは、そのエンド ユーザーだけです。

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>個人データの表示

管理者は Intune UI のさまざまなブレードでエンド ユーザーの個人情報を見ることができます。 次の記事では、管理者がアクセスできる情報とできない情報について説明しています。
- 「[Intune でデバイスの詳細を確認する](../remote-actions/device-inventory.md)」では、エンド ユーザーのデバイスに関する詳細を確認する方法について説明しています。
- 「[Microsoft Intune でアプリの情報と割り当てを監視する](../apps/apps-monitor.md)」では、エンド ユーザーのデバイスにインストールされているアプリに関する詳細を表示する方法について説明しています。
- 「[デバイスを登録した場合に会社が確認できる情報](https://docs.microsoft.com/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune)」の記事では、エンド ユーザーに自社で表示できるデータまたは表示できないデータのリストを提供します。 収集するデータの種類とその理由をユーザーに明確に伝えることをお勧めします。 この記事は、その透明性のための第一歩となります。

### <a name="who-can-view-the-data"></a>データを表示できる人

Microsoft では、厳格な制御を使用して顧客データへのアクセスを統制しています。付与されるアクセス権は重要なタスクを完了するために必要な最低レベルのものであり、アクセスが不要になったときは取り消されます。 

ロール ベースの管理制御 (RBAC) を使用することで、エンド ユーザーの個人データをセキュリティで保護し、アクセスを制御することができます。 詳細については、「[Microsoft Intune でのロール ベースの管理制御 (RBAC)](../fundamentals/role-based-access-control.md)」を参照してください。

Microsoft のデータ管理の実施に関する詳細については、オンライン サービス条件と [Microsoft のプライバシーに関する声明](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409)を参照してください。 

## <a name="correct-end-user-personal-data"></a>エンド ユーザーの個人データの修正

管理者は、デバイスまたはアプリに固有の情報を更新することはできません。 エンド ユーザーが個人データ (デバイス名など) を修正する場合は、自身のデバイスで直接修正する必要があります。 このような変更は、次に Intune に接続したときに同期されます。


## <a name="next-steps"></a>次のステップ

Intune で個人データを[監査、エクスポート、または削除](privacy-data-audit-export-delete.md)する方法について確認します。
