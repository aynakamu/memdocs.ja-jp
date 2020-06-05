---
title: iOS/iPadOS デバイスの登録 - Device Enrollment Program
titleSuffix: Microsoft Intune
description: Device Enrollment Program を使用して企業が所有する iOS/iPadOS デバイスを登録する方法を説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2db33dbe94ff5aef62563531149250fbd4268acc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986991"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>Apple の自動デバイス登録を使用して iOS または iPadOS デバイスを自動登録する

> [!IMPORTANT]
> Apple は、Apple Device Enrollment Program (DEP) の使用から Apple の自動デバイス登録 (ADE) に最近変更しました。 Intune では、それを反映するために Intune のユーザー インターフェイスを更新しています。 このような変更が完了するまで、Intune ポータルでは *[Device Enrollment Program]* が引き続き表示されます。 表示される場所では、自動デバイス登録が使用されるようになっています。

Apple の[自動デバイス登録 (ADE)](https://deploy.apple.com) (以前の Device Enrollment Program) を使用して購入した iOS または iPadOS デバイスを登録するように Intune を設定できます。 自動デバイス登録によって、多数のデバイスをそれに触れることなく登録できます。 iPhone、iPad、MacBook などのデバイスは、ユーザーに直接配布できます。 ユーザーがデバイスの電源をオンにすると、Apple 製品の一般的な out-of-box-experience が含まれるセットアップ アシスタントが構成済み設定で実行され、デバイスが管理対象として登録されます。

ADE 登録を有効にするには、Intune と [Apple Business Manager (ABM)](https://business.apple.com/) または [Apple School Manager (ASM)](https://school.apple.com/) のポータルの両方を使用します。 いずれかの Apple ポータルで管理するために Intune にデバイスを割り当てられるように、シリアル番号のリストまたは注文番号が必要になります。 登録時にデバイスに適用された設定を含む ADE 登録プロファイルを Intune で作成します。 ADE は、[デバイス登録マネージャー](device-enrollment-manager-enroll.md) アカウントと共に使用できません。

> [!NOTE]
> ADE で設定されるデバイス構成は、エンド ユーザーが必ずしも削除できるわけではありません。 そのため、[ADE に移行する](../fundamentals/migration-guide-considerations.md)前に、デバイスをワイプして既定 (新規) の状態に戻す必要があります。

## <a name="automated-device-enrollment-and-the-company-portal"></a>自動デバイス登録とポータル サイト

ADE 登録には、App Store バージョンのポータル サイト アプリとの互換性はありません。 ADE デバイス上のポータル サイト アプリへのアクセス権をユーザーに付与することが可能です。 デバイスで使用する会社のアプリをユーザーが選択できるようにする場合や、最新の認証を使用して登録プロセスを完了する場合に、このアクセス権を付与することができます。 

登録中に最新の認証を有効にするには、ADE プロファイル内で **[VPP によるポータル サイトのインストール]** (Volume Purchase Program) を使用して、アプリをデバイスにプッシュします。 詳細については、[Apple の ADE を使用した iOS または iPadOS デバイスの自動登録](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)に関する記事を参照してください。

ポータル サイトが自動的に更新され、ADE に既に登録されているデバイスでポータル サイト アプリを提供できるようにするには、Intune を使用して、そのポータル サイト アプリを[アプリケーション構成ポリシー](../apps/app-configuration-policies-use-ios.md)が適用された必要な Volume Purchase Program (VPP) アプリとして展開します。

## <a name="what-is-supervised-mode"></a>監視モードとは何か。

Apple では、iOS/iPadOS 5 において監視モードが導入されました。 監視モードの iOS/iPadOS デバイスは、画面キャプチャのブロックや App Store からのアプリのインストールのブロックなど、より多くの制御を使用して管理できます。 そのため、企業所有のデバイスでは特に役立ちます。 Intune では、ADE の一部として監視モードのデバイスを構成できます。

監視されていない ADE デバイスのサポートは、iOS または iPadOS 11 で非推奨となりました。 iOS または iPadOS 11 以降では、ADE 構成済みデバイスを常に監視する必要があります。 ADE の *is_supervised* フラグは iOS/iPadOS 13.0 以降では無視されます。 バージョンが 13.0 以降の iOS/iPadOS デバイスはすべて、自動化されたデバイス登録で登録されるとき、自動的に監視されます。 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>[前提条件]
- [Apple の ADE](https://deploy.apple.com) で購入したデバイス
- [モバイル デバイス管理 (MDM) 機関](../fundamentals/mdm-authority-set.md)
- [Apple MDM プッシュ証明書](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>サポートされるボリューム

- トークンあたりの登録プロファイルの最大数:1,000  
- プロファイルあたりの自動デバイス登録デバイスの最大数: 無制限 (トークンあたりのデバイスの最大数)
- Intune アカウントあたりの自動デバイス登録トークンの最大数:2,000
- トークンあたりの自動デバイス登録デバイスの最大数:75,000

## <a name="get-an-apple-ade-token"></a>Apple ADE トークンの取得

ADE で iOS または iPadOS デバイスを登録するには、Apple の ADE トークン (.p7m) ファイルが必要です。 このトークンにより、Intune は企業所有の ADE デバイスに関する情報を同期できるようになります。 また、Intune は Apple に登録プロファイルをアップロードして、デバイスをそれらのプロファイルに割り当てられるようになります。

[Apple Business Manager (ABM)](https://business.apple.com/) または [Apple School Manager (ASM)](https://school.apple.com/) のポータルを使用して、トークンを作成します。 また、管理のためにデバイスを Intune に割り当てる場合にも ABM/ASM のポータルを使用します。

> [!NOTE]
> Azure に移行する前に Intune クラシック ポータルからトークンを削除すると、削除された Apple ADE トークンが Intune で復元される場合があります。 Azure portal から ADE トークンを再び削除できます。

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>手順 1. トークンを作成するために必要な Intune 公開キー証明書をダウンロードする

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]**  >  **[追加]** を選択します。

    ![Enrollment Program トークンを取得します。](./media/device-enrollment-program-enroll-ios/image01.png)

2. **[同意する]** を選択して、Microsoft がユーザーとデバイスの情報を Apple に送信できるようにします。

   > [!NOTE]
   > 手順 2 以降に進んで Intune 公開キー証明書をダウンロードしたら、ウィザードを閉じたり、このページから移動したりしないでください。 そうすると、ダウンロードした証明書が無効になるため、このプロセスを再度繰り返す必要があります。 このような状況が発生した場合、通常は **[確認および作成]** タブの **[作成]** ボタンが灰色表示され、プロセスを完了できなくなります。

   ![公開キーをダウンロードするための [Apple 証明書] ワークスペースの [Enrollment Program トークン] のスクリーンショット。](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. **[公開キーをダウンロードします]** を選択し、暗号化キー (.pem) ファイルをダウンロードしてローカルに保存します。 .pem ファイルは、Apple ポータルから信頼関係証明書を要求するために使用します。


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>手順 2. キーを使用して Apple からトークンをダウンロードする

1. **[Apple Device Enrollment Program 用のトークンを作成します]** を選択して Apple の Business ポータルを開き、会社の Apple ID でサインインします。 この Apple ID を使って、ADE トークンを更新できます。
2. Apple の [Business ポータル](https://business.apple.com)で、 **[Device Enrollment Program]** の **[開始]** を選択します。

3. **[Manage Servers\(サーバーの管理\)]** ページで、 **[Add MDM Server\(MDM サーバーの追加\)]** を選びます。
4. **MDM サーバー名**を入力し、 **[Next]** (次へ) をクリックします。 サーバー名は、自分がモバイル デバイス管理 (MDM) サーバーを識別できるようにするための名前です。 Microsoft Intune サーバーの名前または URL ではありません。

5. **[Add &lt;ServerName&gt;\(<サーバー名> の追加\)]** ダイアログ ボックスが開き、 **[Upload Your Public Key\(公開キーをアップロードする\)]** と表示されます。 **[ファイルの選択…]** を選択して .pem ファイルをアップロードし、 **[Next]** (次へ) を選択します。

6. **[Deployment Programs]** &gt; **[Device Enrollment Program]** &gt; **[デバイスの管理]** の順に移動します。
7. **[Choose Devices By\(デバイスの選択方法\)]** で、デバイスを識別する方法を指定します。
    - **Serial Number\(シリアル番号\)**
    - **Order Number\(注文番号\)**
    - **Upload CSV File\(CSV ファイルのアップロード\)**

   ![シリアル番号でデバイスを選択するように指定し、アクションの選択でサーバーへの割り当てを設定し、サーバー名を選択したスクリーンショット。](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. **[アクションの選択]** で **[Assign to Server]\(サーバーに割り当てる\)** を選択し、Microsoft Intune に指定した **ServerName** を選択して、&lt;[OK]&gt; を選択します。 指定したデバイスが管理用に Intune サーバーに割り当てられて、 **[Assignment Complete\(割り当て完了\)]** と表示されます。

   Apple ポータルで、 **[Deployment Programs]\(配備プログラム\)** &gt; **[Device Enrollment Program]\(Device Enrollment Program\)** &gt; **[View Assignment History]\(割り当て履歴の表示\)** の順に移動して、デバイスとその MDM サーバーの割り当てのリストを表示します。

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>手順 3. このトークンの作成に使用した Apple ID を保存する

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、今後の参照用に Apple ID を指定します。

![Enrollment Program トークンの作成に使った Apple ID の指定と、Enrollment Program トークンの参照のスクリーンショット。](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>手順 4. トークンをアップロードして、スコープのタグを選択します。

1. **[Apple トークン]** ボックスで、証明書 (.p7m) ファイルを参照し、 **[開く]** を選択します。
2. この DEP トークンに[スコープのタグ](../fundamentals/scope-tags.md)を適用する場合は、 **[スコープ (タグ)]** を選択して、必要なスコープのタグを選択します。 トークンに適用されるスコープのタグは、このトークンに追加されたプロファイルとデバイスによって継承されます。
3. **[作成]** を選択します。

このプッシュ証明書を使用して、Intune はモバイル デバイスを登録し、登録したモバイル デバイスにポリシーを適用して iOS/iPadOS デバイスを管理できます。 Intune は、Apple と自動的に同期して、Enrollment Program アカウントを表示します。

## <a name="create-an-apple-enrollment-profile"></a>Apple 登録プロファイルの作成

これでトークンがインストールされました。ADE デバイスの登録プロファイルを作成することができます。 デバイス登録プロファイルで、デバイス グループに対して登録時に適用する設定を定義します。 ADE トークンあたり 100 個の登録プロファイルという制限があります。

> [!NOTE]
> VPP トークンに十分なポータル サイト ライセンスがない場合、またはトークンの有効期限が切れている場合は、デバイスがブロックされます。 トークンの有効期限が近づいている場合、またはライセンスが不足している場合は、Intune でアラートが表示されます。
 

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択します。
2. トークンを選択して、 **[プロファイル]**  >  **[プロファイルの作成]**  >  **[iOS]** の順に選択します。

    ![プロファイルの作成のスクリーンショット。](./media/device-enrollment-program-enroll-ios/image04.png)

3. **[基本]** ページ上で、管理用にプロファイルの **[名前]** と **[説明]** を入力します。 ユーザーには、これらの詳細は表示されません。 

    ![プロファイル名と説明。](./media/device-enrollment-program-enroll-ios/image05.png)

4. **[Next:Device Management Settings]\(次へ: デバイス管理の設定\)** を選択します。

5. **[ユーザー アフィニティ]** で、このプロファイルに対応するデバイスを割り当て済みユーザーとともに登録する必要があるかどうかを選択します。
    - **[ユーザー アフィニティとともに登録する]** - このオプションは、ユーザーに属しているデバイスであって、かつアプリのインストールなどのサービスにポータル サイトを使用する必要があるデバイスの場合に選択します。 ADFS を使用しており、セットアップ アシスタントを使用して認証している場合、[WS-Trust 1.3 ユーザー名/混合エンドポイント](https://technet.microsoft.com/library/adfs2-help-endpoints) [詳細](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint) が必要です。

    - **[ユーザー アフィニティなしで登録する]** - このオプションは、1 人のユーザーに関連付けられていないデバイスの場合に選択します。 ローカルのユーザー データにアクセスしないデバイスには、このオプションを使用します。 ポータル サイト アプリなどのアプリは動作しません。

5. **[ユーザー アフィニティとともに登録する]** を選択した場合は、Apple セットアップ アシスタントではなく、ポータル サイトを使ってユーザーに認証させることが可能です。

    ![ポータル サイトで認証します。](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > 次のいずれかを実行する場合は、 **[ユーザーが認証する必要がある場所を選択する]** を **[ポータル サイト]** に設定します。
    >    - 多要素認証の使用
    >    - 最初のサインイン時にパスワードの変更が必要なユーザーにプロンプトを表示する
    >    - 登録の間に有効期限が切れたパスワードのリセットをユーザーに求める
    >
    > Apple セットアップ アシスタントによって認証している場合は、これらはサポートされません。

6. **[ユーザーが認証する必要がある場所を選択する]** に **[ポータル サイト]** を選択した場合は、VPP トークンを使用してデバイス上にポータル サイトを自動的にインストールできます。 この場合、ユーザーは Apple ID を指定する必要はありません。 VPP トークンを使用して Intune ポータル サイトをインストールするには、 **[VPP によるポータル サイトのインストール]** でトークンを選択します。 ポータル サイトが既に VPP トークンに追加されている必要があります。 登録後もポータル サイト アプリが引き続き更新されるようにするには、Intune でアプリの展開を構成していることを確認してください ([Intune] > [クライアント アプリ])。 ユーザー操作を不要にするためには、ほとんどの場合、ポータル サイトを iOS/iPadOS VPP アプリとして取得し、これを必須アプリにして、割り当てにデバイス ライセンスを使用する必要があります。 トークンの期限が切れていないことと、ポータル サイト アプリの十分なデバイス ライセンスがあることを確認してください。 トークンの期限が切れているか、ライセンスがなくなっている場合、Intune では代わりに App Store ポータル サイトをインストールして、Apple ID の入力を求めます。 

    > [!NOTE]
    > **[ユーザーが認証する必要がある場所を選択する]** が **[ポータル サイト]** になっている場合、ポータル サイトが ADE デバイスにダウンロードされる最初の 24 時間以内に、必ずデバイス登録プロセスが実行されるようにします。 そうでないと、登録に失敗して、デバイスを登録するために工場出荷時の設定にリセットする必要が生じます。
    
    ![[VPP によるポータル サイトのインストール] のスクリーンショット。](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

7. **[ユーザーが認証する必要がある場所を選択する]** に **[セットアップ アシスタント]** を選択していても、条件付きアクセスを利用するか、デバイス上に会社のアプリを展開する場合は、デバイス上にポータル サイトをインストールする必要があります。 これを行うには、 **[ポータル サイトのインストール]** に **[はい]** を選択します。  アプリ ストアへの認証を行わずにユーザーがポータル サイトを受信できるようにする場合は、 **[VPP によるポータル サイトのインストール]** を選択して、VPP トークンを選択します。 トークンの期限が切れていないことと、ポータル サイト アプリを適切に展開できるだけの十分なデバイス ライセンスを保持していることを確認してください。

8. **[VPP によるポータル サイトのインストール]** に 1 つのトークンを選択した場合、セットアップ アシスタントの完了直後にシングル アプリ モードでデバイスをロックできます (具体的には、ポータル サイト アプリ)。 **[Run Company Portal in Single App Mode until authentication]\(認証されるまでシングル アプリ モードでポータル サイトを実行する\)** に **[はい]** を選択すると、このオプションが設定されます。 デバイスを使用するには、ポータル サイトを使用したサインインで最初に認証する必要があります。

    シングル アプリ モードでロックされている単一のデバイス上では、多要素認証はサポートされていません。 そのデバイスでは別のアプリに切り替えて認証の 2 番目の要素を完了することができないため、この制限が設けられています。 そのため、シングル アプリ モードのデバイス上で多要素認証を使用する場合は、2 番目の要素が別のデバイス上にあることが必要になります。

    この機能は iOS/iPadOS 11.3.1 以降でのみサポートされます。

   ![単一アプリ モードのスクリーンショット。](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

9. このプロファイルを使用しているデバイスを監視対象にする場合は、 **[監視]** に **[はい]** を選択します。

    ![[デバイス管理の設定] のスクリーンショット。](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    **[監視下]** デバイスでは、より多くの管理オプションを使用できるようになり、既定で [アクティベーション ロック] は無効になります。 Microsoft では、特に多数の iOS または iPadOS デバイスを展開している場合に、監視モードを有効にするメカニズムとして ADE の利用をお勧めしています。

    デバイスが監視対象であることは次の 2 つの方法でユーザーに通知されます。

   - ロック画面には次のように表示されます。"This iPhone is managed by Contoso." (この iPhone は Contoso によって管理されています。)
   - **[設定]**  >  **[全般]**  >  **[情報]** 画面には、次のように表示されます。"This iPhone is supervised. (この iPhone は監視されています。) Contoso はインターネット トラフィックを監視し、このデバイスの位置を特定できます。" と、

     > [!NOTE]
     > 監視なしで登録されているデバイスは、Apple Configurator でのみ監視対象にリセットすることができます。 この方法でデバイスをリセットするには、USB ケーブルを使用して iOS/iPadOS デバイスを Mac に接続する必要があります。 詳細については、[Apple Configurator ドキュメント](http://help.apple.com/configurator/mac/2.3)を参照してください。

10. このプロファイルを使用するデバイスの登録をロックするかどうかを選択します。 **[ロックされた登録]** を選択すると、 **[設定]** メニューから管理プロファイルを削除する操作を許可する iOS/iPadOS 設定が無効になります。 デバイスの登録後は、デバイスをワイプしないと、この設定を変更できません。 そのようなデバイスについては、 **[監視下]** 管理モードを *[はい]* に設定する必要があります。 

    > [!NOTE]
    > デバイスが **[ロックされた登録]** に登録されると、ユーザーはポータル サイト アプリで **[デバイスの削除]** または **[出荷時の設定にリセット]** を使用できなくなります。 このオプションは、ユーザーが使用できなくなります。 また、ユーザーはポータル サイト Web サイト (https://portal.manage.microsoft.com) でデバイスを削除することもできなくなります。
    > さらに、BYOD デバイスが Apple 自動デバイス登録デバイスに変換され、 **[ロックされた登録]** 対応プロファイルに登録された場合、ユーザーは 30 日間 **[デバイスの削除]** と **[出荷時の設定にリセット]** を使用できますが、その後、このオプションは無効または使用不可になります。 参照: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859 。

11. このプロファイルを使用するデバイスを**コンピューターと同期**できるようにするかどうかを選択します。 **[証明書による Apple Configurator の許可]** を選択した場合は、 **[Apple Configurator の証明書]** で証明書を選択する必要があります。

     > [!NOTE]
     > **[コンピューターと同期する]** が **[すべて拒否]** に設定されている場合、iOS と iPadOS デバイス上でポートが制限されます。 このポートは課金用にのみ使用でき、それ以外の場合は使用できません。 このポートは、iTunes または Apple Configurator 2 の使用に対してブロックされます。
     **[コンピューターと同期する]** が **[証明書による Apple Configurator の許可]** に設定されている場合、後でアクセスできる証明書のローカル コピーを必ず保持するようにしてください。 アップロードされたコピーを変更することはできません。今後この証明書にアクセスできるように維持することが重要です。 macOS のデバイスまたは PC から iOS/iPadOS デバイスに接続するには、この構成と証明書を使用して自動デバイス登録プロファイルに登録された iOS/iPadOS デバイスへの接続を行うデバイスに、同じ証明書をインストールする必要があります。

12. 前の手順で **[証明書による Apple Configurator の許可]** を選択した場合は、インポートする Apple Configurator の証明書を選択します。

13. デバイスに対して登録時に自動的に適用される名前付け形式と、連続する各チェックインにおける名前付け形式を指定することができます。 名前付けテンプレートを作成するには、 **[デバイス名のテンプレートを適用する]** に **[はい]** を選択します。 次に、 **[デバイス名のテンプレート]** ボックスに、このプロファイルを使用する名前に使うテンプレートを入力します。 デバイスの種類とシリアル番号を含むテンプレート形式を指定できます。 

14. **[Next: Setup Assistant Customization]\(次へ: セットアップ アシスタントのカスタマイズ\)** を選択します。

15. **[セットアップ アシスタントのカスタマイズ]** ページで、次のプロファイル設定を構成します。![セットアップ アシスタントのカスタマイズ。](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | 部門の設定 | [説明] |
    |---|---|
    | <strong>部門名</strong> | アクティブ化中にユーザーが <strong>[構成について]</strong> をタップすると表示されます。 |
    |    <strong>部署の電話番号</strong>     | アクティブ化中にユーザーが <strong>[ヘルプが必要ですか]</strong> ボタンをクリックすると表示されます。 |

    ユーザーのセットアップ時に、デバイス上でセットアップ アシスタントの画面を非表示にすることを選択できます。
    - **[非表示]** を選択した場合、セットアップ時に画面は表示されません。 その場合でも、デバイスを設定した後、ユーザーは **[設定]** メニューから機能を設定できます。
    - **[表示]** を選択した場合、セットアップ時に画面が表示されます。 ユーザーは、何も行わずに画面をスキップできる場合があります。 しかし、後でデバイスの **[設定]** メニューから機能を設定できます。 


    | セットアップ アシスタントの画面の設定 | **[表示]** を選択した場合の、セットアップ時のデバイスの動作... |
    |------------------------------------------|------------------------------------------|
    | <strong>パスコード</strong> | ユーザーにパスコードの入力を求めます。 デバイスがセキュリティで保護されていない場合は、他の何らかの方法 (デバイスを 1 つのアプリに制限するキオスク モードなど) でアクセスが制御されていない限り、パスコードを常に必須にします。 iOS/iPadOS 7.0 以降が対象です。 |
    | <strong>ロケーション サービス</strong> | ユーザーに場所の指定を求めます。 macOS 10.11 以降と、iOS/iPadOS 7.0 以降が対象です。 |
    | <strong>復元</strong> | [アプリとデータ] 画面が表示されます。 この画面では、ユーザーはデバイスを設定するときに iCloud Backup からデータを復元または転送できます。 macOS 10.9 以降と、iOS/iPadOS 7.0 以降が対象です。 |
    | <strong>iCloud と Apple ID</strong> | 自分の Apple ID を使ってサインインし iCloud を使用するオプションをユーザーに提示します。 macOS 10.9 以降と、iOS/iPadOS 7.0 以降が対象です。   |
    | <strong>使用条件</strong> | ユーザーに Apple の使用条件への同意を求めます。 macOS 10.9 以降と、iOS/iPadOS 7.0 以降が対象です。 |
    | <strong>Touch ID</strong> | ユーザーに、デバイスの指紋識別を設定するオプションを表示します。 macOS 10.12.4 以降と、iOS/iPadOS 8.1 以降が対象です。 |
    | <strong>Apple Pay</strong> | ユーザーに、デバイスで Apple Pay を設定するオプションを表示します。 macOS 10.12.4 以降と、iOS/iPadOS 7.0 以降が対象です。 |
    | <strong>Zoom</strong> | ユーザーに、デバイスを設定するときに表示を拡大するオプションを表示します。 iOS/iPadOS 8.3 以降が対象です。 |
    | <strong>Siri</strong> | ユーザーに、Siri を設定するオプションを表示します。 macOS 10.12 以降と、iOS/iPadOS 7.0 以降が対象です。 |
    | <strong>診断データ</strong> | [診断] 画面をユーザーに表示します。 この画面では、ユーザーは Apple に診断データを送信できます。 macOS 10.9 以降と、iOS/iPadOS 7.0 以降が対象です。 |
    | <strong>トーンの表示</strong> | [トーンの表示] をオンにするオプションをユーザーに表示します。 macOS 10.13.6 以降と、iOS/iPadOS 9.3.2 以降が対象です。 |
    | <strong>プライバシー</strong> | [プライバシー] 画面をユーザーに表示します。 macOS 10.13.4 以降と、iOS/iPadOS 11.3 以降が対象です。 |
    | <strong>Android の移行</strong> | Android デバイスからデータを移行するオプションをユーザーに表示します。 iOS/iPadOS 9.0 以降が対象です。|
    | <strong>iMessage と FaceTime</strong> | iMessage と FaceTime を設定するオプションをユーザーに提示します。 iOS/iPadOS 9.0 以降が対象です。 |
    | <strong>オンボード</strong> | 送付状、マルチタスク コントロール センターなど、ユーザー教育用のオンボード情報画面を表示します。 iOS/iPadOS 11.0 以降が対象です。 |
    | <strong>Watch の移行</strong> | Watch デバイスからデータを移行するオプションをユーザーに表示します。 iOS/iPadOS 11.0 以降が対象です。|
    | <strong>画面の表示時間</strong> | [画面の表示時間] 画面を表示します。 macOS 10.15 以降と、iOS/iPadOS 12.0 以降が対象です。 |
    | <strong>ソフトウェア更新プログラム</strong> | 必須のソフトウェア更新プログラム画面を表示します。 iOS/iPadOS 12.0 以降が対象です。 |
    | <strong>SIM のセットアップ</strong> | セルラー プランを追加するオプションをユーザーに表示します。 iOS/iPadOS 12.0 以降が対象です。 |
    | <strong>外観</strong> | [表示] 画面をユーザーに表示します。 macOS 10.14 以降と、iOS/iPadOS 13.0 以降が対象です。 |
    | <strong>簡易言語</strong>| [Express Language]\(簡易言語\) 画面をユーザーに表示します。 |
    | <strong>優先する言語</strong> | **[優先する言語]** を選択するオプションをユーザーに提示します。 |
    | <strong>デバイスからデバイスへの移行</strong> | 古いデバイスからこのデバイスへデータを移行するオプションをユーザーに提示します。 iOS/iPadOS 13.0 以降が対象です。 |
    | <strong>登録</strong> | [登録] 画面をユーザーに表示します。 macOS 10.9 以降が対象です。 |
    | <strong>FileVault</strong> | FileVault 2 encryption\(FileVault 2 の暗号化\) 画面をユーザーに表示します。 macOS 10.10 以降が対象です。 |
    | <strong>iCloud 診断</strong> | [iCloud Analytics] 画面をユーザーに表示します。 macOS 10.12.4 以降が対象です。 |
    | <strong>iCloud ストレージ</strong> | [iCloud Documents and Desktop]\(iCloud の書類とデスクトップ\) 画面をユーザーに表示します。 macOS 10.13.4 以降が対象です。 |
    

16. **[次へ]** を選択して、 **[Review + Create]\(確認および作成\)** ページへ移動します。

17. プロファイルを保存するには、 **[作成]** を選択します。

### <a name="dynamic-groups-in-azure-active-directory"></a>Azure Active Directory の動的グループ

登録の **[名前]** フィールドを使用して、Azure Active Directory で動的グループを作成できます。 詳細については、[Azure Active Directory の動的グループ](/azure/active-directory/users-groups-roles/groups-dynamic-membership)に関する記事をご覧ください。

プロファイル名を使用して、この登録プロファイルに対応するデバイスを割り当てるために [enrollmentProfileName パラメーター](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices)を定義できます。

ユーザー アフィニティを使用して ADE デバイスで最速のポリシー配信を行うには、デバイスのセットアップの前に、登録ユーザーが AAD ユーザー グループのメンバーであることを確認してください。 

動的グループを登録プロファイルに割り当てると、登録後にデバイスに対してアプリケーションとポリシーを配信する際に、遅延が発生する可能性があります。


## <a name="sync-managed-devices"></a>マネージド デバイスを同期する
デバイスを管理するアクセス許可を Intune に割り当てたので、Intune と Apple を同期して、マネージド デバイスを Azure ポータルの Intune に表示できます。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]** > **[iOS]** > **[iOS の登録]** > **[Enrollment Program トークン]** を選択しし、一覧からトークンを選択して、 **[デバイス]** > **[同期]** を選択します。![Enrollment Program デバイス ノードと同期リンクのスクリーンショット。](./media/device-enrollment-program-enroll-ios/image06.png)

   許容される Enrollment Program トラフィックについての Apple の規約に準拠するために、Intune では次の制限が課せられています。
   - 完全な同期は 7 日に 1 回だけ実行できます。 完全な同期中に、Intune に接続された Apple MDM サーバーに割り当てられているシリアル番号の完全な最新の一覧を Intune がフェッチします。 ADE デバイスが Intune ポータルから削除された場合、ADE ポータルでは Apple MDM サーバーからの割り当てを解除する必要があります。 割り当てが解除されていない場合、完全な同期が実行されるまでは Intune に再インポートされません。   
   - 同期は 12 時間ごとに自動的に実行されます。 **[同期]** ボタンをクリックして同期することもできます (15 分以内に 2 回以上は同期できません)。 すべての同期要求は、完了までに 15 分与えられます。 同期が完了するまで、 **[同期]** ボタンは無効になっています。 この同期により、既存のデバイスの状態が更新され、Apple MDM サーバーに割り当てられている新しいデバイスがインポートされます。   


## <a name="assign-an-enrollment-profile-to-devices"></a>登録プロファイルをデバイスに割り当てる
登録する前に、Enrollment Program プロファイルをデバイスに割り当てる必要があります。

>[!NOTE]
>**[Apple Serial Numbers\(Apple シリアル番号\)]** ブレードでプロファイルにシリアル番号を割り当てることもできます。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択し、一覧からトークンを選択します。
2. **[デバイス]** を選択し、リスト内でデバイスを選択し、 **[プロファイルの割り当て]** を選択します。
3. **[プロファイルの割り当て]** の下でデバイス用のプロファイルを選択し、 **[割り当て]** を選択します。

### <a name="assign-a-default-profile"></a>既定のプロファイルを割り当てる

特定のトークンを使用して登録するすべてのデバイスに適用される既定のプロファイルを選択することができます。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択し、一覧からトークンを選択します。
2. **[既定のプロファイルの設定]** を選択し、ドロップダウン リストでプロファイルを選択し、 **[保存]** を選択します。 このプロファイルは、トークンに登録されたすべてのデバイスに適用されます。

## <a name="distribute-devices"></a>デバイスを配布する
Apple と Intune の間の管理と同期を有効にし、ADE デバイスを登録できるようにプロファイルを割り当てました。 ユーザーにデバイスを配布できるようになりました。 ユーザー アフィニティがあるデバイスでは、各ユーザーに Intune ライセンスを割り当てる必要があります。 ユーザー アフィニティがないデバイスでは、デバイスのライセンスが必要です。 デバイスがワイプされるまで、アクティブ化されたデバイスでは登録プロファイルを適用できません。

[Device Enrollment Program を使用して Intune に iOS/iPadOS デバイスを登録する方法](../user-help/enroll-your-device-dep-ios.md)に関する記事をご覧ください。

## <a name="renew-an-ade-token"></a>ADE トークンの更新  

> [!NOTE]
> ADE トークンの毎年の更新に加えて、Apple Business Manager でトークンを設定したユーザーの管理対象 Apple ID のパスワードが変更された場合、またはそのユーザーが Apple Business Manager 組織を脱退した場合に、Intune および Apple Business Manager 内の Enrollment Program トークンを更新する必要があります。

1. business.apple.com に移動します。  
2. **[サーバーの管理]** で、更新するトークン ファイルに関連付けられた MDM サーバーを選択します。
3. **[新しいトークンの生成]** を選択します。

    ![生成された新しいトークンのスクリーンショット。](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

4. **[Your Server Token]\(サーバー トークン\)** を選択します。  
5. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択して、トークンを選択します。
    ![Enrollment Program トークンのスクリーンショット。](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. **[トークンを更新する]** を選択し、元のトークンの作成に使用した Apple ID を入力します。  
    ![生成された新しいトークンのスクリーンショット。](./media/device-enrollment-program-enroll-ios/renewtoken.png)

8. 新しくダウンロードしたトークンをアップロードします。  
9. **[トークンを更新する]** を選択します。 トークンが更新されたことの確認が表示されます。   
    ![確認のスクリーンショット。](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-ade-token-from-intune"></a>Intune から ADE トークンを削除する

次の場合に限り、Intune から登録プロファイル トークンを削除できます
- トークンに割り当てられているデバイスがない
- 既定のプロファイルに割り当てられているデバイスがない

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS/macOS]**  >  **[iOS/macOS の登録]**  >  **[Enrollment Program トークン]** を選択して、トークン > **[デバイス]** を選択します。
2. トークンに割り当てられているすべてのデバイスを削除します。
3. **[デバイス]**  >  **[iOS/macOS]**  >  **[iOS/macOS 登録]**  >  **[Enrollment Program トークン]** を選択して、トークン > **[プロファイル]** を選択します。
4. 既定のプロファイルがある場合は、それを削除します。
5. **[デバイス]**  >  **[iOS/macOS]**  >  **[iOS/macOS 登録]**  >  **[Enrollment Program トークン]** を選択して、トークン > **[削除]** を選択します。
