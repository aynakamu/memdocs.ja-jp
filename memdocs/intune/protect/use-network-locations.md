---
title: Microsoft Intune - Azure でネットワークの場所に基づいて Android デバイスをバインドする | Microsoft Docs
description: Microsoft Intune で Android デバイスのネットワークの場所を作成または構成します。 デバイスのネットワークの場所に基づいて、デバイスを非準拠としてマークすることができます。 デバイスがネットワークの場所の外に移動された場合、会社のリソースへのアクセスをブロックすることができます。
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ayesham
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4da3a8e9e59f1f6a4d1c38354f14163c4773fd7d
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325302"
---
# <a name="use-locations-network-fence-in-intune"></a>Intune で場所 (ネットワーク フェンス) を使用する

デバイスが場所を離れた場合、企業ネットワークへのアクセスをブロックすることができます。 Intune の**場所**機能では、この機能が提供されます。 

ネットワーク フェンスとも呼ばれる、ネットワークの場所ベースのコンプライアンス ポリシーを作成できます。 ポリシーは、デバイスが準拠するように社内ネットワークに接続されるようにします。 このポリシーを条件付きアクセス ポリシーと共に使用して、デバイスが社内ネットワークに接続されているときに "*のみ*"、職場のリソースにアクセスできるようにします。 デバイスが社内ネットワークに接続されていない場合、そのデバイスは非準拠となり、社内ネットワークにアクセスできなくなります。

次のシナリオを想定してください。

製造工場では、一部の従業員が Android デバイスを使用しています。 ある従業員は、工場の外に Android デバイスを持ち出しています。 無許可のアクセスを防止するために、次の操作を行うことができます。

1. **製造フロア**という IPv4 範囲で場所を作成します。
2. これらのデバイスを企業ネットワークに接続することを要求するコンプライアンス ポリシーを作成し、このポリシーを割り当てます。
3. デバイスが製造工場の外に移動された場合、そのデバイスは非準拠と見なされ、企業リソースにアクセスできなくなります。

さらに、[コンプライアンス非対応に対するアクション](#configure-the-actions-for-noncompliance)を追加することができます。 デバイスがオンプレミスとネットワークの場所に戻された場合は、企業リソースに再度アクセスできるようになります。

## <a name="prerequisites"></a>[前提条件]

場所ベースのコンプライアンス ポリシーを作成するには

- デバイスが接続されるゲートウェイ サーバー、DHCP サーバー、または DNS サーバーの IPV4 ネットワーク範囲として、ネットワークの場所を作成する
- これらの場所を使用し、デバイスがネットワークの場所に接続されなくなったときに実行するアクションを定義するコンプライアンス ポリシーを作成する
- Android デバイス 6.0 以降 (ポータル サイト アプリ更新済み)

## <a name="create-a-location"></a>場所を作成する

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[場所]**  >  **[作成]** を選択します。

2. 次のプロパティを入力します。  

   - 必須。 場所の**名前** (**製造フロア**や **Building 44-secure** など) を入力します。
   - 任意。 CIDR (クラスレス ドメイン間ルーティング) 表記で **IPv4 の範囲** (`aaa.bbb.ccc.ddd/n` など) を入力します。
   - 任意。 **IPv4 ゲートウェイ** アドレス (`aaa.bbb.ccc.ddd` など) を入力します。
   - 任意。 **IPv4 DHCP サーバー** アドレス (`aaa.bbb.ccc.ddd` など) を入力します。
   - 任意。 **IPv4 DNS サーバー** アドレスのリストを入力します。 この設定では**サブセット照合**を使用します。 デバイスの IPv4 DNS サーバーが定義されている値のサブセットである場合、デバイスはフェンス内にあると見なされます。 次のように、必ず 1 行に 1 つのアドレスを入力してください。  
     `aaa.bbb.ccc.ddd`  
     `aaa.bbb.ccc.ddd`
   - 任意。 **DNS サフィックス**のリストを入力します。 この設定では**サブセット照合**を使用します。 デバイスの DNS サフィックスが定義されている値のサブセットである場合、デバイスはフェンス内にあると見なされます。 次のように、必ず 1 行に 1 つのドメイン名を入力してください。  
     `contoso.com`  
     `contoso.org`

3. 変更内容を**保存**します。

## <a name="create-the-location-compliance-policy"></a>場所のコンプライアンス ポリシーを作成する

[コンプライアンス ポリシーを作成する](create-compliance-policy.md)ときは、 **[プラットフォーム]** として **[Android]** を選択します。 **場所**では、追加した 1 つ以上のネットワークの場所を選択できます。 これらの場所は、デバイス用に作成するネットワーク フェンスの一部です。

## <a name="configure-the-actions-for-noncompliance"></a>コンプライアンス違反に対するアクションを構成する

コンプライアンス ポリシーが作成されると、コンプライアンス違反に対する既定のアクションがデバイスに適用されます。 さらにアクションを追加することができます。 たとえば、デバイスが場所に準拠しなくなった場合に、ユーザーにメールを送信するアクションを追加します。

ガイダンスについては、「[コンプライアンス違反に対するアクションを追加する](actions-for-noncompliance.md)」を参照してください。

## <a name="company-portal-app"></a>ポータル サイト アプリ

デバイスがご利用の場所に接続されている場合、そのデバイスはポータル サイト アプリに準拠として表示されます。 デバイスがどの場所にも接続されていない場合、そのデバイスは非準拠として表示されます。

## <a name="next-steps"></a>次のステップ

[Intune デバイスのコンプライアンス対応ポリシーの監視](compliance-policy-monitor.md)  
[Intune のコンプライアンス ポリシーの概要](device-compliance-get-started.md)
