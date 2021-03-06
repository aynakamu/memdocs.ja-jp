---
title: ファイルを含める
description: インクルード ファイル
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/10/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: e63bb965b8fed4c0266e359493bbfa67100862cb
ms.sourcegitcommit: f575b13789185d3ac1f7038f0729596348a3cf14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2020
ms.locfileid: "90045146"
---
以下の通知では、今後の Intune の変更と機能に備えるために役立つ重要な情報が提供されます。

### <a name="updated-end-user-experience-for-android-device-administrator-wi-fi-profiles---7662680----"></a>Android デバイス管理者の Wi-Fi プロファイルのエンド ユーザー エクスペリエンスの更新<!-- 7662680  -->
Google によって加えられた変更により、新しい Wi-Fi プロファイルのエンド ユーザー エクスペリエンスは、10 月のポータル サイト アプリのリリースとは大幅に異なります。 ユーザーは追加のアクセス許可を付与し、展開時に Wi-Fi 構成を明示的に受け入れる必要があります。 Wi-Fi の構成は、既知の Wi-Fi ネットワークの一覧には表示されませんが、範囲内の場合は自動的に接続されます。 既存の Wi-Fi プロファイルの動作に変更はありません。 エンドポイント マネージャー管理センターでの管理者エクスペリエンスにも変更はありません。

適用対象:
- Android デバイス管理者、Android 10 以降

### <a name="microsoft-intune-ends-support-for-windows-phone-81-and-windows-10-mobile---3544938-3544909---"></a>Microsoft Intune での Windows Phone 8.1 と Windows 10 Mobile のサポートが終了<!-- 3544938, 3544909 -->
Windows Phone 8.1 に対する Microsoft のメインストリーム サポートは 2017 年 7 月に終了し、拡張サポートは 2019 年 6 月に終了しました。 Windows Phone 8.1 用のポータル サイト アプリは、2017 年 10 月から維持モードになっています。 さらに、2020 年 2 月 20 日に、Windows Phone 8.1 に対する Microsoft Intune のサポートが終了しました。 

Windows 10 Mobile の Microsoft メインストリーム サポートは、2019 年 12 月に終了しました。 サポートの声明に記載されているように、Windows 10 Mobile のユーザーは、新しいセキュリティ更新プログラム、セキュリティ以外の修正プログラム、無償のサポート オプション、Microsoft からのオンライン技術コンテンツ更新プログラムを受け取ることができなくなります。 Microsoft Intune は、すべてのモバイル OS のサポートに基づいて、2020 年 8 月 10 日に Windows 10 Mobile アプリと Windows 10 Mobile オペレーティング システムの両方のポータル サイトのサポートを終了します。

8 月 10 日の時点で、Windows Phone 8.1 と Windows 10 Mobile デバイスの登録は失敗し、Windows Mobile のプロファイルの種類は Intune UI から削除されます。 登録済みのデバイスは Intune サービスにチェックインされなくなり、デバイスとポリシーのデータが削除されます。

### <a name="end-of-support-for-legacy-pc-management"></a>従来の PC 管理のサポート終了

従来の PC 管理は 2020 年 10 月 15 日にサポートが終了します。 デバイスを Windows 10 にアップグレードし、Intune による管理が継続されるようにモバイル デバイス管理 (MDM) デバイスとして再登録してください。

[詳細情報](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Intune のすべての管理を Microsoft Endpoint Manager 管理センターに移行する
今年 3 月に掲載された MC208118 で、Microsoft Endpoint Manager での Intune 管理のための新しい簡単な URL ([https://endpoint.microsoft.com](https://endpoint.microsoft.com)) が発表されました。 Microsoft Endpoint Manager は、Microsoft Intune と Configuration Manager を含む統合プラットフォームです。 **2020 年 8 月 1 日以降**、[https://portal.azure.com](https://portal.azure.com) での Intune の管理を削除します。代わりに、すべてのエンドポイント管理に [https://endpoint.microsoft.com](https://endpoint.microsoft.com) をご使用になることをお勧めします。 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Android デバイス管理者のサポートの縮小<!--7371518-->
Android デバイス管理者の管理は、Android デバイスを管理する方法の 1 つとして Android 2.2 でリリースされました。 その後、Android 5 で、より最新の管理フレームワークである [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (Google Mobile Services に確実に接続できるデバイス向け) がリリースされました。 Google は、新しい Android リリースでのデバイス管理者の管理サポートを縮小して、管理を移行することを奨励しています。

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響
Google によるこれらの変更により、2020 年 10 月には、影響を受ける、デバイス管理者によって管理されるデバイスで、広範な管理機能を使用できなくなります。 

> [!NOTE]
> 以前、この日付は 2020 年第 4 四半期と伝えられていましたが、[Google の最新情報](https://www.blog.google/products/android-enterprise/da-migration/)によると変更されています。

##### <a name="device-types-that-will-be-impacted"></a>影響を受けるデバイスの種類
デバイス管理者のサポート縮小によって影響を受けるデバイスは、次の 3 つの条件すべてに該当するデバイスです。
- デバイス管理者の管理に登録されている。
- Android 10 以降が実行されている。
- Samsung を除く、すべての Android 製造元。

次のいずれかに該当するデバイスは影響を受けません。
- デバイス管理者の管理に登録されていない。
- Android 10 より下のバージョンの Android が実行されている。
- Samsung デバイスである。 Samsung Knox デバイスは、この時間枠内に影響を受けることはありません。これは、Intune と Knox プラットフォームとの統合によって延長サポートが提供されるためです。 このため、Samsung デバイスについては、デバイス管理者の管理を移行するまで時間的な余裕があり、十分な計画を立てることができます。

##### <a name="settings-that-will-be-impacted"></a>影響を受ける設定
[Google がデバイス管理者のサポートを縮小](https://developers.google.com/android/work/device-admin-deprecation)することによって、次の設定の構成が、影響を受けるデバイスに適用されなくなります。

###### <a name="configuration-profile-device-restriction-settings"></a>構成プロファイルのデバイス制限の設定

- **カメラ**のブロック
- **[パスワードの最小文字数]** の設定
- **[デバイスがワイプされるまでのサインイン失敗回数]** の設定 (パスワードを設定していないデバイスは該当しませんが、パスワードを設定しているデバイスは該当します)
- **[パスワードの有効期限 (日数)]** の設定
- **[必要なパスワードの種類]** の設定
- **[以前のパスワードを再利用できないようにする]** の設定
- **Smart Lock などの信頼できるエージェント**のブロック

###### <a name="compliance-policy-settings"></a>コンプライアンス ポリシーの設定

- **[必要なパスワードの種類]** の設定
- **[パスワードの最小文字数]** の設定
- **[パスワードの有効期限が切れるまでの日数]** の設定
- **[再使用を禁止するパスワード世代数]** の設定


![[Android コンプライアンス ポリシー] ページのスクリーンショット](../fundamentals/media/notices/android-compliance-settings.png)

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>影響を受けるデバイスの影響を受ける設定のユーザー エクスペリエンス

影響を受ける構成設定:
- 既に登録済みで、設定が既に適用されているデバイスについては、影響を受ける構成設定が引き続き適用されます。
- 新たに登録されるデバイス、新しく割り当てられる設定、更新された設定については、影響を受ける構成設定が適用されません (ただし、他のすべての構成設定は適用されます)。

影響を受けるコンプライアンス設定:
- 既に登録済みで、設定が既に適用されているデバイスについては、影響を受けるコンプライアンス設定が、コンプライアンス違反の理由として [デバイスの更新設定] ページに表示され、デバイスはコンプライアンスに準拠しなくなります。さらに、設定アプリでは、パスワード要件が引き続き適用されます。
- 新たに登録されるデバイス、新しく割り当てられる設定、更新された設定については、影響を受けるコンプライアンス設定が、コンプライアンス違反の理由として [デバイスの更新設定] ページに表示され、デバイスはコンプライアンスに対応していませんが、設定アプリでは、より厳格なパスワード要件が適用されることはありません。

Wi-Fi プロファイルに対する追加のユーザー エクスペリエンスの変更
- ユーザーは追加のアクセス許可を付与し、展開時に Wi-Fi 構成を明示的に受け入れる必要があります。 Wi-Fi の構成は、既知の Wi-Fi ネットワークの一覧には表示されませんが、範囲内の場合は自動的に接続されます。 既存の Wi-Fi プロファイルに対する動作の変更はありません。 エンドポイント マネージャー管理センターでの管理者エクスペリエンスにも変更はありません。  

#### <a name="cause-of-impact"></a>影響の原因 
デバイスへの影響が出始めるのは、2020 年 10 月からです。 そのときに、([Google の要求に応じて](https://www.blog.google/products/android-enterprise/da-migration/)) ポータル サイト API のターゲットをレベル 28 からレベル 29 に上げるポータル サイト アプリの更新があります。 

その時点で、ユーザーが次の両方のアクションを完了すると、デバイス管理者によって管理されるデバイスで、Samsung 製以外のものは影響を受けることになります。
- Android 10 以降に更新する。
- ポータル サイト アプリを、API レベル 29 を対象とするバージョンに更新する。

#### <a name="additional-impacts-based-on-android-os-version"></a>Android OS のバージョンに基づくその他の影響 
**Android 10**:  Google では、Android 10 以降が実行されているすべてのデバイス管理者のマネージド デバイス (Samsung を含む) に対して、ポータル サイトなどのデバイス管理者の管理エージェントによってデバイス識別子の情報にアクセスする機能を制限しています。 この制限により、Android 10 以降にデバイスを更新すると、次の Intune 機能が影響を受けます。 
- VPN のネットワーク アクセス制御が機能しなくなる 
- IMEI またはシリアル番号を使用した企業所有のデバイスの識別で、デバイスが企業所有として自動的にマークされなくなる 
- Intune で IT 管理者に IMEI とシリアル番号が表示されなくなる 

**Android 11**: Android 11 に更新した場合、デバイス管理者のマネージド デバイスに影響を与える変更は次のとおりです。 
- Google では、Android 11 以降が実行されているデバイス管理者のデバイス (Samsung を除く) に対して、ポータル サイト アプリへの 10 月の更新より前に、ポータル サイトなどの管理エージェントによってカメラのブロックを強制する機能を削除しました。 Android 11 に更新する前にデバイスに適用されているカメラをブロックするポリシーは、引き続き適用されます。  
- Android 11 では、信頼されたルート証明書は、デバイス管理者で登録されたデバイスに展開できなくなりました (Samsung デバイスを除く)。 ユーザーは、信頼されたルート証明書をデバイスに手動でインストールする必要があります。 信頼されたルート証明書をデバイスに手動でインストールすると、SCEP を使用して、デバイスに証明書をプロビジョニングできます。 このシナリオでも、信頼された証明書ポリシーを作成してデバイスに展開し、そのポリシーを SCEP 証明書プロファイルにリンクする必要があります。 
    - 信頼されたルート証明書がデバイス上にある場合、SCEP 証明書プロファイルは正常にインストールされます。  
    - 信頼された証明書が見つからない場合、SCEP 証明書プロファイルは失敗します。 


#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備
2020 年 10 月に実施される機能の縮小を回避するために、次のことをお勧めします。
- **新規登録**: 新しいデバイスを [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理 (利用可能な場合) および[アプリ保護ポリシー](../apps/app-protection-policies.md)にオンボードします。 新しいデバイスをデバイス管理者の管理にオンボードしないようにしてください。 
- **以前に登録されたデバイス**: デバイス管理者によって管理されているデバイスが Android 10 以降を実行している場合、または Android 10 以降に更新する可能性がある場合 (特に Samsung デバイスではない場合)、そのデバイスをデバイス管理者の管理から [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理または[アプリ保護ポリシー](../apps/app-protection-policies.md)に移行します。 [Android デバイスをデバイス管理者から仕事用プロファイル管理に移動する](../enrollment/android-move-device-admin-work-profile.md)には、合理化されたフローを利用できます。
- **パスワードの複雑さを構成する**: 影響を受ける Android 10 以降が実行されているデバイスの場合、パスワードの複雑さと呼ばれる今後の設定によって、パスワードの制限とコンプライアンスを引き続き適用できます。 パスワードの複雑さは、パスワードの種類、長さ、品質を考慮に入れるパスワードの強度を測定するものです。

#### <a name="what-if-i-have-non-samsung-devices-that-cannot-move-to-android-enterprise"></a>Android Enterprise に移行できない Samsung 以外のデバイスがある場合はどうすればよいですか? 
一部のデバイスでは、デバイス管理者から Android Enterprise 管理に移行できません。 たとえば、[Google は Android Enterprise を一部の市場では利用できなくしています](https://support.google.com/work/android/answer/6270910?hl=en)。 デバイス管理者で Samsung 以外のデバイスを管理するために、引き続き Intune を使用できますが、この投稿で言及されている機能への変更が適用されます。 Android Enterprise が使用できない場合のデバイス管理に関するガイダンスについては、「[Google Mobile Services のない環境で Intune を使用する方法](../apps/manage-without-gms.md)」を参照してください。 


#### <a name="additional-information"></a>追加情報
- [Android デバイスをデバイス管理者から仕事用プロファイル管理に移動する](../enrollment/android-move-device-admin-work-profile.md)
- [Android Enterprise 仕事用プロファイル デバイスの登録を設定する](../enrollment/android-work-profile-enroll.md)
- [Android Enterprise 専用デバイスの登録を設定する](../enrollment/android-kiosk-enroll.md)
- [Android Enterprise フル マネージド デバイスの Intune 登録を設定する](../enrollment/android-fully-managed-enroll.md)
- [アプリ保護ポリシーを作成して割り当てる方法](../apps/app-protection-policies.md)
- [Google Mobile Services のない環境で Intune を使用する方法](../apps/manage-without-gms.md)
- [Android エンタープライズ デバイス上のアプリケーション保護ポリシーと仕事用プロファイルの概要](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [デバイス管理者機能の廃止について知っておく必要があることに関する Google のブログ](https://www.blog.google/products/android-enterprise/da-migration/)
- [デバイス管理者から Android Enterprise への移行に関する Google のガイダンス](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [非推奨のデバイス管理者 API に関する Google のドキュメント](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>変更の計画: Apple の iOS/iPadOS 向け Automated Device Enrollment のための Intune 登録フローの更新
7 月のポータル サイト リリースでは、Apple の Automated Device Enrollment (旧称 DEP) の iOS/iPadOS 登録フローを変更する予定です。 登録フローの変更は、[ユーザー アフィニティに登録する] フローでのみ発生します。 以前は、構成の一部として [ポータル サイトのインストール] を [いいえ] に設定しても、ユーザーはストアからポータル サイト アプリをインストールでき、その後、登録がトリガーされ、ユーザーは適切なシリアル番号を追加することができました。 この次回のポータル サイト リリースでは、そのシリアル番号確認画面を削除する予定です。 代わりに、対応するアプリ構成ポリシーを作成し、ポータル サイトと一緒に送信して、ユーザーが無事に登録できるようにするか、または構成の一部として [ポータル サイトのインストール] を [はい] に設定することをお勧めします。 
 - 詳細については、[こちら](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629)の投稿記事を参照してください。
