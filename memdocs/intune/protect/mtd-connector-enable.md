---
title: Microsoft Intune で Mobile Threat Defense コネクタを有効にする
titleSuffix: Microsoft Intune
description: Mobile Threat Defense (MTD) パートナーと Microsoft Intune の間のコネクタを有効にします。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dbb6a37e-ba47-4b69-922c-d25e66c279f6
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee2d88e444941f2b75e6dcc716748c442de459a6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351514"
---
# <a name="enable-the-mobile-threat-defense-connector-in-intune"></a>Intune で Mobile Threat Defense コネクタを有効にする

Mobile Threat Defense (MTD) のセットアップ中、Mobile Threat Defense パートナー コンソールで脅威を分類するためのポリシーを構成し、Intune でデバイスのコンプライアンス ポリシーを作成しました。 MTD パートナー コンソールで Intune コネクタを既に構成している場合、MTD パートナー アプリケーションに対して MTD 接続を有効にすることができます。

> [!NOTE]
> このトピックは、すべての Mobile Threat Defense パートナーに適用されます。

## <a name="classic-conditional-access-policies-for-mtd-apps"></a>MTD アプリ用の従来の条件付きアクセス ポリシー

新しいアプリケーションを Intune Mobile Threat Defense に統合し、Intune への接続を有効にすると、Intune によって Azure Active Directory 内に従来の条件付きアクセス ポリシーが作成されます。 統合する各 MTD アプリ ([Defender ATP](advanced-threat-protection.md) や追加の [MTD パートナー](mobile-threat-defense.md#mobile-threat-defense-partners)など) によって、新しい従来の条件付きアクセス ポリシーが作成されます。 これらのポリシーは無視してもかまいませんが、編集、削除、または無効にすることはできません。

従来のポリシーを削除した場合は、その作成に使用された Intune への接続を削除してから、それを再設定する必要があります。 このプロセスにより、従来のポリシーが再作成されます。 MTD アプリ用の従来のポリシーを、条件付きアクセス用の新しいポリシーの種類に移行することは、サポートされていません。

MTD アプリ用の従来の条件付きアクセス ポリシーは:

- デバイスが Azure AD に登録され、MTD パートナーと通信する前にデバイス ID を持っていることを要求するために、Intune MTD によって使用されます。 ID は、デバイスが Intune に正常に自身の状態を報告できるようにするために必要です。

- 他のクラウド アプリやリソースには影響しません。

- MTD の管理を支援するために作成する条件付きアクセス ポリシーとは異なります。

- 既定では、評価に使用する他の条件付きアクセス ポリシーとは対話しません。

従来の条件付きアクセス ポリシーを表示するには、[Azure](https://portal.azure.com/#home) で **[Azure Active Directory]**  >  **[条件付きアクセス]**  >  **[クラシック ポリシー]** の順に移動します。

## <a name="to-enable-the-mobile-threat-defense-connector"></a>Mobile Threat Defense コネクタを有効にするには

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[Mobile Threat Defense]** の順に選択します。

3. **[Mobile Threat Defense]** ウィンドウで、 **[追加]** を選択します。

4. **[セットアップする Mobile Threat Defense コネクタを選択する]** で、ドロップダウン リストからお使いの MTD ソリューションを選択します。

5. 組織の要件に合わせて切り替えオプションを有効にします。 表示される切り替えオプションは、MTD パートナーによって異なります。  たとえば、次の図では、Symantec Endpoint Protection で使用できるオプションが示されています。

   ![Intune Azure Portal での MTD のセットアップ](./media/mtd-connector-enable/enable-mtd-connector-1.png)

## <a name="mobile-threat-defense-toggle-options"></a>Mobile Threat Defense 切り替えオプション

組織の要件に基づき、有効にする MTD 切り替えオプションを決定できます。 すべての Mobile Thread Defense パートナーでは、次のすべてのオプションがサポートされているわけではありません。

**MDM コンプライアンス ポリシー設定**

- **[バージョン \<_サポートされているバージョン_> 以上の Android デバイスを \<_MTD パートナー名_> に接続します]** : このオプションを有効にすると、Android 4.1+ デバイスはセキュリティ上のリスクを Intune に報告します。

- **[バージョン \<_サポートされているバージョン_> 以上の iOS デバイスを \<_MTD パートナー名_> に接続します]** : このオプションを有効にすると、iOS 8.0 以降のデバイスはセキュリティ上のリスクを Intune に報告します。

- **[iOS デバイスのアプリの同期を有効にする]** :この Mobile Threat Defense パートナーに、Intune から iOS アプリケーションのメタデータを脅威分析用に要求することを許可します。

- **[サポートされていない OS バージョンをブロックする]** :デバイスがサポートされる最低バージョン以前のオペレーティング システムを実行している場合は、ブロックします。

**アプリ保護ポリシー設定**

- **[アプリ保護ポリシーの評価のため、バージョン \<*サポートされているバージョン*> 以降の Android デバイスを \<*MTD パートナー名*> に接続します]** : このオプションを有効にすると、デバイスの脅威レベルの規則を使用したアプリ保護ポリシーによって、このコネクタのデータを含むデバイスが評価されます。

- **[アプリ保護ポリシーの評価のため、バージョン \<*サポートされているバージョン*> 以降の iOS デバイスを \<*MTD パートナー名*> に接続します]** : このオプションを有効にすると、デバイスの脅威レベルの規則を使用したアプリ保護ポリシーによって、このコネクタのデータを含むデバイスが評価されます。

Intune アプリ保護ポリシーを評価するために Mobile Threat Defense コネクタを使用する方法について詳しくは、[登録されていないデバイスに対する Mobile Threat Defense の設定](mtd-enable-unenrolled-devices.md)に関するページをご覧ください。

**共通の共有設定**

- **[パートナーが無応答になるまでの日数]** :接続が失われたためにパートナーが応答していないと Intune が判断するまでの、非アクティブ状態の日数。 Intune は、応答しない MTD パートナーのコンプライアンス対応状態を無視します。

> [!IMPORTANT]
> 可能な場合には、デバイス コンプライアンスと条件付きアクセス ポリシー ルールを作成する前に、MTD アプリを追加して割り当てることをお勧めします。 これにより、MTD アプリはエンド ユーザーがインストールできる状態になり、アプリをインストールするとエンド ユーザーは電子メールや他の会社のリソースにアクセスできます。

> [!TIP]
> [Mobile Threat Defense] ウィンドウで、 **[接続の状態]** や、Intune と MTD パートナー間の **[最終同期]** 時刻を確認できます。

## <a name="next-steps"></a>次のステップ

- [Intune で Mobile Threat Defense (MTD) アプリ保護ポリシーを作成します](mtd-app-protection-policy.md)。
