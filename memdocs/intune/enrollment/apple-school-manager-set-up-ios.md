---
title: iOS/iPadOS デバイスのための Apple School Manager プログラム登録
titleSuffix: Microsoft Intune
description: 企業所有の iOS/iPadOS デバイスを Intune で登録するために、Apple School Manager プログラム登録を設定する方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4c35a23e-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1bbca477b389b568d2aca1ab0f9394ec09fe2b24
ms.sourcegitcommit: e17fc618d4c56c38a65c489b73ba27baa133ee7b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80696551"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-school-manager"></a>Apple School Manager での iOS/iPadOS デバイス登録の設定

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

[Apple School Manager](https://school.apple.com/) プログラムで購入した iOS/iPadOS デバイスを登録するよう Intune を設定できます。 Apple School Manager と共に Intune を使用して、デバイスに触れることなく、大量の iOS/iPadOS デバイスを登録できます。 学生や教師がデバイスの電源をオンにすると、セットアップ アシスタントが構成済み設定で実行され、デバイスが管理対象として登録されます。

Apple School Manager 登録を有効にするには、Intune と Apple School Manager ポータルの両方を使用します。 管理するために Intune にデバイスを割り当てられるように、シリアル番号のリストまたは注文番号が必要になります。 登録時にデバイスに適用された設定を含む自動デバイス登録 (ADE) の登録プロファイルを作成します。

Apple School Manager 登録を、[Apple の Device Enrollment Program](device-enrollment-program-enroll-ios.md) や[デバイス登録マネージャー](device-enrollment-manager-enroll.md)で使用することはできません。

**必要条件**
- [Apple モバイル デバイス管理 (MDM) プッシュ証明書](apple-mdm-push-certificate-get.md)
- [MDM 機関](../fundamentals/mdm-authority-set.md)
- ADFS を使用している場合、ユーザー アフィニティには [WS-Trust 1.3 Username/Mixed エンドポイント](https://technet.microsoft.com/library/adfs2-help-endpoints)が必要です。 [詳細については、こちらを参照してください](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)。
- [Apple School Management](http://school.apple.com) プログラムで購入されたデバイス

## <a name="get-an-apple-token-and-assign-devices"></a>Apple トークンを取得し、デバイスを割り当てる

Apple School Manager で企業所有の iOS/iPadOS デバイスを登録するには、Apple のトークン (.p7m) ファイルが必要です。 このトークンにより、Intune は Apple School Manager 参加デバイスに関する情報を同期できるようになります。 また、Intune は Apple への登録プロファイルのアップロードを実行して、デバイスをそれらのプロファイルに割り当てられるようになります。 Apple ポータルでは、管理するデバイスのシリアル番号も割り当てることができます。

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-an-apple-token"></a>手順 1. Apple トークンを作成するために必要な Intune 公開キー証明書をダウンロードする

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]**  >  **[追加]** を選択します。

   ![Enrollment Program トークンを取得します。](./media/device-enrollment-program-enroll-ios/image01.png)

2. **[Enrollment Program トークン]** ブレードで、 **[公開キーをダウンロードします]** を選択して、暗号化キー (.pem) ファイルをダウンロードし、ローカルに保存します。 .pem ファイルは、Apple School Manager ポータルから信頼関係証明書を要求するために使用します。
     ![[Enrollment Program トークン] ブレード](./media/apple-school-manager-set-up-ios/image02.png)

### <a name="step-2-download-a-token-and-assign-devices"></a>手順 2. トークンをダウンロードしてデバイスを割り当てる
1. **[Apple School Manager を使用してトークンを作成します]** を選択し、会社の Apple ID で Apple School にサインインします。 この Apple ID を使用して、Apple School Manager トークンを更新することができます。
2. [Apple School Manager ポータル](https://school.apple.com)で、 **[MDM Servers]\(MDM サーバー\)** に移動し、 **[Add MDM Server]\(MDM サーバーの追加\)** (右上) を選択します。
3. **MDM サーバー名**を入力します。 サーバー名は、自分がモバイル デバイス管理 (MDM) サーバーを識別できるようにするための名前です。 Microsoft Intune サーバーの名前または URL ではありません。
   ![シリアル番号オプションが選択された Apple School Manager ポータルのスクリーンショット](./media/apple-school-manager-set-up-ios/asm-server-assignment.png)

4. Apple ポータルで **[ファイルのアップロード...]** を選択し、.pem ファイルを参照して、 **[Save MDM Server]\(MDM サーバーの保存\)** (右下) を選択します。
5. **[トークンの取得]** を選択し、サーバー トークン (.p7m) ファイルをコンピューターにダウンロードします。
6. **[デバイスの割り当て]** に移動し、**シリアル番号**、**注文番号** を手動で入力するか、**CSV ファイルのアップロード**で **[デバイスの選択]** を行います。
     ![シリアル番号オプションが選択された Apple School Manager ポータルのスクリーンショット](./media/apple-school-manager-set-up-ios/asm-device-assignment.png)
7. **[Assign to Server]\(サーバーに割り当てる\)** を選択し、作成した **MDM サーバー**を選択します。
8. **デバイスの選択**方法を指定してから、デバイス情報と詳細を提供します。
9. **[Assign to Server]** (サーバーに割り当てる) を選択し、Microsoft Intune に指定した &lt;ServerName&gt; を選択して、 **[OK]** を選択します。

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>手順 3. このトークンの作成に使用した Apple ID を保存する

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、今後の参照用に Apple ID を指定します。

![Enrollment Program トークンの作成に使った Apple ID の指定と、Enrollment Program トークンの参照のスクリーンショット。](./media/apple-school-manager-set-up-ios/image03.png)

### <a name="step-4-upload-your-token"></a>手順 4. トークンをアップロードする
**[Apple トークン]** ボックスで、証明書 (.pem) ファイルを参照し、 **[開く]** を選択して、 **[作成]** を選択します。 このプッシュ証明書を使用して、Intune はモバイル デバイスを登録し、登録したモバイル デバイスにポリシーを適用して iOS/iPadOS デバイスを管理できます。 Intune は、Apple の Apple School Manager デバイスを自動的に同期します。

## <a name="create-an-apple-enrollment-profile"></a>Apple 登録プロファイルの作成
これでトークンがインストールされました。Apple School デバイスの登録プロファイルを作成することができます。 デバイス登録プロファイルで、デバイス グループに対して登録時に適用する設定を定義します。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択します。
2. トークンを選択し、 **[プロファイル]** を選択し、 **[プロファイルの作成]** を選択します。

3. **[プロファイルの作成]** で、管理用にプロファイルの **[名前]** と **[説明]** を入力します。 ユーザーには、これらの詳細は表示されません。 この **[名前]** フィールドを使用して、Azure Active Directory で動的グループを作成できます。 この登録プロファイルに対応するデバイスを割り当てるために enrollmentProfileName パラメーターを定義する場合はプロファイル名を使用します。 Azure Active Directory の動的グループの詳細については[こちら](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices)を参照してください。

    ![プロファイル名と説明。](./media/apple-school-manager-set-up-ios/image05.png)

4. **[ユーザー アフィニティ]** で、このプロファイルに対応するデバイスを割り当て済みユーザーとともに登録する必要があるかどうかを選択します。
    - **[ユーザー アフィニティとともに登録する]** - このオプションは、ユーザーに属しているデバイスであって、かつアプリのインストールなどのサービスにポータル サイトを使用する必要があるデバイスの場合に選択します。 このオプションにより、ユーザーは会社ポータルを使用して自分のデバイスを認証することもできます。 ADFS を使用している場合、ユーザー アフィニティには [WS-Trust 1.3 Username/Mixed エンドポイント](https://technet.microsoft.com/library/adfs2-help-endpoints)が必要です。 [詳細については、こちらを参照してください](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)。   Apple School Manager の [共有 iPad] モードでは、ユーザーはユーザー アフィニティなしで登録する必要があります。

    - **[ユーザー アフィニティなしで登録する]** - このオプションは、共有デバイスなど、1 人のユーザーに関連付けられていないデバイスの場合に選択します。 このオプションは、ローカルのユーザー データにアクセスせずにタスクを実行するデバイスで使用します。 ポータル サイト アプリなどのアプリは動作しません。

5. **[ユーザー アフィニティとともに登録する]** を選択した場合は、Apple セットアップ アシスタントではなく、ポータル サイトを使ってユーザーに認証させることが可能です。

    ![ポータル サイトで認証します。](./media/apple-school-manager-set-up-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > 次のいずれかを実行する場合は、 **[Apple セットアップ アシスタントの代わりにポータル サイトで認証します]** を **[はい]** に設定します。
    >    - 多要素認証の使用
    >    - 最初のサインイン時にパスワードの変更が必要なユーザーにプロンプトを表示する
    >    - 登録の間に有効期限が切れたパスワードのリセットをユーザーに求める
    >
    > Apple セットアップ アシスタントによって認証している場合は、これらはサポートされません。

6. **[デバイス管理の設定]** を選択し、このプロファイルを使用するデバイスを監視するかどうかを選択します。
    **[監視下]** デバイスでは、より多くの管理オプションを使用できるようになり、既定で [アクティベーション ロック] は無効になります。 Microsoft では、多数の iOS または iPadOS デバイスを展開する組織に対して特に、監視モードを有効にするメカニズムとして ADE の利用をお勧めしています。

    デバイスが監視対象であることは次の 2 つの方法でユーザーに通知されます。

   - ロック画面には次のように表示されます。"This iPhone is managed by Contoso." (この iPhone は Contoso によって管理されています。)
   - **[設定]**  >  **[全般]**  >  **[情報]** 画面には、次のように表示されます。"This iPhone is supervised. (この iPhone は監視されています。) Contoso はインターネット トラフィックを監視し、このデバイスの位置を特定できます。" と、

     > [!NOTE]
     > 監視なしで登録されているデバイスは、Apple Configurator でのみ監視対象にリセットすることができます。 この方法でデバイスをリセットするには、USB ケーブルを使用して iOS/iPadOS デバイスを Mac に接続する必要があります。 詳細については、[Apple Configurator ドキュメント](http://help.apple.com/configurator/mac/2.3)を参照してください。

7. このプロファイルを使用するデバイスの登録をロックするかどうかを選択します。 **[ロックされた登録]** を選択すると、 **[設定]** メニューから管理プロファイルを削除する操作を許可する iOS/iPadOS 設定が無効になります。 デバイスの登録後は、デバイスをワイプしないと、この設定を変更できません。 そのようなデバイスについては、 **[監視下]** 管理モードを *[はい]* に設定する必要があります。 

8. 管理された Apple ID を使用して、複数のユーザーが登録済みの iPad にサインオンすることを許可できます。 これを行うには、 **[共有 iPad]** で **[はい]** を選択します (このオプションを使用するには、 **[ユーザー アフィニティなしで登録する]** と **[監視下]** モードで **[はい]** が設定されている必要があります。)管理された Apple ID は、Apple School Manager ポータルで作成されます。 [共有 iPad](../fundamentals/education-settings-configure-ios-shared.md) と [Apple の共有 iPad の要件](https://help.apple.com/classroom/ipad/2.0/#/cad7e2e0cf56)についての詳細をご覧ください。

9. このプロファイルを使用するデバイスを**コンピューターと同期**できるようにするかどうかを選択します。 **[すべて拒否]** を選択すると、このプロファイルを使用しているすべてのデバイスでは、どのコンピューターのどのデータとも同期できなくなります。 **[証明書による Apple Configurator の許可]** を選択した場合は、 **[Apple Configurator の証明書]** で証明書を選択する必要があります。

10. 前の手順で **[証明書による Apple Configurator の許可]** を選択した場合は、インポートする Apple Configurator の証明書を選択します。

11. デバイスに対して登録時に自動的に適用される名前付け形式を指定することができます。 これを行うには、 **[デバイス名のテンプレートを適用する]** で **[はい]** を選択します。 次に、 **[デバイス名のテンプレート]** ボックスに、このプロファイルを使用する名前に使うテンプレートを入力します。 デバイスの種類とシリアル番号を含むテンプレート形式を指定できます。

12. **[OK]** を選びます。

13. **[セットアップ アシスタントの設定]** を選択し、次のプロファイル設定を構成します。![セットアップ アシスタントのカスタマイズ。](./media/apple-school-manager-set-up-ios/setupassistantcustom.png)


    |                 設定                  |                                                                                               [説明]                                                                                               |
    |------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     <strong>部門名</strong>     |                                                             アクティブ化中にユーザーが <strong>[構成について]</strong> をタップすると表示されます。                                                              |
    |    <strong>部署の電話番号</strong>     |                                                          アクティブ化中にユーザーが <strong>[ヘルプが必要ですか]</strong> ボタンをクリックすると表示されます。                                                          |
    | <strong>セットアップ アシスタントのオプション</strong> |                                                     次の省略可能な設定は、後で iOS/iPadOS の <strong>[設定]</strong> メニューで設定できます。                                                      |
    |        <strong>パスコード</strong>         | アクティブ化時にパスコードの入力を求めます。 デバイスがセキュリティで保護されていない場合は、他の何らかの方法 (デバイスを 1 つのアプリに制限するキオスク モードなど) でアクセスが制御されていない限り、パスコードを常に必須にします。 |
    |    <strong>ロケーション サービス</strong>    |                                                                 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます。                                                                  |
    |         <strong>復元</strong>         |                                                                有効にすると、アクティブ化時に、セットアップ アシスタントによって iCloud バックアップがプロンプトされます。                                                                 |
    |   <strong>iCloud と Apple ID</strong>   |                         有効にすると、セットアップ アシスタントによって Apple ID でサインインするように求められ、[アプリとデータ] 画面で iCloud バックアップからデバイスを復元できるようになります。                         |
    |  <strong>使用条件</strong>   |                                                   有効にすると、アクティブ化時に、セットアップ アシスタントによって Apple の使用条件に同意するように求められます。                                                   |
    |        <strong>Touch ID</strong>         |                                                                 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます。                                                                 |
    |        <strong>Apple Pay</strong>        |                                                                 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます。                                                                 |
    |          <strong>Zoom</strong>           |                                                                 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます。                                                                 |
    |          <strong>Siri</strong>           |                                                                 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます。                                                                 |
    |     <strong>診断データ</strong>     |                                                                 有効にすると、アクティブ化時に、セットアップ アシスタントによってこのサービスがプロンプトされます。                                                                 |


14. **[OK]** を選びます。

15. プロファイルを保存するには、 **[作成]** を選択します。

## <a name="connect-school-data-sync"></a>School Data Sync の接続
(省略可能) Apple School Manager では、Microsoft School Data Sync (SDS) を使用した Azure Active Directory (AD) へのクラス リスト データの同期がサポートされています。 SDS と同期できるのは 1 つのトークンのみです。 School Data Sync で別のトークンを設定した場合、SDS を含んでいる以前のトークンから SDS が削除されます。 新しい接続によって現在のトークンが置き換えられます。 SDS を使用して学校のデータを同期するには、次の手順を完了します。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択します。
2. Apple School Manager トークンを選択し、 **[School Data Sync]** を選択します。
3. **[School Data Sync]** で、 **[許可]** を選択します。 この設定により、Intune は Office 365 で SDS に接続できます。
4. Apple School Manager と Azure AD の間の接続を有効にするには、 **[Microsoft School Data Sync の設定]** を選択します。[School Data Sync の設定方法](https://support.office.com/article/Install-the-School-Data-Sync-Toolkit-8e27426c-8c46-416e-b0df-c29b5f3f62e1)について詳しく学びます。
5. **[保存]**  >  **[OK]** をクリックします。

## <a name="sync-managed-devices"></a>マネージド デバイスを同期する

Intune に Apple School Manager デバイスを管理するためのアクセス許可を割り当てたら、Intune と Apple サービスを同期して、Intune でマネージド デバイスを表示させます。

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択し、一覧からトークンを選択して、 **[デバイス]**  >  **[同期]** を選択します。![Enrollment Program デバイス ノードと同期リンクのスクリーンショット。](./media/apple-school-manager-set-up-ios/image06.png)

許容される Enrollment Program トラフィックについての Apple の規約に準拠するために、Intune では次の制限が課せられています。
- 完全な同期は 7 日に 1 回だけ実行できます。 Intune は、完全な同期中に、Intune に割り当てられているすべての Apple シリアル番号を更新します。 前回の完全同期の 7 日以内に完全同期が試みられると、Intune では、Intune にまだ一覧表示されていないシリアル番号のみが更新されます。
- すべての同期要求は、完了までに 15 分与えられます。 この時間中または要求が成功するまで、 **[同期]** ボタンは無効にされます。
- Intune は、24 時間ごとに新規のデバイスと削除されたデバイスを Apple と同期します。

>[!NOTE]
>**[Enrollment Program デバイス]** ブレードで、Apple School Manager のシリアル番号をプロファイルに割り当てることもできます。

## <a name="assign-a-profile-to-devices"></a>デバイスにプロファイルを割り当てる
Intune によって管理される Apple School Manager デバイスを登録する前に、デバイスに登録プロファイルを割り当てる必要があります。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、 **[デバイス]**  >  **[iOS]**  >  **[iOS の登録]**  >  **[Enrollment Program トークン]** を選択し、一覧からトークンを選択します。
2. **[デバイス]** を選択し、リスト内でデバイスを選択し、 **[プロファイルの割り当て]** を選択します。
3. **[プロファイルの割り当て]** の下でデバイス用のプロファイルを選択し、 **[割り当て]** を選択します。

## <a name="distribute-devices-to-users"></a>デバイスのユーザーへの配布

Apple と Intune の間の同期と管理を有効にし、Apple School デバイスを登録できるようにプロファイルを割り当てました。 ユーザーにデバイスを配布できるようになりました。 iOS/iPadOS Apple School Manager デバイスの電源をオンにすると、それが Intune の管理対象として登録されます。 現在使用中のアクティブ化されたデバイスでは、そのデバイスがワイプされるまで、プロファイルを適用することはできません。
