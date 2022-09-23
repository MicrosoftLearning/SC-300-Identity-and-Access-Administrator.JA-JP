---
lab:
  title: 27 - Azure AD データ ソースの Microsoft Sentinel Kusto クエリ
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: eac2b28212e21982e38208936be912ebd1f22f85
ms.sourcegitcommit: 80c5c0ef60c1d74fcc58c034fe6be67623013cc0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2022
ms.locfileid: "146823233"
---
# <a name="lab-27---microsoft-sentinel-kusto-queries-for-azure-ad-data-sources"></a>ラボ 27 - Azure AD データ ソースの Microsoft Sentinel Kusto クエリ

**注** - このラボでは Azure Pass が必要です。 手順については、ラボ 00 を参照してください。

## <a name="lab-scenario"></a>ラボのシナリオ

Microsoft Sentinel は、スケーラブルでクラウドネイティブの SIEM および SOAR ソリューションです。  Microsoft とサードパーティのセキュリティ ソリューションからデータ ソースを接続すると、セキュリティ操作タスクを実行できます。  このラボ演習では、Kusto 照会言語 (KQL) を使用してハンティング クエリを実行するための Azure AD へのデータ コネクタを備えた Microsoft Sentinel ワークスペースを作成します。 

#### <a name="estimated-time-30-minutes"></a>予想所要時間: 30 分

### <a name="exercise-1---configure-microsoft-sentinel-for-kusto-queries"></a>演習 1 - Kusto クエリ用に Microsoft Sentinel を構成する

#### <a name="task-1---create-a-microsoft-sentinel-workspace"></a>タスク 1 - Microsoft Sentinel ワークスペースを作成する

1. グローバル管理者として [https://portal.azure.com](https://portal.azure.com) にサインインします。

1. **Microsoft Sentinel** を検索して選択します。 

1. **[Create Microsoft Sentinel](Microsoft Azure Sentinel の作成)** を選択します。

1. **[ワークスペースへの Microsoft Sentinel の追加]** タイルで、 **[新しいワークスペースの作成]** を選択します。

1. **[リソース グループ]** で、 **[新規作成]** を選択し、「**Sentinel-RG**」と入力します。

1. ワークスペースに名前を付けます。  例 - SentinelLogAnalytics。

1. お近くのリージョンを選択します。

1. **[確認および作成]** 、 **[作成]** の順に選択します。

1. Log Analytics ワークスペースのデプロイが完了したら、ワークスペースを選択し、 **[追加]** を選択します。  これにより、ワークスペースが Microsoft Sentinel に追加され、Microsoft Sentinel が開きます。

1. ダイアログが表示されたら、 **[OK]** を選択して Microsoft Sentinel の無料試用版をアクティブにします。

#### <a name="task-2---add-azure-ad-as-a-data-source"></a>タスク 2 - Azure AD をデータ ソースとして追加する

1. **Microsoft Sentinel** で、メニューの **[構成]** に移動し、 **[データ コネクタ]** を選択します。

1. データ コネクタのリストで、**Azure Active Directory** を見つけて選択します。

1. 右側にプレビュー タイルが開きます。  **[Open connector page]\(コネクタ ページを開く\)** を選択します。

1. コネクタ ページに、データ コネクタの手順と次のステップが提供されます。 **構成** を続行するための各 **前提条件** の横にチェック マークがあることを確認します。

1. **[構成]** で、 **[サインイン ログ]** と **[監査ログ]** のチェック ボックスをオンにします。 追加のログ ソースを利用できますが、現在 **プレビュー** 段階であり、このコースの対象外です。

1. **[変更の適用]** を選択します。 

1. 変更が正常に適用されたことを示す通知が表示されます。 コネクタ ページの右上にある **[X]** を選択して、**Microsoft Sentinel** ワークスペースに移動します。

1. **[Microsoft Sentinel | データ コネクタ]** タイルで **[更新]** を選択すると、数値 1 が **[接続済み]** の数に表示されます。

   **注** - Azure AD データ コネクタがアクティブな数で表示されるまでに数分かかる場合があります。 

#### <a name="task-3---run-kusto-query-on-user-activity"></a>タスク 3 - ユーザー アクティビティで Kusto クエリを実行する

1. **Microsoft Sentinel** で、 **[全般]** メニュー見出しの下にある **[ログ]** に移動します。

1. **[Log Analytics へようこそ]** ウィンドウを閉じます。

1. サンプル クエリが表示されているウィンドウが開き、 **[監査]** を選択し、スクロールして **[ユーザー ID]** を検索します。

1. **[実行]** を選択します。 

1. これにより、Azure AD 上のユーザー ID のリストが提供されます。  ワークスペースを作成したばかりのため、結果が表示されない場合があります。  クエリの形式に注意してください。

1. メニューの **[脅威の管理]** で **[ハンティング]** を選択します。 

1. 下にスクロールして、 **[ユーザー アカウントと認証アプリケーションによる異常なサインインの場所]** を見つけます。  Azure Active Directory サインインに対するこのクエリでは、各 Azure Active Directory アプリケーションのすべてのユーザー サインインが考慮され、個々のアプリケーション内のユーザーの場所プロファイルから最も異常な変更が選択されます。 この意図は、特定のアプリケーション ベクターを使用して、ユーザー アカウントの侵害を検出することです。 

1. **[クエリ結果の表示]** を選択してクエリを実行します。

1. 新しいワークスペースでは結果が得られない場合がありますが、情報を収集したり、潜在的な脅威を追及したりするためにクエリを実行する方法を確認できました。
