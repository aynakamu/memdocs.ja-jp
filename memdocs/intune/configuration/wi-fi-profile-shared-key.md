---
title: Microsoft Intune で事前共有キーを使用して WiFi プロファイルを作成する - Azure | Microsoft Docs
description: カスタム プロファイルを使用して、事前共有キーで Wi-Fi プロファイルを作成し、Microsoft Intune で Android、Windows、EAP ベースの Wi-Fi プロファイル用のサンプルの XML コードを取得します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c6fd72a6-7dc8-48fc-9df1-db5627a51597
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: df5c33e1e8e589f430fe8265ee4762b4755f3618
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086445"
---
# <a name="use-a-custom-device-profile-to-create-a-wifi-profile-with-a-pre-shared-key-in-intune"></a>Intune でカスタム デバイス プロファイルを使用し、事前共有キーを含む WiFi プロファイルを作成する

通常、事前共有キー (PSK) は、WiFi ネットワーク、またはワイヤレス LAN のユーザーを認証するために使用されます。 Intune では、事前共有キーを使用して WiFi プロファイルを作成できます。 プロファイルを作成するには、Intune 内で**カスタム デバイス プロファイル**機能を使用します。 この記事には、EAP ベースの Wi-Fi プロファイルを作成する方法の例も含まれています。

この機能では以下をサポートします。

- Android デバイス管理者
- Android Enterprise 仕事用プロファイル
- Windows
- EAP ベースの Wi-Fi

> [!IMPORTANT]
> - Windows 10 で事前共有キーを使用すると、Intune に修復エラーが表示されます。 この場合は、Wi-Fi プロファイルがデバイスに正常に割り当てられ、プロファイルは想定どおりに動作します。
> - 事前共有キーが含まれている Wi-Fi プロファイルをエクスポートする場合は、ファイルが保護されていることを確認します。 キーはプレーン テキスト形式であるため、ユーザーはキーを保護する必要があります。

## <a name="before-you-begin"></a>始める前に

- この記事の後半に示されているように、そのネットワークに接続されているコンピューターからコードをコピーした方が簡単な場合があります。
- OMA-URI 設定をさらに追加することにより、複数のネットワークとキーを追加できます。
- iOS/iPadOS でプロファイルを設定するには、Mac ステーションで Apple Configurator を使用します。
- PSK には、64 桁の 16 進数文字列、または 8 から 63 個の印刷可能な ASCII 文字のパスフレーズが必要です。 アスタリスク (*) など、一部の文字はサポートされていません。

## <a name="create-a-custom-profile"></a>カスタム プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **名前**:ポリシーのわかりやすい名前を入力します。 後で簡単に識別できるよう、ポリシーに名前を付けます。 たとえば、「**Android デバイス管理者デバイス向けカスタム OMA-URI Wi-F プロファイル設定**」は適切なポリシー名です。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **[プラットフォーム]** :お使いのプラットフォームを選択します。
    - **[プロファイルの種類]** : **[カスタム]** を選択します。

4. **[設定]** で **[追加]** を選択します。 次のプロパティで新しい OMA-URI 設定を入力します。

    1. **名前**:OMA-URI 設定の名前を入力します。
    2. **説明**:OMA-URI 設定の説明を入力します。 この設定は省略可能ですが、推奨されます。
    3. **OMA-URI**:次のいずれかのオプションを入力します。

        - **Android の場合**: `./Vendor/MSFT/WiFi/Profile/SSID/Settings`
        - **Windows の場合**: `./Vendor/MSFT/WiFi/Profile/SSID/WlanXml`

        > [!NOTE]
        > 先頭にピリオドを必ず入力してください。

        SSID は、作成しているポリシーの SSID です。 たとえば、Wi-Fi に `Hotspot-1` という名前が付けられている場合は、「`./Vendor/MSFT/WiFi/Profile/Hotspot-1/Settings`」と入力します。

    4. **データ型**: **[文字列]** を選択します。

    5. **値**:XML コードを貼り付けます。 この記事の[例](#android-or-windows-wi-fi-profile-example)を参照してください。 ご利用のネットワーク設定に一致する値にそれぞれ更新します。 コードのコメント セクションには、一部のポインターが含まれます。

5. 完了したら、 **[OK]**  >  **[作成]** を選択して変更を保存します。

プロファイルの一覧にプロファイルが表示されます。 次に、ユーザー グループに[このプロファイルを割り当て](device-profile-assign.md)ます。 このポリシーは、ユーザー グループにのみ割り当てることができます。

次回各デバイスがチェックインするときに、ポリシーが適用され、そのデバイスに Wi-Fi プロファイルが作成されます。 これで、デバイスは自動的にネットワークに接続できるようになります。

## <a name="android-or-windows-wi-fi-profile-example"></a>Android または Windows の Wi-Fi プロファイルの例

Android または Windows の Wi-Fi プロファイルの XML コードの例は、次のとおりです。 この例は、適切な形式を表示し、詳細情報を提供するために用意されています。 これは単なる例であり、ご使用の環境に推奨される構成として意図されたものではありません。

### <a name="what-you-need-to-know"></a>知っておく必要がある情報

- `<protected>false</protected>` は **false** に設定する必要があります。 **true** に設定すると、デバイスはパスワードが暗号化されているものと見なし、暗号化の解除を試みます。その結果、接続が失敗する場合があります。

- `<hex>53534944</hex>` は、`<name><SSID of wifi profile></name>` の 16 進値に設定する必要があります。 Windows 10 デバイスで、"`x87D1FDE8 Remediation failed`" という間違ったエラーが返される場合がありますが、デバイスには引き続きプロファイルが含まれています。

- XML には `&` (アンパサンド) などの特殊文字があります。 特殊文字を使用すると、XML が期待どおりに動作しないことがあります。 

### <a name="example"></a>例

``` xml
<!--
<hex>53534944</hex> = The hexadecimal value of <name><SSID of wifi profile></name>
<Name of wifi profile> = Name of profile shown to users. It could be <name>Your Company's Network</name>.
<SSID of wifi profile> = Plain text of SSID. Does not need to be escaped. It could be <name>Your Company's Network</name>.
<nonBroadcast><true/false></nonBroadcast>
<Type of authentication> = Type of authentication used by the network, such as WPA2PSK.
<Type of encryption> = Type of encryption used by the network, such as AES.
<protected>false</protected> do not change this value, as true could cause device to expect an encrypted password and then try to decrypt it, which may result in a failed connection.
<password> = Plain text of the password to connect to the network
-->

<WLANProfile
xmlns="http://www.microsoft.com/networking/WLAN/profile/v1">
  <name><Name of wifi profile></name>
  <SSIDConfig>
    <SSID>
      <hex>53534944</hex>
 <name><SSID of wifi profile></name>
    </SSID>
    <nonBroadcast>false</nonBroadcast>
  </SSIDConfig>
  <connectionType>ESS</connectionType>
  <connectionMode>auto</connectionMode>
  <autoSwitch>false</autoSwitch>
  <MSM>
    <security>
      <authEncryption>
        <authentication><Type of authentication></authentication>
        <encryption><Type of encryption></encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <sharedKey>
        <keyType>passPhrase</keyType>
        <protected>false</protected>
        <keyMaterial>password</keyMaterial>
      </sharedKey>
      <keyIndex>0</keyIndex>
    </security>
  </MSM>
</WLANProfile>
```

### <a name="eap-based-wi-fi-profile-example"></a>EAP ベースの Wi-Fi プロファイルの例

EAP ベースの Wi-Fi プロファイルの XML コードの例は、次のとおりです。この例は、適切な形式を表示し、詳細情報を提供するために用意されています。 これは単なる例であり、ご使用の環境に推奨される構成として意図されたものではありません。


```xml
    <WLANProfile xmlns="http://www.microsoft.com/networking/WLAN/profile/v1">
      <name>testcert</name>
      <SSIDConfig>
        <SSID>
          <hex>7465737463657274</hex>
          <name>testcert</name>
        </SSID>
        <nonBroadcast>true</nonBroadcast>
      </SSIDConfig>
      <connectionType>ESS</connectionType>
      <connectionMode>auto</connectionMode>
      <autoSwitch>false</autoSwitch>
      <MSM>
        <security>
          <authEncryption>
            <authentication>WPA2</authentication>
            <encryption>AES</encryption>
            <useOneX>true</useOneX>
            <FIPSMode     xmlns="http://www.microsoft.com/networking/WLAN/profile/v2">false</FIPSMode>
          </authEncryption>
          <PMKCacheMode>disabled</PMKCacheMode>
          <OneX xmlns="http://www.microsoft.com/networking/OneX/v1">
            <cacheUserData>false</cacheUserData>
            <authMode>user</authMode>
            <EAPConfig>
              <EapHostConfig     xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
                <EapMethod>
                  <Type xmlns="http://www.microsoft.com/provisioning/EapCommon">13</Type>
                  <VendorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorId>
                  <VendorType xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorType>
                  <AuthorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</AuthorId>
                </EapMethod>
                <Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
                  <Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1">
                    <Type>13</Type>
                    <EapType xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1">
                      <CredentialsSource>
                        <CertificateStore>
                          <SimpleCertSelection>true</SimpleCertSelection>
                        </CertificateStore>
                      </CredentialsSource>
                      <ServerValidation>
                        <DisableUserPromptForServerValidation>false</DisableUserPromptForServerValidation>
                        <ServerNames></ServerNames>
                      </ServerValidation>
                      <DifferentUsername>false</DifferentUsername>
                      <PerformServerValidation xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</PerformServerValidation>
                      <AcceptServerName xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</AcceptServerName>
                      <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">
                        <FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3">
                          <AllPurposeEnabled>true</AllPurposeEnabled>
                          <CAHashList Enabled="true">
                            <IssuerHash>75 f5 06 9c a4 12 0e 9b db bc a1 d9 9d d0 f0 75 fa 3b b8 78 </IssuerHash>
                          </CAHashList>
                          <EKUMapping>
                            <EKUMap>
                              <EKUName>Client Authentication</EKUName>
                              <EKUOID>1.3.6.1.5.5.7.3.2</EKUOID>
                            </EKUMap>
                          </EKUMapping>
                          <ClientAuthEKUList Enabled="true"/>
                          <AnyPurposeEKUList Enabled="false">
                            <EKUMapInList>
                              <EKUName>Client Authentication</EKUName>
                            </EKUMapInList>
                          </AnyPurposeEKUList>
                        </FilteringInfo>
                      </TLSExtensions>
                    </EapType>
                  </Eap>
                </Config>
              </EapHostConfig>
            </EAPConfig>
          </OneX>
        </security>
      </MSM>
    </WLANProfile>
```

## <a name="create-the-xml-file-from-an-existing-wi-fi-connection"></a>既存の Wi-Fi 接続からの XML ファイルの作成

既存の Wi-Fi 接続から XML ファイルを作成することもできます。 Windows コンピューターで、次の手順を実行します。

1. エクスポートされた Wi-Fi プロファイル用のローカル フォルダー (c:\WiFi など) を作成します。
2. 管理者としてコマンド プロンプトを開きます ([`cmd`] を右クリックし、 >  **[管理者として実行]** を選択します)。
3. `netsh wlan show profiles`を実行します。 すべてのプロファイルの名前が一覧表示されます。
4. `netsh wlan export profile name="YourProfileName" folder=c:\Wifi`を実行します。 このコマンドでは、c:\Wifi 内に `Wi-Fi-YourProfileName.xml` という名前のファイルが作成されます。

    - 事前共有キーが含まれている Wi-Fi プロファイルをエクスポートする場合は、`key=clear` をコマンドに追加します。
  
        `netsh wlan export profile name="YourProfileName" key=clear folder=c:\Wifi`

        `key=clear` を指定すると、キーがプレーン テキストでエクスポートされます。プロファイルを正常に使用するにはこれが必要です。

XML ファイルを作成した後、XML 構文をコピーして OMA-URI 設定の **[データの種類]** に貼り付けます。 「[カスタム プロファイルの作成](#create-a-custom-profile)」(この記事) に、手順が示されています。

> [!TIP]
> `\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces\{guid}` にも、すべてのプロファイルが XML 形式で含まれています。

## <a name="best-practices"></a>ベスト プラクティス

- PSK で Wi-Fi プロファイルを展開する前に、デバイスがエンドポイントに直接接続できることを確認します。

- キー (パスワードまたはパスフレーズ) をローテーションで使用するときは、ダウンタイムを予想し、展開を適切に計画します。 新しい Wi-Fi プロファイルは非稼働時間中にプッシュすることを検討してください。 また、接続に影響が出る可能性をユーザーに知らせます。

- 切り替えがスムーズに行われるように、エンド ユーザーのデバイスにインターネットへの代替接続があることを確認します。 たとえば、エンド ユーザーをゲスト WiFi (または他の何らかの WiFi ネットワーク) に戻したり、セルラー接続で Intune と通信したりする必要があります。 追加の接続により、ユーザーは、企業の Wi-Fi プロファイルがデバイスで更新されたときに、ポリシーの更新を受信できます。

## <a name="next-steps"></a>次のステップ

必ず[プロファイルを割り当て](device-profile-assign.md)、その状態を[監視](device-profile-monitor.md)してください。
