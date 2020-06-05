---
title: Microsoft Intune によるモバイル アプリケーション管理のためにアプリを準備する
description: このトピックの情報は、カスタム基幹業務アプリでモバイル アプリ管理ポリシーを使用できるようにするために、アプリ ラッピング ツールとアプリ SDK を使用するタイミングを判断するときに役立ちます。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 739ebebe18628279e5242ab227cf0f43993eff08
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330867"
---
# <a name="prepare-line-of-business-apps-for-app-protection-policies"></a>アプリ保護ポリシーを利用するために基幹業務アプリで準備を行う

Intune アプリ ラッピング ツールまたは Intune アプリ SDK のどちらかを使って、アプリでアプリ保護ポリシーを使えるようにできます。 ここでは、これら 2 つの方法の内容と用途について説明します。

## <a name="intune-app-wrapping-tool"></a>Intune アプリ ラッピング ツール

アプリ ラッピング ツールは、主として、**内部**基幹業務 (LOB) アプリケーションに使います。 このツールは、アプリのラッパーを作成するコマンド ライン アプリケーションです。このラッパーにより、アプリを Intune アプリ保護ポリシーで管理できるようになります。 独立系ソフトウェア ベンダー (ISV) から提供されるアプリを保護するときは、ラッピングされたアプリが ISV によってサポートされるかどうかを明確にすることが重要です。

このツールを使うためにソース コードは必要ありませんが、署名資格情報が必要です。 署名資格情報の詳細については、[Intune のブログ](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/)を参照してください。 アプリ ラッピング ツールのドキュメントとしては、[Android アプリ ラッピング ツール](app-wrapper-prepare-android.md)と [iOS アプリ ラッピング ツール](app-wrapper-prepare-ios.md)に関するページをご覧ください。

アプリ ラッピング ツールは、Apple App Store または Google Play ストアのアプリを**サポートしていません**。 また、開発ツールの統合が必要な一部の機能もサポートしていません (次の機能比較表を参照してください)。

Intune に登録されていないデバイスのアプリ保護ポリシー用アプリ ラッピング ツールの詳細については、「[Microsoft Intune に登録されていないデバイスの基幹業務アプリとデータを保護する](../apps/apps-add.md)」を参照してください。

### <a name="reasons-to-use-the-app-wrapping-tool"></a>アプリ ラッピング ツールを使用する理由

* アプリに組み込みのデータ保護機能がない。
* アプリが内部的に展開される。
* アプリのソース コードにアクセスできない。
* 自分で開発したアプリではない。
* アプリのユーザー認証エクスペリエンスが最小限である。

### <a name="supported-app-development-platforms"></a>サポートされるアプリ開発プラットフォーム

|**アプリ ラッピング ツール** | **Xamarin** |**Cordova** |
|------|----|----|
|**Android** |はい|はい|
|**Android**|いいえ - [Intune App SDK Xamarin Bindings](app-sdk-xamarin.md) を使用します。|はい|

## <a name="intune-app-sdk"></a>Intune App SDK

App SDK は、主として、Apple App Store または Google Play ストアにあるアプリを Intune で管理できるようにするお客様向けに設計されています。 ただし、どのようなアプリでも (基幹業務アプリでさえ)、SDK の統合を利用できます。

SDK の詳細については、「[概要](app-sdk.md)」を参照してください。 SDK で作業を開始するには、「[Microsoft Intune App SDK を使ってみる](app-sdk-get-started.md)」を参照してください。

### <a name="reasons-to-use-the-sdk"></a>SDK を使用する理由

* アプリに組み込みのデータ保護機能がない。
* アプリが Google Play や Apple の App Store などのパブリック アプリ ストアに展開される。
* 自分が開発したアプリであり、SDK を使用するための技術的な背景を備えている。
* アプリに他の SDK 統合がある。
* アプリが頻繁に更新される。

### <a name="supported-app-development-platforms"></a>サポートされるアプリ開発プラットフォーム

|**Intune App SDK** |**Xamarin** |**Cordova**
|------|----|----|
|**Android**|はい – [Intune App SDK Xamarin Bindings](app-sdk-xamarin.md) を使用します。|いいえ|
|**Android**| はい – [Intune App SDK Xamarin Bindings](app-sdk-xamarin.md) を使用します。|いいえ|

## <a name="not-using-an-app-development-platform-listed-above"></a>上記のアプリ開発プラットフォームを使用していない場合

Intune SDK の開発チームは、ネイティブの Android、iOS (Obj-C、Swift)、Xamarin、および Xamarin.Forms プラットフォームを使ってビルドされたアプリに対するサポートを、積極的にテストして管理しています。 一部のお客様は、Intune SDK とその他のプラットフォーム (React Native や NativeScript など) の統合に成功されていますが、Microsoft では、サポートされているプラットフォーム以外を使うアプリ開発者に向けた明示的なガイダンスやプラグインは提供されません。 

## <a name="feature-comparison"></a>機能の比較

次の表には、アプリで App SDK または App Wrapping Tool を使用する場合に有効になる設定が一覧表示されています。 一部の機能では、アプリ開発者が Intune SDK との基本的な統合の外側でいくつかのロジックを適用する必要があります。その結果、アプリで App Wrapping Tool を使用する場合は、これらは有効になりません。 

|機能|アプリ SDK|アプリ ラッピング ツール|
|-----------|---------------------|-----------|
|[Web コンテンツを会社の管理対象ブラウザーで表示するように制限する]|○|○|
|[Android、iTunes、iCloud のバックアップを禁止する]|○|○|
|[アプリで他のアプリへのデータ転送を許可する]|○|○|
|[アプリで他のアプリからのデータの受信を許可する]|○|○|
|他のアプリとの間で切り取り、コピー、貼り付けを制限する|○|○|
|マネージド アプリから切り取りまたはコピーできる文字数を指定する|○|○|
|[アクセスには簡易暗証番号が必要]|○|○|
|[PIN をリセットするまでの試行数を指定する]|○|○|
|PIN の代わりに指紋を要求する|○|○|
|PIN の代わりに顔認識を許可する (iOS のみ)|○|○|
|[アクセスには会社の資格情報が必要]|○|○|
|PIN の有効期限を設定する|○|○|
|[脱獄またはルート化されたデバイスで管理対象アプリが実行されないようにブロックする]|○|○|
|[アプリ データの暗号化]|○|○|
|[指定した時間 (分) 後にアクセス要件を再確認する]|○|○|
|[オフラインの猶予期間を指定する]|○|○|
|[画面キャプチャをブロック (Android のみ)]|○|○|
|デバイスの登録なしで MAM をサポート|○|○|
|アプリ データのフル ワイプ|○|○|
|複数 ID のシナリオにおける職場および学校のデータの選択的ワイプ <br><br>**注:** iOS と iPadOS では、管理プロファイルを削除するとアプリも削除されます。|○||
|[名前を付けて保存] を禁止する|○||
|対象のアプリケーション構成 (または "MAM チャネル" を介したアプリ構成)|○|○|
|[マルチ ID アプリのサポート]|○||
|カスタマイズ可能なスタイル |○|||
|Citrix mVPN でのオンデマンドのアプリケーション VPN 接続|○|○| 
|連絡先の同期を無効にする|○|○|
|印刷を無効にする|○|○|
|アプリの最小バージョン要件|○|○|
|最低限のオペレーティング システムを必要とする|○|○|
|Android の最小セキュリティ パッチ バージョン要件 (Android のみ)|○|○|
|iOS 用 Intune SDK の最小要件 (iOS のみ)|○|○|
|SafetyNet デバイス構成証明 (Android のみ)|○|○|
|アプリの脅威のスキャン (Android のみ)|○|○|
|Mobile Threat Defense ベンダー デバイスの最大リスク レベルを必要とする|○||
|組織アカウント向けのアプリ通知の内容を構成する|○|○|
|承認済みキーボードの使用を要求する (Android のみ)|○|○|
|アプリの保護ポリシーが必要 (条件付きアクセス)|○||

## <a name="next-steps"></a>次のステップ

アプリ保護ポリシーと Intune の詳細については、次のトピックをご覧ください。

- [Android アプリ ラッピング ツール](app-wrapper-prepare-android.md)<br>
- [iOS アプリ ラッピング ツール](app-wrapper-prepare-ios.md)<br>
- [SDK を使用してモバイル アプリケーション管理に対応する](app-sdk.md)
