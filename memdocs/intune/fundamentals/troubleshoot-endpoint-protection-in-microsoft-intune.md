---
title: Intune での一般的なエンドポイント保護メッセージ - Azure | Microsoft Docs
description: Microsoft Intune でエンドポイント保護と Microsoft Defender を使用し、トラブルシューティングする際の一般的なメッセージと考えられる解決方法について説明します。
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e31df2d2-bb1b-491b-9a71-04e0b18829c1
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 16b7cc65ae043fb48b7f500bfcd65195c7ff7561
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79355700"
---
# <a name="endpoint-protection-issues-and-possible-solutions-in-microsoft-intune"></a>Microsoft Intune のエンドポイント保護の問題と考えられる解決方法

この記事では、いくつかのエラーと警告に対して考えられる原因と解決方法について説明します。 Endpoint Protection の使用中に発生した問題を解決するには、この情報を参考にしてください。

## <a name="microsoft-defender-error-codes"></a>Microsoft Defender のエラー コード

イベント ログとエラー コードを調べて [Microsoft Defender AV での問題をトラブルシューティング](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/troubleshoot-windows-defender-antivirus)します。

## <a name="common-intune-errors-and-possible-resolutions"></a>一般的な Intune のエラーと考えられる解決方法

### <a name="endpoint-protection-engine-unavailable"></a>Endpoint Protection エンジンを使用できません。

**考えられる原因**: Intune Endpoint Protection エンジンが壊れているか、削除されています。

**考えられる解決方法**:

- エンドポイント保護が破損しているか更新されない場合は、プログラムを更新するか再インストールします。
- 即時の更新を強制します。 エンドポイント保護クライアント プログラム (おそらくタスクバーにあります) で、 **[更新]** を選択します。
- [コントロール パネル] > [プログラム] で、 **[Microsoft Intune Endpoint Protection エージェント]** を選択します。 アプリケーションをアンインストールします。
- 次回更新プログラムを同期するときに、Microsoft Online Management 更新マネージャーが不足しているプログラムを検出し、スケジュールされているインストール時間にそのプログラムを再インストールします。

### <a name="features-are-disabled"></a>機能が無効になっている

一部の機能が無効になっているというメッセージが表示されることがあります。 これらのメッセージは、管理者が構成プロファイルを使用して Intune エンドポイント保護または Microsoft Defender を無効にした場合に発生することがあります。 または、デバイスのエンド ユーザーが無効にしています。 考えられるメッセージ:

`Endpoint Protection disabled`  
`Real-time protection disabled`  
`Download scanning disabled`  
`File and program activity monitoring disabled`  
`Behavior monitoring disabled`  
`Script scanning disabled`  
`Network Inspection System disabled`  

**考えられる解決方法**: これらの機能を有効にします。 ガイダンスについては、以下を参照してください。

- [エンドポイント保護設定を追加する](../protect/endpoint-protection-configure.md)
- [Microsoft Defender ウイルス対策](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)
- [エンド ユーザー: Windows Defender をオンにし、会社のリソースにアクセスする](../user-help/turn-on-defender-windows.md)

### <a name="malware-definitions-out-of-date"></a>マルウェア定義が最新ではない

このメッセージは、デバイスのマルウェア定義の更新が 14 日以上遅れた場合に表示されます。 たとえば、デバイスがインターネットから切断されているか、マルウェア定義が古くなっているかを示すメッセージが表示されることがあります。

**考えられる解決方法**: マルウェア定義が古い場合は、[Microsoft Defender ウイルス対策](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)を使用して定義を更新することができます。

### <a name="full-scan-overdue-or-quick-scan-overdue"></a>フル スキャンの期限が過ぎています、またクイック スキャンの期限が過ぎています

フル スキャンまたはクイック スキャンが 14 日間完了していません。 このシナリオは、フル スキャン中にデバイスが再起動した場合に発生する可能性があります。

**考えられる解決方法**: スキャンの期限が過ぎている場合は、1 回限りのスキャンを実行するか、定期的なスキャンのスケジュールを設定することができます。 「[Microsoft Defender ウイルス対策](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)」を参照してください。

### <a name="another-endpoint-protection-application-running"></a>別のエンドポイント保護アプリケーションが実行されています。

別のエンドポイント保護アプリケーションが実行されており、デバイスの状態は正常です。

**考えられる解決方法**: 別のエンドポイント保護アプリケーションがインストールされていて、Intune がそのアプリケーションを検出した場合、デバイスが不安定になる可能性があります。

## <a name="next-steps"></a>次のステップ

[Microsoft からサポート](get-support.md)を受けるか、[コミュニティ フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune)を使用します。
