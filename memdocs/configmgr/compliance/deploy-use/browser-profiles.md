---
title: Microsoft Edge の設定の構成
titleSuffix: Configuration Manager
description: Windows 10 クライアントで Microsoft Edge レガシ Web ブラウザーの設定を構成する
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: deededfe18275837ae93859c4075837eac870c35
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694782"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Configuration Manager で Microsoft Edge のレガシ設定を構成する

> [!IMPORTANT]
> Microsoft Edge バージョン 77 以降を使用していて、設定ペインを開こうとしている場合は、検索ではなく、ブラウザーのアドレス バーに「`edge://settings/profiles`」と入力します。 詳細については、「[Microsoft Edge の概要](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know)」を参照してください。
>
> この記事は、Microsoft Endpoint Configuration Manager を使用して Microsoft Edge のレガシ設定を管理する IT プロフェッショナル向けです。

*適用対象:Configuration Manager (Current Branch)*

<!-- 1357310 -->
Windows 10 クライアントで [Microsoft Edge レガシ](/microsoft-edge/deploy/) Web ブラウザーを使用しているお客様は、Configuration Manager コンプライアンス ポリシーを作成してブラウザー設定を構成します。

このポリシーは、Windows 10 バージョン 1703 以降、および Microsoft Edge レガシ バージョン 45 以前のクライアントにのみ適用されます。 <!--511552-->

Microsoft Edge バージョン 77 以降を Configuration Manager で管理する方法の詳細については、「[Microsoft Edge バージョン 77 以降の展開](../../apps/deploy-use/deploy-edge.md)」を参照してください。 Microsoft Edge バージョン 77 以降のポリシーの構成の詳細については、「[Microsoft Edge - ポリシー](/DeployEdge/microsoft-edge-policies)」を参照してください。

## <a name="policy-settings"></a>ポリシー設定

現在、このポリシーには次の設定が含まれます。

- **[Set Microsoft Edge browser as default]\(Microsoft Edge ブラウザーを既定として設定する\)** : Windows 10 既定アプリの設定で、Web ブラウザーを Microsoft Edge に構成します

- **[アドレス バーのドロップダウンを許可する]** :Windows 10 バージョン 1703 以降が必要です。 詳細については、[AllowAddressBarDropdown ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)に関する説明を参照してください。

- **Microsoft のブラウザー間でお気に入りの同期を許可する**:Windows 10 バージョン 1703 以降が必要です。 詳細については、[SyncFavoritesBetweenIEAndMicrosoftEdge ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)に関する説明を参照してください。

- **終了時に閲覧データをクリアすることを許可する**:Windows 10 バージョン 1703 以降が必要です。 詳細については、[ClearBrowsingDataOnExit ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)に関する説明を参照してください。

- **トラッキング拒否ヘッダーを許可する**:詳細については、[AllowDoNotTrack ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)に関する記事を参照してください。

- **オートコンプリートを使用する**:詳細については、[AllowAutofill ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)に関する記事を参照してください。

- **Cookie を使用する**:詳細については、[AllowCookies ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)に関する記事を参照してください。

- **ポップアップ ブロックを許可する**:詳細については、[AllowPopups ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)に関する記事を参照してください。

- **アドレス バーで検索候補を許可する**:詳細については、[AllowSearchSuggestionsinAddressBar ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)に関する記事を参照してください。

- **Internet Explorer へのイントラネット トラフィックの送信を許可する**:詳細については、[SendIntranetTraffictoInternetExplorer ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)に関する記事を参照してください。

- **Password Manager を許可する**:詳細については、[AllowPasswordManager ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)に関する記事を参照してください。

- **開発者ツールを許可する**:詳細については、[AllowDeveloperTools ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)に関する記事を参照してください。

- **拡張機能を許可する**:詳細については、[AllowExtensions ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)に関する記事を参照してください。

> [!TIP]
> グループ ポリシーを使用してこれらおよびその他の設定を構成する方法の詳細については、「[Microsoft Edge レガシ グループ ポリシー](/microsoft-edge/deploy/group-policies/)」を参照してください。

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Microsoft Edge レガシ用に Windows Defender SmartScreen 設定を構成する
<!--1353701-->
このポリシーにより [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) に 3 つの設定が追加されます。 ポリシーには、 **[SmartScreen の設定]** ページの次の追加設定が含まれるようになりました。

- **SmartScreen を許可する**:Windows Defender SmartScreen を許可するかどうかを指定します。 詳細については、[AllowSmartScreen ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)に関するページを参照してください。

- **サイトの SmartScreen プロンプトをユーザーがオーバーライドできる**:悪意のある可能性がある Web サイトに関する Windows Defender SmartScreen フィルターの警告をユーザーがオーバーライドできるかどうかを指定します。 詳細については、[PreventSmartScreenPromptOverride ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)に関するページを参照してください。

- **ファイルの SmartScreen プロンプトをユーザーがオーバーライドできる**:確認されていないファイルのダウンロードに関する Windows Defender SmartScreen フィルターの警告をユーザーがオーバーライドできるかどうかを指定します。 詳細については、[PreventSmartScreenPromptOverrideForFiles ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)に関するページを参照してください。

## <a name="create-the-browser-profile"></a>ブラウザー プロファイルを作成する

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。 **[コンプライアンス設定]** を展開し、 **[Microsoft Edge ブラウザーのプロファイル]** ノードを選びます。 リボンで、 **[Microsoft Edge のプロファイルを作成する]** を選択します。

2. ポリシーの **[名前]** を指定し、必要に応じて **[説明]** を入力してから、 **[次へ]** を選択します。

3. **[全般設定]** ページで、このポリシーに含める設定の値を **[構成済み]** に変更します。 ウィザードを続行するには、設定を必ず **[Edge ブラウザーを既定として設定する]** に構成します。

4. **[SmartScreen の設定]** ページで設定を構成します。

5. **[サポートされているプラットフォーム]** ページで、このポリシーを適用する OS のバージョンとアーキテクチャを選択します。

6. ウィザードを完了します。

## <a name="deploy-the-policy"></a>ポリシーを展開する

1. ポリシーを選択し、リボンで **[展開]** を選択します。

2. **[参照]** を使用して、ポリシーを展開するユーザー コレクションまたはデバイス コレクションを選択します。

3. 必要に応じて、追加のオプションを選びます。

    1. ポリシーに準拠していない場合は、アラートを生成します。

    2. クライアントがこのポリシーについてデバイスのコンプライアンスを評価するスケジュールを設定します。

4. **[OK]** を選択して展開を作成します。

## <a name="next-steps"></a>次のステップ

他のコンプライアンス設定ポリシーと同様に、クライアントは指定されたスケジュールで設定を修復します。 Configuration Manager コンソールで、[デバイスのコンプライアンス対応を監視およびレポート](monitor-compliance-settings.md)します。