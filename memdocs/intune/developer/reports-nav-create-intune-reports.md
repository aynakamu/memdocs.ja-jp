---
title: Intune データ ウェアハウスを使用する
titleSuffix: Microsoft Intune
description: Intune データ ウェアハウスを使用して、社内のモバイル環境を分析できるレポートを構築します。
keywords: Intune データ ウェアハウス
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 57019B11-DF9B-4D8A-95FE-254C75398DDE
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: dad1ecb2ed86158e510b0f554e3fd7e12e21a814
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79360224"
---
# <a name="use-the-microsoft-intune-data-warehouse"></a>Microsoft Intune データ ウェアハウスを使用する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune データ ウェアハウスを使用して、社内のモバイル環境を分析できるレポートを構築します。 たとえば、次のようなレポートがあります。
- ライセンス購入の最適化に利用できる Intune に登録されているユーザーの傾向
- モバイル デバイスの状態を確認できるアプリと OS バージョンの内訳
- ポリシーの更新をスムーズにロールアウトできる登録とデバイス コンプライアンスの傾向

## <a name="data-warehouse-benefits"></a>データ ウェアハウスの利点

データ ウェアハウスを使用すると、モバイル環境について Azure Portal よりも詳細な情報にアクセスできます。 Intune データ ウェアハウスでは、次の情報にアクセスできます。

- Intune の履歴データ
- 日単位の更新データ
- OData 標準を使用するデータ モデル

> [!Note]
> Microsoft Endpoint Configuration Manager と Microsoft Intune で共同管理モバイル デバイス管理 (MDM) を使用している場合は、Configuration Manager からデータを取得する必要があります。 Intune データが含まれるのは Intune データ ウェアハウスのみです。 カスタム レポートには Configuration Manager Power BI ダッシュボードを使用できます。 詳細については、[Configuration Manager 用 Power BI ソリューション テンプレートの発表](https://powerbi.microsoft.com/blog/sccm-solution-template)に関する記事と、[Dynamics 365 の Power BI コンテンツ](https://docs.microsoft.com/dynamics365/unified-operations/dev-itpro/analytics/power-bi-home-page)に関するページを参照してください。

> [!Important]  
> クエリ パラメーター  `api-version=v1.0` を設定することにより、Intune データ ウェアハウスの v1.0 バージョンを使用できるようになりました。 Data Warehouse 内のコレクションに対する更新は本質的に追加であり、既存のシナリオが使用できなくなることはありません。<br><br>
> データ ウェアハウスの最新機能については、ベータ バージョンを使用して試すことができます。 ベータ バージョンを使用するには、URL にクエリ パラメーター  `api-version=beta` を含める必要があります。 ベータ バージョンは、サポートされるサービスとして一般公開される前の機能を提供しています。 Intune に新しい機能が追加されると、ベータ バージョンの動作とデータ コントラクトが変わる可能性があります。 カスタム コードまたはレポート ツールがベータ バージョンに依存していると、今後の更新プログラムで使用できなくなる可能性があります。

## <a name="next-steps"></a>次のステップ

- リンクを取得し、Power BI を使用して分析します。 手順については、「[Connect to the Intune Data Warehouse with Power BI](reports-proc-get-a-link-powerbi.md)」(Power BI で Intune データ ウェアハウスに接続する) を参照してください。
- リンクを使用して Power BI でカスタム レポートを作成します。 方法は、「[Power BI で OData フィードからレポートを作成する](reports-proc-create-with-odata.md)」を参照してください。
- Intune データ ウェアハウス API、データ モデル、エンティティ間の関係の詳細については、<!-- , and an example of creating a custom client to retrieve data,--> 「[Intune データ ウェアハウス API](reports-nav-intune-data-warehouse.md)」を参照してください。
