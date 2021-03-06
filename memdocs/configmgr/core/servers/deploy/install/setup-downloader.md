---
title: セットアップ ダウンローダー ツール
titleSuffix: Configuration Manager
description: スタンドアロン ツールを使用して、セットアップのための現在のバージョンの主要なインストール ファイルをダウンロードします。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428829"
---
# <a name="setup-downloader-for-configuration-manager"></a>Configuration Manager のセットアップ ダウンローダー

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager セットアップを実行してサイトをインストールまたはアップグレードする前に、セットアップ ダウンローダー スタンドアロン ツールを使用して、更新されたセットアップ ファイルをダウンロードすることができます。 インストールする Configuration Manager のバージョンからツールを実行します。 更新されたセットアップ ファイルを使って、サイト インストールで主要なインストール ファイルの最新バージョンが確実に使用されるようにします。

セットアップ ダウンローダーを使用するときに、ファイルを格納するフォルダーを指定します。 ツールの実行に使用するアカウントには、ダウンロード フォルダーへの**フル コントロール** アクセス許可が必要です。 サイトをインストールまたはアップグレードするためのセットアップを実行するときに、前にダウンロードしたこのファイルのローカル コピーを指定できます。 この動作により、サイトのインストールやアップグレードを開始するときに、セットアップで Microsoft に接続することはなくなります。 同じバージョンの他のサイトのインストールまたはアップグレードには、セットアップ ファイルの同じローカル コピーを使用できます。

セットアップ ダウンローダー ツールでは、次の種類のファイルがダウンロードされます。

- 前提条件となる必須の再頒布可能ファイル
- 言語パック
- セットアップ用の最新の製品の更新プログラム

セットアップ ダウンローダーを実行するための 2 つのオプションがあります。

- ユーザー インターフェイスを使用してアプリケーションを実行する
- その他のコマンドライン オプションの場合は、コマンド プロンプトでアプリケーションを実行する

組織でファイアウォールまたはプロキシ デバイスを使用してインターネットとのネットワーク通信が制限されている場合は、ツールによるインターネット エンドポイントへのアクセスを許可する必要があります。 ツールを実行するデバイスでは、サービス接続ポイントと同じインターネット アクセスが必要です。 詳細については、「[Internet access requirements (インターネット アクセスの要件)](../../../plan-design/network/internet-endpoints.md#bkmk_scp)」を参照してください。<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> ユーザー インターフェイスでセットアップ ダウンローダーを実行する

1. インターネットにアクセスできるコンピューターで、インストールする Configuration Manager のバージョン用のインストール メディアを参照します。

1. **SMSSETUP\BIN\X64** サブフォルダーで、**Setupdl.exe** を実行します。

1. 更新されたインストール ファイルを格納するフォルダーのパスを指定してから、 **[ダウンロード]** を選択します。 セットアップ ダウンローダーにより、現在ダウンロード フォルダーにあるファイルが検証されます。 失われているファイルまたは既存のファイルより新しいファイルだけをダウンロードします。 ダウンロードされた言語のサブフォルダーと、その他の必要なコンポーネントが作成されます。

1. ダウンロード結果を確認する場合は、**C:\ConfigMgrSetup.log** を参照してください。

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> コマンド プロンプトからセットアップ ダウンローダーを実行する

1. コマンド プロンプトを開き、インストールする Configuration Manager のバージョン用のインストール メディアにディレクトリを変更します。

1. ディレクトリを **SMSSETUP\BIN\X64** サブフォルダーに変更し、必要なオプションを使用して **Setupdl.exe** を実行します。

1. ダウンロード結果を確認する場合は、**C:\ConfigMgrSetup.log** を参照してください。

### <a name="command-line-options"></a>コマンド ライン オプション

次のコマンド ライン オプションを **Setupdl.exe** で使用できます。

- **/VERIFY**:ダウンロード フォルダーにあるファイル (言語ファイルを含む) を検証します。 古いファイルの一覧については、**C:\ConfigMgrSetup.log** を確認してください。 このオプションを使用すると、どのファイルもダウンロードされません。

- **/VERIFYLANG**:ダウンロード フォルダーにある言語ファイルのみを検証します。 古い言語ファイルの一覧については、**C:\ConfigMgrSetup.log** を確認してください。

- **/LANG**:言語ファイルのみをダウンロード フォルダーにダウンロードします。

- **/NOUI**:ユーザー インターフェイスを使用せずにセットアップ ダウンローダーを起動します。 このオプションを使用する場合は、**ダウンロード パス**が必要です。

- **ダウンロード パス**:検証またはダウンロード プロセスを自動的に開始するには、ダウンロード フォルダーへのパスを指定します。 **/NOUI** オプションを使用する場合は、ダウンロード パスが必要です。 ダウンロード パスを指定しない場合、セットアップ ダウンローダーでパスを指定するように求められます。 フォルダーが存在しない場合は、セットアップ ダウンローダーによって作成されます。

### <a name="example-commands"></a>コマンドの例

#### <a name="example-1"></a>例 1

セットアップ ダウンローダーで、指定されたダウンロード フォルダーにあるファイルが検証されてから、ファイルがダウンロードされます。

`setupdl.exe C:\Download`

#### <a name="example-2"></a>例 2

セットアップ ダウンローダーで、指定されたダウンロード フォルダーにあるファイルのみが検証されます。

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>例 3

セットアップ ダウンローダーで、指定されたダウンロード フォルダーにあるファイルが検証されてから、ファイルがダウンロードされます。 このツールでは、ユーザー インターフェイスは表示されません。

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>例 4

セットアップ ダウンローダーで、指定されたダウンロード フォルダーにある言語ファイルが検証されてから、言語ファイルのみがダウンロードされます。

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> セットアップ ダウンローダー ファイルを別のコンピューターにコピーする

1. エクスプローラーで、次のいずれかの場所に移動します。

    - **&lt;Configuration Manager インストール メディア>\SMSSETUP\BIN\X64**

    - **&lt;Configuration Manager インストール パス>\BIN\X64**

1. 次のファイルを別のコンピューターの同じフォルダーにコピーします。

    - **setupdl.exe**

    - **.\\&lt;言語>\\setupdlres.dll**

        > [!NOTE]
        > このファイルはインストール言語のサブフォルダーにあります。 たとえば、英語は `00000409` サブフォルダーにあります。

    デバイス上の宛先フォルダーは、次の例のようになるはずです。

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. セットアップ先のコンピューターからセットアップ ダウンローダーを実行します。 [ユーザー インターフェイス](#bkmk_ui)または[コマンド プロンプト](#bkmk_cmd)を使用します。
