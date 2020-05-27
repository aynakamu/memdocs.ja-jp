---
title: 管理対象の iOS/iPadOS デバイス用アプリ構成ポリシーを追加する
titleSuffix: Microsoft Intune
description: アプリ構成ポリシーを使用して、実行時に構成データを iOS/iPadOS アプリに提供する方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c9163693-d748-46e0-842a-d9ba113ae5a8
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65ecc658b0a63b943a1008c879ae63cfc2c4e8a1
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988736"
---
# <a name="add-app-configuration-policies-for-managed-iosipados-devices"></a>管理対象の iOS/iPadOS デバイス用アプリ構成ポリシーを追加する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Microsoft Intune のアプリ構成ポリシーを使用して、iOS/iPadOS アプリのカスタム構成設定を指定できます。 これらの構成設定では、アプリのサプライヤーの指示に基づいてアプリをカスタマイズすることができます。 これらの構成設定 (キーと値) は、アプリのサプライヤーから取得する必要があります。 アプリを構成するには、キーと値として、またはキーと値を含む XML として設定を指定します。

Microsoft Intune 管理者は、マネージド デバイス上の Microsoft Office アプリケーションにどのユーザー アカウントを追加するかを制御することができます。 許可されている組織ユーザー アカウントのみにアクセスを制限したり、登録済みデバイス上の個人アカウントをブロックしたりできます。 サポートされているアプリケーションがアプリの構成を処理し、未承認のアカウントを削除してブロックします。 構成ポリシー設定は、アプリがポリシーをチェックするとき (通常はアプリの初回実行時) に使用されます。

アプリ構成ポリシーを追加すると、アプリ構成ポリシーの割り当てを設定できます。 ポリシーの割り当てを設定するときに、ポリシーを適用するユーザーのグループを含めたり、除外したりできます。 含めるグループを選ぶとき、含める特定のグループを選ぶか、組み込みグループを選ぶことができます。 組み込みグループには、**すべてのユーザー**、**すべてのデバイス**、**すべてのユーザーとすべてのデバイス**が含まれます。 

> [!NOTE]
> Intune では、便利なように、最適化が組み込まれた **[すべてのユーザー]** グループと **[すべてのデバイス]** グループがコンソールで提供されています。 "すべてのユーザー" または "すべてのデバイス" グループを自分で作るのではなく、これらのグループを使ってすべてのユーザーおよびすべてのデバイスを対象にすることを強くお勧めします。

アプリケーション構成ポリシーの含まれるグループを選ぶと、除外される特定のグループも選べます。 詳細については、「[Microsoft Intune でのアプリ割り当ての組み込みと除外](apps-inc-exl-assignments.md)」を参照してください。

> [!TIP]
> この種類のポリシーは現在、iOS/iPadOS 8.0 以降を実行しているデバイスでのみ有効です。 次の種類のアプリ インストールをサポートします。
>
> - **アプリ ストアの管理対象 iOS アプリまたは iPadOS アプリ**
> - **iOS 用アプリ パッケージ**
>
> アプリのインストールの種類の詳細については、「[How to add an app to Microsoft Intune (Microsoft Intune にアプリを追加する方法)](apps-add.md)」を参照してください。 マネージド デバイスの .ipa アプリ パッケージにアプリ構成を組み込む方法の詳細については、[iOS 開発者向けドキュメント](https://developer.apple.com/library/archive/samplecode/sc2279/Introduction/Intro.html)の「Managed App Configuration (マネージド アプリの構成)」を参照してください。

## <a name="create-an-app-configuration-policy"></a>アプリ構成ポリシーを作成する

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[アプリ]**  >  **[アプリ構成ポリシー]**  >  **[追加]**  >  **[マネージド デバイス]** を選択します。 **[マネージド デバイス]** と **[マネージド アプリ]** のどちらかを選択できます。 詳細については、「[アプリ構成をサポートするアプリ](app-configuration-policies-overview.md#apps-that-support-app-configuration)」を参照してください。
3. **[基本]** ページで、次の詳細を設定します。
    - **名前**: Azure portal に表示されるプロファイルの名前。
    - **説明**: Azure portal に表示されるプロファイルの説明。
    - **[デバイス登録の種類]** - この設定は、 **[マネージド デバイス]** に設定されています。
4. **[プラットフォーム]** として **[iOS/iPadOS]** を選択します。
5. **[対象アプリ]** の横にある **[アプリの選択]** をクリックします。 **[関連アプリ]** ペインが表示されます。 
6. **[対象アプリ]** ペインで、構成ポリシーに関連付けるマネージド アプリを選択し、 **[OK]** をクリックします。
7. **[次へ]** をクリックして、 **[設定]** ページを表示します。
8. ドロップダウン ボックスで、 **[構成設定の形式]** を選択します。 次のいずれかの方法を選択して、構成情報を追加します。
    - **構成デザイナーを使用する**
    - **XML データを入力する**<br><br>
    構成デザイナーの使用の詳細については、「[構成デザイナーの使用](#use-configuration-designer)」を参照してください。 XML データの入力の詳細については、「[XML データを入力する](#enter-xml-data)」を参照してください。 
9. **[次へ]** をクリックして、 **[割り当て]** ページを表示します。
10. **[割り当て先]** の横のドロップダウン ボックスで、アプリ構成ポリシーの割り当て先として **[選択したグループ]** 、 **[すべてのユーザー]** 、 **[すべてのデバイス]** 、または **[All users and all devies]\(すべてのユーザーとすべてのデバイス\)** を選択します。

    ![ポリシーの割り当ての [含める] タブのスクリーンショット](./media/app-configuration-policies-use-ios/app-config-policy01.png)

11. ドロップダウン ボックスで **[すべてのユーザー]** を選択します。

    ![ポリシーの割り当ての [すべてのユーザー] ドロップダウン オプションのスクリーンショット](./media/app-configuration-policies-use-ios/app-config-policy02.png)

12. **[含めないグループを選択]** をクリックして、関連するウィンドウを表示します。

    ![ポリシーの割り当てのスクリーンショット - [含めないグループを選択] ウィンドウ](./media/app-configuration-policies-use-ios/app-config-policy03.png)

13. 除外するグループを選んで、 **[選択]** をクリックします。

    >[!NOTE]
    >グループを追加するときに、他のグループが特定の割り当て種類に既に含まれる場合は、あらかじめ選択されており、他の含める割り当て種類には変更できません。 そのため、使われているそのグループは、含まれないグループとして使えません。

14. **[次へ]** をクリックして、 **[確認と作成]** ページを表示します。
15. **[作成]** をクリックして、アプリ構成ポリシーを Intune に追加します。

## <a name="use-configuration-designer"></a>構成デザイナーの使用

Microsoft Intune には、アプリに固有の構成設定が用意されています。 Microsoft Intune に登録されているデバイスかどうかにかかわらず、アプリには構成デザイナーを使用できます。 デザイナーでは、基になる XML の作成に役立つ特定の構成キーと値を構成できます。 各値のデータ型も指定する必要があります。 これらの設定は、アプリのインストール時に自動で行われます。

### <a name="add-a-setting"></a>設定を追加する

1. 構成の各キーと値について、以下を設定します。
   - **構成キー**: 特定の設定構成を一意に識別するキー。
   - **値の型:** 構成値のデータ型。 整数型、実数型、文字列型、またはブール型があります。
   - **構成値**: 構成の値。
2. **[OK]** を選択して構成の設定を行います。

### <a name="delete-a-setting"></a>設定の削除

1. 設定の横の省略記号 ( **[...]** ) を選択します。
2. **[削除]** を選択します。

\{\{ 文字と \}\} 文字を使用できるのはトークンの種類のみであり、他の目的には使用しないでください。

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>複数 ID アプリで構成済みの組織アカウントのみを許可する 

Microsoft Intune 管理者は、マネージド デバイス上の Microsoft アプリにどのユーザー アカウントを追加するかを制御できます。 許可されている組織ユーザー アカウントのみにアクセスを制限したり、登録済みデバイス上の個人アカウントをブロックしたりできます。 iOS/iPadOS デバイスでは、次のキー/値ペアを使用します。

| **Key** | **値** |
|----|----|
| IntuneMAMAllowedAccountsOnly | <ul><li>**[有効]** : [IntuneMAMUPN](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm) キーによって定義された管理対象のユーザー アカウントのみが許可されます。</li><li>**[無効]** ( **[有効]** と大文字小文字を問わず一致しないすべての値): すべてのアカウントが許可されます。</li></ul> |
| IntuneMAMUPN | <ul><li>アプリへのサインインが許可されているアカウントの UPN。</li><li> Intune に登録されているデバイスでは、<code>{{userprincipalname}}</code> のトークンを使用して登録済みのユーザー アカウントを表すことができます。</li></ul>  |

   > [!NOTE]
   > 次のアプリでは、上記のアプリ構成が処理され、組織アカウントのみが許可されます。
   > - iOS 用 Edge (44.8.7 以降)
   > - OneDrive for iOS (10.34 以降)
   > - Outlook (iOS 2.99.0 以降用)

## <a name="enter-xml-data"></a>XML データを入力する

Intune に登録されているデバイスのアプリ構成設定を含む XML プロパティ リストを入力または貼り付けることができます。 XML プロパティ リストの形式は、構成するアプリによって異なります。 使用する正確な形式の詳細については、アプリの供給元にお問い合わせください。

Intune では XML 形式が検証されます。 ただし、Intune では XML プロパティ リスト (PList) が対象アプリで動作するかどうかは確認されません。

XML プロパティ リストの詳細情報:

- iOS Developer Library の「[Understand XML Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)」 (XML プロパティ リストの概要) を参照してください。

### <a name="example-format-for-an-app-configuration-xml-file"></a>アプリ構成 XML ファイルの形式の例

アプリ構成ファイルを作成する場合、この形式を使用して次の値を 1 つ以上指定できます。

```xml
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
  <key>aaddeviceid</key>
  <string>{{aaddeviceid}}</string>
</dict>
```

### <a name="supported-xml-plist-data-types"></a>サポートされている XML PList データ型

Intune は、プロパティ リストの次のデータ型をサポートしています。

- &lt;integer&gt;
- &lt;real&gt;
- &lt;string&gt;
- &lt;array&gt;
- &lt;dict&gt;
- &lt;true /&gt; または &lt;false /&gt;

### <a name="tokens-used-in-the-property-list"></a>プロパティ リストで使用されるトークン

また、Intune は次のトークンの種類をプロパティ リストでサポートしています。
- \{\{userprincipalname\}\} — たとえば、**John\@contoso.com**
- \{\{mail\}\} — たとえば、**John\@contoso.com**
- \{\{partialupn\}\} — たとえば、**John**
- \{\{accountid\}\} — たとえば、**fc0dc142-71d8-4b12-bbea-bae2a8514c81**
- \{\{deviceid\}\} — たとえば、**b9841cd9-9843-405f-be28-b2265c59ef97**
- \{\{userid\}\} — たとえば、**3ec2c00f-b125-4519-acf0-302ac3761822**
- \{\{username\}\} — たとえば、**John Doe**
- \{\{serialnumber\}\} — たとえば、**F4KN99ZUG5V2** (iOS/iPadOS デバイスの場合)
- \{\{serialnumberlast4digits\}\} — たとえば、**G5V2** (iOS/iPadOS デバイスの場合)
- \{\{aaddeviceid\}\} — たとえば、**ab0dc123-45d6-7e89-aabb-cde0a1234b56**

## <a name="configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices"></a>iOS と iPadOS の DEP デバイスをサポートするようにポータル サイト アプリを構成する

DEP (Apple の Device Enrollment Program) の登録には、アプリ ストア バージョンのポータル サイト アプリとの互換性はありません。 ただし、次の手順に従って、iOS/iPadOS DEP デバイスをサポートするようにポータル サイト アプリを構成できます。

1. Intune で、必要に応じて Intune ポータル サイトを追加します。そのためには、 **[Intune]**  >  **[アプリ]**  >  **[すべてのアプリ]**  >  **[追加]** に移動します。
2. **[アプリ]**  >  **[アプリ構成ポリシー]** に移動し、ポータル サイト アプリのアプリ構成ポリシーを作成します。
3. 次の XML を使用して、アプリ構成ポリシーを作成します。 アプリ構成ポリシーを作成して XML データを入力する方法について詳しくは、「[管理対象の iOS/iPadOS デバイス用アプリ構成ポリシーを追加する](app-configuration-policies-use-ios.md)」をご覧ください。

    ``` xml
    <dict>
        <key>IntuneCompanyPortalEnrollmentAfterUDA</key>
        <dict>
            <key>IntuneDeviceId</key>
            <string>{{deviceid}}</string>
            <key>UserId</key>
            <string>{{userid}}</string>
        </dict>
    </dict>
    ```

3. 目的のグループを対象としたアプリ構成ポリシーを使用して、ポータル サイトをデバイスに展開します。 ポリシーは、既に DEP に登録されているデバイスのグループにのみ展開してください。
4. ポータル サイト アプリが自動的にインストールされたらサインインするように、エンド ユーザーに指示します。

## <a name="monitor-iosipados--app-configuration-status-per-device"></a>デバイスごとに iOS/iPadOS のアプリ構成の状態を監視する 
構成ポリシーが割り当てられたら、マネージド デバイスごとに iOS/iPadOS アプリ構成の状態を監視することができます。 Azure Portal の **[Microsoft Intune]** から、 **[デバイス]**  >  **[すべてのデバイス]** の順に選びます。 マネージド デバイスの一覧から、デバイス用のウィンドウを表示する特定のデバイスを選択します。 デバイスのウィンドウで、 **[アプリの構成]** を選択します。  

## <a name="additional-information"></a>追加情報

- [iOS/iPadOS および Android 用 Outlook のアプリ構成設定の展開](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>次のステップ

アプリの[割り当て](apps-deploy.md)と[監視](apps-monitor.md)に進みます。
