---
title: iOS/iPadOS デバイスの登録 - Apple Configurator - セットアップ アシスタント
titleSuffix: Microsoft Intune
description: Apple Configurator を使用して、セットアップ アシスタントで会社所有の iOS/iPadOS デバイスを登録する方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/04/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 671e4d76-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71563a44e991e7324b9ce258d66d288d4b5a6cdb
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327258"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-configurator"></a>Apple Configurator を使用した iOS/iPadOS デバイス登録の設定

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune では、Mac コンピューター上で実行される [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344) を使用した iOS/iPadOS デバイスの登録がサポートされています。 Apple Configurator を使用して登録するには、各 iOS/iPadOS デバイスを Mac コンピューターに USB 接続し、会社の登録を設定する必要があります。 Apple Configurator では、次の 2 つの方法でデバイスを Intune に登録できます。
- **セットアップ アシスタントを使用した登録** - デバイスをワイプし、セットアップ アシスタント実行時に登録するように準備します。
- **直接登録** - デバイスをワイプせず、iOS/iPadOS 設定を通してデバイスを登録します。 この方法は、**ユーザー アフィニティなし**のデバイスのみに使用できます。

Apple Configurator の登録方法は、[デバイス登録マネージャー](device-enrollment-manager-enroll.md)と同時に使用することはできません。

## <a name="prerequisites"></a>[前提条件]

- iOS/iPadOS デバイスへの物理的なアクセス
- [MDM 機関の設定](../fundamentals/mdm-authority-set.md)
- [Apple MDM プッシュ証明書](apple-mdm-push-certificate-get.md)
- デバイスのシリアル番号 (セットアップ アシスタントでの登録時のみ)
- USB 接続ケーブル
- [Apple Configurator 2.0](https://itunes.apple.com/app/apple-configurator-2/id1037126344) が実行されている macOS コンピューター

## <a name="create-an-apple-configurator-profile-for-devices"></a>デバイスの Apple Configurator プロファイルを作成する

デバイス登録プロファイルで、登録時に適用する設定を定義します。 これらの設定は、1 回だけ適用されます。 Apple Configurator を使用して iOS/iPadOS デバイスを登録するための登録プロファイルを作成するには、以下の手順に従います。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Apple Configurator]**  >  **[プロファイル]**  >  **[作成]** を選択します。

    ![Apple Configurator のプロファイルを作成する](./media/apple-configurator-enroll-ios/apple-config-create-profile.png)

2. **[登録プロファイルの作成]** で、管理用にプロファイルの **[名前]** と **[説明]** を入力します。 ユーザーにはこれらの詳細は表示されません。 この [名前] フィールドを使用して、Azure Active Directory で動的グループを作成できます。 この登録プロファイルに対応するデバイスを割り当てるために enrollmentProfileName パラメーターを定義する場合はプロファイル名を使用します。 Azure Active Directory の動的グループの詳細についてはこちらを参照してください。

    ![[ユーザー アフィニティとともに登録する] が選択されているプロファイル作成画面のスクリーン ショット](./media/apple-configurator-enroll-ios/apple-configurator-profile-create.png)

3. **[ユーザー アフィニティ]** で、このプロファイルに対応するデバイスを割り当て済みユーザーとともに登録する必要があるかどうかを選択します。

    - **[ユーザー アフィニティとともに登録する]** - このオプションは、ユーザーに属しているデバイスであって、かつアプリのインストールなどのサービスにポータル サイトを使用する必要があるデバイスの場合に選択します。 セットアップ アシスタントを使用してデバイスをユーザーに関連付ける必要があります。その後、デバイスは会社のデータや電子メールにアクセスできます。 セットアップ アシスタントでの登録でのみサポートされています。 ユーザー アフィニティには [WS-Trust 1.3 Username/Mixed エンドポイント](https://technet.microsoft.com/library/adfs2-help-endpoints)が必要です。 [詳細については、こちらを参照してください](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)。

    - **[ユーザー アフィニティなしで登録する]** - このオプションは、1 人のユーザーに関連付けられていないデバイスの場合に選択します。 ローカルのユーザー データにアクセスせずにタスクを実行するデバイスで使用します。 ユーザー アフィリエーションが必要なアプリ (基幹業務アプリのインストールに使用されるポータル サイト アプリを含む) は機能しません。 直接登録の場合は必須です。

     > [!NOTE]
     > **[ユーザー アフィニティとともに登録する]** がオンの場合、デバイスが登録されてから最初の 24 時間以内に設定アシスタントを使用してデバイスがユーザーと関連付けられていることを確認します。 そうでないと、登録に失敗して、デバイスを登録するために工場出荷時の設定にリセットする必要が生じます。

4. **[ユーザー アフィニティとともに登録する]** を選択した場合は、Apple セットアップ アシスタントではなく、ポータル サイトでユーザーに認証を行わせるオプションがあります。

    > [!NOTE]
    > 次のいずれかを実行する場合は、 **[Apple セットアップ アシスタントの代わりにポータル サイトで認証します]** を **[はい]** に設定します。
    >    - 多要素認証の使用
    >    - 最初のサインイン時にパスワードの変更が必要なユーザーにプロンプトを表示する
    >    - 登録の間に有効期限が切れたパスワードのリセットをユーザーに求める
    >
    > Apple セットアップ アシスタントで認証を行っているときは、これらはサポートされません。


6. **[作成]** を選択してプロファイルを保存します。

## <a name="setup-assistant-enrollment"></a>Setup Assistant の登録

### <a name="add-apple-configurator-serial-numbers"></a>Apple Configurator のシリアル番号を追加する

1. ヘッダーなしで 2 列のコンマ区切り値 (.csv) リストを作成します。 シリアル番号を左側の列に、詳細を右側の列に追加します。 リストで許可されている現在の最大行数は 5,000 行です。 この .csv リストをテキスト エディターで表示すると次のようになります。

    F7TLWCLBX196,デバイスの詳細</br>
    DLXQPCWVGHMJ,デバイスの詳細

   [iOS/iPadOS デバイスのシリアル番号の見つけ方](https://support.apple.com/HT204073)をご確認ください。
2. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Apple Configurator]**  >  **[デバイス]**  >  **[追加]** を選択します。

5. インポートするシリアル番号に適用する**登録プロファイル**を選択します。 新しいシリアル番号の詳細で既存の詳細を上書きする場合は、 **[既存の ID の詳細を上書きします]** を選択します。
6. **[デバイスのインポート]** でシリアル番号の csv ファイルを参照して、 **[追加]** を選択します。

### <a name="reassign-a-profile-to-device-serial-numbers"></a>デバイス シリアル番号へのプロファイルの再割り当て

Apple Configurator 登録用の iOS/iPadOS シリアル番号をインポートするときに、登録プロファイルを割り当てることができます。 Azure Portal の 2 つの場所からプロファイルを割り当てることができます。
- **Apple Configurator デバイス**
- **AC プロファイル**

#### <a name="assign-from-apple-configurator-devices"></a>Apple Configurator デバイスからの割り当て
1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Apple Configurator]**  >  **[デバイス]** を選択し、シリアル番号を選択して、 **[プロファイルの割り当て]** を選択します。
2. **[プロファイルの割り当て]** で、割り当てる**新しいプロファイル**を選択し、 **[割り当て]** を選択します。

#### <a name="assign-from-profiles"></a>プロファイルからの割り当て
1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Apple Configurator]**  >  **[プロファイル]** を選択し、プロファイルを選択します。
2. プロファイルで **[割り当てられたデバイス]** を選択し、次に **[割り当て]** を選択します。
3. フィルターを使って、プロファイルに割り当てるシリアル番号を見つけ、デバイスを選択して、 **[割り当て]** を選択します。

### <a name="export-the-profile"></a>プロファイルのエクスポート
プロファイルを作成してシリアル番号を割り当てた後、Intune からプロファイルを URL としてエクスポートする必要があります。 エクスポートしたプロファイルは、Mac の Apple Configurator にインポートしてデバイスに展開します。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Apple Configurator]**  >  **[プロファイル]** を選択し、エクスポートするプロファイルを選択します。
2. プロファイルで、 **[プロファイルのエクスポート]** を選択します。
3. **プロファイルの URL** をコピーします。 Apple Configurator にこれを追加すれば、iOS/iPadOS デバイスで使用する Intune プロファイルを定義できます。

   次に、以下の手順に従ってこのプロファイルを Apple Configurator にインポートし、iOS/iPadOS デバイスで使用する Intune プロファイルを定義します。

### <a name="enroll-devices-with-setup-assistant"></a>セットアップ アシスタントを使用したデバイスの登録

1. Mac コンピューターで **Apple Configurator 2** を開きます。 メニュー バーで、 **[Apple Configurator 2]** を選択し、 **[基本設定]** を選択します。
    > [!WARNING]
    > デバイスは、登録プロセス中に、出荷時の構成にリセットされます。 ベスト プラクティスとして、デバイスをリセットし、オンにします。 デバイスを接続するときはデバイスの **[こんにちは]** 画面を表示する必要があります。
    > デバイスが Apple ID アカウントに既に登録されている場合は、登録プロセスを開始する前に、Apple iCloud からデバイスを削除する必要があります。 "Unable to activate [Device name]" (<デバイス名> をアクティブ化できません) というプロンプト エラーが表示されます。

2. **基本設定**ウィンドウで **[サーバー]** を選択し、プラス記号 (+) を選択して MDM サーバー ウィザードを起動します。 **[次へ]** を選択します。
3. Microsoft Intune を使用した iOS/iPadOS デバイスのセットアップ アシスタントの登録の MDM サーバーの**ホスト名または URL** と**登録 URL** を入力します。 登録 URL には、Intune からエクスポートされた登録プロファイル URL を入力します。 **[次へ]** を選択します。  
    "サーバー URL が検証されていない" ことを示す警告は、無視して構いません。 操作を続行するには、ウィザードが完了するまで **[次へ]** を選択します。
4. USB アダプターを使用して iOS/iPadOS モバイル デバイスを Mac コンピューターに接続します。
5. 管理する iOS/iPadOS デバイスを選択し、 **[準備]** を選択します。 **[Prepare iOS/iPadOS Device]\(iOS/iPadOS デバイスを準備\)** ウィンドウで、 **[手動]** を選択してから **[次へ]** を選択します。
6. **[MDM サーバーに登録]** ウィンドウで、作成したサーバーの名前を選択してから **[次へ]** を選択します。
7. **[デバイスを監視]** ウィンドウで、監視レベルを選択してから **[次へ]** を選択します。
8. **[組織を作成]** ウィンドウで、 **[組織]** を選択するか、新しい組織を作成して **[次へ]** を選択します。
9. **[Configure iOS/iPadOS Setup Assistant]\(iOS/iPadOS 設定アシスタントを構成\)** ウィンドウで、ユーザーに表示する手順を選択し、 **[準備]** を選択します。 メッセージが表示されたら、認証して信頼の設定を更新します。  
10. iOS/iPadOS デバイスの準備が完了したら、USB ケーブルを取り外します。  

### <a name="distribute-devices"></a>デバイスを配布する
これで、デバイスを企業登録できるようになりました。 デバイスをオフにし、ユーザーにデバイスを配布します。 ユーザーがデバイスをオンにすると、セットアップ アシスタントが開始されます。

ユーザーは、デバイスを受け取った後、セットアップ アシスタントを完了する必要があります。 ユーザー アフィニティが構成されているデバイスは、会社のポータル アプリをインストールして実行することにより、アプリをダウンロードしてデバイスを管理できるようになります。

## <a name="direct-enrollment"></a>直接登録
iOS/iPadOS デバイスを Apple Configurator で直接登録する場合は、デバイスのシリアル番号を取得しなくてもデバイスを登録できます。 登録時に Intune がデバイス名をキャプチャする前に、デバイスを識別するための名前を指定することもできます。 会社のポータル アプリは、直接登録されているデバイスではサポートされていません。 この方法では、デバイスはワイプされません。

ユーザー アフィリエーションが必要なアプリ (基幹業務アプリのインストールに使用されるポータル サイト アプリを含む) はインストールできません。

### <a name="export-the-profile-as-mobileconfig-to-iosipados-devices"></a>プロファイルを .mobileconfig として iOS/iPadOS デバイスにエクスポートする

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Apple Configurator]**  >  **[プロファイル]** を選択し、エクスポートするプロファイルを選択して、 **[プロファイルのエクスポート]** を選択します。
2. **[直接登録]** で、 **[プロファイルのダウンロード]** を選択して、ファイルを保存します。 登録プロファイルのファイルは 2 週間のみ有効で、これを過ぎると再作成が必要です。
3. [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) を実行している Mac コンピューターにファイルを転送し、管理プロファイルとして iOS/iPadOS デバイスに直接プッシュします。
4. 次の手順に従って、Apple Configurator を使用してデバイスを準備します。
    1. Mac コンピューターで Apple Configurator 2.0 を開きます。
    2. iOS/iPadOS デバイスを USB ケーブルで Mac コンピューターに接続します。 デバイスの検出時にそのデバイス用に開かれた写真、iTunes、その他のアプリを閉じます。
    3. Apple Configurator で、接続された iOS/iPadOS デバイスを選択し、 **[追加]** ボタンを選択します。 デバイスに追加できるオプションがドロップダウン リストに表示されます。 **[プロファイル]** を選択します。

        ![[プロファイル URL] が強調表示された、[プロファイルのエクスポート] の [セットアップ アシスタントの登録] のスクリーンショット](./media/apple-configurator-enroll-ios/ios-apple-configurator-add-profile.png)

    4. ファイル ピッカーを使用して、Intune からエクスポートした .mobileconfig ファイルを選択し、 **[追加]** を選択します。 プロファイルがデバイスに追加されます。 デバイスが "監視対象外" の場合は、インストール時にデバイスの承認が必要です。
5. 次の手順を使用して、iOS/iPadOS デバイスにプロファイルをインストールします。 デバイスでセットアップ アシスタントが既に完了し、使用する準備ができている必要があります。 登録のためにアプリの展開が必要な場合は、アプリの展開時に Apple ID で App Store にサインインする必要があるため、デバイスに Apple ID が設定されている必要があります。
    1. iOS/iPadOS デバイスのロックを解除します。
    2. **[管理プロファイル]** の **[プロファイルのインストール]** ダイアログ ボックスで、 **[インストール]** を選択します。
    3. 必要に応じて、デバイスのパスコードまたは Apple ID を入力します。
    4. **[警告]** を受け入れ、 **[インストール]** を選択します。
    5. **[リモート警告]** を受け入れ、 **[信頼]** を選択します。
    6. **[インストール完了]** ボックスでプロファイルがインストール済みであることを確認したら、 **[完了]** を選択します。

6. iOS/iPadOS デバイスで、 **[設定]** を開き、 **[全般]**  >  **[デバイス管理]**  >  **[管理プロファイル]** の順に移動します。 プロファイルのインストールが一覧表示されていることを確認し、iOS/iPadOS のポリシー制限とインストールされているアプリを確認します。 ポリシー制限とアプリがデバイスに表示されるまでに、最大 10 分かかることがあります。

7. デバイスを配布します。 これで、iOS/iPadOS デバイスが Intune に登録され、管理対象になりました。





