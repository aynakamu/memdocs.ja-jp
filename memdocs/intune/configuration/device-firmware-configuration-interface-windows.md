---
title: Microsoft Intune で MDM ポリシーを使用して Windows の BIOS 機能を更新する - Azure | Microsoft Docs
description: デバイスのファームウェア構成インターフェイス (DFCI) プロファイルを追加して、Microsoft Intune で Windows 10 デバイスの CPU、組み込みハードウェア、ブート オプションなどの UEFI 設定を管理します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb45550f8c38237bebcc54db5531ab244ab10d84
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531521"
---
# <a name="use-device-firmware-configuration-interface-profiles-on-windows-devices-in-microsoft-intune-public-preview"></a>Microsoft Intune で Windows デバイスに対してデバイスのファームウェア構成インターフェイス プロファイルを使う (パブリック プレビュー)

Intune を使用して Autopilot デバイスを管理するときは、デバイスのファームウェア構成インターフェイス (DFCI) を使用して、デバイスの登録後に UEFI (BIOS) の設定を管理できます。 利点、シナリオ、前提条件の概要については、「[DFCI の概要](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/)」を参照してください。

管理コマンドを Intune から UEFI (Unified Extensible Firmware Interface) に渡すことが、DFCI によって [Windows で可能](https://docs.microsoft.com/windows/client-management/mdm/uefi-csp)になります。

Intune では、この機能を使用して BIOS の設定を制御します。 通常、ファームウェアは悪意のある攻撃に対して高い回復性があります。 エンド ユーザーによる BIOS の制御が制限され、侵害された状況に適しています。

たとえば、セキュリティで保護された環境で Windows 10 デバイスを使用しており、カメラを無効にしたいものとします。 ファームウェア レイヤーでカメラを無効にすることができるので、エンド ユーザーが何を行っても関係ありません。 OS を再インストールしたり、コンピューターをワイプしても、カメラが有効に戻ることはありません。 別の例としては、ユーザーが別の OS を起動したり、同じセキュリティ機能を持たない古いバージョンの Windows を起動したりできないように、ブート オプションをロックダウンします。

古いバージョンの Windows を再インストールしたり、別の OS をインストールしたり、ハード ドライブをフォーマットしたりしても、DFCI の管理をオーバーライドすることはできません。 この機能を使用すると、管理者特権の OS プロセスも含めて、マルウェアが OS プロセスと通信するのを防ぐことができます。 DFCI の信頼チェーンでは、公開キー暗号化が使用され、ローカルの UEFI (BIOS) パスワード セキュリティには依存しません。 このセキュリティ レイヤーでは、ローカル ユーザーがデバイスの UEFI (BIOS) メニューから管理された設定にアクセスするのがブロックされます。

この機能は、以下に適用されます。

- サポートされている UEFI での Windows 10 RS5 (1809) 以降

## <a name="before-you-begin"></a>始める前に

- デバイスの製造元により、製造プロセスにおいて、またはユーザーがインストールするファームウェアの更新プログラムとして、UEFI ファームウェアに DFCI が追加されている必要があります。 デバイスのベンダーと協力して、[DFCI をサポートしている製造元](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/#oems-that-support-dfci)、または DFCI を使用するために必要なファームウェアのバージョンを確認します。

- デバイスは、[Microsoft クラウド ソリューション プロバイダー (CSP) パートナー](https://partner.microsoft.com/cloud-solution-provider)によって Windows Autopilot 用に登録されているか、OEM によって直接登録されている必要があります。 

  [csv ファイルからインポートされたものなど](../enrollment/enrollment-autopilot.md#add-devices)、手動で Autopilot 用に登録されたデバイスでは、DFCI を使用できません。 仕様により、DFCI の管理には、OEM または Microsoft CSP パートナーによる Windows Autopilot への登録により、デバイスの商用購入の外部構成証明が必要です。

  デバイスが登録されると、そのシリアル番号が Windows Autopilot デバイスの一覧に表示されます。

  要件など、Autopilot の詳細については、「[Windows Autopilot を使用して Intune に Windows デバイスを登録する](../enrollment/enrollment-autopilot.md)」を参照してください。

## <a name="create-your-azure-ad-security-groups"></a>Azure AD セキュリティ グループを作成する

Autopilot Deployment プロファイルは、Azure AD セキュリティ グループに割り当てられます。 必ず、DFCI でサポートされているデバイスが含まれるグループを作成してください。 DFCI デバイスの場合、ほとんどの組織ではユーザー グループではなくデバイス グループを作成できます。 次のシナリオを考慮してください。

- 人事部門 (HR) にはさまざまな Windows デバイスがあります。 セキュリティ上の理由から、このグループ内のすべてのユーザーがデバイスのカメラを使用できないようにします。 このシナリオでは、HR セキュリティ ユーザー グループを作成し、デバイスの種類に関係なく、HR グループのユーザーにポリシーが適用されるようにすることができます。
- 製造現場には、10 台のデバイスがあります。 すべてのデバイスで、USB デバイスからデバイスを起動できないようにします。 このシナリオでは、セキュリティ デバイス グループを作成し、10 台のデバイスをグループに追加することができます。

Intune でのグループの作成について詳しくは、「[ユーザーとデバイスを整理するためのグループを追加する](../fundamentals/groups-add.md)」をご覧ください。

## <a name="create-the-profiles"></a>プロファイルを作成する

DFCI を使用するには、次のプロファイルを作成し、グループにそれを割り当てます。

### <a name="create-an-autopilot-deployment-profile"></a>Autopilot Deployment プロファイルを作成する

このプロファイルでは、新しいデバイスが設定されて事前に構成されます。 [Autopilot Deployment プロファイル](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile)に関する記事では、プロファイル作成手順の一覧が示されています。

### <a name="create-an-enrollment-state-page-profile"></a>登録ステータス ページ プロファイルを作成する

このプロファイルにより、Windows のセットアップ中にデバイスが DFCI に対して検証されて、有効になります。 このプロファイルを使用して、すべてのアプリとプロファイルがインストールされるまで、デバイスの使用をブロックすることを強くお勧めします。 [登録ステータス ページ プロファイル](../enrollment/windows-enrollment-status.md)に関する記事では、プロファイル作成手順の一覧が示されています。

### <a name="create-the-dfci-profile"></a>DFCI プロファイルを作成する

このプロファイルには、構成する DFCI の設定が含まれています。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイル]** : **[デバイスのファームウェア構成インターフェイス]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 適切なプロファイル名の例は、"**Windows: Windows デバイスで DFCI 設定を構成する**" です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** で、次の設定を構成します。

    - **[ローカル ユーザーが UEFI 設定を変更できるようにする]** : 次のようなオプションがあります。
      - **[構成されていない設定のみ]** : ローカル ユーザーは、Intune によって明示的に**有効**または**無効**に設定されているものを "*除き*"、任意の設定を変更することができます。
      - **なし**: ローカル ユーザーは、DFCI プロファイルに示されていない設定も含めて、UEFI (BIOS) のすべての設定を変更できません。

    - **[CPU と IO の仮想化]** : 次のようなオプションがあります。
        - **[未構成]** :Intune では、この設定は変更または更新されません。
        - **有効**: BIOS によって、プラットフォームの CPU と IO の仮想化機能が有効にされ、OS で使用できるようになります。 Windows の仮想化ベースのセキュリティと Device Guard のテクノロジが有効になります。
    - **[カメラ]** : 次のようなオプションがあります。
        - **[未構成]** :Intune では、この設定は変更または更新されません。
        - **有効**: UEFI (BIOS) によって直接管理されているすべての組み込みカメラが有効になります。 USB カメラのような周辺機器は影響を受けません。
        - **Disabled**:UEFI (BIOS) によって直接管理されているすべての組み込みカメラが無効になります。 USB カメラのような周辺機器は影響を受けません。
    - **[マイクおよびスピーカー]** : 次のようなオプションがあります。
        - **[未構成]** :Intune では、この設定は変更または更新されません。
        - **有効**: UEFI (BIOS) によって直接管理されているすべての組み込みのマイクとスピーカーが有効になります。 USB デバイスのような周辺機器は影響を受けません。
        - **Disabled**:UEFI (BIOS) によって直接管理されているすべての組み込みのマイクとスピーカーが無効になります。 USB デバイスのような周辺機器は影響を受けません。
    - **[無線 (Bluetooth、Wi-Fi、NFC など)]** : 次のようなオプションがあります。
        - **[未構成]** :Intune では、この設定は変更または更新されません。
        - **有効**: UEFI (BIOS) によって直接管理されているすべての組み込み無線機能が有効になります。 USB デバイスのような周辺機器は影響を受けません。
        - **Disabled**:UEFI (BIOS) によって直接管理されているすべての組み込み無線機能が無効になります。 USB デバイスのような周辺機器は影響を受けません。

        > [!WARNING]
        > **[無線]** の設定を無効にした場合、デバイスには有線ネットワーク接続が必要になります。 そうしないと、デバイスを管理できない可能性があります。

    - **[外部メディア (USB、SD) からのブート]** : 次のようなオプションがあります。
        - **[未構成]** :Intune では、この設定は変更または更新されません。
        - **有効**: UEFI (BIOS) で、ハード ドライブ以外のストレージから起動できます。
        - **Disabled**:UEFI (BIOS) で、ハード ドライブ以外のストレージから起動できません。
    - **[ネットワーク アダプターからのブート]** : 次のようなオプションがあります。
        - **[未構成]** :Intune では、この設定は変更または更新されません。
        - **有効**: UEFI (BIOS) で、組み込みネットワーク インターフェイスから起動できます。
        - **Disabled**:UEFI (BIOS) で、組み込みネットワーク インターフェイスから起動できません。

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはユーザー グループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

ポリシーは、次に各デバイスがチェックインするときに適用されます。

## <a name="assign-the-profiles-and-reboot"></a>プロファイルを割り当てて再起動する

必ず、DFCI デバイスが含まれる Azure AD セキュリティ グループにプロファイルを[割り当て](../configuration/device-profile-assign.md)てください。 プロファイルは、作成時または後で割り当てることができます。

デバイスで Windows Autopilot が実行されると、DFCI によって登録ステータス ページの間に再起動が強制される場合があります。 この最初の再起動により、UEFI が Intune に登録されます。 

デバイスが登録されていることを確認する場合は、デバイスをもう一度再起動することができますが、これは必須ではありません。 デバイスの製造元の指示に従って、UEFI メニューを開き、UFEI がマネージド状態になっていることを確認します。

次にデバイスが Intune と同期されたときに、Windows は DFCI 設定を受信します。 デバイスを再起動します。 この 3 回目の再起動は、UEFI が Windows から DFCI 設定を受信するために必要です。

## <a name="update-existing-dfci-settings"></a>既存の DFCI の設定を更新する

使用中のデバイスで、既存の DFCI の設定を変更することができます。 既存の DFCI プロファイルで、設定を変更し、変更を保存します。 プロファイルは既に割り当てられているため、新しい DFCI の設定は次の場合に有効になります。

1. デバイスが Intune サービスでチェックインして、プロファイルの更新を確認します。 チェックインはさまざまなタイミングで行われます。 詳細については、[デバイスがポリシー、プロファイル、またはアプリの更新を取得するタイミング](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)に関する記事を参照してください。

2. 強制的に新しい設定を適用するには、[リモート](../remote-actions/device-restart.md)またはローカルでデバイスを再起動します。

また、[チェックインするようデバイスに指示する](../remote-actions/device-sync.md)こともできます。 同期が成功したら、[再起動するように指示](../remote-actions/device-restart.md)します。

>[!NOTE]
> DFCI プロファイルを削除するか、プロファイルに割り当てられているグループからデバイスを削除しても、DFCI の設定は削除されず、UEFI (BIOS) メニューが再び有効になることもありません。 DFCI の使用を停止する場合は、既存の DFCI プロファイルを更新します。 手順の詳細については、この記事の[デバイスのインベントリからの削除](#retire)に関する説明を参照してください。

## <a name="reuse-retire-or-recover-the-device"></a>デバイスを再利用、インベントリから削除、または復旧する

### <a name="reuse"></a>再利用する

デバイスの用途を変更するために Windows をリセットする場合は、[デバイスをワイプ](../remote-actions/devices-wipe.md)します。 Autopilot デバイス レコードは**削除しない**でください。

デバイスをワイプした後、新しい DFCI と Autopilot プロファイルが割り当てられているグループにデバイスを移動します。 必ず、デバイスを再起動して Windows セットアップを再実行してください。

### <a name="retire"></a>インベントリから削除

デバイスをインベントリから削除して管理から解放する準備ができたら、終了状態で使用する UEFI (BIOS) の設定に DFCI プロファイルを更新します。 通常は、すべての設定を有効にします。 次に例を示します。

1. DFCI プロファイルを開きます ( **[デバイス]**  >  **[プロファイル]** )。
2. **[ローカル ユーザーが UEFI 設定を変更できるようにする]** を **[構成されていない設定のみ]** に変更します。
3. その他の設定はすべて、 **[未構成]** に設定します。
4. 設定を保存します。

これらの手順により、デバイスの UEFI (BIOS) メニューのロックが解除されます。 値はプロファイルと同じままになり (**有効**または**無効**)、OS の既定値には戻されません。

これで、デバイスをワイプする準備ができました。 デバイスがワイプされたら、Autopilot レコードを削除します。 レコードを削除すると、再起動してもデバイスは自動的に再登録されません。

### <a name="recover"></a>復旧する

デバイスをワイプし、UEFI (BIOS) メニューのロックを解除する前に Autopilot レコードを削除すると、メニューはロックされたままになります。 Intune では、プロファイルの更新を送信してロックを解除することはできません。

デバイスのロックを解除するには、UEFI (BIOS) メニューを開き、ネットワークから管理を更新します。 復旧によってメニューのロックが解除されますが、UEFI (BIOS) 設定はすべて、前の Intune DFCI プロファイルの値に設定されたままになります。

## <a name="end-user-impact"></a>エンド ユーザーへの影響

DFCI ポリシーが適用されると、ローカル ユーザーは、UEFI (BIOS) メニューがパスワードで保護されている場合でも、DFCI によって構成された設定を変更することはできません。 構成した設定によっては、ハードウェア コンポーネントが見つからない、または診断できないというエラーが、エンド ユーザーに表示されることがあります。 無効にされているオプションについて説明したドキュメントを、エンド ユーザーに提供してください。  

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当てた](device-profile-assign.md)後は、[その状態を監視](device-profile-monitor.md)します。
