---
title: Microsoft Intune の使用条件の設定
titleSuffix: ''
description: Intune 用ポータル サイトでユーザーに表示する使用条件を設定します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/20/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4a3a11a8-9c0c-4334-8c6b-6fea4d0a2efb
ms.reviewer: amyro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26c30c947c6db1d44d8438aa63972fd5a3f663cd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79363435"
---
# <a name="terms-and-conditions-for-user-access"></a>ユーザー アクセスに関する使用条件

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune 管理者は、ユーザーがポータル サイトを使用して以下の操作を行う前に、会社の使用条件に同意することを必須にすることができます。
- デバイスを登録する
- 会社のアプリやメールなどのリソースにアクセスする。

使用条件の構成は任意です。

複数の条件セットを作成し、異なるグループに割り当てることができます。それにより、たとえば、さまざまな言語をサポートします。

会社の使用条件を作成する方法は 2 つあります。
- この記事で説明されているように Intune を使用する。
- [Azure Active Directory の利用規約機能](https://docs.microsoft.com/azure/active-directory/governance/active-directory-tou)を使用する。

どちらの方法が最適かについては、[「Choosing the right Terms solution for your organization (組織に適した利用規約ソリューションの選択)」のブログ記事](https://go.microsoft.com/fwlink/?linkid=2010506&clcid=0x409)を参照してください。 

## <a name="create-terms-and-conditions"></a>使用条件を作成する
次の手順で使用条件を作成します。 表示名と説明は管理目的で使用されます。条件のプロパティはポータル サイトでユーザーに表示されます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[テナント管理]**  >  **[使用条件]** の順に選択します。
2. **[作成]** を選択します。
3. **[基本]** ページで、次の情報を指定します。

   - **名前**:Azure portal における条件の名前。 ユーザーにはこの名前は表示されません。
   - **説明**:Azure portal 上でこの条件セットの識別に役立つ任意の説明。

    ![使用条件の [基本] ページを示した Azure portal のスクリーンショット](./media/terms-and-conditions-create/terms-basics-page.png)

4. **[次へ]** を選択して、 **[使用条件]** ページへ移動し、次の情報を指定します。

   - **[タイトル]** :ポータル サイト上で **[概要]** の上に表示される使用条件の名前。
   - **[使用条件]** :ユーザーに確認と承諾または拒否を求める使用条件。
   - **[使用条件の概要]** :使用条件に対するユーザーの同意が意味することを説明するテキスト。 たとえば、「デバイスを登録すると、Contoso が定めている利用規約に同意することになります。 条件をよく読んでから続行してください。」のように入力します。

5. **[次へ]** を選択して、 **[スコープ タグ]** ページへ移動します。

6. **[スコープ タグを選択]** を選択し、これらの使用条件に割り当てるスコープ タグを選択し、 **[選択]** を選択します。 

7. **[次へ]** を選択して **[割り当て]** ページへ移動し、 **[割り当て先]** に次のオプションから 1 つを選択します。
    - **[すべてのユーザー]** : これらの使用条件をすべてのユーザーに割り当てるには、このオプションを選択します。
    - **[グループの選択]** : これらの使用条件を、 **[含めるグループを選択]** を選択して特定したグループの全員に割り当てるには、このオプションを選択します。

8. **[次へ]**  >  **[作成]** の順に選択します。

## <a name="see-how-terms-are-displayed-to-your-users"></a>ユーザーにどのように条項が表示されるか確認する
次の例は、管理コンソールとポータル サイトに表示される **[タイトル]** と **[使用条件の概要]** です。

![管理コンソールとポータル サイトに表示されるタイトルと使用条件の概要のスクリーンショット。](./media/terms-and-conditions-create/terms-summary-terms.png)

次の例は、管理コンソールとポータル サイトに表示される使用条件です。

![管理コンソールとポータル サイトに表示される使用条件のスクリーンショット。](./media/terms-and-conditions-create/terms-properties-terms.png)


## <a name="monitor-terms-and-conditions"></a>使用条件の監視

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[テナント管理]**  >  **[使用条件]** の順に選択します。
2. 使用条件の一覧で、承諾を表示する条件を選択し、 **[Acceptance Reporting]\(承諾報告\)** を選択します。

## <a name="work-with-multiple-versions-of-terms-and-conditions"></a>使用条件の複数のバージョンを使用する
使用条件を編集し、そのバージョンを管理できます。 使用条件に重大な変更を加えるたびに、以下を行うようにします。
- バージョン番号を増やします。
- 新しい使用条件に同意することをユーザーに要求します。

誤植の修正や書式設定の変更などを行った場合は、現在のバージョン番号をそのまま保持します。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[テナント管理]**  >  **[使用条件]** の順に選択し、変更する使用条件を選択してから、 **[プロパティ]** を選択します。

2. **[プロパティ]** ウィンドウで、 **[使用条件]** を選択し、必要に応じて **[タイトル]** 、 **[使用条件の概要]** 、 **[使用条件]** を変更します。 変更を加えた結果、ユーザーが新しい条件を承諾する必要が生じた場合は、 **[ユーザーに対してもう一度同意を求めて、バージョン番号を <番号> に上げます。]** を選択します。

3. **[OK]**  >  **[保存]** の順に選択します。

ユーザーは、更新された使用条件に 1 回だけ同意する必要があります。 複数のデバイスを持つユーザーは、各デバイスで使用条件に同意する必要はありません。
