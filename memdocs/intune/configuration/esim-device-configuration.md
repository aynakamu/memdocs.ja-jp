---
title: Microsoft Intune - Azure で eSIM データ接続を有効にする | Microsoft Docs
description: eSIM を追加または使用し、さまざまなデータ通信プランを利用してインターネットおよびデータ アクセスを行います。 Intune で、アクティブ化コードを追加またはインポートし、構成プロファイルを使用してそのアクティブ化コードを割り当てます。 eSIM プロファイルを監視し、eSIM 対応デバイスの状態を確認することもできます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17c0c83452f7b67ad2fef660e8f0c81bc6d4b78f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989135"
---
# <a name="configure-esim-cellular-profiles-in-intune-public-preview"></a>Intune で eSIM 携帯電話プロファイルを構成する (パブリック プレビュー)

eSIM は埋め込み SIM チップであり、[Surface LTE Pro](https://www.microsoft.com/surface/business/surface-pro) などの eSIM 対応デバイス上で携帯データネットワーク接続を介してインターネットに接続することができます。 eSIM を利用する場合、携帯電話会社から SIM カードを入手する必要はありません。 世界中を旅行する場合でも、携帯電話会社やデータ プランを切り替え、常に回線接続を維持できます。

たとえば、仕事用には携帯データ通信プランを、個人用には異なる携帯電話会社による別のデータ通信プランを利用できます。 旅行時には、現地で通信プランを提供している携帯電話会社を見つけて、インターネットにアクセスすることができます。

この機能は、以下に適用されます。

- Windows 10 以降

Intune では、携帯電話会社によって提供される 1 回限りのアクティブ化コードをインポートすることができます。 eSIM モジュール上で携帯データ通信プランを構成するには、そのアクティブ化コードをご利用の eSIM 対応デバイスに展開します。 Intune でアクティブ化コードがインストールされると、eSIM ハードウェア モジュールはアクティブ化コードのデータを利用して、携帯電話会社に接続します。 完了すると、eSIM プロファイルがデバイスにダウンロードされ、携帯電話のアクティブ化のために構成されます。

Intune を使ってご利用のデバイスに eSIM を展開するには、次のものが必要です。

- **eSIM 対応デバイス** (Surface LTE など): [ご利用のデバイスで eSIM がサポートされている](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data)かどうかを確認してください。 または、(この記事の) [既知の eSIM 対応デバイスがいくつか](#esim-capable-devices)示されている一覧を参照してください。
- **Windows 10 Fall creators Update PC** (1709 以降): Intune で登録され、MDM 管理されているものです。
- **アクティブ化コード**: 携帯電話会社によって提供されます。 これらの 1 回限りのアクティブ化コードは Intune に追加され、ご利用の eSIM 対応デバイスに展開されます。 eSIM アクティブ化コードを取得する場合は、携帯電話会社にお問い合わせください。

## <a name="deploy-esim-to-devices---overview"></a>eSIM をデバイスに展開する - 概要

管理者は、eSIM をデバイスに展開するために次のタスクを実行します。

1. 携帯電話会社によって提供されるアクティブ化コードをインポートする
2. eSIM 対応デバイスを含む Azure Active Directory (Azure AD) デバイス グループを作成する
3. インポートされたサブスクリプション プールに Azure AD グループを割り当てる
4. 展開を監視する

この記事ではこれらの手順を説明します。

## <a name="esim-capable-devices"></a>eSIM 対応デバイス

お使いのデバイスが eSIM をサポートしているかどうかわからない場合は、デバイスの製造元にお問い合わせください。 Windows デバイスに関しては、eSIM がサポートされているかどうかを確認できます。 詳細については、「[eSIM を使って Windows 10 PC で携帯データ ネットワーク接続を利用する](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data)」を参照してください。

## <a name="step-1-add-cellular-activation-codes"></a>手順 1:携帯電話のアクティブ化コードを追加する

携帯電話のアクティブ化コードは、コンマ区切りファイル (csv) として、携帯電話会社によって提供されます。 このファイルがある場合は、次の手順を使用して Intune に追加します。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]** 、 **[eSIM 携帯電話のプロファイル]** 、 **[追加]** の順に選択します。
3. ご利用のアクティブ化コードが含まれている CSV ファイルを選択します。
4. **[OK]** を選択して変更を保存します。

### <a name="csv-file-requirements"></a>CSV ファイルの要件

アクティブ化コードを含む csv ファイルを操作する場合は、ご自分が、あるいはご利用の携帯電話会社が次の要件に従っていることを確認してださい。

- ファイルは、csv 形式 (ファイル名.csv) である必要があります。
- ファイル構造は厳密な形式に従う必要があります。 そうしないと、インポートは失敗します。 Intune では、インポート時にファイルが確認され、エラーが見つかった場合、インポートは失敗します。
- アクティブ化コードは 1 回使用されます。 以前にインポートしたアクティブ化コードをインポートすることは、同じデバイスまたは異なるデバイスへの展開時に問題が発生する可能性があるため、お勧めしません。
- 各ファイルは単一の携帯電話会社に固有であり、すべてのアクティブ化コードは同じ料金プランに固有である必要があります。 Intune では、アクティブ化コードがターゲット デバイスにランダムに配布されます。 特定のアクティブ化コードがどのデバイスで取得されるかは保証されません。
- 最大 1000 個のアクティブ化コードを、1 つの csv ファイルでインポートすることができます。

### <a name="csv-file-example"></a>CSV ファイルの例

1. csv の最初の行と最初のセルは、SM-DP+ (Subscription Manager Data Preparation サーバー) と呼ばれる、携帯電話会社の eSIM アクティブ化サービスの URL です。 URL は、コンマなしの完全修飾ドメイン名 (FQDN) である必要があります。
2. 2 番目の行とそれ以降のすべての行は、次の 2 つの値を含む、一意の 1 回限りのアクティブ化コードです。

    1. 最初の列は一意の ICCID (SIM チップの識別子) です。
    2. 2 番目の列は、1 つのコンマのみで区切られている (末尾にコンマがない) 照合 ID です。 次の例を参照してください:

        :::image type="content" source="./media/esim-device-configuration/url-activation-code-examples.png" alt-text="携帯電話会社のアクティブ化コード サンプルの csv ファイル。":::

3. csv ファイル名は、Endpoint Manager admin center の携帯電話サブスクリプション プール名となります。 上記のイメージでは、ファイル名が `UnlimitedDataSkynet.csv` となっています。 したがって、次のように、Intune ではサブスクリプション プールに `UnlimitedDataSkynet.csv` という名前が付けられます。

    :::image type="content" source="./media/esim-device-configuration/subscription-pool-name-csv-file.png" alt-text="携帯電話サブスクリプション プールに、アクティブ化コード サンプルの csv ファイルの名前が付けられている。":::

## <a name="step-2-create-an-azure-ad-device-group"></a>手順 2:Azure AD デバイス グループを作成する

eSIM 対応デバイスを含むデバイス グループを作成します。 手順については、「[グループの追加](../fundamentals/groups-add.md)」を参照してください。

> [!NOTE]
> - デバイスのみがターゲットとなり、ユーザーはターゲットになりません。
> - ご利用の eSIM デバイスを含む静的な Azure AD デバイス グループを作成することをお勧めします。 グループを使用すれば、確実に eSIM デバイスのみがターゲットとなります。

## <a name="step-3-assign-esim-activation-codes-to-devices"></a>手順 3:eSIM アクティブ化コードをデバイスに割り当てる

ご利用の eSIM デバイスを含む Azure AD グループにプロファイルを割り当てます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]** 、 **[eSIM 携帯電話のプロファイル]** の順に選択します。
3. プロファイルの一覧で、割り当てる eSIM 携帯電話サブスクリプション プールを選び、 **[割り当て]** を選択します。
4. グループを**含める**か**除外する**かを選んでから、グループを選択します。

    :::image type="content" source="./media/esim-device-configuration/include-exclude-groups.png" alt-text="Microsoft Intune でプロファイルを割り当てるデバイス グループを含める。":::

5. グループを選択するときに、Azure AD グループを選択します。 風数のグループを選択するには、**Ctrl** キーを使用してグループを選びます。
6. 完了したら、変更内容を**保存**します。

eSIM アクティブ化コードは一度使用されます。 Intune によってデバイスにアクティブ化コードがインストールされた後、eSIM モジュールは携帯電話プロファイルをダウンロードするために携帯電話会社に接続します。 この接続により、携帯電話会社ネットワークへのデバイスの登録が完了します。

## <a name="step-4-monitor-deployment"></a>手順 4:展開を監視する

### <a name="review-the-deployment-status"></a>展開状態を確認する

プロファイルを割り当てた後、サブスクリプション プールの展開状態を監視することができます。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]** 、 **[eSIM 携帯電話のプロファイル]** の順に選択します。 既存の eSIM 携帯電話サブスクリプション プールがすべて一覧表示されます。
3. サブスクリプションを選択して、 **[展開状態]** を確認します。

### <a name="check-the-profile-status"></a>プロファイルの状態を確認する

デバイス プロファイルを作成すると、Intune でグラフィカルなチャートが提供されるようになります。 これらのチャートには、プロファイルがデバイスに正常に割り当てられていることや、プロファイルが競合を示しているかどうかなど、プロファイルの状態が表示されます。

1. **[デバイス]** 、 **[eSIM 携帯電話のプロファイル]** の順に選択し、既存のサブスクリプションを選択します。
2. **[概要]** タブでは、上のグラフィカル チャートに、特定の eSIM 携帯電話サブスクリプション プールの展開に割り当てられたデバイスの数が表示されます。

    また、同じデバイス プロファイルが割り当てられている他のプラットフォーム用のデバイスの数も表示されます。

    Intune には、デバイスをターゲットとするアクティブ化コードに関する配信とインストールの状態が表示されます。

    - **同期されていないデバイス:** eSIM 展開ポリシーの作成以降、ターゲット デバイスは Intune に接続されていません
    - **アクティブ化の保留中**: Intune によってデバイスにアクティブ化コードがアクティブにインストールされているときの一時的な状態
    - **アクティブ**: アクティブ化コードは正常にインストールされました
    - **アクティブ化に失敗**: アクティブ化コードのインストールに失敗しました。トラブルシューティング ガイドを参照してください。

#### <a name="view-the-detailed-device-status"></a>詳細なデバイスの状態を表示する

[デバイスの状態] で表示できるデバイスの詳細な一覧を監視して、表示することができます。**

1. **[デバイス]** 、 **[eSIM 携帯電話のプロファイル]** の順に選択し、既存のサブスクリプションを選択します。
2. **[デバイスの状態]** を選択します。 Intune には、以下のデバイスに関する追加の詳細情報が表示されます。

    - **デバイス名**: ターゲットとなるデバイスの名前
    - **ユーザー**: 登録済みデバイスのユーザー
    - **ICCID**: デバイス上にインストールされたアクティブ化コード内にある、携帯電話会社によって提供される一意のコード
    - **アクティブ化の状態**: Intune に表示される、デバイスでのアクティブ化コードの配信とインストールの状態
    - **携帯電話の状態**: 携帯電話会社によって提供される状態。 携帯電話会社に連絡して、トラブルシューティングを行ってください。
    - **最後のチェックイン**: デバイスが Intune と最後に通信を行った日付

### <a name="monitor-esim-profile-details-on-the-actual-device"></a>実際のデバイスで eSIM プロファイルの詳細を監視する

1. ご利用のデバイスで、 **[設定]** を開き、 **[ネットワークとインターネット]** に移動します。
2. **[携帯電話]**  >  **[eSIM プロファイルの管理]** の順に選択します。
3. 次のように eSIM プロファイルが一覧表示されます。

    :::image type="content" source="./media/esim-device-configuration/device-settings-cellular-profiles.png" alt-text="ご利用のデバイス設定で eSIM プロファイルを表示する。":::

## <a name="remove-the-esim-profile-from-device"></a>デバイスから eSIM プロファイルを削除する

Azure AD グループからデバイスを削除すると、eSIM プロファイルも削除されます。 必ず、次の作業を行ってください。

1. eSIM デバイスの Azure AD グループを使用していることを確認します。
2. Azure AD グループに移動して、グループからデバイスを削除します。
3. 削除されたデバイスが Intune に接続したときに、更新済みポリシーが評価され、eSIM プロファイルが削除されます。

デバイスが[インベントリから削除](../remote-actions/devices-wipe.md#retire)されたとき、ユーザーによって登録解除されたとき、[リセット デバイス リモート アクション](../remote-actions/devices-wipe.md#wipe)がデバイス上で実行されたときにも、eSIM プロファイルが削除されます。

> [!NOTE]
> プロファイルを削除しても、課金が停止されない場合があります。 携帯電話会社に問い合わせて、ご利用のデバイスでの課金状態を確認してください。

## <a name="best-practices--troubleshooting"></a>ベスト プラクティスとトラブルシューティング

- csv ファイルが正しく書式設定されていることを確認してください。 ファイルに重複コード、複数の携帯電話会社、異なるデータ通信プランが含まれていないことを確認します。 各ファイルは携帯電話会社および携帯データ通信プランに固有である必要があることに注意してください。
- ターゲットとなる eSIM デバイスのみを含む、静的なデバイスの Azure AD グループを作成します。
- 展開の状態に問題がある場合は、以下を確認します。
  - **ファイル形式が正しくありません**: 「**手順 1: 携帯電話のアクティブ化コードを追加する**」 (この記事内) で、ファイルを正しく書式設定する方法について参照してください。
  - **携帯電話アクティブ化エラー、携帯電話会社に問い合わせる**: このアクティブ化コードは、ネットワーク内でアクティブ化されていない可能性があります。 または、プロファイルのダウンロードと携帯電話のアクティブ化に失敗しています。

## <a name="next-steps"></a>次のステップ

[デバイス プロファイルを構成する](device-profiles.md)
