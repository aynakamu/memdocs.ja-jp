---
title: Microsoft Intune のテナントの状態ページ
titleSuffix: Microsoft Intune
description: Intune の [Tenant Status] (テナントの状態) ページを使用して、Intune ポータルを離れることなく、重要なテナントの詳細を表示します
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 7954a686-25dc-4fce-b395-324816f46d3b
ms.reviewer: crisk
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d309b295281c88dff717c5f609905b3e541e3fed
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696431"
---
# <a name="use-the-intune-tenant-status-page"></a>Intune の [テナントの状態] ページを使用する
Microsoft Intune の [テナントの状態] ページは、ご利用のテナントに関する現在の重要な詳細を表示できる一元的なハブです。 詳細には、ライセンスの可用性と使用、コネクタの状態、および Intune サービスに関する重要な連絡が含まれます。  

ダッシュボードを表示するには、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[テナント管理]** に移動して、 **[テナントの状態]** を選択します。

このページは、次の 3 つのタブに分かれています。

## <a name="tenant-details"></a>テナントの詳細
テナントの詳細では、テナントに関する概要情報が提供されます。 テナント名と場所、MDM 機関、およびテナント サービスのリリース番号などの詳細を表示します。 サービスのリリース番号はリンクになっており、Microsoft docs 上の "*Intune の新機能*" に関する記事が開きます。"*新機能*" に関する記事では、Intune サービスの最新機能と更新プログラムを確認することができます。  

このタブでは、利用可能なライセンスに関する基本情報と、ユーザーに割り当てられている数を確認することもできます。 デバイス用のライセンスは表示されません。

## <a name="connector-status"></a>コネクタの状態
コネクタの状態を使用すれば、Intune で利用可能なすべてのコネクタの状態を 1 か所で確認することができます。  

コネクタは次のとおりです。
- **外部サービスに対して構成する接続**。 たとえば、*Apple Volume Purchase Program* サービスや *Windows Autopilot* サービスです。  この種のコネクタの状態は、前回成功した同期の時刻に基づきます。
- *Apple Push Notification Services* (APNS) 証明書など、**外部のアンマネージド サービスへの接続に必要な証明書や資格情報**。 この種のコネクタの状態は、証明書や資格情報の有効期限のタイムスタンプに基づきます。  

*[コネクタの状態]* タブを開くと、一覧の先頭に異常なコネクタが表示されます。 次に警告のあるコネクタ、その後に正常なコネクタがリストされます。 まだ構成していないコネクタは、最後に *[有効になっていません]* として表示されます。

いずれか 1 つの種類に複数のコネクタがある場合、状態は同じすべてのコネクタの概要となります。 任意の 1 つのコネクタの最低レベルの正常な状態が、グループの正常性として使用されます。  

**コネクタの状態:**
- **異常:**
  - 証明書または資格情報の有効期限が切れています
  - 最後の同期は 3 日以上前に行われています
- **警告:**
  - 証明書または資格情報の有効期限は 7 日以内に切れます
  - 最後の同期は 2 日以上前に行われています
- **正常:**
  - 証明書または資格情報の有効期限は、次の 7 日以内に切れません
  - 最後の同期日から 1 日経過していません  

一覧からコネクタを選択すると、そのコネクタに関するポータル ページがポータルに表示されます。 [コネクタ] ページから、構成済みのコネクタの状態を確認したり、同じ種類の新しいコネクタを追加または作成するためのオプションを選択したりできます。

たとえば、 **[VPP の有効期限日]** コネクタを選択すると、 **[iOS ボリューム購入プログラム トークン]** ページが開き、そこでそのコネクタの詳細を確認できます。 また、新しい構成を作成したり、既存のものを編集して問題を解決したりすることもできます。

## <a name="service-health-dashboard"></a>サービス正常性ダッシュボード  
サービス正常性ダッシュボードでは、テナントに影響を与える "*サービス インシデント*" の詳細と、更新プログラムと予定されている変更に関する情報を提供する "*Intune ニュース*" を確認できます。

### <a name="intune-service-health"></a>Intune サービスの正常性
アクティブなインシデントやアドバイザリの詳細が表示されます。その際に、Microsoft 365 のサービス正常性ダッシュボードにもメッセージ センターにも移動する必要はありません。これらは両方とも、[Microsoft 365 管理センター](https://admin.microsoft.com)にあります。 テナントに影響を与えるインシデントのみが表示されます。  

インシデントを選択すると、[Tenant Status]\(テナントの状態\) ページに直接インシデントの詳細が表示されます。 過去のアドバイザリとインシデントを表示するには、 **[過去のインシデント/アドバイザリを参照してください]** を選択します。 Microsoft 365 管理センターが開き、テナントの過去 30 日間のアドバイザリとインシデントを表示できます。  

*Intune サービスの正常性*の情報を表示するには、Azure Active Directory または Microsoft 365 管理センターでの**グローバル管理者**ロールまたは**サービス管理者**ロールがご利用のアカウントに割り当てられている必要があります。 これらの権限を割り当てるには、グローバル管理者権限で [Microsoft 365 管理センター](https://admin.microsoft.com)にサインインします。 **[ユーザー] > [アクティブ ユーザー]** の順に選択し、アクセスが必要なアカウントを選択します。 ロールに対して **[編集]** を選択し、*サービス管理者* または*グローバル管理者* を選んでから、編集内容を**保存**して権限を割り当てます。  

Microsoft 365 管理センターを通じて設定できるのは、Intune サービスの正常性の通信設定のみとなります。

### <a name="intune-news"></a>Intune ニュース  
Intune サービス チームからの通信情報を表示します。その際に、Office メッセージ センターに移動する必要はありません。 通信には、Intune サービスに対して最近行われた変更や、テナントについて実行中の変更に関するメッセージが含まれます。  

既定では、最新のアクティブなメッセージが 10 件表示されます。 古いメッセージを表示するには、 **[過去のメッセージを参照してください]** を選択し、Microsoft 365 管理センターで*メッセージ センター* を開きます。  

Intune ニュースの情報を表示するには、Azure Active Directory での**グローバル管理者**ロールもしくは**サービス管理者**ロール、または Microsoft 365 管理センターでの**メッセージ センター閲覧者**ロールがアカウントに割り当てられている必要があります。  この権限を割り当てるには、管理者権限で [Microsoft 365 管理センター](https://admin.microsoft.com)にサインインします。 **[ユーザー] > [アクティブ ユーザー]** の順に選択し、アクセスが必要なアカウントを選択します。 *ロール* に対して **[編集]** を選択し、*Teams 通信管理者* を選んでから、編集内容を**保存**して権限を割り当てます。  

Microsoft 365 管理センターを通じて設定できるのは、Intune ニュースの通信設定のみとなります。