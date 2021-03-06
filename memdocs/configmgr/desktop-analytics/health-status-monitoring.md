---
title: 正常性状態の監視
titleSuffix: Configuration Manager
description: Desktop Analytics での正常性状態の監視のしくみについて説明します。
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b4663ca5640bcfea4338912ff471a3253b744d5f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125833"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Desktop Analytics での正常性状態の監視

[運用環境に更新プログラムを展開する](deploy-prod.md)ときに、Desktop Analytics を使用して、デバイスの正常性状態を監視できます。 この記事では、正常性監視のしくみについて詳しく説明します。

この機能の使用方法の詳細については、「[更新されたデバイスの正常性の監視](deploy-prod.md#bkmk_monitor)」を参照してください。

![Desktop Analytics の [正常性の監視] ページのスクリーンショット](media/monitor-health.png)

> [!NOTE]  
> Desktop Analytics を使用すると、分母として使用できる使用状況データを提供するデバイスから正常性データのみが収集されます。 これは、診断データを [省略可能 (制限あり)] レベルで共有するように設定されていない Windows 7 と Windows 10 を実行中のデバイスは含まれないことを意味します。 Windows 10 を実行中のデバイスのうち、診断データを [省略可能 (制限あり)] 以外のレベルで共有するように設定されているデバイスが 10% を超える場合、 **[モニターの正常性]** ページのバナー領域に警告が表示されます。  

特定のアプリに関する詳細情報を表示するには、一覧から選択します。

## <a name="apps"></a>アプリ

### <a name="health-status-factors"></a>正常性状態の要因

![Desktop Analytics でのアプリの正常性状態の要因](media/monitor-health-status-factors.png)

Desktop Analytics を使用すると、アプリの次の正常性状態の要因が監視されます。

- **クラッシュが発生したデバイスの割合 (%)** :過去 2 週間でこの特定のアプリがクラッシュしたデバイスの数を、アプリが使用されているデバイスの数で除算したもの。 このビューによって、新しい OS バージョンでアプリの安定性が向上しているか低下しているかどうかを確認できます。 Desktop Analytics では、次のセットについてこの割合が計算されます。  

  - **更新後**:展開計画で指定されているターゲット OS バージョンに更新済みのデバイス。 データ不足の資産の数を減らすために、Desktop Analytics によって、更新済みのすべてのデバイスでこのデータが収集されます。 このセットには、展開計画に含まれていないデバイスも含まれます。  

  - **更新前**:展開計画に指定されているものよりも前の OS バージョン上のデバイス。 この一覧には、Windows 7 を実行中のデバイスは含まれません。  

  - **商用 ID**: すべての商用デバイスでの平均クラッシュ率。 この平均は、アプリの "*すべての*" バージョンにわたって計算されます。 バージョンのクラッシュ率が商用平均を上回っている場合は、より安定したバージョンを使用できる可能性があります。  

- **クラッシュが発生したセッションの割合 (%)** :前のものと似ていますが、過去 2 週間にクラッシュしたセッションの割合がカウントされます。  

Desktop Analytics によってアプリの正常性状態を確認するには、少なくとも 20 台のデバイスのデータが必要です。 そうでない場合は、アプリの**データが不十分**であることが報告されます。 サービスでは、これらのデバイスからの "*セッションのクラッシュ率*" に基づいて、正常性状態が計算されます。 デバイスのクラッシュ率は、情報提供のみを目的としています。 正常性状態の計算では使用されません。

### <a name="usage"></a>使用方法

<!-- 5533890 -->

- **アクティブなデバイス**: この値は、ユーザーが選択されたアプリを過去 2 週間の間に起動したデバイスの数です。 これは、選択された展開プランにおいて Windows 10 の対象バージョンを実行しているデバイスに基づいています。

- **セッション**: この値は、Windows の対象バージョンにおいて、ユーザーが選択されたアプリを起動した合計回数です。

### <a name="additional-tabs"></a>その他のタブ

アプリの詳細ページの下部にある次の 3 つのタブを使用して、トラブルシューティングを行うことができます。

- **その他のバージョン**:このアプリの代替バージョンの一覧。 各バージョンについて、組織内のクラッシュ率と商用平均の相対的な変化が示されます。 アプリの新しいバージョンのほうがクラッシュ率が低いことがわかった場合は、アプリを更新すると有用である可能性があります。  

    また、バージョンに高度な分析情報があるかどうかも表示されます。 詳細については、「[互換性の評価](compat-assessment.md)」を参照してください。  

- **主要な問題**:インスタンス数別の最も頻繁に発生したエラー ID の一覧。 エラー ID によって、クラッシュに関連付けられているスタック トレースが識別されます。 アプリのベンダーに問い合わせてサポートを求めるときに、この ID を使用できます。  

- **最近のクラッシュ**:アプリが最近クラッシュしたデバイスの一覧。 エラー ID やその他の条件によってフィルター処理できます。 より広範な展開を試す前に、この情報を使用して特定のデバイスでのログの収集や修正を行って、問題をトラブルシューティングします。  

修正できない深刻な正常性の後退が見つかった場合は、アプリの **[アップグレードの決定]** を **[不可能]** に変更します。 この操作によって、この資産を使用しているデバイスに更新プログラムが展開されなくなります。

## <a name="see-also"></a>関連項目

- [Desktop Analytics での互換性評価](compat-assessment.md)  

- [Desktop Analytics を使用して運用環境に展開する方法](deploy-prod.md)  
