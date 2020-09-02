---
title: Windows 10 ポータル サイト アプリを手動で追加する
titleSuffix: Microsoft Intune
description: 従業員が Microsoft Store から自分の PC へ Windows 10 ポータル サイト アプリを手動で追加できる方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: bfe1a2d3-f611-4dbb-adef-c0dff4d7b810
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e359a87cb9e62b6d7542d82d9819b5c132a8bc2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910266"
---
# <a name="add-the-windows-10-company-portal-app-by-using-microsoft-intune"></a>Microsoft Intune を使用して Windows 10 ポータル サイト アプリを追加する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

デバイスを管理し、アプリをインストールするために、エンド ユーザーは Microsoft Store からポータル サイト アプリをインストールすることができます。 ただし、ビジネスでポータル サイト アプリを割り当てる必要がある場合は、Intune から直接 Windows 10 ポータル サイト アプリを割り当てることができます。 Intune をビジネス向け Microsoft Store と統合していない場合でも、同様に割り当てることができます。

 > [!IMPORTANT]
 > ポータル サイト アプリをダウンロードする場合、この記事で説明されたオプションでは、アプリの更新プログラムがリリースされるたびに、手動で更新プログラムを割り当てる必要があります。 Windows 10 Autopilot でプロビジョニングされたデバイス用のポータル サイト アプリを展開するには、[Windows 10 ポータル サイト アプリのオートパイロット デバイスの追加](store-apps-company-portal-autopilot.md)に関するページをご覧ください。

## <a name="configure-settings-to-show-offline-apps"></a>オフライン アプリ表示するように設定を構成する
1. 自分の管理アカウントを使って[ビジネス向け Microsoft Store](https://www.microsoft.com/business-store) にサインインします。
2. ウィンドウの上部付近にある **[管理]** タブを選択します。
3. 左側のウィンドウで、 **[設定]** を選択します。
4. **[Shopping experience]\(ショッピング体験\)** の **[Show offline apps]\(オフライン アプリの表示\)** を **[オン]** に設定します。  
    オフラインのライセンスされたアプリが表示されます。

## <a name="download-the-offline-company-portal-app"></a>オフラインのポータル サイト アプリをダウンロードする
1. **ポータル サイト** アプリを検索して選択します。
2. **[ライセンスの種類]** を **[オフライン]** に設定します。
3. **[アプリの取得]** を選択し、オフラインのポータル サイト アプリを取得して、インベントリに追加します。
4. **[ポータル サイト]** アプリ ページの **[管理]** を選択します。
5. **プラットフォーム**に **[Windows 10 *all devices*]\(Windows 10 の*すべてのデバイス*\)** を選択し、適切な**最小バージョン**、**アーキテクチャ**、**アプリ メタデータのダウンロード**の各値を選択します。 
6. **[パッケージの詳細]** の下の **[ダウンロード]** を選択して、ローカル コンピューターにファイルを保存します。

    ![Windows 10 デバイス、X86 のアーキテクチャが選択されている状態](./media/app-sideload-windows/Win10CP-all-devices.png)

7. **[ダウンロード]** を選択して、[必要なフレームワーク] の下のすべてのパッケージをダウンロードします。  

    x86、x64、および ARM アーキテクチャでこのアクションを完了する必要があります。<br> 
    *最小 OS バージョンとして 1507 を選択した場合は 9 個の必須フレームワーク パッケージ、1511 を選択した場合は 12 個のパッケージ、1607 を選択した場合は 15 個のパッケージがあります。*

8. Azure Portal の Microsoft Intune で、新しいアプリとしてポータル サイト アプリをアップロードします。 **[アプリケーションの種類の選択]** ペインで **[アプリの種類]** として [基幹業務アプリ] を選択してアプリケーションを追加します。 次に、アプリ パッケージ ファイル (拡張子 .AppxBundle) を選択します。

9. **[Select dependency app files]\(依存関係アプリ ファイルの選択\)** で、Shift キーを押しながらクリックして手順 7 でダウンロードしたすべての依存関係を選択し、必要なアーキテクチャの **[追加済み]** 列に **[はい]** が表示されることを確認します。

     > [!NOTE]
     > 依存関係が追加済みでない場合は、指定したデバイスの種類にアプリがインストールされていない可能性があります。

10. **[OK]** をクリックし、必要な **[追加情報]** を入力し、 **[追加]** .をクリックします。

11. 選択した一連のユーザーまたはデバイス グループに、必要なアプリとしてポータル サイト アプリを割り当てます。  

Intune がユニバーサル アプリ用に依存関係をどのように処理するかについて詳しくは、「[Deploying an appxbundle with dependencies via Microsoft Intune MDM](/archive/blogs/configmgrdogs/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm)」 (Microsoft Intune MDM 経由で依存関係を使用して appxbundle を展開する) をご覧ください。  

## <a name="frequently-asked-questions"></a>よく寄せられる質問 
### <a name="how-do-i-update-the-company-portal-app-on-my-users-devices-if-they-have-already-installed-the-older-apps-from-the-store"></a>ユーザーがストアから古いアプリを既にインストールしている場合に、ユーザーのデバイスのポータル サイト アプリを更新する方法
ユーザーが Microsoft Store から Windows 8.1 ポータル サイト アプリを既にインストールしている場合は、お客様またはお客様のユーザーが特に操作を行わなくても、彼らのアプリは最新バージョンに自動的に更新されます。 更新が実行されない場合は、デバイスでストア アプリの自動更新を有効にしているかどうかをユーザーに確認してください。   

### <a name="how-do-i-upgrade-my-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>サイドロードした Windows 8.1 のポータル サイト アプリを Windows 10 のポータル サイト アプリにアップグレードする方法
推奨される移行パスとして、割り当てアクションを **[アンインストール]** に設定して、Windows 8.1 ポータル サイト アプリの割り当てを削除します。 この設定を選択したら、前述のオプションのいずれかを使用して、Windows 10 ポータル サイト アプリを割り当てることができます。  

アプリをサイドロードする必要があり、Symantec 証明書で署名せずに Windows 8.1 ポータル サイトを割り当てた場合は、この記事の前のセクションの手順を実行してアップグレードを完了します。

アプリをサイドロードする必要があり、Symantec コード署名証明書で Windows 8.1 ポータル サイト アプリに署名し割り当てた場合は、次のセクションの手順に従ってください。

### <a name="how-do-i-upgrade-my-signed-and-sideloaded-windows-81-company-portal-app-to-the-windows-10-company-portal-app"></a>署名およびサイドロードした Windows 8.1 のポータル サイト アプリを Windows 10 のポータル サイト アプリにアップグレードする方法
推奨される移行パスとして、割り当てアクションを **[アンインストール]** に設定して、Windows 8.1 ポータル サイト アプリの既存の割り当てを削除します。 この設定を選択したら、通常、Windows 10 ポータル サイト アプリを割り当てることができます。  

これ以外の場合は、アップグレードのパスが確実に考慮されるように、Windows 10 ポータル サイト アプリを適切に更新し、署名する必要があります。  

この方法で Windows 10 ポータル サイト アプリに署名し割り当てた場合、ストアで入手可能になった新しいアプリの更新プログラムごとにこのプロセスを繰り返す必要があります。 ストアが更新されたときに、アプリは自動的に更新されません。  

この場合のアプリへの署名および割り当て方法は、次のとおりです。

1. [Microsoft Intune Windows 10 ポータル サイト アプリの署名スクリプト](https://aka.ms/win10cpscript)をダウンロードします。  
    このスクリプトでは、Windows SDK for Windows 10 をホスト コンピューターにインストールする必要があります。 [Windows SDK for Windows 10 をダウンロードします](https://go.microsoft.com/fwlink/?LinkId=619296)。
2. 上記の説明のように、ビジネス向け Microsoft Store から Windows 10 ポータル サイト アプリをダウンロードします。  
3. Windows 10 ポータル サイト アプリに署名するには、次の表のように、スクリプト ヘッダーに記載された入力パラメーターを使用してスクリプトを実行します。  
    スクリプトに依存関係を渡す必要はありません。 依存関係は、アプリが Intune 管理コンソールにアップロードされる場合にのみ必要です。

| パラメーター |  [説明]  |
|---|---|
| InputWin10AppxBundle  |  ソース appxbundle ファイルへのパス |
| OutputWin10AppxBundle | 署名された appxbundle ファイルの出力パス 
| Win81Appx  | Windows 8.1 ポータル サイト (.APPX) ファイルへのパス |
| PfxFilePath  |  Symantec エンタープライズ モバイル コード署名証明書 (.PFX) ファイルへのパス  |
| PfxPassword  | Symantec エンタープライズ モバイル コード署名証明書のパスワード |
| PublisherId | エンタープライズの発行者 ID 指定しない場合、Symantec エンタープライズ モバイル コード署名証明書の Subject フィールドが使用されます。 |
| SdkPath | Windows SDK for Windows 10 のルート フォルダーへのパス この引数は省略可能で、既定値は ${env:ProgramFiles(x86)}\Windows Kits\10 です。  |

スクリプトの実行が終了したら、スクリプトにより Windows 10 ポータル サイト アプリの署名されたバージョンが出力されます。 その後、アプリの署名されたバージョンを Intune 経由で基幹業務 (LOB) アプリとして割り当てることができます。これにより、現在割り当てられているバージョンがこの新しいアプリにアップグレードされます。  

## <a name="next-steps"></a>次のステップ

- [アプリをグループに割り当てる](apps-deploy.md)