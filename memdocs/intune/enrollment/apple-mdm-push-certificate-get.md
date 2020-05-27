---
title: Intune 用の Apple MDM プッシュ証明書を取得する
titleSuffix: ''
description: Intune を使用して iOS/iPadOS デバイスを管理するために Apple MDM プッシュ証明書を取得します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/08/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a66171d678ffd19e424fb399633c3fed3db9a588
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986996"
---
# <a name="get-an-apple-mdm-push-certificate"></a>Apple MDM プッシュ証明書を取得する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune で iOS/iPadOS および macOS デバイスを管理するには、Apple MDM プッシュ証明書が必要です。 証明書を Intune に追加すると、ユーザーは以下を使用して、自分のデバイスを登録できます。

- ポータル サイト アプリ。

- Apple の一括登録方法 (Device Enrollment Program、Apple School Manager、Apple Configurator)。

登録オプションについて詳しくは、[iOS/iPadOS デバイスの登録方法の選択](ios-enroll.md)に関する記事をご覧ください。

プッシュ証明書の有効期限が切れた場合は、更新する必要があります。 更新する際には、必ず、最初にプッシュ証明書を作成したときに使用したのと同じ Apple ID を使用してください。


## <a name="steps-to-get-your-certificate"></a>証明書を取得する手順
[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[デバイス]**  >  **[デバイスの登録]**  >  **[Apple の登録]**  >  **[Apple MDM プッシュ通知証明書]** を選択してから、次の手順を行います。

### <a name="step-1-grant-microsoft-permission-to-send-user-and-device-information-to-apple"></a>手順 1. Microsoft がユーザーとデバイスの情報を Apple に送信できるようにする
**[同意する。]** を選択し、 Microsoft がデータを Apple に送信できるようにします。

![MDM プッシュが設定されていない MDM プッシュ証明書構成画面](./media/apple-mdm-push-certificate-get/create-mdm-push-certificate.png)

### <a name="step-2-download-the-intune-certificate-signing-request-required-to-create-an-apple-mdm-push-certificate"></a>手順 2. Apple MDM プッシュ証明書の作成に必要な Intune 証明書署名要求をダウンロードする
**[CSR のダウンロード]** を選び、要求ファイルをダウンロードしてローカルに保存します。 このファイルは、Apple Push Certificates Portal からの信頼関係証明書を要求するために使用します。

### <a name="step-3-create-an-apple-mdm-push-certificate"></a>手順 3. Apple MDM プッシュ証明書を作成する
**[MDM プッシュ証明書を作成する]** を選択して、Apple Push Certificates Portal に移動します。 会社の Apple ID でサインインし、 **[証明書の作成]** をクリックします。 **[ファイルの選択]**  を選択し、証明書署名要求ファイルを参照して、 **[アップロード]** を選択します。 [確認] ページで **[ダウンロード]** を選択して証明書 (.pem) ファイルをダウンロードし、ファイルをローカルに保存します。

> [!NOTE]
> 証明書は、証明書の作成に使用した Apple ID と関連付けられています。 ベスト プラクティスとしては、管理タスクのため会社の Apple ID を使用し、配布リストのように複数のユーザーがメールボックスを監視するようにします。 個人の Apple ID は使用しないでください。

### <a name="step-4-enter-the-apple-id-used-to-create-your-apple-mdm-push-certificate"></a>手順 4. Apple MDM プッシュ証明書の作成に使用した Apple ID を入力する
この証明書を更新する場合に備え、この ID をヒントとして記録します。

### <a name="step-5-browse-to-your-apple-mdm-push-certificate-to-upload"></a>手順 5. アップロードする Apple MDM プッシュ証明書を参照する
証明書 (.pem) ファイルに移動し、 **[開く]** を選択して、 **[アップロード]** を選択します。 プッシュ証明書を使用すると、Intune で Apple デバイスを登録して管理することができます。

## <a name="renew-apple-mdm-push-certificate"></a>Apple MDM プッシュ証明書を更新する
Apple MDM プッシュ証明書の有効期間は 1 年間です。iOS/iPadOS と macOS のデバイス管理を維持するには毎年更新する必要があります。 証明書の有効期限が切れると、登録されている Apple デバイスに接続できなくなります。

証明書は、証明書の作成に使用した Apple ID と関連付けられています。 MDM プッシュ証明書を更新するには、作成時と同じ Apple ID を使用してください。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインし、 **[デバイス]**  >  **[デバイスの登録]**  >  **[Apple の登録]**  >  **[Apple MDM プッシュ通知証明書]** を選択します。
2. **[CSR のダウンロード]** を選び、要求ファイルをダウンロードしてローカルに保存します。 このファイルは、Apple Push Certificates Portal からの信頼関係証明書を要求するために使用します。
3. **[MDM プッシュ証明書を作成する]** を選択して、Apple Push Certificates Portal に移動します。 更新する証明書を検索し、 **[更新]** を選択します。
4. **[Renew Push Certificate]\(プッシュ証明書の更新\)** 画面で、今後証明書を識別しやすいようにメモを入力し、 **[ファイルの選択]** を選んで、ダウンロードした新しい要求ファイルを参照し、 **[アップロード]** を選びます。
   > [!TIP]
   > 証明書は、その UID で識別できます。 UID の GUID 部分を確認するには、証明書の詳細の**サブジェクト ID** を調べます。 または、登録済みの iOS/iPadOS デバイスで、 **[設定]**  >  **[全般]**  >  **[デバイス** **管理]**  >  **[管理プロファイル]**  >  **[詳細]**  >  **[管理プロファイル]** に移動します。 2 行目の項目 **[トピック]** に、Apple Push Certificates Portal で証明書と照合できる一意の GUID が含まれます。
 
6. **[確認]** 画面で **[ダウンロード]** を選択し、.pem ファイルをローカルに保存します。
7. [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) で **[Apple MDM プッシュ証明書]** 参照アイコンを選択し、Apple からダウンロードした .pem ファイルを選択し、 **[アップロード]** を選択します。

Apple MDM プッシュ証明書は **[有効]** と表示され、有効期限まで 365 日と表示されます。
