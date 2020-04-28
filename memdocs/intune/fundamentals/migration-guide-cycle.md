---
title: 標準的な Intune 移行サイクルのしくみ
titleSuffix: Microsoft Intune
description: この記事では、Microsoft Intune 移行サイクルのしくみを説明し、移行サイクルの対応方法の例を示します。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3688b724-9521-4210-bf4d-bcf47d8d4ca0
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: cdef53672c46fe4e49a5d21a22e585654c504f03
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075950"
---
# <a name="typical-migration-cycle"></a>標準的な移行サイクル

通常、組織が Intune を移行する場合、IT 部門内の一部の対象ユーザーで小規模なパイロットを開始します。 また、グループの変更への意志、ユーザー数、複雑さ、要件、場所、およびビジネス上のリスクなどの要因を、組織で必要に応じて話し合い、移行期間を決定します。

対象グループのスケジュール例を次に示します。

  | **移行対象グループ** | **期間 1** | **期間 2** | **期間 3** | **期間 4** | **...**
|:---:|:---:|:---:|:---:|:---:|:---:|
| 限定パイロット運用の IT 部門 (50 ユーザー) | 計画の発表 | 登録の指示 | 期限の設定 | 条件付きアクセスを強制的に適用 |  |                                                        
| 拡張パイロット運用の IT 部門 (200 ユーザー) |  | 計画の発表 | 登録の指示 | 期限の設定 | 条件付きアクセスを強制的に適用 |
| 移行フェーズ 1 技術に精通したユーザー (2000人) |  |  | 計画の発表 | 登録の指示 | 期限の設定 |
| 移行フェーズ 2 米国東部 |  |  |  | 計画の発表 | 登録の指示 |
| すべての地域 |  |  |  |  | 計画の発表 |

## <a name="customer-migration-case-study"></a>お客様の移行のケース スタディ

### <a name="adatum-corporation"></a>Adatum Corporation

[Adatum Corporation のサード パーティ MDM プロバイダーから Intune への移行プロセス](https://gallery.technet.microsoft.com/Intune-migration-guide-893a95e3?redir=0)をご覧ください。

## <a name="monitoring-migration"></a>移行の監視

Intune は、移行を監視する方法をいくつか用意しています。

* Intune ユーザー グループのビュー

* 組み込みレポートのセット

* コンソール内のアラート

各フェーズ後にデバイスを登録したユーザー数を追跡することで、次のことができます。

- 情報伝達計画の効果を評価する。

- 条件付きアクセスの強制的な適用の影響を評価する。


## <a name="post-migration"></a>Post-migration

Intune への移行後に、以前の MDM プロバイダーをインベントリから削除したり、サービスのサブスクリプションを解除したりします。 また、MDM プロバイダーの指示に従って、不要なインフラストラクチャの要件を削除します。
