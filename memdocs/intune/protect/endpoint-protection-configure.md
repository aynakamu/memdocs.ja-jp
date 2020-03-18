---
title: Microsoft Intune - Azure でエンドポイント保護設定を構成する | Microsoft Docs
description: Microsoft Intune で macOS または Windows 10 デバイス プロファイルを作成するとき、エンドポイント保護設定を作成します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 64a11cf9dca110a4a802ddff3e9176ec1ce88345
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352177"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Intune でエンドポイント保護設定を追加する

Intune でデバイスの構成プロファイルを使用し、次などのデバイスで、共通のエンドポイント保護セキュリティ機能を管理できます。

- ファイアウォール
- BitLocker
- アプリの許可とブロック
- Microsoft Defender と暗号化

たとえば、macOS ユーザーに Mac App Store からのみアプリのインストールを許可するエンドポイント保護プロファイルを作成できます。 あるいは、Windows 10 デバイスでアプリを実行しているとき、Windows SmartScreen を有効にします。

プロファイルを作成する前に、サポート対象のそれぞれのプラットフォームで Intune が管理できる、エンドポイント保護設定の詳細が記述されている次の記事を確認してください。

- [macOS の設定](endpoint-protection-macos.md)
- [Windows 10 の設定](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>エンドポイント保護設定を含むデバイス プロファイルを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. エンドポイント保護プロファイルの **[名前]** と **[説明]** を入力します。

4. **[プラットフォーム]** ドロップダウン リストで、カスタム設定を適用するデバイス プラットフォームを選択します。 現時点では、デバイスの制限設定に対応している次のいずれかのプラットフォームを選択できます。

   - **macOS**
   - **Windows 10 以降**

5. **[プロファイルの種類]** ドロップダウン リストで、 **[Endpoint Protection]** を選択します。

6. 選択したプラットフォームによって構成できる設定が異なります。 関連項目

   - [macOS の設定](endpoint-protection-macos.md)
   - [Windows 10 の設定](endpoint-protection-windows-10.md)

7. 適切な設定を構成したら、 **[プロファイルの作成]** ページで **[作成]** を選択します。

   プロファイルが作成され、プロファイルの一覧ページに表示されます。 このプロファイルをグループに割り当てる場合は、[デバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Windows 10 デバイスのカスタム ファイアウォール規則を追加する

Windows 10 のエンドポイント保護規則を含むプロファイルの一部として Microsoft Defender ファイアウォールを構成する場合は、ファイアウォールのカスタム規則を構成できます。 カスタム規則を使用すると、Windows 10 でサポートされているファイアウォール規則の定義済みセットを拡張できます。

カスタム ファイアウォール規則を含むプロファイルを計画する場合は、次の情報を考慮してください。これは、プロファイルでファイアウォール規則をグループ化する際に選択する方法に影響する可能性があります。

- 各プロファイルでは、最大 150 個のファイアウォール規則がサポートされます。 150 個を超える規則を使用する場合は、それぞれ 150 個の規則に限定された、追加のプロファイルを作成します。

- プロファイルごとに、単一の規則を適用できなかった場合、そのプロファイルのすべての規則が失敗し、デバイスにはどの規則も適用されません。

- 規則を適用できなかったときは、プロファイル内のすべての規則が失敗として報告されます。 Intune では、失敗した個々の規則を識別することはできません。  

Intune で管理できるファイアウォール規則については、Windows の[ファイアウォール構成サービス プロバイダー]( https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP) に関するページで詳しく説明されています。 Intune でサポートされる Windows 10 デバイスのカスタム ファイアウォール設定のリストを確認する場合は、[カスタム ファイアウォール規則](endpoint-protection-windows-10.md#firewall-rules)に関するセクションを参照してください。

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Endpoint Protection プロファイルにカスタム ファイアウォール規則を追加するには

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. *[プラットフォーム]* では **[Windows 10 以降]** を選択し、 *[プロファイルの種類]* では **[Endpoint protection]** を選択します。

4. **[Microsoft Defender ファイアウォール]** を選択して構成ページを開き、 *[ファイアウォール規則]* に対して **[追加]** を選択して、 **[規則の作成]** ページを開きます。

5. ファイアウォール規則の設定を指定し、 **[OK]** を選択して保存します。 ドキュメントで利用可能なカスタム ファイアウォール規則のオプションを確認する場合は、[カスタム ファイアウォール規則](endpoint-protection-windows-10.md#firewall-rules)に関するセクションを参照してください。

6. 保存した規則は、 *[Microsoft Defender ファイアウォール]* ページの規則の一覧に表示されます。

7. 規則を変更するには、リストから規則を選択して **[規則の編集]** ページを開きます。

8. プロファイルから規則を削除するには、その規則の省略記号 **(...)** を選択し、 **[削除]** を選びます。

9. 規則の表示順序を変更するには、規則リストの上部にある*上矢印、下矢印* アイコンを選択します。

## <a name="next-steps"></a>次のステップ

プロファイルをグループに割り当てる場合は、[デバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。
