---
title: Microsoft Intune 内でインポートした PFX 証明書を使用する - Azure | Microsoft Docs
description: Microsoft Intune でインポートした公開キー暗号化標準 (PKCS) 証明書を使用します。 証明書をインポートし、証明書テンプレートを構成し、Intune にインポートした PFX 証明書コネクタをインストールし、インポートした PKCS 証明書プロファイルを作成します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda; rimarram
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 13824c82b426e1efb00dce2db7c9f4a2dd5bb9ee
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990337"
---
# <a name="configure-and-use-imported-pkcs-certificates-with-intune"></a>Intune でインポートした PKCS 証明書を構成して使用する

Microsoft Intune では、インポートした公開キー ペア (PKCS) 証明書の使用がサポートされます。これは通常、電子メール プロファイルを使用した S/MIME 暗号化に使用されます。 Intune 内の特定の電子メール プロファイルでは、S/MIME 署名証明書と S/MIME 暗号化証明書を定義できる S/MIME を有効にするオプションがサポートされています。

電子メールは特定の証明書で暗号化されるため、S/MIME 暗号化は困難です。

- 暗号化を解除できるように、電子メールを暗号化した証明書の秘密キーが電子メールを読んでいるデバイス上に必要です。
- デバイス上の証明書の有効期限が切れる前に、新しい証明書をインポートして、デバイスが新しいメールの暗号化を解除できるようにする必要があります。 これらの証明書の更新はサポートされていません。
- 暗号化証明書は定期的に更新されます。つまり、古いメールを引き続き暗号化解除できるように、デバイスに過去の証明書を保持することが必要な場合があります。  

同じ証明書を複数のデバイスで使用する必要があるため、[SCEP](certificates-scep-configure.md) または [PKCS](certficates-pfx-configure.md) 証明書プロファイルをこの目的で使用することはできません。これらの証明書配信メカニズムではデバイスごとに固有の証明書が提供されるからです。

Intune で S/MIME を使用する方法について詳しくは、[S/MIME を使用した電子メールの暗号化](certificates-s-mime-encryption-sign.md)に関する記事をご覧ください。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

Intune では、次のプラットフォーム用の PFX 証明書のインポートをサポートします。

- Android - デバイス管理者
- Android Enterprise - フル マネージド
- Android Enterprise - 仕事用プロファイル
- iOS/iPadOS
- macOS
- Windows 10

## <a name="requirements"></a>要件

インポートした PKCS 証明書を Intune で使用するには、次のインフラストラクチャが必要です。

- **PFX Certificate Connector for Microsoft Intune**:

  各 Intune テナントでは、このコネクタの 1 つのインスタンスがサポートされます。 Microsoft Intune Certificate Connector のインスタンスと同じサーバー上に、このコネクタをインストールできます。

  このコネクタでは、特定のユーザーを対象にした S/MIME メールの暗号化のために Intune にインポートされる PFX ファイルに対する要求を処理します。

  このコネクタは、新しいバージョンが利用可能になったときに自動更新することができます。 更新機能を使用するには、ファイアウォールがオープンになっていることを確認し、コネクタがポート **443** 上で **autoupdate.msappproxy.net** にコンタクトできるようにする必要があります。

  詳細については、「[Microsoft Intune のネットワーク エンドポイント](../fundamentals/intune-endpoints.md)」および「[Intune のネットワーク構成の要件と帯域幅](../fundamentals/network-bandwidth-use.md)」をご覧ください。

- **Windows サーバー**:

  Windows Server を使用して、PFX Certificate Connector for Microsoft Intune をホストします。  コネクタは、Intune にインポートされる証明書の要求を処理するために使用されます。
  
  コネクタは、マネージド デバイスの詳細で説明しているポートと同じポートにアクセスする必要があります。[デバイス エンドポイント コンテンツ](https://docs.microsoft.com/intune/fundamentals/intune-endpoints#access-for-managed-devices)を参照してください。

  Intune では、*PFX Certificate Connector for Microsoft Intune* と同じサーバー上に *Microsoft Intune Certificate Connector* をインストールすることができます。

  コネクタをサポートするには、サーバーで .NET 4.6 Framework 以降を実行する必要があります。 コネクタのインストールを開始したときに .NET 4.6 Framework がインストールされていない場合は、コネクタのインストールによって自動的にインストールされます。

- **Visual Studio 2015 以上** (オプション):

  Visual Studio を使用して、Microsoft Intune に PFX 証明書をインポートするためのコマンドレットを含むヘルパー PowerShell モジュールを構築します。 ヘルパー PowerShell コマンドレットを入手するには、[GitHub の PFXImport PowerShell プロジェクト](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell)に関するページをご覧ください。

## <a name="how-it-works"></a>しくみ

Intune を使用して、**インポートした PFX 証明書**をユーザーにデプロイする場合、デバイスに加えて次の 2 つのコンポーネントが役割を果たします。

- **Intune サービス**:PFX 証明書を暗号化された状態で格納し、ユーザー デバイスへの証明書のデプロイを処理します。  証明書の秘密キーを保護するパスワードは、ハードウェア セキュリティ モジュール (HSM) または Windows 暗号化を使用してアップロード前に暗号化され、どの時点でも Intune が秘密キーにアクセスできないようにします。

- **PFX Certificate Connector for Microsoft Intune**:Intune にインポートされた PFX 証明書がデバイスによって要求されると、暗号化されたパスワード、証明書、およびデバイスの公開キーがコネクタに送信されます。  コネクタでは、オンプレミスの秘密キーを使用してパスワードが復号化され、Intune に証明書を戻す前に、デバイス キーを使用してパスワード (および iOS を使用している場合はすべての plist プロファイル) が再暗号化されます。  その後、Intune によってデバイスに証明書が配信され、デバイスではデバイスの秘密キーを使用して暗号化の解除と証明書のインストールができるようになります。

## <a name="download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune"></a>PFX Certificate Connector for Microsoft Intune のダウンロード、インストール、および構成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[証明書のコネクタ]**  >  **[追加]** の順に選択します。

   ![PFX Certificate Connector for Microsoft Intune のダウンロード](./media/certificates-imported-pfx-configure/download-imported-pfxconnector.png)

3. ガイダンスに従って、*PFX Certificate Connector for Microsoft Intune* を、コネクタをインストールしようとしているサーバーからアクセスできる場所にダウンロードします。

4. ダウンロードが完了したら、サーバーにサインインし、インストーラー (PfxCertificateConnectorBootstrapper) を実行します。  
   - 既定のインストール場所を受け入れると、コネクタは `Program Files\Microsoft Intune\PFXCertificateConnector` にインストールされます。
   - コネクタ サービスはローカル システム アカウントの下で実行されます。 インターネットにアクセスするためにプロキシが必要な場合は、ローカル サービス アカウントがサーバー上のプロキシ設定にアクセスできることを確認します。

5. インストール後、PFX Certificate Connector for Microsoft Intune によって **[登録]** タブが開かれます。 Intune への接続を有効にするには、 **[サインイン]** を選択し、Azure 全体管理者のアクセス許可または Intune 管理者のアクセス許可を持つアカウントを入力します。

   > [!WARNING]
   > 既定では、Windows Server の **[IE セキュリティ強化の構成]** が **[オン]** に設定されています。これにより、Office 365 へのサインインに関する問題が発生する可能性があります。

6. ウィンドウを閉じます。

7. Microsoft Endpoint Manager admin center で、 **[テナント管理]**  >  **[コネクタとトークン]**  >  **[証明書のコネクタ]** に戻ります。 しばらくすると、緑のチェック マークが表示され、接続状態が更新されます。 これでコネクタ サーバーは Intune と通信できます。

## <a name="import-pfx-certificates-to-intune"></a>Intune への PFX 証明書のインポート

[Microsoft Graph](https://docs.microsoft.com/graph) を使用して、ユーザーの PFX 証明書を Intune にインポートします。 [GitHub のヘルパー PFXImport PowerShell プロジェクト](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell)では、操作を簡単に行うためのコマンドレットが提供されています。

Graph を使用して独自のカスタム ソリューションを使用する場合は、[userPFXCertificate リソースの種類](https://docs.microsoft.com/graph/api/resources/intune-raimportcerts-userpfxcertificate?view=graph-rest-beta)を使用します。

### <a name="build-pfximport-powershell-project-cmdlets"></a>"PFXImport PowerShell プロジェクト" コマンドレットの構築

PowerShell コマンドレットを使用するには、Visual Studio を使用してプロジェクトをご自身でビルドします。 そのプロセスは簡単で、サーバー上で実行できますが、ワークステーション上で実行することをお勧めします。  

1. GitHub 上の [Intune-Resource-Access](https://github.com/microsoft/Intune-Resource-Access) リポジトリのルートに移動し、Git を使用してリポジトリをコンピューターにダウンロードまたは複製します。

   ![GitHub のダウンロード ボタン](./media/certificates-imported-pfx-configure/github-download.png)

2. `.\Intune-Resource-Access-develop\src\PFXImportPowershell\` に移動し、**PFXImportPS.sln** ファイルを使用してプロジェクトを Visual Studio で開きます。

3. 上部で、 **[デバッグ]** から **[リリース]** に変更します。

4. **[ビルド]** に移動し、 **[PFXImportPS のビルド]** を選択します。 しばらくすると、Visual Studio の左下に "**ビルドに成功しました**" という確認メッセージが表示されます。

   ![Visual Studio のビルド オプション](./media/certificates-imported-pfx-configure/vs-build-release.png)

5. ビルド プロセスによって、PowerShell モジュールを含む新しいフォルダーが `.\Intune-Resource-Access-develop\src\PFXImportPowershell\PFXImportPS\bin\Release` に作成されます。

   この **Release** フォルダーは次の手順で使用します。

### <a name="create-the-encryption-public-key"></a>暗号化公開キーの作成

PFX 証明書とその秘密キーを Intune にインポートします。 秘密キーを保護するパスワードは、オンプレミスに格納されている公開キーを使用して暗号化されます。 Windows 暗号化、ハードウェア セキュリティ モジュール、または別の種類の暗号化を使用して、公開キーと秘密キーのペアを生成し、格納することができます。  使用する暗号化の種類によっては、バックアップの目的で公開キーと秘密キーのペアをファイル形式でエクスポートできます。

PowerShell モジュールには、Windows 暗号化を使用してキーを作成するためのメソッドが用意されています。 他のツールを使用してキーを作成することもできます。  

#### <a name="to-create-the-encryption-key-using-windows-cryptography"></a>Windows 暗号化を使用して暗号化キーを作成するには

1. Visual Studio によって作成された *Release* フォルダーを、**PFX Certificate Connector for Microsoft Intune** をインストールしたサーバーにコピーします。 このフォルダーには、PowerShell モジュールが格納されています。

2. サーバー上で、管理者として *PowerShell* を開き、PowerShell モジュールが格納されている *Release* フォルダーに移動します。

3. モジュールをインポートするには、`Import-Module .\IntunePfxImport.psd1` を実行してモジュールをインポートします。

4. 次に、`Add-IntuneKspKey -ProviderName "Microsoft Software Key Storage Provider" -KeyName "PFXEncryptionKey"` を実行します

   > [!TIP]
   > PFX 証明書をインポートするときに、使用するプロバイダーをもう一度選択する必要があります。 **Microsoft ソフトウェア キー記憶域プロバイダー**を使用できますが、別のプロバイダーの使用もサポートされています。 キー名も例として提供されていますが、別のキー名を使用することもできます。

   ワークステーションから証明書をインポートする計画がある場合は、次のコマンドを使用してこのキーをファイルにエクスポートできます: `Export-IntunePublicKey -ProviderName "<ProviderName>" -KeyName "<KeyName>" -FilePath "<File path\Filename.PFX>"`

   インポートした PFX 証明書を正常に処理できるように、PFX Certificate Connector for Microsoft Intune をホストしているサーバーに秘密キーをインポートする必要があります。

#### <a name="to-use-a-hardware-security-module-hsm"></a>ハードウェア セキュリティ モジュール (HSM) を使用するには

ハードウェア セキュリティ モジュール (HSM) を使用して、公開キーと秘密キーのペアを生成し、格納することができます。 詳しくは、HSM プロバイダーのドキュメントをご覧ください。

### <a name="import-pfx-certificates"></a>PFX 証明書のインポート

次のプロセスでは、PFX 証明書をインポートする方法の例として、PowerShell コマンドレットを使用します。 ご自身の要件に応じて、さまざまなオプションを選択できます。

次のオプションがあります。

- 使用目的 (タグに基づいて証明書をグループ化):
  - 未割り当て
  - smimeEncryption
  - smimeSigning

- パディング スキーム:
  - oaepSha256
  - oaepSha384
  - oaepSha512

キーの作成に使用したプロバイダーに一致するキー記憶域プロバイダーを選択します。

#### <a name="to-import-the-pfx-certificate"></a>PFX 証明書をインポートするには  

1. プロバイダーのドキュメントに従って、任意の証明機関 (CA) から証明書をエクスポートします。  Microsoft Active Directory 証明書サービスの場合は、[こちらのサンプル スクリプト](https://gallery.technet.microsoft.com/Export-CMPfxCertificatesFro-d55f687b)を使用できます。

2. サーバー上で、管理者として *PowerShell* を開き、PowerShell モジュールが格納されている *Release* フォルダーに移動します。

3. モジュールをインポートするには、`Import-Module .\IntunePfxImport.psd1` を実行します

4. Intune Graph を認証するには、`Set-IntuneAuthenticationToken  -AdminUserName "<Admin-UPN>"` を実行します

   > [!NOTE]
   > 認証は Graph に対して実行されるので、AppID にアクセス許可を付与する必要があります。 このユーティリティを初めて使用する場合は、"*全体管理者*" が必要です。 PowerShell コマンドレットでは、[PowerShell Intune サンプル](https://github.com/microsoftgraph/powershell-intune-samples)で使用されるものと同じ AppID が使用されます。

5. `$SecureFilePassword = ConvertTo-SecureString -String "<PFXPassword>" -AsPlainText -Force` を実行して、インポートする各 PFX ファイルのパスワードをセキュリティで保護された文字列に変換します。

6. **UserPFXCertificate** オブジェクトを作成するには、`$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>"` を実行します

   例: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "C:\temp\userA.pfx" $SecureFilePassword "userA@contoso.com" "Microsoft Software Key Storage Provider" "PFXEncryptionKey" "smimeEncryption"`

   > [!NOTE]
   > コネクタがインストールされているサーバー以外のシステムから証明書をインポートする場合、キー ファイルのパスを含む次のコマンドを使用する必要があります: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>" "<PaddingScheme>" "<File path to public key file>"`
   >
   > *VPN* は IntendedPurpose としてサポートされていません。 


7. `Import-IntuneUserPfxCertificate -CertificateList $userPFXObject` を実行して、**UserPFXCertificate** オブジェクトを Intune にインポートします

8. 証明書がインポートされたことを確認するには、`Get-IntuneUserPfxCertificate -UserList "<UserUPN>"` を実行します

9.  ベスト プラクティスとして、AAD トークン キャッシュが有効期限切れになるまで待たずにクリーンアップするため、`Remove-IntuneAuthenticationToken` を実行することをお勧めします。

その他の使用可能なコマンドについて詳しくは、[GitHub の PFXImport PowerShell プロジェクト](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell)にある readme ファイルをご覧ください。

## <a name="create-a-pkcs-imported-certificate-profile"></a>PKCS のインポートされた証明書プロファイルを作成する

証明書を Intune にインポートしたら、 **[PKCS のインポートされた証明書]** プロファイルを作成し、それを Azure Active Directory グループに割り当てます。

> [!NOTE]
> PKCS のインポートされた証明書プロファイルの作成後は、プロファイルの **[使用目的]** と **[キー記憶域プロバイダー]** (KSP) 値は読み取り専用になり、編集できなくなります。 これらのいずれかの設定に別の値が必要な場合は、新しいプロファイルを作成して展開します。 

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に移動します。

3. 次のプロパティを入力します。
   - **[プラットフォーム]** :デバイスのプラットフォームを選択します。
   - **[プロファイル]** : **[PKCS のインポートされた証明書]** を選択します

4. **[作成]** を選択します。

5. **[Basics]\(基本\)** で次のプロパティを入力します。
   - **名前**:プロファイルのわかりやすい名前を入力します。 後で簡単に識別できるよう、プロファイルに名前を付けます。 たとえば、「*会社全体の PKCS のインポートされた証明書プロファイル*」は適切な名前です。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** で、次のプロパティを入力します。

   - **使用目的**:このプロファイルに対してインポートされた証明書の使用目的を指定します。 管理者は、証明書をさまざまな使用目的でインポートできます (S/MIME 署名、S/MIME 暗号化など)。 証明書プロファイル内で選択された使用目的によって、証明書プロファイルは適切なインポートされた証明書と対応させられます。 使用目的は、インポートした証明書をグループ化するためのタグであり、そのタグを使用してインポートされた証明書が使用目的を満たすことを保証するものではありません。  

   <!-- Not in new UI:
   - **Certificate validity period**: Unless the validity period was changed in the certificate template, this option defaults to one year.
   -->
   - **キー記憶域プロバイダー (KSP)** :Windows では、デバイス上のキーを格納する場所を選択します。

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

   **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. (*Windows 10 のみに適用*) **[適用性ルール]** で、適用性ルールを指定してこのプロファイルの割り当てを調整します。 デバイスの OS エディションまたはバージョンに基づいて、プロファイルを割り当てるかどうかを選択できます。

    詳細については、「*Microsoft Intune でのデバイス プロファイルの作成*」の「[適用性ルール](../configuration/device-profile-create.md#applicability-rules)」を参照してください。

    **[次へ]** を選択します。

12. **[確認と作成]** で、設定を確認します。 [作成] を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

## <a name="support-for-third-party-partners"></a>サードパーティ パートナーのサポート

次のパートナーからは、PFX 証明書を Intune にインポートするために使用できるサポートされた方法またはツールが提供されています。

### <a name="digicert"></a>DigiCert

DigiCert PKI プラットフォーム サービスを使用する場合は、DigiCert の **Intune S/MIME 証明書用インポート ツール**を使用して、PFX 証明書を Intune にインポートすることができます。 このツールを使用すると、この記事で既に説明した「[Intune への PFX 証明書のインポート](#import-pfx-certificates-to-intune)」の手順に従う必要がなくなります。

ツールの入手方法など、DigiCert のインポート ツールの詳細については、DigiCert のサポート技術情報の https://knowledge.digicert.com/tutorials/microsoft-intune.html を参照してください。

## <a name="next-steps"></a>次のステップ

プロファイルは作成されましたが、まだ何も行われていません。 新しいデバイス プロファイルを[割り当てます](../configuration/device-profile-assign.md)。
