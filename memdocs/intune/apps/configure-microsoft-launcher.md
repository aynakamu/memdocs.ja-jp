---
title: Intune を使用して Android Enterprise 用に Microsoft Launcher を構成する
titleSuffix: ''
description: Microsoft Launcher で Intune 構成ポリシーを使用します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0711b407b185b3a9621ff80a371bd3aaa5032ead
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407728"
---
# <a name="configure-microsoft-launcher"></a>Microsoft Launcher の構成

Android アプリケーションの Microsoft Launcher を使用すると、ユーザーは、電話を個人用に設定し、外出先でも整理された状態を保ち、携帯電話から PC に作業を転送することができます。 

Android Enterprise のフル マネージド デバイスで Launcher を使用すると、エンタープライズ IT 管理者は、壁紙、アプリ、アイコンの位置を選択して、マネージド デバイスのホーム画面をカスタマイズできます。 これにより、OEM デバイスやシステムのバージョンの違いに関係なく、すべてのマネージド Android デバイスのルック アンド フィールが標準化されます。 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>Microsoft ランチャー アプリの構成方法 

Microsoft ランチャー アプリケーションが [Intune に追加](../apps/apps-add.md)されたら、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動し、 **[アプリ]** 、 **[アプリ構成ポリシー]** の順に選択します。 **Android** が実行されている**マネージド デバイス**用の構成ポリシーを追加し、関連付けられているアプリとして **[Microsoft Launcher]** を選択します。 **[構成設定]** をクリックして、利用可能なさまざまな Microsoft Launcher 設定を構成します。 

## <a name="choosing-a-configuration-settings-format"></a>構成設定の形式を選択する 

Microsoft Launcher の構成設定を定義するのに使用できる 2 つの方法があります。 

- **構成デザイナー**は、機能のオン/オフを切り替えたり、値を設定できる使いやすい UI を使用して設定を構成することができます。 この方法では、値の型 BundleArray で無効になるいくつかの構成キーがあります。 これらの構成キーは、JSON データを入力することによってのみ構成できます。 

- **JSON データ**を使用すると、JSON スクリプトを使用してすべての可能な構成キーを定義することができます。 

**構成デザイナー**でプロパティを追加する場合、次に示す **[構成設定の形式]** ドロップダウン リストから **[JSON データを入力]** を選択することで、これらのプロパティを自動的に JSON に変換できます。

   ![構成設定の形式 - 構成デザイナーを使用する](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > プロパティを構成デザイナーで構成すると、JSON データも、それらのプロパティを反映させる目的でのみ更新されます。 JSON データに構成キーを追加するには、[JSON スクリプト例](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example)を利用し、構成キーごとに必要な行をコピーします。 

## <a name="using-configuration-designer"></a>構成デザイナーを使用する

構成デザイナーを使用すると、あらかじめ設定されている設定とそれらに関連付けられている値を選択できます。

   ![構成設定の形式 - JSON データを入力する](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

次の表に、Microsoft Launcher の使用可能な構成キー、値の型、既定値、および説明を示します。 説明では、選択した値に基づいて予想されるデバイスの動作を説明します。 構成デザイナーで無効になっている構成キーは、この表には含まれていません。

|    Configuration キー    |    値の種類    |    既定値    |    [説明]     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    登録の種類    |    文字列型     |    Default    |    このポリシーで適用する登録の種類を設定できます。 現時点では、値 **[既定値]** は **CorporateOwnedBuisnessOnly** を示します。 現在、他の登録の種類はサポートされていません。        JSON キー名: management_mode_key        |
|    Home Screen App Order User Change Allowed (ホーム画面のアプリの順序の変更をユーザーに許可する)    |    ブール型    |    True    |    エンド ユーザーが **[Home Screen App Order]\(ホーム画面のアプリの順序\)** の設定を変更できるかどうかを指定できます。<ul><li>**True** に設定した場合、ポリシーで定義されているアプリの順序は、初期展開に対してのみ適用されます。 その後は、ポリシーは適用されず、ユーザーが行った変更が尊重されます。</li><li>**False** に設定すると、すべての同期でアプリの順序が適用されます。</li></ul><br>**注:** ホーム画面のアプリの順序は、JSON エディターによってのみ構成できます。<br><br>JSON キー名:<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    グリッド サイズの設定    |    文字列型    |    自動    |    ホーム画面に配置するアプリのグリッド サイズを設定できます。 アプリの行と列の数を設定して、`columns;rows` の形式でグリッド サイズを定義することができます。 グリッド サイズを定義すると、設定した行数がホーム画面の 1 行に表示されるアプリの最大数になり、設定した列数がホーム画面の 1 列に表示されるアプリの最大数になります。<br><br>        JSON キー名:<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    Set Device Wallpaper (デバイスの壁紙を設定する)    |    文字列型    |    Null    |    壁紙として設定する画像の URL を入力して、好みの壁紙を設定することができます。<br><br>JSON キー名:<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    Set Device Wallpaper User Change Allowed (デバイスの壁紙の変更をユーザーに許可する)    |    Bool    |    True    |    エンド ユーザーが [Set Device Wallpaper]\(デバイスの壁紙の設定\) の設定を変更できるかどうかを指定できます。<ul><li>**True** に設定した場合、ポリシーの壁紙は、初期展開に対してのみ適用されます。 その後は、ポリシーは適用されず、ユーザーが行った変更が尊重されます。</li><li>**False** に設定すると、すべての同期で壁紙が適用されます。</li></ul><br>JSON キー名:<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    Feed Enable (フィードの有効化)    |    ブール型    |    True    |    ユーザーがホーム画面を右側にスワイプしたときの、デバイスでのランチャー フィードの有効化を許可します。<ul><li>**True** に設定すると、フィードが有効になります。</li><li>**False** に設定すると、フィードが無効になります。</li></ul><br>JSON キー名:<br>`com.microsoft.launcher.Feed.Enabled`    |
|    Feed Enable User Change Allowed (フィード有効化のユーザーによる変更を許可)    |    ブール型    |    True    |     エンド ユーザーが **[Feed Enable]\(フィードの有効化\)** の設定を変更できるかどうかを指定できます。<ul><li>**True** に設定した場合、フィードは初期展開に対してのみ適用されます。 その後は、ポリシーは適用されず、ユーザーが行った変更が尊重されます。</li><li>**False** に設定すると、すべての同期でフィードが適用されます。</li></ul><br>JSON キー名: `com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    検索バーの配置   |    文字列型    |    下    |  ホーム画面の**検索バーの配置**を指定できます。 <ul><li>**[最下部]** に設定した場合、検索バーはホーム画面の一番下に配置されます。</li><li>**[最上部]** に設定した場合、検索バーはホーム画面の一番上に配置されます。</li><li>**[非表示]** に設定した場合、検索バーはホーム画面から取り除かれます。</li></ul><br>JSON キー名:<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    検索バーの配置をユーザーが変更することを許可する   |    Bool    |    True    |  **[検索バーの配置]** 設定をエンド ユーザーが変更できるかどうかを指定できます。 <ul><li>**True** に設定した場合、検索バーの配置は初期展開に対してのみ適用されます。 その後は、ポリシーは適用されず、ユーザーが行った変更が尊重されます。</li><li>**False** に設定すると、すべての同期で検索バーの配置が適用されます。</li></ul><br>JSON キー名:<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`    |
|    ドック モード  |    文字列型    |    表示    | ユーザーがホーム画面を右側にスワイプしたときの、デバイスでのドックの有効化を許可します。<ul><li>**[表示]** に設定すると、ドックが有効になります。</li><li>**[非表示]** に設定すると、ホーム画面からドックが消えますが、ユーザーは必要なときに表示できます。</li><li>**[無効]** に設定すると、ドックは無効になります。</li></ul><br>JSON キー名:<br>`com.microsoft.launcher.Dock.Mode`    |
|   ドック モードをユーザーが変更することを許可する   |    文字列型    |    True    |  ドック モード設定をエンド ユーザーが変更できるかどうかを指定できます。<ul><li>**True** に設定した場合、ドック モード設定は初期展開に対してのみ適用されます。 その後は、ポリシーは適用されず、ユーザーが行った変更が尊重されます。</li><li>**False** に設定すると、すべての同期でドック モード設定が適用されます。</li></ul><br>JSON キー名:<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>JSON データの入力

次の図のように、JSON データを入力して、Microsoft Launcher で使用可能なすべての設定と、**構成デザイナー**で無効にされた設定を構成します。

   ![構成デザイナー - JSON データ](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

構成デザイナーの表 (上) に一覧表示されている構成可能な設定のリストに加え、次の表では、JSON データを使用してのみ構成できる構成キーを示します。

|    Configuration キー    |    値の種類    |    既定値    |    [説明]     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Set Allow-Listed Applications (許可リストに登録されたアプリケーションの設定)<br>JSON キー: `com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | 関連項目[許可リストに登録されたアプリケーションの設定](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    デバイス上にインストールされているアプリの中から、ホーム画面に表示するアプリのセットを定義することができます。 表示できるようにするアプリのアプリ パッケージ名を入力することで、アプリを定義できます。たとえば、`com.android.settings` と入力すると、ホーム画面上で設定にアクセスできるようになります。 このセクション内で許可リストに登録するアプリは、ホーム画面上に表示するためには、デバイス上に既にインストールされている必要があります。<p>［プロパティ］:<ul><li>**[Package]\(パッケージ\):** アプリケーション パッケージの名前</li><li>**[Class]\(クラス\):** 特定のアプリ ページに固有のアプリケーション アクティビティ。 この値が空の場合、既定のアプリ ページが使用されます。</li></ul>      |
|    Home Screen App Order (ホーム画面アプリの順序)<br>JSON キー: `com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    関連項目[ホーム画面アプリの順序](configure-microsoft-launcher.md#home-screen-app-order)      |    ホーム画面でのアプリの順序を指定できます。<p>［プロパティ］:<br><ul><li>**種類:** アプリの位置を指定する場合、サポートされる唯一の種類は `application` です。 Web リンクの位置を指定する場合、種類は `weblink` です。</li><li>**[Position]\(位置\):** これによってホーム画面上のアプリケーション アイコン スロットが指定されます。 左上の位置 1 から開始して、左から右、上から下に移動します。</li><li>**[Package]\(パッケージ\):** これは、アプリの順序を指定するときに使用されるアプリケーション パッケージ名です。</li><li>**[Class]\(クラス\):** これは、特定のアプリ ページに固有のアプリケーション アクティビティです。 この値が空の場合、既定のアプリ ページが使用されます。 このプロパティはアプリに使用されます。</li><li>**ラベル:** これは、特定のアプリ ページに固有のアプリケーション アクティビティです。 この値が空の場合、既定のアプリ ページが使用されます。 このプロパティはアプリに使用されます。</li><li>**リンク:** エンド ユーザーが Web リンク アイコンをクリックすると起動する URL。 このプロパティは Web リンクに使用されます。</li></ul>    |
|    ピン留めされた Web リンクの設定<br>JSON キー: `com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    関連項目[ピン留めされた Web リンクの設定](configure-microsoft-launcher.md#set-pinned-web-link)      |    このキーによって、Web サイトをクイック起動アイコンとしてホーム画面にピン留めすることができます。 この方法で、ユーザーは重要な Web サイトにすばやく簡単にアクセスできます。 "ホーム画面アプリの順序" 構成で各 Web リンク アイコンの場所を変更できます。<p>［プロパティ］:<br><ul><li>**• ラベル:** MS ランチャー ホーム画面に表示される Web リンク タイトル。</li><li>**リンク:** エンド ユーザーが Web リンク アイコンをクリックすると起動する URL。</li></ul>    |


### <a name="set-allow-listed-applications"></a>許可リストに登録されたアプリケーションの設定

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>ホーム画面アプリの順序

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>ピン留めされた Web リンクの設定

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Microsoft ランチャーの構成例

以下は、使用可能なすべての構成キーが含まれた JSON スクリプトの例です。

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueBool": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>次のステップ

- Android Enterprise フル マネージド デバイスの詳細については、「[Android Enterprise フル マネージド デバイスの Intune 登録を設定する](../enrollment/android-fully-managed-enroll.md)」を参照してください。
