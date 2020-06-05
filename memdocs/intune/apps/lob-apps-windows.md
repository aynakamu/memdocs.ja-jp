---
title: Windows の基幹業務アプリを Microsoft Intune に追加する
titleSuffix: ''
description: Microsoft Intune を使って Windows の基幹業務 (LOB) アプリを追加する方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f81c5f82-5cfa-4b97-9f73-d6cf77c06896
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2614dfc903bf7f10633bf05414ed8a71cdd2e03b
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990626"
---
# <a name="add-a-windows-line-of-business-app-to-microsoft-intune"></a>Windows の基幹業務アプリを Microsoft Intune に追加する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

基幹業務 (LOB) アプリとは、アプリのインストール ファイルから追加するアプリのことです。 通常、この種類のアプリは社内で作成されます。 次に、Microsoft Intune に Windows の LOB アプリを追加するのに役立つ手順を示します。

> [!IMPORTANT]
> 拡張子が .msi のインストール ファイル (コンテンツ準備ツールを使用して .intunewin ファイルにパッケージ化されている) を使用して Win32 アプリを展開する場合、[Intune 管理拡張機能](../apps/intune-management-extension.md)の使用を検討してください。 AutoPilot 登録中に Win32 アプリと基幹業務アプリのインストールを混在させると、アプリのインストールが失敗する場合があります。  

## <a name="select-the-app-type"></a>アプリの種類を選択する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[すべてのアプリ]**  >  **[追加]** の順に選択します。
3. **[アプリの種類の選択]** ペインの **[その他]** のアプリの種類で、 **[基幹業務アプリ]** を選択します。
4. **[選択]** をクリックします。 **[アプリの追加]** 手順が表示されます。

## <a name="step-1---app-information"></a>ステップ 1 - アプリ情報

### <a name="select-the-app-package-file"></a>アプリ パッケージ ファイルを選択する

1. **[アプリの追加]** ウィンドウで、 **[アプリ パッケージ ファイルの選択]** をクリックします。 
2. **[アプリのパッケージ ファイル]** ウィンドウで、参照ボタンを選択します。 次に、拡張子が **.msi**、 **.appx**、または **.appxbundle** の Windows インストール ファイルを選択します。
   アプリの詳細が表示されます。

    > [!NOTE]
    > Windows アプリのファイル拡張子には、 **.msi**、 **.appx**、 **.appxbundle**、 **.msix**、 **.msixbundle** が含まれます。 **.msix** の詳細については、[MSIX のドキュメント](https://docs.microsoft.com/windows/msix/)および「[MSIX アプリの配布](https://docs.microsoft.com/windows/msix/desktop/managing-your-msix-deployment-enterprise)」を参照してください。

3. 操作を完了したら、 **[アプリ パッケージ ファイル]** ペインの **[OK]** を選択してアプリを追加します。

### <a name="set-app-information"></a>アプリ情報を設定する

1. **[アプリ情報]** ページで、アプリの詳細を追加します。 選択したアプリによっては、このウィンドウ内の一部の値が自動的に入力されている場合があります。
    - **名前**:アプリの名前を入力します。これは会社のポータルに表示されます。 使用するアプリ名はすべて一意にします。 同じアプリ名が 2 つ存在する場合、いずれか 1 つのアプリのみが会社のポータルに表示されます。
    - **説明**:アプリの説明を入力します。 説明はポータル サイトに表示されます。
    - **[発行元]** : アプリの発行元の名前を入力します。
    - **アプリのインストール コンテキスト**: このアプリに関連付けるインストール コンテキストを選択します。 デュアル モード アプリの場合は、このアプリに必要なコンテキストを選択します。 他のすべてのアプリの場合は、パッケージに基づいて事前に選択されているため、変更することはできません。
    - **[アプリのバージョンを無視する]** :アプリ開発者がアプリを自動的に更新する場合は、 **[はい]** に設定します。 このオプションは、モバイル .msi アプリにのみ適用されます。
    - **コマンドライン引数**:必要に応じて、実行時に .msi ファイルに適用するコマンド ライン引数を入力します。  たとえば、「 **/q**」と入力します。 **/i** や **/x** などの msiexec コマンドまたは引数は、自動的に使用されるため、含めないでください。 詳細については、「[Command-Line Options (コマンド ライン オプション)](https://docs.microsoft.com/windows/desktop/Msi/command-line-options)」をご覧ください。 .MSI ファイルで追加のコマンドライン オプションが必要な場合は、[Win32 アプリ管理](app-management.md)の使用を検討してください。
    - **[カテゴリ]** : 1 つまたは複数の組み込みアプリ カテゴリを選択するか、ご自身で作成したカテゴリを選択します。 カテゴリを使用すれば、ユーザーはポータル サイトを参照する際にアプリを見つけやすくなります。
    - **[会社のポータルでおすすめアプリとして表示します]** : ユーザーがアプリを参照するとき、会社のポータルのメイン ページにアプリが目立つように表示されます。
    - **[情報 URL]** : このアプリに関する情報が含まれる Web サイトの URL を入力することもできます。 この URL はポータル サイトに表示されます。
    - **[プライバシー URL]** : このアプリのプライバシー情報が含まれる Web サイトの URL を入力することもできます。 この URL はポータル サイトに表示されます。
    - **[開発者]** : (省略可能) アプリ開発者の名前を入力します。
    - **[所有者]** : (省略可能) このアプリの所有者の名前を入力します。 たとえば、「**人事部**」と入力します。
    - **[メモ]** : このアプリに関連付けるメモを入力します。
    - **[ロゴ]** : アプリに関連付けるアイコンをアップロードします。 ユーザーが会社のポータルを参照するとき、アプリにアイコンが表示されます。
2. **[次 へ]** をクリックして **[スコープ タグ]** ページを表示します。

## <a name="step-2---select-scope-tags-optional"></a>ステップ 2 - スコープのタグを選択する (省略可能)

スコープのタグを使って、Intune のクライアント アプリの情報を表示できるユーザーを決定することができます。 スコープのタグの詳細については、[分散 IT のためのロールベースのアクセス制御とスコープのタグの使用](../fundamentals/scope-tags.md)に関するページをご覧ください。

1. **[スコープ タグを選択]** をクリックして、必要に応じてアプリのスコープ タグを追加します。 
2. **[次へ]** をクリックして、 **[割り当て]** ページを表示します。

## <a name="step-3---assignments"></a>ステップ 3 - 割り当て

1. アプリのグループ割り当てについて、 **[必須]** 、 **[登録済みデバイスで使用可能]** 、または **[アンインストール]** を選択します。 詳細については、「[ユーザーとデバイスを整理するためのグループを追加する](../fundamentals/groups-add.md)」と「[Microsoft Intune を使用してアプリをグループに割り当てる](apps-deploy.md)」を参照してください。
2. **[次へ]** をクリックして、 **[確認と作成]** ページを表示します。

## <a name="step-4---review--create"></a>ステップ 4 - 確認と作成

1. アプリに入力した値と設定を確認します。
2. 完了したら、 **[作成]** をクリックしてアプリを Intune に追加します。

    基幹業務アプリの **[概要]** ブレードが表示されます。

作成したアプリがアプリ一覧に表示されます。 一覧から、選択したグループにアプリを割り当てることができます。 詳細については、[アプリをグループに割り当てる方法](apps-deploy.md)に関するページを参照してください。

## <a name="update-a-line-of-business-app"></a>基幹業務アプリを更新する

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

   > [!NOTE]
   > Intune サービスで新しい appx ファイルをデバイスへ正常に展開するには、APK パッケージ内の AndroidManifest.xml ファイルの `Version` 文字列の値を増やす必要があります。

## <a name="configure-a-self-updating-mobile-msi-app-to-ignore-the-version-check-process"></a>バージョン チェック プロセスを無視する自己更新モバイル MSI アプリの構成

バージョン チェック プロセスを無視するように、既知の自己更新モバイル MSI アプリを構成することができます。

一部の MSI インストーラー ベースのアプリは、アプリケーション開発者または別の更新方法によって自動更新されます。 これらの自動更新される MSI アプリには、 **[アプリ情報]** ウィンドウで **[アプリのバージョンを無視する]** を設定できます。 この設定を **[はい]** に切り替えると、Microsoft Intune で Windows クライアントにインストールされているアプリのバージョンが強制されることはありません。

この機能は、競合状態になるのを防ぐのに役立ちます。 たとえば、アプリ開発者によってアプリが自動的に更新され、Intune によって更新される場合、競合状態が発生する可能性があります。 両方が Windows クライアント上のアプリのバージョンを強制しようとして、競合が発生することがあります。

## <a name="next-steps"></a>次のステップ

- 作成したアプリはアプリの一覧に表示されます。 選択したグループにアプリを割り当てることができます。 詳細については、[アプリをグループに割り当てる方法](apps-deploy.md)に関するページを参照してください。

- アプリのプロパティと割り当てを監視する方法について説明します。 「[アプリ情報と割り当てを監視する方法](apps-monitor.md)」を参照してください。

- Intune におけるアプリのコンテキストについて説明します。 「[Microsoft Intune のアプリ ライフサイクルの概要](app-lifecycle.md)」を参照してください。

- Win32 アプリの詳細について学習します。 「[Win32 アプリの管理](apps-win32-app-management.md)」を参照してください。
