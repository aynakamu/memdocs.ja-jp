---
title: Microsoft Managed Home Screen アプリを構成する
titleSuffix: Microsoft Intune
description: Microsoft Managed Home Screen アプリの構成方法を学習します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 865c7f03-f525-4dfa-b3a8-d088a9106502
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3bcb9d86cf413407bc1e0812be4b0c9e17d0f88d
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093221"
---
# <a name="configure-the-microsoft-managed-home-screen-app-for-android-enterprise"></a>Android Enterprise 用 Microsoft Managed Home Screen アプリを構成する

Managed Home Screen は、Intune 経由で登録され、マルチアプリ キオスク モードで実行されている企業所有の Android エンタープライズ専用デバイスで使用するためのアプリケーションです。 これらのデバイスでは、Managed Home Screen は、その上で他の承認済みのアプリを実行するためのランチャーとして機能します。 Managed Home Screen では、IT 管理者がデバイスをカスタマイズして、エンド ユーザーがアクセスできる機能を制限する機能が提供されています。 

## <a name="when-to-configure-the-microsoft-managed-home-screen-app"></a>Microsoft Managed Home Screen アプリを構成するタイミング

通常、デバイス構成から設定が使用できる場合は、ここで設定を構成します。 これにより時間が節約され、エラーを最小限にし、Intune サポート エクスペリエンスの向上が可能になります。 ただし、Managed Home Screen の設定の中には、現在、Intune コンソールの **[アプリ構成ポリシー]** ウィンドウ経由でしか利用できないものがあります。 このドキュメントを使用して、構成デザイナーまたは JSON スクリプトのいずれかを使用して、さまざまな設定を構成する方法について学習します。 

> [!NOTE]
> 現在、 **[アプリ]** と **[デバイス構成]** を使用して許可リストに登録されたアプリケーションとピン留めされた Web リンクを設定することが可能であり、また推奨されます。 Managed Home Screen に影響を与える**デバイス構成**で使用可能な設定の完全なリストについては、「[専用のデバイス設定](../configuration/device-restrictions-android-for-work.md#device-experience)」を参照してください。  

最初に、[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) に移動し、 **[アプリ]**  >  **[アプリ構成ポリシー]** を選択します。 **Android** を実行している**マネージド デバイス**に構成ポリシーを追加し、関連付けられているアプリとして **[Managed Home Screen]** を選択します。 **[構成設定]** をクリックして、利用可能なさまざまな Managed Home Screen 設定を構成します。 

## <a name="choosing-a-configuration-settings-format"></a>構成設定の形式を選択する

Managed Home Screen の構成設定を定義するのに使用できる 2 つの方法があります。

- **構成デザイナー**は、機能のオン/オフを切り替えたり、値を設定できる使いやすい UI を使用して設定を構成することができます。 この方法では、値の型 `BundleArray` で無効になるいくつかの構成キーがあります。 これらの構成キーは、JSON データを入力することによってのみ構成できます。 
- **JSON データ**を使用すると、JSON スクリプトを使用してすべての可能な構成キーを定義することができます。 

構成デザイナーでプロパティを追加する場合、 **[構成設定の形式]** ドロップダウンから **[JSON データを入力]** を選択することで、これらのプロパティを自動的に JSON に変換できます。

![構成設定の形式オプションのスクリーンショット](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_01.png)

## <a name="using-configuration-designer"></a>構成デザイナーを使用する

構成デザイナーを使用すると、あらかじめ設定されている設定とそれらに関連付けられている値を選択できます。 

![追加された構成設定のスクリーンショット](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_02.png)

次の表に、Managed Home Screen の使用可能な構成キー、値の型、既定値、および説明を示します。 説明では、選択した値に基づいて予想されるデバイスの動作を説明します。 構成デザイナーで無効になっている構成キーは、この表には含まれていません。

| 構成キー | ［値の種類］ | 既定値 | [説明] |
|---------------------------------------------------------------------------------------------------------------------------|-------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| グリッド サイズの設定 | string | 自動 | Managed Home Screen に配置するアプリのグリッド サイズを設定できます。 アプリの行と列の数を設定して、`columns;rows` の形式でグリッド サイズを定義することができます。 グリッド サイズを定義すると、設定した行数がホーム画面の 1 行に表示されるアプリの最大数になり、設定した列数がホーム画面の 1 列に表示されるアプリの最大数になります。 |
| 通知バッジの有効化 | ブール | FALSE | アプリ上の新しい通知数を示す、アプリ アイコン用の通知バッジを有効にします。 この設定を有効にすると、エンド ユーザーに未読の通知があることを知らせる通知バッジがアプリに表示されます。 この構成キーを無効のままにすると、アプリに未読の通知があっても、エンド ユーザーに知らせる通知バッジが表示されなくなります。 |
| ホーム画面のロック | ブール | TRUE | ホーム画面上のアプリ アイコンをエンド ユーザーが移動できないようにします。 この構成キーを有効にすると、ホーム画面上のアプリ アイコンがロックされ、エンド ユーザーがホーム画面の別のグリッドの位置にドラッグ アンド ドロップできなくなります。 `false` にすると、エンド ユーザーが Managed Home Screen 上のアプリケーションと Web リンクのアイコンを移動できるようになります。  |
| デバイスの壁紙の設定 | string | Default | 壁紙として設定する画像の URL を入力して、好みの壁紙を設定することができます。 |
| アプリ アイコンのサイズの設定 | integer | 2 | ホーム画面に表示されるアプリのアイコンのサイズを設定することができます。 この構成では、サイズごとに次の値を選択できます - 0 (最小)、1 (小)、2 (標準)、3 (大)、4 (最大)。 |
| アプリ フォルダー アイコンの設定 | integer | 0 | ホーム画面上のアプリ フォルダーの外観を定義することができます。 外観は、次の値から選択できます:濃色の正方形 (0)、濃色の円 (1)、淡色の正方形 (2)、淡色の円 (3)。 |
| 画面の向きの設定 | integer | 1 | ホーム画面の向きを縦モード、横モード、または自動回転に設定することができます。 向きを設定するには、値 1 (縦モード)、2 (横モード)、3 (自動回転) を入力します。 |
| 許可リストに登録されたアプリケーションの設定 | bundleArray | FALSE | デバイス上にインストールされているアプリの中から、ホーム画面に表示するアプリのセットを定義することができます。 表示できるようにするアプリのアプリ パッケージ名を入力することで、アプリを定義できます。たとえば、com.microsoft.emmx と入力すると、ホーム画面上で設定にアクセスできるようになります。 このセクション内で許可リストに登録するアプリは、ホーム画面上に表示するためには、デバイス上に既にインストールされている必要があります。 |
| ピン留めされた Web リンクの設定 | bundleArray | FALSE | Web サイトをクイック起動アイコンとしてホーム画面にピン留めすることができます。 この構成では、エンド ユーザーがブラウザー内で 1 回のタップで起動できるように、URL を定義して、それをホーム画面に追加することができます。 |
| スクリーン セーバーを有効にする | ブール | FALSE | スクリーン セーバー モードを有効または無効にします。 true に設定すると、**screen_saver_image**、**screen_saver_show_time**、**inactive_time_to_show_screen_saver**、**media_detect_screen_saver** を構成できます。 |
| スクリーン セーバーの画像 | string |   | スクリーン セーバーの画像の URL を設定します。 URL を設定しない場合、スクリーン セーバーがアクティブになると、既定のスクリーン セーバー画像がデバイスに表示されます。 既定の画像では、Managed Home Screen アプリのアイコンが表示されます。  |
| スクリーン セーバーの表示時間 | integer | 0 | スクリーン セーバー モード時にデバイスでスクリーン セーバーが表示される時間を秒単位で設定するオプションを提供します。 0 に設定すると、スクリーン セーバー モードではスクリーン セーバーが、デバイスがアクティブになるまで無期限に表示されます。  |
| スクリーン セーバーが有効になるまでの非アクティブ状態の時間 | integer | 30 | スクリーン セーバーをトリガーするまでにデバイスが非アクティブな状態の秒数。 0 に設定すると、デバイスはスクリーン セーバー モードにされません。 |
| スクリーン セーバーを表示する前のメディアの検出 | ブール | TRUE | デバイスでオーディオ/ビデオが再生されている場合に、デバイスの画面にスクリーン セーバーを表示するかどうかを選択します。 true に設定すると、**inactive_time_to_show_scree_saver** の値に関係なく、デバイスでオーディオ/ビデオが再生されなくなります。 false に設定すると、**inactive_time_to_show_screen_saver** に設定されている値に従って、デバイスの画面でスクリーン セーバーが表示されます。   |
| 仮想ホーム ボタンの有効化 | ブール | FALSE | エンド ユーザーに Managed Home Screen のホーム ボタンへのアクセスを許可するには、この設定を `True` にします。このボタンを使用すると、ユーザーが現在行っているタスクから Managed Home Screen へ戻ることができます。  |
| 仮想ホーム ボタンの種類 | string | swipe_up | 上方向にスワイプのジェスチャでホーム ボタンにアクセスするには、**swipe_up** を使用します。 エンド ユーザーが画面を移動できる固定の永続的なホーム ボタンにアクセスするには、**float** を使用します。 |
| バッテリと信号の強さのインジケーター バー | ブール | True  | この設定を `True` にすると、バッテリと信号の強さのインジケーター バーが表示されます。 |
| ロック タスク モード終了のパスワード | string |   | トラブルシューティングのためにロック タスク モードを一時的に停止するために使用する 4 - 6 桁のコードを入力します。 |
| Show Managed Setting (マネージド設定の表示) | ブール | TRUE | "マネージド設定" とは、 **[Wi-Fi 設定の表示]** 、 **[Bluetooth の設定の表示]** 、 **[Show volume setting]\(音量設定の表示\)** 、 **[Show flashlight setting]\(懐中電灯設定の表示\)** など、クイック アクセス用の設定を構成してある場合にのみ表示される Managed Home Screen アプリです。 画面を下方向にスワイプして、これらの設定にアクセスすることもできます。 このキーを `False` に設定すると、"マネージド設定" アプリが非表示になり、エンドユーザーが下方向にスワイプすることでのみ設定にアクセスできます。    |
| Enable easy access debug menu (簡易アクセス デバッグ メニューの有効化) | ブール | FALSE | この設定を `True` にすると、Managed Home Screen の使用中に、マネージド設定アプリから、または下方向にスワイプすることで、デバッグ メニューにアクセスできます。 デバッグ メニューには現在、キオスク モードを終了する機能があり、戻るボタンを 15 回ほどクリックするとアクセスできます。 この設定を `False` に設定したままにすると、戻るボタンでのみアクセスできるデバッグ メニューへのエントリ ポイントが保持されます。   |
| Wi-Fi 設定の表示 | ブール | FALSE | この設定を `True` にすると、エンド ユーザーが Wi-Fi をオン/オフにしたり、別の Wi-Fi ネットワークに接続できるようになります。  |
| Enable Wi-Fi allow-list (Wi-Fi 許可リストの有効化) | ブール | FALSE | この設定を `True` にし、 **[Wi-Fi allow-list] (Wi-Fi 許可リスト)** キーに値を入力すると、Managed Home Screen 内に表示される Wi-Fi ネットワークを制限できます。 `False` に設定すると、デバイスによって検出された使用可能なすべての Wi-Fi ネットワークが表示されます。 この設定は、 **[Wi-Fi 設定の表示]** が `True` に設定され、 **[Wi-Fi allow-list] (Wi-Fi 許可リスト)** が入力されている場合にのみ関係することに注意してください。   |
| Wi-Fi allow-list (Wi-Fi 許可リスト)| bundleArray | FALSE | デバイスで Managed Home Screen 内に表示させたい Wi-Fi ネットワークのすべての SSID を一覧表示できます。 この一覧は、**Wi-Fi 設定の表示** と **Enable Wi-Fi allow-list (Wi-Fi 許可リストの有効化)** が `True` に設定されている場合にのみ関係します。 それらのどちらかが `False` に設定されている場合は、この構成を変更する必要はありません。    |
| Bluetooth の設定の表示 | ブール | FALSE | この設定を `True` にすると、エンド ユーザーが Bluetooth をオン/オフにしたり、別の Bluetooth 対応デバイスに接続できるようになります。   |
| Show volume setting (音量設定の表示) | ブール | FALSE | この設定を `True` にすると、エンド ユーザーは音量スライダーを使用してメディアの音量を調整できます。   |
| Show flashlight setting (懐中電灯設定の表示) | ブール | FALSE | この設定を `True` にすると、エンド ユーザーはデバイスの懐中電灯のオン/オフを切り替えることができます。 デバイスで懐中電灯がサポートされていない場合、この設定は `True` に構成されていても表示されません。   |
| Show device info setting (デバイス情報設定の表示) | ブール | FALSE | この設定を `True` にすると、エンド ユーザーは、マネージド設定アプリから、または下方向にスワイプすることで、デバイスに関するクイック ヒントにアクセスできます。 アクセス可能な情報には、デバイスの製造元、モデル、シリアル番号などがあります。   |
| フォルダー内のアプリケーションは、名前順に並べ替えられます | ブール | TRUE | この設定を `False` にすると、フォルダー内の項目を指定されている順序で表示できます。 それ以外の場合は、アルファベット順でフォルダーに表示されます。   |
| Application order enabled (アプリケーションの順序の有効化) | ブール | FALSE | この設定を `True` にすると、Managed Home Screen でアプリケーション、Web リンク、フォルダーの順序を設定できるようになります。 有効になったら、**app_order** で順序を設定します。   |
| Application order (アプリケーションの順序) | bundleArray | FALSE | Managed Home Screen でアプリケーション、Web リンク、フォルダーの順序を指定できます。 この設定を使うには、 **[Lock Home Screen]\(ホーム画面のロック\)** を有効にし、 **[Set grid size]\(グリッド サイズの設定\)** を定義し、 **[Application order enabled]\(アプリケーションの順序の有効化\)** を `True` に設定する必要があります。   |

## <a name="enter-json-data"></a>JSON データの入力

JSON データを入力して、Managed Home Screen で使用可能なすべての設定と、**構成デザイナー**しで無効にされた設定を構成します。

![追加された JSON データのスクリーンショット](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_03.png)

**構成デザイナー**の表 (上) に一覧表示されている構成可能な設定のリストに加え、次の表では、JSON データを使用してのみ構成できる構成キーを示します。

|    構成キー    |    値の型    |    既定値    |    [説明]    |
|-------------------------------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    許可リストに登録されたアプリケーションの設定    |    bundleArray    | <img alt="JSON - Example 1" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson01.png" width="300"> |    デバイスにインストールされているアプリの中からホーム画面に表示するアプリのセットを定義することができます。 表示したいアプリのアプリ パッケージ名を入力することで、アプリを定義できます。たとえば、com.android.settings を使用すると、ホーム画面上でアクセスできる設定になります。 このセクション内で許可リストに登録するアプリは、ホーム画面上に表示するためには、デバイス上に既にインストールされている必要があります。    |
|    ピン留めされた Web リンクの設定    |    bundleArray    | <img alt="JSON - Example 2" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson02.png" width="300"> |    Web サイトをクイック起動アイコンとしてホーム画面にピン留めすることができます。 この構成では、エンド ユーザーがブラウザー内で 1 回のタップで起動できるように、URL を定義して、それをホーム画面に追加することができます。    |
|    アプリをグループ化するためのマネージド フォルダーの作成    |    bundleArray    | <img alt="JSON - Example 3" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson03.png" width="300"> |    フォルダーを作成し、名前を付けて、これらのフォルダー内にアプリをグループ化することができます。 エンド ユーザーはフォルダーを移動したり、フォルダーの名前を変更したり、フォルダー内でアプリを移動したりすることができなくなります。   フォルダーは作成された順に表示され、フォルダー内のアプリはアルファベット順に表示されます。         注: フォルダーにグループ化するすべてのアプリは、必要に応じてデバイスに割り当てる必要があり、また Managed Home Screen に追加されている必要があります。     |

以下は、使用可能なすべての構成キーが含まれた JSON スクリプトの例です。

```json
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "com.microsoft.launcher.enterprise",
    "managedProperty": [
        {
            "key": "lock_home_screen",
            "valueBool": true
        },
        {
            "key": "wallpaper",
            "valueString": "default"
        },
        {
            "key": "icon_size",
            "valueInteger": 2
        },
        {
            "key": "app_folder_icon",
            "valueInteger": 0
        },
        {
            "key": "screen_orientation",
            "valueInteger": 1
        },
        {
            "key": "applications",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "app package name here"
                        }
                    ]
                }
            ]
        },
        {
            "key": "weblinks",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "link",
                            "valueString": "link here"
                        },
                        {
                            "key": "label",
                            "valueString": "weblink label here"
                        }
                    ]
                }
            ]
        },
        {
            "key": "show_virtual_home",
            "valueBool": false
        },
        {
            "key": "virtual_home_type",
            "valueString": "swipe_up"
        },
        {
            "key": "show_virtual_status_bar",
            "valueBool": true
        },
        {
            "key": "exit_lock_task_mode_code",
            "valueString": ""
        },
        {
            "key": "show_wifi_setting",
            "valueBool": false
        },
        {
            "key": "show_bluetooth_setting",
            "valueBool": false
        },
        {
            "key": "show_flashlight_setting",
            "valueBool": false
        },
        {
            "key": "show_volume_setting",
            "valueBool": false
        },
        {
            "key": "show_device_info_setting",
            "valueBool": false
        },
        {
            "key": "show_managed_setting",
            "valueBool": false
        },
        {
            "key": "enable_easy_access_debugmenu",
            "valueBool": false
        },
        {
            "key": "enable_wifi_allowlist",
            "valueBool": false
        },
        {
            "key": "wifi_allowlist",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "SSID",
                            "valueString": "name of Wi-Fi network 1 here"
                        }
                    ]
                },   
                {
                    "managedProperty": [
                        {
                            "key": "SSID",
                            "valueString": "name of Wi-Fi network 2 here"
                        }
                    ]
                }  
            ]
        },
        {
            "key": "grid_size",
            "valueString": "4;5"
        },
        {
            "key": "app_order_enabled",
            "valueBool": true
        },
        {
            "key": "apps_in_folder_ordered_by_name",
            "valueBool": true
        },
        {
            "key": "app_orders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.Microsoft.emmx"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 1
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Work"
                        },
                        {
                            "key": "type",
                            "valueString": "managed_folder"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 2
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.microsoft.launcher.enterprise"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "class",
                            "valueString": "com.microsoft.launcher.launcher"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 3
                        }
                    ]
                }
            ]
        },
        {
            "key": "managed_folders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Folder name here"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.emmx"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.bing"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "link",
                                            "valueString": "https://microsoft.com/"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Example folder name 2"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.office.word"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="googles-android-device-policy-app"></a>Google の Android デバイス ポリシー アプリ
マネージド ホーム スクリーン アプリで、Google の Android デバイス ポリシー アプリにアクセスできるようになりました。 マネージド ホーム スクリーン アプリは、マルチアプリ キオスク モードを使用する Android Enterprise (AE) 専用デバイスとして Intune に登録されているデバイスで使用されるカスタム ランチャーです。 Android デバイス ポリシー アプリにアクセスしたり、ユーザーを Android デバイス ポリシー アプリに案内したりして、サポートとデバッグを行うことができます。 この起動機能は、デバイスが登録され、マネージド ホーム スクリーンにロックされているときに使用できます。 この機能を使用するために追加のインストールは必要ありません。

## <a name="managed-home-screen-debug-screen"></a>Managed Home Screen のデバッグ画面
Managed Home Screen のデバッグ画面にアクセスするには、デバッグ画面が表示されるまで**戻る**ボタンをクリックします (**戻る**ボタンを 15 回以上クリックします)。 このデバッグ画面から、Android デバイス ポリシー アプリケーションを起動したり、ログの表示とアップロードを行ったり、キオスク モードを一時的に停止してデバイスを更新したりできます。 キオスク モードの一時停止について詳しくは、Android Enterprise の「[専用デバイスの設定](../configuration/device-restrictions-android-for-work.md#device-experience)」に記載されている **[キオスク モードを終了する]** 項目をご覧ください。 Managed Home Screen のデバッグ画面に簡単にアクセスできるようにする場合は、アプリケーション構成ポリシーを使用して **[Enable easy access debug menu (簡易アクセス デバッグ メニューの有効化)]** を `True` に設定できます。 

## <a name="next-steps"></a>次のステップ

- Android エンタープライズ専用デバイスの詳細については、「[Android エンタープライズ専用デバイスの Intune 登録を設定する](../enrollment/android-kiosk-enroll.md)」を参照してください。
