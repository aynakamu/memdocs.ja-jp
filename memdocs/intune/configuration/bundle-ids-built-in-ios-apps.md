---
title: Microsoft Intune での組み込みアプリ用の iOS および iPadOS バンドル ID - Azure | Microsoft Docs
titleSuffix: ''
description: 組み込み iOS および iPadOS アプリ用のバンドル ID の一覧を参照してください。 Microsoft Intune で、これらのバンドル ID を使用してデバイス構成プロファイルおよびポリシー内でアプリを許可します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7de0b978c24f28988c62854a249505a0598db95
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084073"
---
# <a name="bundle-ids-for-built-in-ios-and-ipados-apps-you-can-use-in-intune"></a>Intune で使用できる組み込み iOS および iPadOS アプリ用のバンドル ID

iOS および iPadOS デバイス上で機能を構成すると、iOS および iPadOS デバイス上に組み込みアプリを追加することもできます。 この記事では、一部の一般的な組み込み iOS および iPadOS アプリのバンドル ID を一覧します。 他のアプリのバンドル ID を調べるには、ソフトウェア ベンダーにお問い合わせください。 Apple の [iOS および iPadOS バンドル ID](https://support.apple.com/guide/mdm/ios-bundle-ids-mdm90f60c1ce/web) (Apple の Web サイトが開きます) の一覧を参照してください。

## <a name="bundle-ids"></a>バンドル ID

| バンドル ID                   | アプリ名     | 発行者 |
|-----------------------------|--------------|-----------|
| com.apple.AppStore          | アプリ ストア    | Apple     |
| com.apple.store.Jolly       | Apple ストア  | Apple     |
| com.apple.calculator        | 計算機   | Apple     |
| com.apple.mobilecal         | 予定表     | Apple     |
| com.apple.camera            | カメラ       | Apple     |
| com.apple.mobiletimer       | 時計        | Apple     |
| com.apple.clips             | Clips        | Apple     |
| com.apple.compass           | コンパス      | Apple     |
| com.apple.MobileAddressBook | 連絡先     | Apple     |
| com.apple.facetime          | FaceTime     | Apple     |
| com.apple.DocumentsApp      | ファイル        | Apple     |
| com.apple.mobileme.fmf1     | 友達を探す | Apple     |
| com.apple.mobileme.fmip1    | Find iPhone  | Apple     |
| com.apple.gamecenter        | Game Center  | Apple     |
| com.apple.mobilegarageband  | GarageBand   | Apple     |
| com.apple.Health            | 正常性       | Apple     |
| com.apple.Home              | Home         | Apple     |
| com.apple.iBooks            | iBooks       | Apple     |
| com.apple.iMovie            | iMovie       | Apple     |
| com.apple.itunesconnect.mobile | iTunes Connect | Apple |
| com.apple.MobileStore       | iTunes Store | Apple     |
| com.apple.itunesu           | iTunes U     | Apple     |
| com.apple.Keynote           | Keynote      | Apple     |
| com.apple.mobilemail        | メール         | Apple     |
| com.apple.Maps              | マップ         | Apple     |
| com.apple.measure           | 基準      | Apple     |
| com.apple.MobileSMS         | メッセージ     | Apple     |
| com.apple.Music             | ミュージック        | Apple     |
| com.apple.news              | News         | Apple     |
| com.apple.mobilenotes       | 注        | Apple     |
| com.apple.Numbers           | 数字      | Apple     |
| com.apple.Pages             | ページ        | Apple     |
| com.apple.mobilephone       | 電話        | Apple     |
| com.apple.Photo-Booth       | Photo Booth  | Apple     |
| com.apple.mobileslideshow   | 写真       | Apple     |
| com.apple.podcasts          | Podcast     | Apple     |
| com.apple.reminders         | リマインダー    | Apple     |
| com.apple.mobilesafari      | Safari       | Apple     |
| com.apple.Preferences       | Settings     | Apple     |
| com.apple.shortcuts         | ショートカット    | Apple     |
| com.apple.SiriViewService   | Siri         | Apple     |
| com.apple.stocks            | 株価       | Apple     |
| com.apple.tips              | ヒント         | Apple     |
| com.apple.tv                | TV           | Apple     |
| com.apple.videos            | ビデオ       | Apple     |
| com.apple.VoiceMemos        | VoiceMemos   | Apple     |
| com.apple.Passbook          | Wallet       | Apple     |
| com.apple.Bridge            | 視聴する        | Apple     |
| com.apple.weather           | 天気      | Apple     |

## <a name="next-steps"></a>次のステップ

これらのバンドル ID を使用して[デバイス機能](ios-device-features-settings.md)を構成すると共に、iOS および iPadOS デバイス上で[一部の設定を許可または制限](device-restrictions-ios.md)します。
