---
title: Microsoft Intune のポリシーのトラブルシューティング - Azure | Microsoft Docs
description: Microsoft Intune でコンプライアンス ポリシーと構成プロファイルを使用するときの、組み込みのトラブルシューティング機能の使用方法と、一般的な問題とその解決方法について説明します
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 99fb6db6-21c5-46cd-980d-50f063ab8ab8
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3aaf2bf895082f3647f0a1ad6b9997a5e97baee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364124"
---
# <a name="troubleshoot-policies-and-profiles-and-in-intune"></a>Intune でのポリシーとプロファイルのトラブルシューティング

Microsoft Intune には、トラブルシューティング機能がいくつか組み込まれています。 これらの機能を使用して、お使いの環境でのコンプライアンス ポリシーと構成プロファイルをトラブルシューティングすることができます。

この記事では、一般的なトラブルシューティング手法の一覧を示し、発生する可能性があるいくつかの問題について説明します。

## <a name="check-tenant-status"></a>テナントの状態の確認

[テナントの状態](../fundamentals/tenant-status.md)をチェックし、サブスクリプションがアクティブであることを確認します。 また、ポリシーやプロファイルの展開に影響する可能性があるアクティブなインシデントとアドバイザリの詳細を表示することもできます。

## <a name="use-built-in-troubleshooting"></a>組み込みのトラブルシューティングを使用する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[トラブルシューティング + サポート]** を選択します。

    ![Intune で、[ヘルプとサポート] に移動し、[トラブルシューティング] を選択する](./media/troubleshoot-policies-in-microsoft-intune/help-and-support-troubleshoot.png)

2. **[ユーザーの選択]** を選択し、問題が発生しているユーザーを選択して、 **[選択]** を選択します。
3. **[Intune ライセンス]** と **[アカウントの状態]** の両方に緑のチェック マークが表示されていることを確認します。

    ![Intune でユーザーを選択し、[アカウントの状態] と [Intune ライセンス] の状態に緑のチェック マークが表示されることを確認する](./media/troubleshoot-policies-in-microsoft-intune/account-status-intune-license-show-green.png)

    **役に立つリンク**:

    - [ユーザーがデバイスを登録できるようにライセンスを割り当てる](../fundamentals/licenses-assign.md)
    - [Intune にユーザーを追加する](../fundamentals/users-add.md)

4. **[デバイス]** で、問題のあるデバイスを探します。 別の列を確認します。

    - **[管理対象]** :デバイスがコンプライアンス ポリシーまたは構成ポリシーを受け取るには、このプロパティに **[MDM]** または **[EAS/MDM]** と表示されている必要があります。

        - **[管理対象]** が **[MDM]** または **[EAS/MDM]** に設定されていない場合、そのデバイスは登録されていません。 登録されるまでは、コンプライアンス ポリシーまたは構成ポリシーを受け取りません。

        - アプリ保護ポリシー (モバイル アプリケーション管理) の場合は、デバイスが登録されている必要はありません。 詳細については、「[アプリ保護ポリシーを作成して割り当てる方法](../apps/app-protection-policies.md)」を参照してください。

    - **[Azure AD の結合の種類]** : **[ワークプレース]** または **[AzureAD]** に設定されている必要があります。
 
        - この列が **[未登録]** の場合は、登録に問題がある可能性があります。 通常、デバイスをいったん登録解除してから再登録すると、この状態は解決します。

    - **[Intune 準拠]** : **[はい]** である必要があります。 **[いいえ]** と表示される場合は、コンプライアンス ポリシーに問題があるか、またはデバイスが Intune サービスに接続されていない可能性があります。 たとえば、デバイスがオフになっていたり、ネットワークに接続していない場合があります。 最終的に、デバイスは非準拠になります (一般に 30 日後)。

        詳細については、「[Intune のデバイス コンプライアンス ポリシーの概要](../protect/device-compliance-get-started.md)」をご覧ください。

    - **[Azure AD 準拠]** : **[はい]** である必要があります。 **[いいえ]** と表示される場合は、コンプライアンス ポリシーに問題があるか、またはデバイスが Intune サービスに接続されていない可能性があります。 たとえば、デバイスがオフになっていたり、ネットワークに接続していない場合があります。 最終的に、デバイスは非準拠になります (一般に 30 日後)。

        詳細については、「[Intune のデバイス コンプライアンス ポリシーの概要](../protect/device-compliance-get-started.md)」をご覧ください。

    - **[最後のチェックイン]** :最近の日時になっている必要があります。 既定では、Intune デバイスは 8 時間ごとにチェックインされます。

        - **[最後のチェックイン]** が 24 時間以上前の場合は、デバイスに問題がある可能性があります。 チェックインできないデバイスは、Intune からポリシーを受信できません。

        - 強制的にチェックインするには:
            - Android デバイスでは、Intune ポータル サイト アプリを開き、 **[デバイス]** を選択し、一覧からデバイスを選択して、 **[デバイス設定の確認]** を選択します。
            - iOS/iPadOS デバイスでは、ポータル サイト アプリを開き、 **[デバイス]** を選択し、一覧からデバイスを選択して、 **[設定の確認]** を選択します。

        - Windows デバイスでは、 **[設定]**  >  **[アカウント]**  >  **[職場または学校にアクセスする]** を開き、アカウントまたは MDM の登録を選択して、 **[情報]**  >  **[同期]** を選択します。

    - ポリシー固有の情報を表示するデバイスを選択します。

        **[デバイスのポリシー準拠]** には、デバイスに割り当てられているコンプライアンス ポリシーの状態が表示されます。

        **[デバイスの構成]** には、デバイスに割り当てられている構成ポリシーの状態が表示されます。

        予期されるポリシーが **[デバイスのポリシー準拠]** または **[デバイスの構成]** に表示されない場合、ポリシーの対象が正しく設定されていません。 ポリシーを開き、このユーザーまたはデバイスにポリシーを割り当てます。

        **[ポリシーの状態]** :

        - **該当なし**:このポリシーは、このプラットフォームではサポートされていません。 たとえば、iOS/iPadOS のポリシーは、Android では機能しません。 Samsung KNOX のポリシーは、Windows デバイスでは機能しません。
        - **[競合]** :Intune でオーバーライドできない既存の設定がデバイス上にあります。 または、デプロイされている 2 つのポリシーで、同じ設定に異なる値が使用されています。
        - **Pending**:デバイスは、ポリシーを取得するために Intune にチェックインされていません。 または、デバイスはポリシーを受け取りましたが、Intune に状態を報告していません。
        - **[エラー]** :エラーと考えられる解決策については、「[Microsoft Intune での会社のリソースへのアクセスに関する問題のトラブルシューティング](../fundamentals/troubleshoot-company-resource-access-problems.md)」をご覧ください。

        **役に立つリンク**: 

        - [デバイス コンプライアンス ポリシーを展開する方法](../protect/device-compliance-get-started.md#ways-to-deploy-device-compliance-policies)
        - [Intune デバイスのコンプライアンス対応ポリシーの監視](../protect/compliance-policy-monitor.md)

## <a name="youre-unsure-if-a-profile-is-correctly-applied"></a>プロファイルが正しく適用されているかどうかわからない

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[すべてのデバイス]** を選択し、デバイスを選択して、 **[デバイスの構成]** を選択します。 

    すべてのデバイスで、プロファイルが一覧表示されます。 各プロファイルには **[状態]** があります。 ハードウェアと OS の制限と要件を含む、すべての割り当てられたプロファイルがまとめて考慮されると、状態が適用されます。 可能性のある状態は次のとおりです。

    - **[準拠]** :デバイスはプロファイルを受け取り、設定に準拠していることを Intune に報告しています。

    - **適用なし**:プロファイルの設定は該当しません。 たとえば、iOS/iPadOS デバイス用の電子メール設定は、Android デバイスには適用されません。

    - **Pending**:プロファイルはデバイスに送信されましたが、Intune に状態を報告していません。 たとえば、Android での暗号化では、ユーザーが暗号化を有効にする必要があるため、保留と表示される可能性があります。

**役に立つリンク**:[デバイス構成プロファイルを監視する](../configuration/device-profile-monitor.md)

> [!NOTE]
> 制限レベルが異なる 2 つのポリシーを同じデバイスまたはユーザーに適用すると、より厳しい方のポリシーが適用されます。

## <a name="policy-troubleshooting-resources"></a>ポリシーのトラブルシューティングに関するリソース

- [デバイスに適用されない iOS/iPadOS または Android ポリシーのトラブルシューティング](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-tip-Troubleshooting-iOS-or-Android-policies-not-applying/ba-p/280154) (別の Microsoft サイトを開きます)
- [Windows 10 Intune ポリシー エラーのトラブルシューティング](https://blogs.technet.microsoft.com/configmgrdogs/2018/08/09/troubleshooting-windows-10-intune-policy-failures/) (ブログを開きます)
- [Windows 10 の CSP カスタム設定のトラブルシューティング](https://support.microsoft.com/en-us/help/4055338/troubleshoot-csp-setting-windows-10-computer-intune) (別の Microsoft サイトを開きます)
- [Windows 10 グループ ポリシーと Intune MDM ポリシー](https://blogs.technet.microsoft.com/cbernier/2018/04/02/windows-10-group-policy-vs-intune-mdm-policy-who-wins/) (別の Microsoft サイトを開きます)

## <a name="alert-saving-of-access-rules-to-exchange-has-failed"></a>アラート:アクセス ルールを Exchange に保存できませんでした

**問題**:管理コンソールで "**アクセス ルールを Exchange に保存できませんでした**" というアラートを受け取ります。

[Exchange On-Premises ポリシー] ワークスペース (管理コンソール) でポリシーを作成したが、Office 365 を使用している場合は、構成されたポリシー設定が Intune によって適用されません。 アラートでポリシー ソースに注意します。 [Exchange On-Premises ポリシー] ワークスペースで、従来のルールを削除します。 従来のルールはオンプレミスの Exchange で使用する、Intune 内のグローバルの Exchange ルールであり、Office 365 に関連しないためです。 次に、Office 365 の新しいポリシーを作成します。

「[Intune のオンプレミス Exchange Connector のトラブルシューティング](../protect/troubleshoot-exchange-connector.md)」が役に立つ場合があります。

## <a name="cant-change-security-policies-for-enrolled-devices"></a>登録済みデバイスのセキュリティ ポリシーを変更できない

Windows Phone デバイスから、MDM または EAS を使用して設定されたセキュリティ ポリシーのセキュリティを一度設定した後に緩くすることはできません。 たとえば、**パスワードの最小文字数** を 8 に設定し、次に 4 に減らしてみます。 より制限の厳しいポリシーがデバイスに適用されます。

Windows 10 デバイスでは、ポリシーの割り当てを解除 (展開を停止) してもセキュリティ ポリシーが削除されない場合があります。 ポリシーを割り当てたままにして、セキュリティ設定を既定値に戻すことが必要になる場合があります。

ポリシーを安全度の低い値に変更する場合、デバイスのプラットフォームによっては、セキュリティ ポリシーをリセットしなければならない場合があります。

たとえば、Windows 8.1 で、デスクトップを右からスワイプして、 **[チャーム]** バーを開きます。 **[設定]**  >  **[コントロール パネル]**  >  **[ユーザー アカウント]** を選択します。 左側で **[セキュリティ ポリシーのリセット]** リンクを選択し、 **[ポリシーのリセット]** を選択します。

Android、iOS/iPadOS、Windows Phone 8.1 などの他のプラットフォームは、より制限の緩いポリシーを適用するために、いったんインベントリから削除し、再登録しなければならない場合があります。

[デバイス登録に関するトラブルシューティング](../enrollment/troubleshoot-device-enrollment-in-intune.md)に関するページが役に立つ場合があります。

## <a name="pcs-using-the-intune-software-client---classic-portal"></a>Intune ソフトウェア クライアントを使用している PC - クラシック ポータル

> [!NOTE]
> このセクションはクラシック ポータルに適用されます。 

### <a name="microsoft-intune-policy-related-errors-in-policyplatformlog"></a>policyplatform.log に記録される Microsoft Intune ポリシー関連エラー

Intune ソフトウェア クライアントで管理されている Windows PC では、`policyplatform.log` ファイルに記録されるポリシー エラーの原因としては、デバイスの Windows ユーザー アカウント制御 (UAC) で既定値以外が設定されていることが考えられます。 いくつかの既定値以外の UAC 設定は、Microsoft Intune クライアントのインストールやポリシーの実行に影響を与えます。

#### <a name="resolve-uac-issues"></a>UAC の問題を解決する

1. コンピューターの使用を終了します。 「[デバイスの削除](../remote-actions/devices-wipe.md)」をご覧ください。

2. クライアント ソフトウェアが削除されるまで、20 分間待ちます。

    > [!NOTE]
    > [プログラムと機能] からクライアントを削除しないでください。

3. スタート メニューで「**UAC**」と入力して、[ユーザー アカウント制御の設定] を開きます。

4. 通知のスライダーを既定の設定に移動します。

### <a name="error-cannot-obtain-the-value-from-the-computer-0x80041013"></a>エラー:コンピューター 0x80041013 から値を取得できません

ローカル システム上の時間が 5 分以上ずれている場合に発生します。 ローカル コンピューターの時間が同期されていない場合は、タイム スタンプが有効でないためセキュリティで保護されたトランザクションが失敗します。

この問題を解決するには、ローカル システム時刻をインターネットの時刻にできるだけ近く設定します。 または、ネットワーク上のドメイン コントローラーの時刻に設定します。

## <a name="next-steps"></a>次のステップ

[電子メール プロファイルの一般的な問題と解決方法](../configuration/troubleshoot-email-profiles-in-microsoft-intune.md)

[Microsoft からサポート](../fundamentals/get-support.md)を受けるか、[コミュニティ フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune)を使用します。
