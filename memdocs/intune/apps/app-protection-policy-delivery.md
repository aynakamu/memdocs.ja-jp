---
title: アプリ保護ポリシーの配信とタイミングの概要
titleSuffix: Microsoft Intune
description: アプリケーション保護ポリシーのさまざまなデプロイ期間について学習し、変更がエンド ユーザーのデバイスにいつ反映されるかを理解します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ec111319-7e02-434f-946b-88647726bf1a
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8318e6dc364d0dfbf38ac278938018b80f703b58
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342037"
---
# <a name="understand-app-protection-policy-delivery-timing"></a>アプリ保護ポリシーの配信タイミングの概要

アプリケーション保護ポリシーのさまざまなデプロイ期間について学習し、変更がエンド ユーザーのデバイスにいつ反映されるかを理解します。

## <a name="delivery-timing-summary"></a>配信タイミングの概要

アプリケーション保護ポリシーの配信は、ユーザーのライセンスの状態と Intune サービス登録によって変わります。  

|    ユーザーの状態    |    アプリ保護の動作     |    再試行間隔 (注を参照してください)    |    これが発生する理由    |
|-----------------------------------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
|    Tenant Not Onboarded (テナントがオンボードされていない)    |    次の再試行間隔を待機します。  このユーザーのアプリ保護がアクティブではありません。    |    24 時間    |    Intune のテナントを設定していない場合に発生します。    |
|    User Not Licensed (ユーザーにライセンスが付与されていません)     |    次の再試行間隔を待機します。  このユーザーのアプリ保護がアクティブではありません。     |    12 時間 - ただし、Android デバイス上では、この間隔には Intune APP SDK バージョン 5.6.0 以降が必要です。 それ以外の Android デバイスの場合、間隔は 24 時間です。   |    Intune のユーザーにライセンスが付与されていない場合に発生します。    |
|    User Not Assigned App Protection Policies (ユーザーにアプリ保護ポリシーが割り当てられていません)    |    次の再試行間隔を待機します。  このユーザーのアプリ保護がアクティブではありません。    |    12 時間        |    アプリ設定がユーザーに割り当てられていない場合に発生します。    |
|    User Assigned App Protection Policies but app is not defined in the App Protection Policies (ユーザーがアプリ保護ポリシーを割り当てたが、アプリ保護ポリシーでアプリが定義されていません)   |    次の再試行間隔を待機します。  このユーザーのアプリ保護がアクティブではありません。    |    12 時間        |    アプリを APP に追加していない場合に発生します。    |
|    User Successfully Registered for Intune MAM (ユーザーが Intune MAM に正常に登録されました)    |    アプリ保護はポリシー設定ごとに適用されます。    更新は再試行間隔で発生します    |    Intune サービスはユーザーの負荷に基づいて定義されます。    通常は 30 分です。     |    ユーザーが MAM 構成用の Intune サービスに正常に登録したときに発生します。    |

> [!NOTE]
> 再試行間隔には、アクティブなアプリの使用の発生 (つまり、アプリが起動され、使用中であること) が必要になることがあります。  再試行間隔が 24 時間で、ユーザーがアプリの起動を 48 時間待つと、アプリケーション保護クライアントは 48 時間後に再試行されます。

## <a name="handling-network-connectivity-issues"></a>ネットワーク接続の問題の処理

ネットワーク接続の問題が原因でユーザー登録が失敗した場合は、高速の再試行間隔が使用されます。  間隔が 60 分に達するか、または接続が成功するまで、アプリケーション保護クライアントでは徐々に長い間隔で再試行されます。  接続が成功するまで、クライアントでは 60 分間隔で再試行が続けられます。 その後、クライアントはユーザー状態に基づいて標準の再試行間隔に戻ります。

## <a name="next-steps"></a>次のステップ

[Intune にデバイスを登録できるようにライセンスをユーザーに割り当てる](../fundamentals/licenses-assign.md)

