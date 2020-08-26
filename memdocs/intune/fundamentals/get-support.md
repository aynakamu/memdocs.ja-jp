---
title: Microsoft Intune のサポートを受ける方法
titleSuffix: Microsoft Intune
description: Microsoft Intune の有料サブスクリプションと試用版サブスクリプションについて、オンラインと電話によるサポートを受けます。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/25/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7fc95d17-098e-4da5-8a09-a96476569dd9
ms.reviewer: crisk
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f71a74c69235e8e079f2cd325582dbbe9bb4a3f1
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820665"
---
# <a name="how-to-get-support-for-microsoft-intune"></a>Microsoft Intune のサポートを受ける方法

Microsoft サポートは、Microsoft Intune に世界的な技術、購入前、請求、およびサブスクリプションのサポートを提供しています。 有料サブスクリプションと試用版サブスクリプションについて、オンラインと電話によるサポートを利用できます。 オンライン テクニカル サポートは、英語と日本語で提供されています。 電話によるサポートとオンライン課金サポートは、他の言語でも利用できます。

Intune 管理者は、 **[ヘルプとサポート]** オプションを使用して、Azure portal から Intune 用のオンライン サポート チケットを提出することができます。 サポート インシデントを作成して管理するには、お使いのアカウントに、"*アクション*" **microsoft.office365.supportTickets** を含む Azure Active Directory (Azure AD) ロールが付与されている必要があります。 サポート チケットを作成するために必要な Azure AD のロールとアクセス許可については、[Azure Active Directory での管理者ロール](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)に関するページを参照してください。

>[!IMPORTANT]
> Intune と連携するサードパーティ製品 (Saaswedo、Cisco、Lookout など) のテクニカル サポートについては、まず、その製品の提供元に連絡してください。 Intune サポート要求を開始する前に、その他の製品が正しく構成されていることを確認します。
>
> Microsoft Intune に関連する問題のトラブルシューティングについては、Intune のドキュメントの[トラブルシューティングに関するセクション](help-desk-operators.md)を参照してください。

## <a name="help-and-support-experience"></a>ヘルプとサポート エクスペリエンス

Intune のヘルプとサポート エクスペリエンスは、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431)、および Azure portal の Intune のすべてのブレード (またはページ) から使用できます。

"*ヘルプとサポート*" のエクスペリエンスは、[Microsoft 365 管理センター](https://admin.microsoft.com/)で表示されるエクスペリエンスと似ており、Azure の他のサービスには残っている以前の "*ヘルプとサポート*" に代わるものです。

### <a name="options-to-access-help-and-support"></a>ヘルプとサポートにアクセスするためのオプション

Intune 用に新しく作成されたテナントを使用するとき、*ヘルプとサポート*を開けず、次のメッセージが返されることがあります。

- *不明な問題が発生しました。ページを更新しても問題が解決されない場合、[M365 管理センター](https://admin.microsoft.com)でサポート案件を作成し、表示されたセッション ID を参照してください。*

エラーの詳細には、*セッション ID* や*拡張機能*の詳細などが含まれます。

この問題は、 https://admin.microsoft.com の **M365 管理センター**または https://portal.office.com の **Office 365 ポータル**で新しいテナント アカウントを認証していない場合に発生します。 この問題を解決するには、メッセージに含まれている *M365 管理センター*のリンクを選択するか、 https://portal.office.com にアクセスしてサインインします。 いずれかの場所での認証後、Intune の*ヘルプとサポート*にアクセスできるようになります。

**ヘルプとサポート**にアクセスする:

- **Azure portal で**

  - Intune の任意のブレードまたはページから **[ヘルプとサポート]** を選択します。

  > [!NOTE]  
  > お使いの Intune のインスタンスが、Azure Government のような政府機関向けのプライベート クラウド (ソブリン クラウドとも呼ばれます) でホストされている場合は、この記事で後述する「[Intune での政府機関向けのプライベート クラウドのサポート](#intune-support-for-private-cloud-for-government)」を参照してください。 Intune の *[ヘルプとサポート]* エクスペリエンスは、来年まで、政府機関向けのプライベート クラウドでは利用できません。

- **Microsoft Endpoint Manager admin center から**

  - Microsoft Endpoint Manager admin center の任意のノードで **[?]** を選択します。 ポータルの右上隅にあるアイコンで **[ヘルプ]** ウィンドウを開きます。 **[ヘルプ + サポート]** を選択すると、 **[管理の種類の選択]** ページが開きます。

    > [!div class="mx-imgBorder"]
    > ![[管理の種類の選択] ページを開く](./media/get-support/management-types.png)

    ドロップダウンを使用し、ヘルプを表示する管理の種類を選択すると、該当するヘルプとサポートのページが開きます。 Microsoft Endpoint Manager admin center では、次の管理の種類をサポートしているため、Intune など、サポートが必要なものを選択する必要があります。

    - Configuration Manager
    - Intune
    - 共同管理

    > [!div class="mx-imgBorder"]
    > ![管理の種類を選択する](./media/get-support/select-management-type.png)

    管理の種類を選択すると、該当する *[ヘルプとサポート]* ページが開き、特定の問題について[解決策を見つける](#find-solutions)ための詳細を指定できます。 詳細は、選択した管理の種類に基づいてフィルター処理されます。

     正しい管理の種類が選択されていない場合 **(1)** は、 *[管理の種類の選択]* **(2)** をクリックし、管理の種類の選択のドロップダウンに戻ります。

    > [!div class="mx-imgBorder"]
    > ![管理の種類を確認する](./media/get-support/confirm-management-selection.png)

  - *[デバイス]* 、 *[アプリ]* 、 *[ユーザー]* などの他のノードまで展開してから *[ヘルプとサポート]* を選択しても、管理の種類は選択できません。また、 *[ヘルプとサポート]* に種類も表示されません。 この場合は *[Intune]* が想定されます。 コンテキストを Intune にしない場合は、 **[?]** オプションを使用し、別の管理の種類を選択できるようにします。

### <a name="the-support-experience"></a>サポート エクスペリエンス

  [ヘルプとサポート] を開くと、ポータルに **[ヘルプが必要ですか?]** ウィンドウが表示されます。

  ![[ヘルプが必要ですか?] ウィンドウを表示する](./media/get-support/need-help.png)

  左上隅には 3 つのアイコンがあります。これらを選択すると、 *[ヘルプが必要ですか?]* ウィンドウのさまざまなウィンドウを開くことができます。 表示中のウィンドウは、下線で示されます。

  **Premier** または**統合**サポート契約を締結しているお客様は、サポートの[追加オプション](#premier-and-unified-support-customers)をご利用いただけます。また、次の画像に似たバナーが *[ヘルプが必要ですか?]* に表示されます:![Premier バナー](./media/get-support/premier-banner.png)

  *[ヘルプが必要ですか?]* を開くと、 *[解決方法の検索]* ウィンドウが表示されます。 ただし、アクティブなサポート ケースがある場合、このウィンドウを開くと *[サービス要求]* ウィンドウが表示されます。ここでは、アクティブなサポート ケースと終了したサポート ケースに関する詳細を確認できます。

#### <a name="find-solutions"></a>解決方法の検索

![[解決方法の検索] ウィンドウを選択する](./media/get-support/find-solutions.png)

*[解決方法の検索]* ウィンドウに表示されたテキスト ボックスに、イシューに関する詳細情報をいくつか指定します。 イシューについてお客様が指定したテキストに基づいて、一致する可能性のある情報がウィンドウに表示されます。 また、イシューの解決に役立つ可能性のある推奨記事へのリンクも表示されます。

記述した詳細との厳密な一致が見つかった場合は、 *[ヘルプが必要ですか?]* ウィンドウの右側にトラブルシューティングのヒントが表示されます。

たとえば、「**パスワード同期のエラー**」と入力したとします。 その結果として、トラブルシューティングのガイダンスがウィンドウに直接表示され、Microsoft のドキュメント ライブラリの推奨記事へのリンクが記載されます。

![トラブルシューティング情報を表示する](./media/get-support/troubleshooting-insights.png)

#### <a name="contact-support"></a>サポートにお問い合わせください

![[サポートにお問い合わせください] ウィンドウを選択する](./media/get-support/contact-support.png)

*[サポートにお問い合わせください]* ウィンドウからは、サポートの要求を送信できます。 このウィンドウは、 *[解決方法の検索]* ウィンドウでいくつかの基本的なキーワードを指定した後に使用できます。

サポートを要求する場合は、問題に関する説明を、必要なだけ詳しく入力してください。  電話とメールの連絡先情報を確認したら、希望する連絡方法を選択します。 ウィンドウには、連絡方法ごとの応答時間が表示されます。これによって、自分がいつ連絡を受けるかを予測できます。 要求を送信する前に、イシューの詳細を補足するのに役立つログやスクリーンショットなどのファイルを添付してください。

![[サポートにお問い合わせください] のフォーム](./media/get-support/contact-support-form.png)

必要な情報を入力したら、 **[連絡する]** を選択して要求を送信します。

#### <a name="service-requests"></a>サービス要求

![[サービス要求] ウィンドウを選択する](./media/get-support/service-requests.png)

*[サービス要求]* ウィンドウには、ご自身のケースの履歴が表示されます。 アクティブなケースが一覧の一番上に表示され、終了したイシューも確認することができます。

![サービス要求の一覧を確認する](./media/get-support/service-requests-pane.png)

アクティブなサポート ケースの番号をお持ちの場合は、ここにそれを入力してそのイシューに移動できます。または、アクティブなインシデントおよび終了したインシデントの一覧から任意のインシデントを選択して、その詳細を確認できます。

インシデントの詳細の確認が完了したら、[サービス要求] ウィンドウの上部 ( *[ヘルプが必要ですか?]* ウィンドウの 3 つのアイコンのすぐ上) に表示されている左矢印を選択します。 [戻る] 矢印により、表示が開いたサポート インシデントの一覧に戻ります。

#### <a name="premier-and-unified-support-customers"></a>Premier および統合サポートのお客様

**Premier** または**統合**サポート契約を締結しているお客様は、イシューの重大度を指定し、特定の日時にサポートのコールバックをスケジュールすることができます。 これらのオプションは、新しいイシューを開いたり送信したりしたときと、アクティブなサポート ケースを編集したときにご利用いただけます。

**[重大度]** - ご自身のサポート契約に応じて、イシューの重大度を指定するオプションです。

- *Premier*:A、B、または C の重大度
- "*統合*":重大、または重大でない

重大度が **A** または**重大**のいずれかであるイシューを選択した場合は、電話によるサポート ケースに制限されます。これが最速でサポートを受けることができるオプションです。

**[Callback schedule]\(コールバックのスケジュール\)** - 特定の日時にコールバックを要求できます。

## <a name="azure-help--support-experience"></a>Azure のヘルプとサポート エクスペリエンス

サブスクリプションが政府機関向けのプライベート クラウドにある場合を除き、Azure の *[ヘルプとサポート]* エクスペリエンスにアクセスして、Intune のサポートを受けることはできなくなりました。
Intune のインスタンスが政府機関向けのプライベート クラウド上で実行されていない場合は、Azure の *[ヘルプとサポート]* に移動すると、サポート インシデントを作成して管理するために Intune の *[ヘルプとサポート]* エクスペリエンスにリダイレクトされます。

左側のナビゲーション ウィンドウの **[ヘルプとサポート]** を使用するか、または **[?]** オプションを使用して *[ヘルプ]* ウィンドウを開き、 **[ヘルプとサポート]** を選択すると、Azure の *[ヘルプとサポート]* ページが開きます。

このページで **[+ 新しいサポート リクエスト]** を選択して、 *[Help + support + New support request]\(ヘルプとサポート + 新しいサポート リクエスト\)* ページの *[基本]* タブを開きます。

![ヘルプとサポート](./media/get-support/help-plus-support.png)

このページで次のようにします。

- *[問題の種類]* で、 **[技術]** を選択します。
- *[サービス]* で、 **[Microsoft Intune]** を選択します。

  次に、[Intune の [ヘルプとサポート] ページ](https://aka.ms/intunehelpsupport)にリダイレクトされるリンクが表示されます。
  
  ![新しいサポート リクエスト](./media/get-support/new-request.png)

## <a name="intune-support-for-private-cloud-for-government"></a>Intune での政府機関向けのプライベート クラウドのサポート

お使いの Intune サブスクリプションが、Azure Government のような政府機関向けのプライベート クラウド (ソブリン クラウドとも呼ばれます) でホストされている場合、Intune の新しい [ヘルプとサポート] エクスペリエンスにはまだアクセスできません。  代わりに、次の情報を使用して Intune のサポートを受けてください。

### <a name="create-an-online-support-ticket"></a>オンライン サポート チケットの作成

>[!IMPORTANT]
> *ヘルプとサポート*は、政府機関向けのプライベート クラウドではまだ使用できない新しいシステムに移行するため、サポート インシデントを作成するときに、ポータルでは 15 桁の識別番号を使用するサポート ケースが識別されます。 15 桁のケースが作成されると、そのケースのミラーが Microsoft サポート用に作成されます。 このミラー ケースは、8 桁のケース ID を使用して新しいサポート システムで作成され、サポート サービスにより、サポート インシデントに関するすべての作業の追跡と通信のために使用されます。 15 桁のケースが作成されるとすぐに、サポート サービスで使用されるミラー化されたサポート ケースの 8 桁の番号を示す電子メールが届きます。
>
> サポート担当者は、8 桁のサポート ケースで作業と通信を行い、通信のログ記録とインシデントの進行状況の追跡には 8 桁のサポート ケースのみを使用します。 したがって、その 8 桁のサポート ケースから、ケースの作業の追跡記録となる電子メールの更新を受け取ります。 15 桁のサポート インシデントには、詳細情報は記録されません。 サポートが終了し、8 桁のサポート ケースが閉じられると、その状態は、Azure portal 内から表示できる 15 桁のサポート ケースに反映されます。  15 桁のサポート ケースについては、他の更新や状態の変更は想定されていません。
>
> 今年の後半にサポート ツールの移行が完了すると、Government Cloud でホストされている Intune のサポート エクスペリエンスは、パブリック クラウドでホストされている Intune サブスクリプションで現在利用可能な既定の "*ヘルプとサポート*" エクスペリエンスと似たものになります。

1. Intune 管理者資格情報を使用して Azure portal (<https://portal.azure.us>) にサインインして、 **[?]** を選択します。 アイコンを選択し、 **[ヘルプとサポート]** を選択して、[Azure のヘルプとサポート](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)のページに移動します。

   ![[ヘルプとサポート] のリンクが強調表示された疑問符マークの画像](./media/get-support/azure-get-support.png)

2. Azure の **[ヘルプとサポート]** のページ上で、 **[新しいサポート要求]** を選択します。

   ![[ヘルプとサポート] ページで [新しいサポート要求] のリンクが強調表示された画像](./media/get-support/azure-support-ticket-link.png)

3. Intune のほとんどのテクニカル サポートの問題では、 **[基本]** タブ上で、次のオプションを選択します。
   - **問題の種類**: **テクニカル**
   - **サブスクリプション**: <"*お使いのサブスクリプション*">
   - **Service**:**Microsoft Intune**
   - **[問題の種類]** : ドロップダウン メニューから、問題の種類を選択します。
   - **[問題のサブタイプ]** : ドロップダウン メニューから、問題のサブタイプを選択します。
   - **[件名]** : ヘルプが必要な問題を簡単に説明します。

   ![[ヘルプとサポート] の [基本] タブの画像 - [新しいサポート要求] ページ](./media/get-support/help-new-support-case-basics.png)

   **[Next: Solutions]\(次へ: ソリューション\)** を選択して続行します。
4. **[ソリューション]** タブ上で、チケットを提出しなくても問題の解決に役立つ可能性がある推奨手順を確認します。 手順を確認した後に、やはりサポート要求を作成することにした場合は、 **[Next: Details]\(次へ: 詳細\)** をクリックします。

   ![[ヘルプとサポート] の [ソリューション] タブの画像 - [新しいサポート要求] ページ](./media/get-support/help-new-support-case-solutions.png)
5. **[詳細]** タブ上で、問題の詳細、サポートの方法、お客様の連絡先情報を入力してから、 **[Next: Review + create]\(次へ: 確認と作成\)** をクリックします。

   ![[ヘルプとサポート] の [詳細] タブの画像 - [新しいサポート要求] ページ](./media/get-support/help-new-support-case-details.png)
6. 情報を見直して、正しいことを確認してから、 **[作成]** を選択してサポート要求を送信します。

   ![[新しいサポート要求] ページの [review + create]\(確認と作成\) タブの画像](./media/get-support/help-new-support-case-create.png)

>[!IMPORTANT]
>請求やサブスクリプションの質問がある場合は、ケースを開いて [Microsoft 365 管理センター](https://admin.microsoft.com/Support/SupportEntry.aspx)からサポートを受けることができます。

### <a name="view-support-requests"></a>サポート要求を表示する  

Azure portal 内からサポート要求を表示できます。 ただし、利用できる情報は限られます。  インシデントを表示するには:

1. Intune 管理者資格情報を使用して Azure (<https://portal.azure.com>) にサインインして、 **[?]** を選択します。 アイコンを選択し、 **[ヘルプとサポート]** を選択して、[Azure のヘルプとサポート](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)のページに移動します。

2. **[ヘルプとサポート]** ページでは、 **[最近のサポート要求]** の一覧を見ることができます。

   > [!IMPORTANT]  
   > 政府機関向けのプライベート クラウドのお客様は、15 桁のサポート ケース番号とインシデントの状態のみを表示できます。 ケースに関するすべての通信および作業またはアラートの追跡はメールによって送信され、Intune コンソール内から開かれたサポート ケースのミラーとして作成された 8 桁のサポート ケース番号が参照されています。

## <a name="additional-resources"></a>その他のリソース  

- [課金とサブスクリプション管理のサポート](https://support.office.com/article/Contact-Office-365-for-business-support-Admin-Help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b)
- [ボリューム ライセンス](https://go.microsoft.com/fwlink/p/?LinkID=282015)
- [Intune の問題のトラブルシューティング](help-desk-operators.md)
