---
title: Microsoft Intune での Windows 10 用の配信の最適化設定 - Azure | Microsoft Docs
description: Intune で管理する Windows 10 デバイスで配信の最適化を使用する方法を構成します。 Intune では、デバイス構成プロファイルを作成してインターネットから更新プログラムをインストールします。 また、既存の更新プログラム リングを配信の最適化プロファイルに置き換える方法についても確認します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 71039737a74aebb3066c001536aaf677a0467696
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79345677"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Microsoft Intune での配信の最適化設定

Intune では、ご利用の Windows 10 デバイスに合わせて配信の最適化設定を使用することで、そのデバイスでアプリケーションおよび更新プログラムをダウンロードする際に消費される帯域幅が削減されます。 デバイスの構成プロファイルの一部として、配信の最適化を構成します。  

この記事では、デバイスの構成プロファイルの一部として配信の最適化の設定を構成する方法について説明します。 プロファイルを作成したら、次に、そのプロファイルをご利用の Windows 10 デバイスに割り当てるか、展開します。

Intune でサポートされる配信の最適化設定の一覧については、「[Intune 用の配信最適化の設定](delivery-optimization-settings.md)」を参照してください。  

Windows 10 での配信の最適化について学習するには、Windows ドキュメントの[配信の最適化更新プログラム](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)に関するページを参照してください。  

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. 次のプロパティを入力します。

    - **名前**:新しいプロファイルのわかりやすい名前を入力します。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイルの種類]** : **[配信の最適化]** を選択します。

4. **[設定]** 、 **[構成]** の順に選択し、更新プログラムやアプリをダウンロードする方法を定義します。 使用可能な設定については、「[Intune の配信の最適化の設定](delivery-optimization-settings.md)」を参照してください。

5. 完了したら、 **[OK]**  >  **[作成]** の順に選択して変更を保存します。

プロファイルが作成され、一覧に表示されます。 次に、[プロファイルを割り当て](device-profile-assign.md)てから、[その状態を監視](device-profile-monitor.md)します。

<!-- ## Move existing update rings to delivery optimization

**Delivery optimization** settings replace **Software updates – Windows 10 Update Rings**. Your existing update rings can be easily changed to use the **Delivery optimization** settings. To maintain the same settings when you create a delivery optimization profile, use the same *Delivery optimization download mode* and then set the same settings as you already use. However, you can choose to reconfigure delivery optimization settings to take advantage of the full range of addition settings that the Delivery Optimization profile can manage. 
-->

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Windows 10 更新リングから配信の最適化を削除する

配信の最適化は、以前はソフトウェア更新リングの一部として構成されていました。 2019 年 2 月以降、配信の最適化設定は、配信の最適化デバイス構成プロファイルの一部として構成されます。これには、デバイスへのソフトウェア更新プログラムの配信よりも影響がある追加の設定が含まれています。 まだ行っていない場合は、配信の最適化設定を *[未構成]* に設定して更新リングから削除し、配信の最適化プロファイルを使用して、使用可能なオプションのより大きな範囲を管理します。

1. 配信の最適化のデバイス構成プロファイルを作成します。

    1. Microsoft Endpoint Manager 管理センターで、 **[デバイス]** 、 **[構成プロファイル]** 、 **[プロファイルの作成]** の順に選択します。
    2. 次のプロパティを入力します。

        - **名前**:新しいプロファイルのわかりやすい名前を入力します。
        - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。
        - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
        - **[プロファイルの種類]** : **[配信の最適化]** を選択します。
        - **設定**:**配信の最適化ダウンロード モード**については、ご利用のデバイスに適用する設定を変更する必要がない限り、既存のソフトウェア更新プログラム リングで使用されているものと同じモードを選択します。 次のようなオプションがあります。
            - **未構成**
            - **HTTP のみ、ピアリングなし**
            - **HTTP blended with peering behind the same NAT (HTTP と同じ NAT でのピアリングの組み合わせ)**
            - **HTTP blended with peering across a private group (HTTP とプライベート グループでのピアリングの組み合わせ)**
            - **HTTP とインターネット ピアリングの組み合わせ**
            - **ピアリングなしの簡易ダウンロード モード**
            - **バイパス モード**
    3. 管理したい追加設定を構成します。

2. 既存のソフトウェア更新プログラム リングと同じデバイスおよびユーザーに、この新しいプロファイルを割り当てます。 [プロファイルの割り当て](device-profile-assign.md)に関するページに手順が記載されています。

3. 既存のソフトウェアのリングの構成を解除します。
    1. Microsoft Endpoint Manager 管理センターで、 **[ソフトウェア更新]** 、[Windows 10 更新リング] の順に進みます。
    2. 一覧から更新プログラム リングを選択します。
    3. 設定で、 **[配信の最適化ダウンロード モード]** を **[未構成]** に設定します。
    4. **[Ok]**  >  変更を **[保存]** します。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)、[その状態を監視](device-profile-monitor.md)します。  
Intune 用の[配信の最適化の設定](delivery-optimization-settings.md)を表示します。
