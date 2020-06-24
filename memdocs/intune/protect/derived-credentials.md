---
title: Microsoft Intune でモバイル デバイスに派生資格情報を使用する - Azure | Microsoft Docs
description: モバイル デバイスで、Intune VPN、メール、Wi-Fi プロファイル、アプリケーション、S/MIME と暗号化の認証方法として、派生資格情報を使用します。 派生資格情報は、Special Publication 800-157 に対する NIST ガイドラインの実装です。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 5/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c244785db3071fd75c89307ce5b902a131124bc6
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531609"
---
# <a name="use-derived-credentials-in-microsoft-intune"></a>Microsoft Intune で派生資格情報を使用する

*この記事は、iOS/iPadOS、バージョン 7.0 以降を実行する Android Enterprise のフル マネージド デバイスに適用されます*

認証または暗号化と署名にスマート カードが必要な環境で、Intune を使用して、ユーザーのスマート カードから派生した証明書でモバイル デバイスをプロビジョニングできるようになりました。 この証明書は、*派生資格情報*と呼ばれます。 Intune では、[複数の派生資格情報の発行者がサポートされています](#supported-issuers)が、一度に使用できる発行者はテナントごとに 1 つだけです。

派生資格情報は、Special Publication (SP) 800-157 に含まれている Derived Personal Identity Verification (PIV) 資格情報に対する米国標準技術研究所 (NIST) ガイドラインの実装です。

**Intune の実装を使用して**:

- Intune 管理者は、サポートされている派生資格情報の発行者と連携するように自身のテナントを構成します。 派生資格情報の発行者のシステムで Intune 固有の設定を構成する必要はありません。
- Intune 管理者は、次のオブジェクトに対し、*認証方法*として**派生資格情報**を指定します。
  
  **iOS/iPadOS の場合**:
  - Wi-Fi、VPN、iOS/iPadOS ネイティブ メール アプリが含まれているメールなどの一般的なプロファイルの種類
  - アプリの認証
  - S/MIME 署名と暗号化

  **Android Enterprise のフル マネージド デバイスの場合**:
  - Wi-Fi や VPN などの一般的なプロファイルの種類
  - アプリの認証
  
- ユーザーは、コンピューターで自身のスマート カードを使用して派生資格情報を取得し、派生資格情報の発行者に対して認証を行います。 その後、発行者が、スマート カードから派生した証明書をモバイル デバイスに発行します。
- デバイスで受信された派生資格情報は、アプリまたはリソース アクセス プロファイルで派生資格情報が必要な場合に、認証および S/MIME 署名と暗号化に使用されます。

## <a name="prerequisites"></a>[前提条件]

派生資格情報を使用するようにテナントを構成する前に、次の情報を確認してください。

### <a name="supported-platforms"></a>サポートされているプラットフォーム

Intune では、次のプラットフォームで派生資格情報がサポートされます。

- iOS/iPadOS
- Android Enterprise - フル マネージド デバイス (バージョン 7.0 以降)

### <a name="supported-issuers"></a>サポートされている発行者

Intune では、テナントごとに 1 つの派生資格情報の発行者がサポートされます。 次の発行者と連携するように Intune を構成することができます。

- **DISA Purebred** (iOS のみ): https://public.cyber.mil/pki-pke/purebred/
- **Entrust Datacard**: https://www.entrustdatacard.com/
- **Intercede**: https://www.intercede.com/

さまざまな発行者の使用に関する重要な詳細については、その発行者に関するガイダンスを確認してください。 詳細については、この記事の「[派生資格情報の計画](#plan-for-derived-credentials)」を参照してください。

> [!IMPORTANT]
> テナントから派生資格情報の発行者を削除すると、その発行者によって設定された派生資格情報は機能しなくなります。
>
> この記事で後述する「[派生資格情報の発行者の変更](#change-the-derived-credential-issuer)」を参照してください。

### <a name="company-portal-app"></a>ポータル サイト アプリ

派生資格情報に登録するデバイスに Intune ポータル サイト アプリを展開する計画を立てます。 デバイス ユーザーは、ポータル サイト アプリを使用して、資格情報の登録プロセスを開始します。

- iOS デバイスの場合は、「[iOS ストア アプリを Microsoft Intune に追加する](../apps/store-apps-ios.md)」を参照してください。
- Android デバイスの場合は、「[Android ストア アプリを Microsoft Intune に追加する](../apps/store-apps-android.md)」を参照してください。

## <a name="plan-for-derived-credentials"></a>派生資格情報の計画

派生資格情報の発行者を設定する前に、次の考慮事項を理解してください。

### <a name="1-review-the-documentation-for-your-chosen-derived-credential-issuer"></a>1) 選択した派生資格情報の発行者のドキュメントを確認する

発行者を構成する前に、発行者のドキュメントを確認して、発行者のシステムが派生資格情報をデバイスに配布する方法を理解してください。

選択した発行者によっては、ユーザーがプロセスを完了するのを支援するため、登録時にスタッフが対応できるようにする必要がある場合があります。 また、現在の Intune 構成を確認して、デバイスまたはユーザーが資格情報の要求を完了するために必要なアクセスがブロックされていないことを確認します。

たとえば、準拠していないデバイスのメールへのアクセスをブロックするため、条件付きアクセスを使用している場合があります。 派生資格情報の登録プロセスの開始をメール通知を使用してユーザーに知らせる場合、ユーザーはポリシーに準拠するまでそれらの指示を受信できない可能性があります。

同様に、一部の派生資格情報要求ワークフローでは、画面上の QR コードをスキャンするためにデバイス カメラを使用する必要があります。 このコードによりそのデバイスが、ユーザーのスマート カード資格情報を持つ派生資格情報の発行者に対して発生した認証要求にリンクされます。 デバイス構成ポリシーでカメラの使用がブロックされている場合、ユーザーは派生資格情報の登録要求を完了できません。

**一般情報**:

- 一度に構成できる発行者はテナントごとに 1 つだけです。この発行者を、テナント内のすべてのユーザーとサポートされているデバイスで使用できます。

- 派生資格情報を必要とするポリシーでユーザーをターゲットにするまで、派生資格情報を登録する必要があることがユーザーに通知されません。

- 通知は、ポータル サイトのアプリ通知、メール、またはその両方を通じて行えます。 メール通知の使用を選択し、有効になっている条件付きアクセスを使用する場合、ユーザーのデバイスが準拠していないと、ユーザーがメール通知を受信できない場合があります。

### <a name="2-review-the-end-user-workflow-for-your-chosen-issuer"></a>2) 選択した発行者のエンドユーザー ワークフローを確認する

サポートされている各パートナーに関する主な考慮事項を次に示します。  この情報をよく理解しておくと、お使いの Intune のポリシーと構成によって、ユーザーとデバイスが、その発行者からの派生資格情報の登録を正常に完了することをブロックされることが確実になくなるようにすることができます。

#### <a name="disa-purebred"></a>DISA Purebred

派生資格情報で使用するデバイスのプラットフォーム固有のユーザー ワークフローを確認します。

- [iOS と iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-disa-purebred)
- [Android Enterprise のフル マネージド デバイス](https://docs.microsoft.com/mem/intune/user-help/enroll-android-device-disa-purebred)

**主な要件には次のものがあります**。

- ユーザーは、自身のスマート カードを使用して発行者に対して認証することができるコンピューターまたはキオスクにアクセスする必要があります。
- 派生資格情報に登録するデバイスに Intune ポータル サイト アプリをインストールする必要があります。
- Intune を使用して、派生資格情報に登録するデバイスに [DISA Purebred アプリを展開](#deploy-the-disa-purebred-app)します。 このアプリは Intune を使用して展開する必要があります。これにより、アプリが管理され、Intune ポータル サイト アプリで使用できるようになります。 このアプリは、派生資格情報要求を完了するためにデバイス ユーザーによって使用されます。
- DISA Purebred アプリでは、派生資格情報の登録時にアプリが DISA Purebred に確実にアクセスすることができるように、[アプリごとの VPN](../configuration/vpn-settings-configure.md) が必要です。
- デバイス ユーザーは、登録プロセス中は、ライブ エージェントで作業する必要があります。 登録時に、ユーザーが登録プロセスを進める中で、時間制限のあるワンタイム パスコードがユーザーに提供されます。
- 新しい Wi-Fi プロファイルの作成など、派生資格情報を使用するポリシーに変更が加えられると、iOS と iPadOS のユーザーにはポータル サイト アプリを開くように通知されます。
- 派生資格情報を更新する必要がある場合、ユーザーにはポータル サイト アプリを開くように通知されます。

DISA Purebred アプリの取得と構成の詳細については、この記事で後述する「[DISA Purebred アプリの展開](#deploy-the-disa-purebred-app)」を参照してください。

#### <a name="entrust-datacard"></a>Entrust Datacard

派生資格情報で使用するデバイスのプラットフォーム固有のユーザー ワークフローを確認します。

- [iOS と iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-entrust-datacard)
- [Android Enterprise のフル マネージド デバイス](../user-help/enroll-android-device-entrust-datacard.md)

**主な要件には次のものがあります**。

- ユーザーは、自身のスマート カードを使用して発行者に対して認証することができるコンピューターまたはキオスクにアクセスする必要があります。
- 派生資格情報に登録するデバイスに Intune ポータル サイト アプリをインストールする必要があります。
- デバイス カメラを使用して、認証要求をモバイル デバイスからの派生資格情報要求にリンクする QR コードをスキャンします。
- ユーザーは、ポータル サイト アプリまたは電子メールを使用して、派生資格情報を登録するように求められます。
- 新しい Wi-Fi プロファイルの作成など、派生資格情報を使用するポリシーに変更が加えられた場合:
  - **iOS と iPadOS** - ユーザーはポータル サイト アプリを開くように通知されます。
  - **Android Enterprise のフル マネージド デバイス** - ポータル サイト アプリを開く必要はありません。
- 派生資格情報を更新する必要がある場合、ユーザーにはポータル サイト アプリを開くように通知されます。

#### <a name="intercede"></a>Intercede

派生資格情報で使用するデバイスのプラットフォーム固有のユーザー ワークフローを確認します。

- [iOS と iPadOS](https://docs.microsoft.com/intune-user-help/enroll-ios-device-intercede)
- [Android Enterprise のフル マネージド デバイス](../user-help/enroll-android-device-intercede.md)

**主な要件には次のものがあります**。

- ユーザーは、自身のスマート カードを使用して発行者に対して認証することができるコンピューターまたはキオスクにアクセスする必要があります。
- 派生資格情報に登録するデバイスに Intune ポータル サイト アプリをインストールする必要があります。
- デバイス カメラを使用して、認証要求をモバイル デバイスからの派生資格情報要求にリンクする QR コードをスキャンします。
- ユーザーは、ポータル サイト アプリまたは電子メールを使用して、派生資格情報を登録するように求められます。
- 新しい Wi-Fi プロファイルの作成など、派生資格情報を使用するポリシーに変更が加えられた場合:
  - **iOS と iPadOS** - ユーザーはポータル サイト アプリを開くように通知されます。
  - **Android Enterprise のフル マネージド デバイス** - ポータル サイト アプリを開く必要はありません。
- 派生資格情報を更新する必要がある場合、ユーザーにはポータル サイト アプリを開くように通知されます。

### <a name="3-deploy-a-trusted-root-certificate-to-devices"></a>3) 信頼されたルート証明書をデバイスに展開する

ルート証明書は、派生資格情報の証明書チェーンが有効で信頼できることを確認するため、派生資格情報と共に使用されます。 ポリシーで直接参照されていない場合でも、信頼されたルート証明書は必要です。 「[Microsoft Intune でデバイスの証明書プロファイルを構成する](certificates-configure.md)」を参照してください。

### <a name="4-provide-end-user-instructions-for-how-to-get-the-derived-credential"></a>4) 派生資格情報の取得方法に関する指示をエンドユーザーに提供する

派生資格情報の登録プロセスの開始方法と、選択した発行者の派生資格情報の登録ワークフローをナビゲートするガイダンスを作成してユーザーに提供します。

ガイダンスをホストする URL を提供することをお勧めします。 テナントの派生資格情報の発行者を構成するときにこの URL を指定すると、その URL がポータル サイト アプリ内から使用できるようになります。 独自の URL を指定しない場合、Intune によって一般的な詳細へのリンクが提供されます。 これらの詳細は、すべてのシナリオに対応しているわけではなく、環境によっては正確ではない可能性があります。

### <a name="dive-idsupported-objects-5-deploy-intune-policies-that-require-derived-credentials"></a><dive id="supported-objects"> 5) 派生資格情報を必要とする Intune ポリシーをデプロイする

新しいポリシーを作成するか、既存のポリシーを編集して、派生資格情報を使用します。 派生資格情報は、次のオブジェクトに対して、他の認証方法を置き換えます。

- アプリの認証
- Wi-Fi
- VPN
- 電子メール (iOS のみ)
- S/MIME 署名と暗号化、Outlook を含む (iOS のみ)

派生資格情報を取得するプロセスの一部として使用するプロセスにアクセスするために、派生資格情報を使用する必要がないようにします。ユーザーが要求を完了できなくなる可能性があるからです。

## <a name="set-up-a-derived-credential-issuer"></a>派生資格情報の発行者の設定

派生資格情報を使用する必要があるポリシーを作成する前に、Intune コンソールで資格情報の発行者を設定します。 派生資格情報の発行者は、テナント全体の設定です。 テナントでサポートされるのは、一度に 1 つの発行者だけです。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[派生資格情報]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![コンソールでの派生資格情報の構成](./media/derived-credentials/configure-provider.png)

3. 派生資格情報の発行者ポリシーにわかりやすい**表示名**を指定します。  この名前は、デバイス ユーザーには表示されません。

4. **[派生資格情報の発行者]** には、テナントに選択した派生資格情報の発行者を選択します。
   - DISA Purebred (iOS のみ)
   - Entrust Datacard
   - Intercede  

5. **[派生資格情報のヘルプ URL]** を指定して、ユーザーが組織の派生資格情報を取得するのを支援するためのカスタムの指示がある場所へのリンクを提供します。 指示は、組織と、選択した発行者から資格情報を取得するために必要なワークフローに固有のものにする必要があります。 このリンクはポータル サイト アプリに表示され、デバイスからアクセスできる必要があります。

   独自の URL を指定しない場合、Intune によって、すべてのシナリオに対応していない、一般的な詳細へのリンクが提供されます。 この一般的なガイダンスは、環境によっては正確ではない場合があります。

6. **[通知の種類]** に 1 つ以上のオプションを選択します。 通知の種類は、次のシナリオについてユーザーに通知するために使用する方法です。

   - 発行者にデバイスを登録して新しい派生資格情報を取得する。
   - 現在の資格情報の有効期限が近づいたときに新しい派生資格情報を取得する。
   - [サポートされているオブジェクト](#supported-objects)で派生資格情報を使用する。

7. 準備ができたら、 **[保存]** を選択して、派生資格情報の発行者の構成を完了します。

構成を保存したら、 *[派生資格情報の発行者]* を除くすべてのフィールドに変更を加えることができます。  発行者を変更するには、「[派生資格情報の発行者の変更](#change-the-derived-credential-issuer)」を参照してください。

## <a name="deploy-the-disa-purebred-app"></a>DISA Purebred アプリの展開

*このセクションは、DISA Purebred を使用する場合にのみ適用されます*。

Intune の派生資格情報の発行者として **DISA Purebred** を使用するには、DISA Purebred アプリを取得し、Intune を使用してデバイスにそのアプリを展開する必要があります。 デバイス ユーザーは、自身のデバイスでアプリを使用して、DISA Purebred からの派生資格情報を要求します。

Intune を使用したアプリの展開に加えて、DISA Purebred アプリケーション用に Intune のアプリごとの VPN を構成します。

**次のタスクを実行します**。
  
1. DISA Purebred アプリケーションをダウンロードします (https:\//cyber.mil/pki-pke/purebred/)。

2. DISA Purebred アプリケーションを Intune に展開します。 

   - 「[iOS の基幹業務アプリを Microsoft Intune に追加する](../apps/lob-apps-ios.md)」を参照してください。
   - 「[Android の基幹業務アプリを Microsoft Intune に追加する](../apps/lob-apps-android.md)」を参照してください

3. DISA Purebred アプリケーション用に[アプリごとの VPN を作成](../configuration/vpn-settings-configure.md)します。

## <a name="use-derived-credentials-for-authentication-and-smime-signing-and-encryption"></a>認証および S/MIME 署名と暗号化に対する派生資格情報の使用

次のプロファイルの種類と目的に対して、**派生資格情報**を指定できます。

- [アプリケーション](#use-derived-credentials-for-app-authentication)
- 電子メール:
  - [iOS と iPadOS](../configuration/email-settings-ios.md)
  - [Android エンタープライズ](../configuration/email-settings-android-enterprise.md)
- VPN:
  - [iOS と iPadOS](../configuration/vpn-settings-ios.md)
  - [Android エンタープライズ](../configuration/vpn-settings-android-enterprise.md)
- [S/MIME 署名と暗号化](certificates-s-mime-encryption-sign.md)
- Wi-Fi:
  - [iOS と iPadOS](../configuration/wi-fi-settings-ios.md)
  - [Android エンタープライズ](../configuration/wi-fi-settings-android-enterprise.md)

  Wi-Fi プロファイルの場合、*認証方法*は、**EAP の種類**が次のいずれかの値に設定されている場合にのみ使用できます。
  - EAP – TLS
  - EAP-TTLS
  - PEAP

### <a name="use-derived-credentials-for-app-authentication"></a>アプリ認証に派生資格情報を使用する

Web サイトおよびアプリケーションに対する証明書ベースの認証には、派生資格情報を使用します。 アプリ認証用の派生資格情報を提供するには:

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次の設定を入力します。

   iOS と iPadOS の場合:
   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、**iOS デバイス プロファイル用の派生資格情報**などは適切なプロファイル名です。
   - **説明**:設定の概要および他の重要な詳細がわかる説明を入力します。
   - **[プラットフォーム]** : **[iOS/iPadOS]** を選択します。
   - **[プロファイルの種類]** : **[派生資格情報]** を選択します。

   Android Enterprise の場合:
   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、**Android Enterprise デバイス プロファイル用の派生資格情報**は適切なプロファイル名です。
   - **説明**:設定の概要および他の重要な詳細がわかる説明を入力します。
   - **[プラットフォーム]** : **[Android エンタープライズ]** を選択します。
   - **[プロファイルの種類]** : *[デバイスの所有者のみ]* で、 **[派生資格情報]** を選択します。

4. **[OK]** を選択して変更を保存します。
5. 終わったら、 **[OK]**  >  **[作成]** の順に選択して Intune プロファイルを作成します。 完了すると、プロファイルが **[デバイス - 構成プロファイル]** の一覧に表示されます。
6. 新しいプロファイルを選択し、 **[割り当て]** を選択します。 ポリシーを受け取る必要があるグループを選択します。

派生資格情報の発行者を設定するときに指定した設定に応じて、アプリまたはメールでユーザーに通知されます。 この通知は、派生資格情報ポリシーを処理できるように、ポータル サイトを起動することをユーザーに知らせます。

## <a name="renew-a-derived-credential"></a>派生資格情報の更新

派生資格情報を延長または更新することはできません。 代わりに、ユーザーは資格情報の要求ワークフローを使用して、デバイスの新しい派生資格情報を要求する必要があります。

**[通知の種類]** に 1 つ以上の方法を構成すると、現在の派生資格情報がその有効期間の 80% に達したときに、Intune によって自動的にユーザーに通知されます。 この通知は、資格情報要求プロセスを通じて新しい派生資格情報を取得するようユーザーに指示します。

デバイスで新しい派生資格情報が受信されると、派生資格情報を使用するポリシーがそのデバイスに再度展開されます。

## <a name="change-the-derived-credential-issuer"></a>派生資格情報の発行者の変更

テナント レベルでは、資格情報の発行者を変更することはできますが、テナントで一度にサポートされるのは 1 つの発行者だけです。

発行者を変更すると、ユーザーは新しい発行者から新しい派生資格情報を取得するように求められます。 これは、認証に派生資格情報を使用する前に行う必要があります。

### <a name="change-the-issuer-for-your-tenant"></a>テナントの発行者を変更する

> [!IMPORTANT]
> 発行者を削除し、同じ発行者をすぐに再構成する場合でも、その発行者からの派生資格情報を使用するようにプロファイルとデバイスを更新する必要があります。 発行者を削除する前に取得した派生資格情報は、有効ではなくなります。

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[派生資格情報]** を選択します。
3. 現在の派生資格情報の発行者を削除するには、 **[削除]** を選択します。
4. 新しい発行者を構成します。

### <a name="update-profiles-that-use-derived-credentials"></a>派生資格情報を使用するプロファイルを更新する

発行者を削除し、新しい発行者を追加したら、派生資格情報を使用する各プロファイルを編集します。 この規則は、前の発行者を復元した場合でも適用されます。 プロファイルを編集すると、更新がトリガーされます。これには、プロファイルの*説明*に対する単純な編集も含まれます。

### <a name="update-derived-credentials-on-devices"></a>デバイスで派生資格情報を更新する

発行者を削除して新しい発行者を追加したら、デバイス ユーザーは新しい派生資格情報を要求する必要があります。 この規則は、削除したのと同じ発行者を追加した場合でも適用されます。 新しい派生資格情報を要求するプロセスは、新しいデバイスを登録したり、既存の資格情報を更新したりする場合と同じです。

## <a name="next-steps"></a>次のステップ

[デバイス構成プロファイルを作成します](../configuration/device-profile-create.md)。
