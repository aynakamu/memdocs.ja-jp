---
title: Microsoft Intune での Windows 8.1 のコンプライアンス設定 - Azure | Microsoft Docs
description: Microsoft Intune で Windows 8.1 デバイスにコンプライアンスを設定するときに使用できるすべての設定の一覧を表示します。 最小と最大のオペレーティング システムでコンプライアンスを確認する、パスワードの制限と長さを設定する、データ ストレージで暗号化を有効にするなどを行います。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b423d289e81c48479adcaa7a594974b23a9476c
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252709"
---
# <a name="windows-81-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Intune を使用してデバイスを準拠または非準拠としてマークするための Windows 8.1 設定

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]
この記事では、Intune で Windows 8.1 デバイスに構成できる、さまざまなコンプライアンス設定の一覧を示して説明します。 モバイル デバイス管理 (MDM) ソリューションの一部として、これらの設定を使用した単純なパスワードのブロック、OS の最小バージョンまたは最大バージョンの設定などを行います。

この機能は、以下に適用されます。

- Windows 8.1 以降

Intune サービス管理者は、組織のリソースの保護に役立てるために、これらのコンプライアンス設定を使用します。 コンプライアンス ポリシーの詳細およびその機能については、[デバイス コンプライアンスの概要](device-compliance-get-started.md)に関するページを参照してください。

## <a name="before-you-begin"></a>始める前に

[コンプライアンス ポリシーの作成](create-compliance-policy.md#create-the-policy)。 **[プラットフォーム]** には、 **[Windows 8.1 以降]** を選択します。

## <a name="device-properties"></a>デバイスのプロパティ

### <a name="operating-system-version"></a>オペレーティング システムのバージョン

**Windows 8.1 以降**
- **[最小 OS バージョン]** :  
  許容される最小バージョンを入力します。 デバイスが最小 OS バージョンの要件を満たしていない場合、非準拠として報告されます。 アップグレード方法に関する情報のリンクが表示されます。 デバイスのユーザーは、デバイスのアップグレードを行うことを選択してから、会社のリソースにアクセスできます。

- **[最大 OS バージョン]** :  
  許容される最大バージョンを入力します。 ルールに入力されたバージョンよりも新しいバージョンの OS がデバイスで使用されている場合、組織のリソースへのアクセスがブロックされます。 デバイスのユーザーは、各自の IT 管理者に問い合わせるように求められます。 その OS バージョンを許可するようにルールが変更されるまで、そのデバイスでは組織のリソースにアクセスできません。

Windows 8.1 PC の場合、バージョン **3** が返されます。 Windows に関して OS バージョンのルールを Windows 8.1 に設定した場合、デバイスに Windows 8.1 がインストールされていても、そのデバイスは非準拠として報告されます。

## <a name="system-security"></a>システム セキュリティ

### <a name="password"></a>パスワード

- **[モバイル デバイスのロック解除にパスワードを必要とする]** :  
  - **[未構成]** ("*既定値*") - この設定に対して準拠であるか非準拠であるかの評価は行われません。
  - **[必須]** - デバイスにアクセスするユーザーにパスワードを入力するよう求めます。

- **[単純なパスワード]** :  
  - **[未構成]** ("*既定*") - ユーザーは、**1234** や **1111** のような単純なパスワードを作成することができます。
  - **[ブロック]** - ユーザーは単純なパスワード (**1234**、**1111** など) を作成できません。  

- **[パスワードの最小文字数]** :  
  パスワードに必要な数字または文字の最小数を入力します。

  Windows が実行されていて Microsoft アカウントでアクセスされるデバイスについては、次のいずれかの条件が満たされる場合、コンプライアンス ポリシーは正常に評価されません。  
  - パスワードの最小文字数が 8 文字を超える
  - 文字セットの最小数が 2 より大きい

- **パスワードの種類**:  
  パスワードの内容を**数字**のみにするかどうか、あるいは数字とその他の文字との組み合わせ (**英数字**) にするかどうかを選択します。

  "*英数字*" に設定した場合は、次の設定を使用できます。  

  - **[パスワードに使用する英数字以外の文字数]** :  
    "*パスワードの種類*" が **[英数字]** に設定されている場合、パスワードに含める必要がある、文字セットの最小数を指定します。 オプションは **0** から **4** までで、既定値は **1** です。
    
    次の 4 つの文字セットがあります。
    - 小文字
    - 大文字
    - 記号
    - 数字

    大きな数値を設定すると、ユーザーはより複雑なパスワードを作成する必要があります。 Microsoft アカウントでアクセスされるデバイスについては、次のいずれかの条件が満たされる場合、コンプライアンス ポリシーは正常に評価されません。

    - パスワードの最小文字数が 8 文字を超える
    - 文字セットの最小数が 2 より大きい

- **[パスワードが要求されるまでの非アクティブの最長時間 (分)]** :  
  ユーザーがパスワードを再入力しなければならなくなるまでのアイドル時間を入力します。

- **[パスワードの有効期限 (日数)]** :  
  パスワードの有効期限が切れ、ユーザーが新しく作成しなければならなくなるまでの日数を選択します。

- **[再使用を禁止するパスワード世代数]** :  
  何回前までのパスワードを使用できないようにするかを入力します。

### <a name="encryption"></a>暗号化

- **[デバイス上のデータ ストレージの暗号化]** :  
  - **[未構成]** ("*既定値*")
  - **[必須]** - デバイス上のデータ ストレージを暗号化するには、 *[必須]* を選択します。


<!-- not on phone   
- **Require encryption on mobile device**: **Require** the device to be encrypted to connect to data storage resources.
--> 

## <a name="next-steps"></a>次のステップ

- [非準拠デバイスに対するアクションを追加](actions-for-noncompliance.md)し、[スコープのタグを使用してポリシーをフィルター処理する](../fundamentals/scope-tags.md)
- [コンプライアンス ポリシーを監視する](compliance-policy-monitor.md)
- [Windows 10 以降のデバイス向けのコンプライアンス ポリシー設定](compliance-policy-create-windows.md)を確認する