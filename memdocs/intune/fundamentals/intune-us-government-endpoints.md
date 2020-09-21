---
title: 米国政府機関のネットワーク エンドポイントのデプロイ - Microsoft Intune
titleSuffix: ''
description: Intune の米国政府機関のエンドポイントを確認します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 032e6468ce326637e264b232cdd4e4d954ea70d8
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081809"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>Microsoft Intune の米国政府機関のエンドポイント

このページには、Intune デプロイでのプロキシ設定に必要な US Government、US Government Community (GCC) High、および Department of Defense (DoD) エンドポイントが一覧表示されます。

ファイアウォールとプロキシ サーバーの背後にあるデバイスを管理するには、Intune に対する通信を有効にする必要があります。

- Intune クライアントは、**HTTP (80)** と **HTTPS (443)** を使用しているため、プロキシ サーバーは両方のプロトコルをサポートする必要があります
- Intune では、一部のタスク (ソフトウェア更新プログラムのダウンロードなど) で、manage.microsoft.com への認証されていないプロキシ サーバー アクセスが必要です

個々のクライアント コンピューターでプロキシ サーバーの設定を変更できます。 また、グループ ポリシーの設定を使用して、指定したプロキシ サーバーの背後にあるすべてのクライアント コンピューターの設定を変更することもできます。

マネージド デバイスは、 **[すべてのユーザー]** がファイアウォール経由でサービスにアクセスできるように構成する必要があります。

米国政府機関のお客様の Windows 10 自動登録とデバイス登録の詳細については、「[Windows デバイスの登録をセットアップする](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration)」を参照してください。

次の表は、Intune クライアントがアクセスするポートとサービスの一覧です。

|**エンドポイント**|**IP アドレス**|
|---------------------|-----------|
|*.manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>米国政府機関のお客様によって指定されたエンドポイント:
- Azure portal: https:\//portal.azure.us/ 
- Microsoft 365: https:\//portal.office365.us/ 
- Intune ポータル サイト: https:\//portal.manage.microsoft.us/ 
- Microsoft Endpoint Manager admin center: https:\//endpoint.microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Intune が依存するパートナー サービス エンドポイント:
- Azure AD Sync サービス: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Directory プロキシ: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- Azure AD Graph: https:\//directory.microsoftazure.us と https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>次のステップ
[Microsoft Intune のネットワーク エンドポイント](intune-endpoints.md)

