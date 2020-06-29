---
title: Microsoft Intune で Microsoft Defender ATP を使用する - Azure | Microsoft Docs
description: Intune で Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を使用して (設定と構成も含みます)、Intune デバイスを ATP にオンボードしてから、Intune デバイス コンプライアンスを使用したデバイスの ATP リスク評価と、条件付きアクセス ポリシーを使用して、ネットワーク リソースを保護します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1141879a282219cdac72273e47c84b51df172d04
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264058"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Intune で条件付きアクセスによる Microsoft Defender ATP のコンプライアンスを強制する

Mobile Threat Defense ソリューションとして Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を Microsoft Intune と統合できます。 統合することで、セキュリティ侵害を防止し、組織内での侵害の影響を抑えることができます。 Microsoft Defender ATP は、Windows 10 以降を実行しているデバイスと Android デバイスで動作します。

正しく設定するには、以下の構成を同時に使用します。

- **Intune と Microsoft Defender ATP の間にサービス間接続を確立する**。 この接続により、Microsoft Defender ATP では、Intune で管理するサポート対象デバイスからコンピューターのリスクに関するデータを収集できるようになります。
- **デバイス構成プロファイルを使用して、デバイスを Microsoft Defender ATP にオンボードする**。 デバイスをオンボードして、Microsoft Defender ATP と通信を行い、そのリスク レベルを評価するのに役立つデータを提供するようにそれらを構成します。
- **デバイス コンプライアンス ポリシーを使用して、許可するリスクのレベルを設定する**。 リスク レベルは Microsoft Defender ATP によって報告されます。 許可されたリスク レベルを超えるデバイスは、非準拠として識別されます。
- **条件付きアクセス ポリシーを使用**して、ユーザーが非準拠のデバイスから企業リソースにアクセスできないようにする。

Intune を Microsoft Defender ATP と統合する場合、Microsoft Defender ATP の脅威と脆弱性の管理 (TVM) を利用し、[Intune を使って TVM によって識別されたエンドポイントの脆弱性を修復](atp-manage-vulnerabilities.md)できます。

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Intune で Microsoft Defender ATP を使用する例

以下の例は、これらのソリューションを連携させて組織を保護するしくみを説明するのに役立ちます。 この例では、Microsoft Defender ATP と Intune は既に統合されています。

誰かが、組織内のユーザーに、悪意のあるコードが埋め込まれた Word の添付ファイルを送信する、というイベントを考えてみましょう。

- そのユーザーは添付ファイルを開き、コンテンツを有効にします。
- 昇格された特権への攻撃が始まります。リモート コンピューターからの攻撃者は犠牲者のデバイスへの管理者権限を持ちます。
- その後、攻撃者はそのユーザーの他のデバイスにリモートでアクセスします。 このセキュリティ違反が組織全体に影響する可能性があります。

Microsoft Defender ATP は、このシナリオのようなセキュリティ イベントを解決するのに役立ちます。

- この例では、Microsoft Defender ATP によって、デバイスで異常なコードが実行され、プロセスの特権エスカレーションが発生し、悪意のあるコードが挿入され、不審なリモート シェルが発行されたことが検出されます。
- デバイスからのこのようなアクションに基づいて、Microsoft Defender ATP により[そのデバイスは危険度が高いと分類され](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity)、Microsoft Defender セキュリティ センターのポータルに疑わしいアクティビティに関する詳細なレポートが追加されます。

リスク レベルが "*中*" または "*高*" であるデバイスを非準拠として分類する Intune デバイス コンプライアンス ポリシーを使用しているため、侵害されたデバイスは非準拠として分類されます。 この分類により、条件付きアクセス ポリシーが適用されて、そのデバイスから企業リソースへのアクセスがブロックされます。

Intune ポリシーを使用して、Android 上の Microsoft Defender ATP の一部の構成を変更することもできます。 詳細については、この記事の後半の「[Android を実行するデバイスで Web 保護を構成する](#configure-web-protection-on-devices-that-run-android)」を参照してください。

## <a name="prerequisites"></a>[前提条件]

Intune で Microsoft Defender ATP を使用する場合は、以下が構成済みであり、使用できる状態であることを確認してください。

- Enterprise Mobility + Security E3 および Windows E5 (または Microsoft 365 Enterprise E5) のライセンス済みテナント
- [Intune で管理されている](../enrollment/windows-enroll.md) Windows 10 デバイスまたは Android デバイス (Azure AD にも参加している) を含む Microsoft Intune 環境
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) および Microsoft Defender セキュリティ センター (ATP ポータル) へのアクセス

> [!NOTE]
> Microsoft Defender ATP は、iOS/iPadOS および Android の Intune アプリ保護ポリシーではサポートされていません。

## <a name="enable-microsoft-defender-atp-in-intune"></a>Intune で Microsoft Defender ATP を有効にする

実行する最初の手順は、Intune と Microsoft Defender ATP の間にサービス間接続を設定することです。 これには、Microsoft Defender セキュリティ センターと Intune の両方に対する管理アクセス権が必要です。

### <a name="to-enable-microsoft-defender-atp"></a>Microsoft Defender ATP を有効にするには

Microsoft Defender ATP を有効にする必要があるのは、テナントごとに 1 回だけです。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[Microsoft Defender ATP]** の順に選択し、 **[Microsoft Defender セキュリティ センターを開く]** を選択します。

   ![選択して Microsoft Defender セキュリティ センターを開く](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. **Microsoft Defender セキュリティ センター**で次の操作を行います。
   1. **[設定]**  >  **[高度な機能]** の順に選択します。
   2. **Microsoft Intune の接続**については、次のように **[オン]** を選択します。

      ![Intune への接続を有効にする](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

   3. **[環境設定の保存]** を選択します。

4. Microsoft Endpoint Manager admin center で **[Microsoft Defender ATP]** に戻ります。 組織のニーズに応じて、 **[MDM コンプライアンスポリシー設定]** で:
   - **[バージョン 10.0.15063 以上の Windows デバイスを Microsoft Defender ATP に接続します]** を **[オン]** に設定します
   - **[バージョン 6.0.0 以上の Android デバイスを Microsoft Defender ATP に接続します]** を **[オン]** に設定します

5. **[保存]** を選択します。

> [!TIP]
> 新しいアプリケーションを Intune Mobile Threat Defense に統合し、Intune への接続を有効にすると、Intune によって Azure Active Directory 内に従来の条件付きアクセス ポリシーが作成されます。 統合する各 MTD アプリ ([Microsoft Defender ATP](advanced-threat-protection.md) や追加の [MTD パートナー](mobile-threat-defense.md#mobile-threat-defense-partners)のいずれかなど) によって、新しい従来の条件付きアクセス ポリシーが作成されます。 これらのポリシーは無視してもかまいませんが、編集、削除、または無効にすることはできません。
>
> 従来のポリシーを削除した場合は、その作成に使用された Intune への接続を削除してから、それを再設定する必要があります。 これにより、従来のポリシーが再作成されます。 MTD アプリ用の従来のポリシーを、条件付きアクセス用の新しいポリシーの種類に移行することは、サポートされていません。
>
> MTD アプリ用の従来の条件付きアクセス ポリシーは:
>
> - デバイスが Azure AD に登録され、MTD パートナーと通信する前にデバイス ID を持っていることを要求するために、Intune MTD によって使用されます。 ID は、デバイスが Intune に正常に自身の状態を報告できるようにするために必要です。
> - 他のクラウド アプリやリソースには影響しません。
> - MTD の管理を支援するために作成する条件付きアクセス ポリシーとは異なります。
> - 既定では、評価に使用する他の条件付きアクセス ポリシーとは対話しません。
>
> 従来の条件付きアクセス ポリシーを表示するには、[Azure](https://portal.azure.com/#home) で **[Azure Active Directory]**  >  **[条件付きアクセス]**  >  **[クラシック ポリシー]** の順に移動します。

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>構成プロファイルを使用して Windows デバイスをオンボードする

Windows プラットフォームでは、Intune と Microsoft Defender ATP の間にサービス間接続を確立した後、Intune のマネージド デバイスを Microsoft Defender ATP にオンボードし、そのリスク レベルに関するデータを収集して使用できるようにします。 デバイスをオンボードするには、Microsoft Defender ATP のデバイス構成プロファイルを使用します。

Microsoft Defender ATP への接続を確立したときに、Intune は Microsoft Defender ATP から Microsoft Defender ATP のオンボード構成パッケージを受け取りました。 このパッケージは、デバイス構成プロファイルを使用してデバイスに展開されます。 この構成パッケージによってデバイスが構成され、[Microsoft Defender ATP サービス](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)と通信し、ファイルのスキャン、脅威の検出、Microsoft Defender ATP へのリスクの報告が行われるようになります。 構成パッケージを使用してデバイスをオンボードした後は、再度これを行う必要はありません。 [グループ ポリシーまたは Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints) を使用して、デバイスをオンボードすることもできます。

### <a name="create-the-device-configuration-profile"></a>デバイス構成プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. **名前**と**説明**を入力します。
4. **[プラットフォーム]** では、 **[Windows 10 以降]** を選択します。
5. **[プロファイルの種類]** では、 **[Microsoft Defender ATP (Windows 10 デスクトップ)]** を選択します。
6. 次のように設定を構成します。

   - **[Microsoft Defender ATP クライアント構成パッケージの種類]** : **[Onboard]\(オンボード\)** を選択し、プロファイルに構成パッケージを追加します。 **[Offboard]** \(オフボード\) を選択し、プロファイルから構成パッケージを削除します。
  
     > [!NOTE]
     > Microsoft Defender ATP との接続を適切に確立している場合、Intune によって自動的に構成プロファイルが**オンボード**され、 **[Microsoft Defender ATP クライアント構成パッケージの種類]** 設定は使用できなくなります。
  
   - **[すべてのファイルのサンプル共有]** : **[有効にする]** では、サンプルを収集し、Microsoft Defender ATP と共有できるようになります。 たとえば、疑わしいファイルがある場合、それを Microsoft Defender ATP に送信して詳しく分析できます。 **[未構成]** では、いかなるサンプルも Microsoft Defender ATP と共有されません。
   - **[テレメトリの報告頻度を早める]** :高リスクのデバイスがある場合は、この設定を **[有効にする]** を選択し、Microsoft Defender ATP サービスに対してより頻繁にテレメトリを報告させることができます。

     これらの Microsoft Defender ATP の設定について詳しくは、[Microsoft Endpoint Configuration Manager を使用する Windows 10 コンピューターのオンボード](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm)に関する記事をご覧ください。

7. **[OK]** 、 **[作成]** の順に選択して変更内容を保存します。これで、プロファイルが作成されます。
8. Microsoft Defender ATP を使用して評価するデバイスに[デバイス構成プロファイルを割り当てます](../configuration/device-profile-assign.md)。

## <a name="onboard-android-devices"></a>Android デバイスをオンボードする
Intune と Microsoft Defender ATP の間にサービス間接続を確立した後、マネージド デバイスを Microsoft Defender ATP にオンボードし、そのリスク レベルに関するデータを収集して使用できるようにする必要があります。

エンド ユーザーと管理者の前提条件を含む、Android デバイスのオンボードの詳細な手順については、Microsoft Defender ATP ドキュメントの「[Android 用の Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android)」を参照してください。

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>デバイスのリスク レベルを設定するコンプライアンス ポリシーを作成して割り当てる

Windows デバイスと Android デバイスのどちらでも、コンプライアンス ポリシーによって、デバイスに対して許容可能と見なすリスク レベルが決まります。

コンプライアンス ポリシーの作成に慣れていない場合は、「*Microsoft Intune でコンプライアンス ポリシーを作成する*」の記事の「[ポリシーを作成する](../protect/create-compliance-policy.md#create-the-policy)」の手順を参照してください。 次の情報は、コンプライアンス ポリシーの一部として Microsoft Defender ATP を構成する場合に固有のものです。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[コンプライアンス ポリシー]**  >  **[ポリシー]**  >  **[ポリシーの作成]** を選択します。

3. **[プラットフォーム]** については、ドロップダウン ボックスを使用して、次のいずれかのオプションを選択します。
   - **Windows 10 以降**
   - **Android デバイス管理者**
   - **Android エンタープライズ**

   次に、 **[作成]** を選択し、 **[ポリシーの作成]** 構成ウィンドウを開きます。

4. 後でこのポリシーを識別するのに役立つ **[名前]** を指定します。 **[説明]** を指定することもできます。
  
5. **[コンプライアンス設定]** タブで、 **[Microsoft Defender ATP]** グループを展開し、オプションの **[デバイスは、次のマシン リスク スコア以下であることが必要]** を目的のレベルに設定します。

   脅威レベルの分類は、[Microsoft Defender ATP によって決定されます](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue)。

   - **[クリア]** :このレベルはセキュリティ上最も安全です。 デバイスには既存のいかなる脅威も存在できず、引き続き会社のリソースにアクセスできます。 いずれかの脅威が見つかった場合、デバイスは非準拠と評価されます。 (Microsoft Defender ATP ユーザーの値は *[セキュア]* です)。
   - **低**:低レベルの脅威が存在する場合にのみ、デバイスは準拠しています。 脅威レベルが中または高のデバイスは非準拠になります。
   - **中**: デバイスに存在する脅威が低または中の場合、デバイスは準拠しています。 高レベルの脅威が検出された場合は、デバイスは非準拠と判定されます。
   - **高**: 最も安全性の低いレベルであり、すべての脅威レベルが許容されます。 脅威レベルが高、中または低のデバイスは準拠していると見なされます。

6. 該当するグループへのポリシーの割り当てを含め、ポリシーの構成を完了します。

## <a name="configure-web-protection-on-devices-that-run-android"></a>Android を実行するデバイスで Web 保護を構成する

既定では、Android 用 Microsoft Defender ATP には Web 保護機能が含まれており、有効になります。 [Web 保護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview)は、Web の脅威からデバイスを保護し、フィッシング攻撃からユーザーを保護するのに役立ちます。

既定では有効になっていますが、一部の Android デバイスでこの保護を無効にする正当な理由があります。 たとえば、Microsoft Defender ATP アプリ スキャン機能のみを使用するか、Web 保護で有害な URL をスキャンするときに VPN を使用しないようにするかを選択できます。

Intune では、Web 保護機能のすべてまたは一部をオフにすることがサポートされます。 使用する方法と無効にできる機能は、Android デバイスが Intune に登録されている方法によって異なります。

- **Android デバイス管理者**: 構成プロファイルを使用して、Web 保護機能全体を無効にするか、VPN の使用のみを無効にするためにデバイスで OMA-URI のカスタム設定を指定します。 Android デバイスのカスタム設定に関する一般的な情報については、[カスタム設定](../configuration/custom-settings-android.md)に関するページを参照してください。

- **Android Enterprise 仕事用プロファイル**: アプリ構成プロファイルと "*構成デザイナー*" を使用して、Web 保護を無効にします。 この方法と登録の種類では、すべての Web 保護機能の無効化がサポートされますが、VPN の使用のみの無効化はサポートされません。 アプリ構成ポリシーに関する一般的な情報については、「[構成デザイナーを使用する](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer)」を参照してください。

デバイスで Web 保護を構成するには、次の手順を使用し、該当する構成を作成して展開します。

### <a name="disable-web-protection-for-android-device-administrator"></a>Android デバイス管理者の Web 保護を無効にする

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. 次の設定を入力します。

   - **[プラットフォーム]** : **[Android デバイス管理者]** を選択します
   - **[プロファイル]** : **[カスタム]** を選択します

   **[作成]** を選択します。

4. **[基本]** で、次の詳細を入力します。

   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、"*Microsoft Defender ATP Web 保護用の Android カスタム プロファイル*" などとします
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

5. **[構成設定]** で、 **[追加]** を選択します。

   展開する構成の設定を指定します。

   - **Web 保護を無効にする**:
     - **名前**:簡単に見つけられるように、この OMA-URI 設定の一意の名前を入力します。 たとえば、"*Microsoft Defender ATP Web 保護を無効にする*" などとします
     - **説明**:(省略可能) 設定の概要および他の重要な詳細を示す説明を入力します。
     - **OMA-URI**:「 **./Vendor/MSFT/DefenderATP/AntiPhishing**」と入力します
     - **[データ型]** :ドロップダウンを使用して、 **[整数]** を選択します
     - **値**:VPN ベースのスキャンを含め、Web 保護を無効にするには「**0**」と入力します。
       > [!NOTE]
       > Web 保護を有効にするには、「**1**」と入力します。これは、Web 保護の既定値です。

   - **Web 保護での VPN の使用のみを無効にする**:
     - **名前**:簡単に見つけられるように、この OMA-URI 設定の一意の名前を入力します。 たとえば、"*Microsoft Defender ATP Web 保護の VPN を無効にする*" などとします
     - **説明**:(省略可能) 設定の概要および他の重要な詳細を示す説明を入力します。
     - **OMA-URI**:「 **./Vendor/MSFT/DefenderATP/Vpn**」と入力します
     - **[データ型]** :ドロップダウンを使用して、 **[整数]** を選択します
     - **値**:VPN ベースのスキャンを無効にするには、「**0**」と入力します。
       > [!NOTE]
       > Web 保護を有効にするには、「**1**」と入力します。これは、Web 保護の既定値です。

   **[追加]** を選択して OMA-URI 設定の構成を保存し、 **[次へ]** を選んで続行します。

6. **[割り当て]** で、このプロファイルを受け取るグループを指定します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

7. **[確認および作成]** で、完了したら、 **[作成]** を選択します。 作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Android Enterprise 仕事用プロファイルの Web 保護を無効にする

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]** の順に選択してから、マネージド デバイスを選びます。

3. **[基本]** で、次の詳細を入力します。

   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、"*Microsoft Defender ATP Web 保護用の Android アプリ構成*" などとします。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
   - **[プラットフォーム]** : **[Android Enterprise]** を選択します
   - **[プロファイルの種類]** : **[仕事用プロファイルのみ]** を選択します
   - **対象アプリ**: **[アプリの選択]** をクリックします。

4. **[関連アプリ]** で、 **[Defender ATP]** を見つけて選択し、 **[OK]**  >  **[次へ]** の順に選びます。

5. **[設定]** で、 **[構成設定の形式]** のドロップダウンを使用し、 **[構成デザイナーを使用する]** を選択してから **[追加]** をクリックします。 JSON エディターが開きます。

6. **[Web 保護]** を見つけて選択し、 **[OK]** を選んで **[設定]** ページに戻ります。

7. **[構成値]** では、「**0**」と入力して Web 保護を無効にします。

   > [!NOTE]
   > Web 保護を有効にするには、「**1**」と入力します。これは、Web 保護の既定値です。

   **[次へ]** を選択して続行します。

8. **[割り当て]** で、このプロファイルを受け取るグループを指定します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

9. **[確認および作成]** で、完了したら、 **[作成]** を選択します。 作成したプロファイルのポリシーの種類を選択すると、新しいプロファイルが一覧に表示されます。

## <a name="create-a-conditional-access-policy"></a>条件付きアクセス ポリシーを作成する

条件付きアクセス ポリシーでは Microsoft Defender ATP からのデータを使用して、お客様が設定した脅威レベルを超えるデバイスによるリソースへのアクセスをブロックすることができます。 デバイスから企業リソース (SharePoint や Exchange Online など) へのアクセスをブロックできます。

> [!TIP]
> 条件付きアクセスは、Azure Active Directory (Azure AD) テクノロジです。 Microsoft Endpoint Manager admin center で検出される "*条件付きアクセス*" ノードは、*Azure AD* からのノードです。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[エンドポイント セキュリティ]**  >  **[条件付きアクセス]**  >  **[新しいポリシー]** の順に選択します。

3. ポリシーの**名前**を入力して、 **[ユーザーとグループ]** を選択します。 含めるオプションまたは除外するオプションを使用して、ポリシーのグループを追加し、 **[完了]** を選択します。

4. **[クラウド アプリ]** を選択し、保護するアプリを選びます。 たとえば、 **[アプリを選択]** を選び、 **[Office 365 SharePoint Online]** と **[Office 365 Exchange Online]** を選択します。

   **[完了]** を選択して変更を保存します。

5. **[条件]**  >  **[クライアント アプリ]** の順に選択して、アプリとブラウザーにポリシーを適用します。 たとえば、 **[はい]** を選択し、 **[ブラウザー]** と **[モバイル アプリとデスクトップ クライアント]** を有効にします。

   **[完了]** を選択して変更を保存します。

6. **[許可]** を選択し、デバイスのコンプライアンスに基づいて条件付きアクセスを適用します。 たとえば、 **[アクセスの許可]**  >  **[デバイスは準拠しているとしてマーク済みである必要があります]** の順に選択します。

    **[選択]** を選んで変更を保存します。

7. **[ポリシーを有効にする]** 、 **[作成]** の順に選択して変更を保存します。

## <a name="monitor-device-compliance"></a>デバイス コンプライアンスを監視する

Microsoft Defender ATP コンプライアンス ポリシーを持つデバイスの状態を監視します。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[モニター]**  >  **[ポリシー コンプライアンス]** の順に選択します。

3. 一覧から Microsoft Defender ATP ポリシーを探し、どのデバイスが準拠または非準拠なのかを確認します。

また、同じ場所から非準拠デバイスに対する "*運用*" レポートを使用することもできます。

1. **[デバイス]**  >  **[モニター]**  >  **[非準拠デバイス]** を選択します。

レポートについて詳しくは、「[Intune のレポート](../fundamentals/reports.md)」をご覧ください。

## <a name="view-onboarding-status"></a>オンボードの状態を表示する

すべての Intune マネージド デバイスのオンボード状態を確認する場合は、 **[エンドポイント セキュリティ]**  >  **[Microsoft Defender ATP]** の順に移動できます。 このページから、さらに多くのデバイスを Microsoft Defender ATP にオンボードするためのデバイス構成プロファイルの作成を開始することもできます。

## <a name="next-steps"></a>次のステップ

[Microsoft Defender ATP の条件付きアクセス](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Microsoft Defender ATP のリスク ダッシュボード](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[ATP の脆弱性の管理を使用したセキュリティ タスクを使用して、デバイスの問題を修復する](atp-manage-vulnerabilities.md)。

[デバイス コンプライアンス ポリシーの概要](device-compliance-get-started.md)
