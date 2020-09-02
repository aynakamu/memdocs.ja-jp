---
title: Microsoft Intune で教育設定を追加または構成する - Azure | Microsoft Docs
description: Windows 10 以降のデバイス上の Microsoft Intune では、デバイス構成プロファイル内にテスト アプリを使用します。 教育設定を使用する構成プロファイルを作成して、テスト アプリの URL の入力、ユーザーのサインイン方法の選択、テスト中の画面の監視、テスト中のテキスト候補の許可または禁止を行います。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b1a605e456edb525afec306ff594ba7cc3895aa
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912731"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Windows 10 デバイス上の Microsoft Intune でテスト アプリを使用する

Intune の [教育] プロファイルは、デバイス上でテストや試験を受ける学生向けに設計されています。 この機能には、**テスト** アプリと、テスト URL の追加、エンドユーザーによるテストへのサインイン方法の選択などの設定が含まれています。 この機能は次のプラットフォームをサポートしています。

- Windows 10 以降

ユーザーがサインインすると、テスト アプリが自動的に開き、入力したテストが表示されます。 テスト中は他のアプリをデバイス上で実行できません。 テスト アプリの詳細については、「[Windows 10 でテストを受ける](/education/windows/take-tests-in-windows-10)」を参照してください。

この記事では、Microsoft Intune でデバイス構成プロファイルを作成する手順を説明します。 また、Windows 10 デバイスに使用できる教育設定について読み、学習するための情報も含まれています。

## <a name="create-a-device-profile"></a>デバイス プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイル]** : **[セキュリティで保護された評価 (教育)]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:新しいプロファイルのわかりやすい名前を入力します。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** で、構成する設定を入力します。

    - [Windows 10 以降](education-settings-windows.md)

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはユーザー グループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

次に各デバイスがチェックインするときに、ポリシーが適用されます。

## <a name="next-steps"></a>次のステップ

[Windows 10 の教育設定](education-settings-windows.md)の一覧とその説明を参照してください。

[プロファイルを割り当てた](device-profile-assign.md)後は、[その状態を監視します](device-profile-monitor.md)。