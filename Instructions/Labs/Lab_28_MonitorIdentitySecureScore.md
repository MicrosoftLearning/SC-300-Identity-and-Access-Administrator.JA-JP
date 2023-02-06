---
lab:
  title: 28 - ID セキュリティ スコアを使用してセキュリティ態勢を監視および管理する
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: 14a8a2a123429f44b84ea45284f34a04bac6aa81
ms.sourcegitcommit: b5fc07c53b5663eaa1883cf38b70c57cd88470ca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "146741691"
---
# <a name="lab-28---monitor-and-managed-security-posture-with-identity-secure-score"></a>ラボ 28 - ID セキュリティ スコアを使用してセキュリティ態勢を監視および管理する

## <a name="lab-scenario"></a>ラボのシナリオ

Azure AD Identity Protection では、ID ベースのリスクに対する自動検出と修復を提供し、潜在的なリスクを調査するためのデータをポータルに提供します。 Azure AD Identity Protection には、ID セキュリティ体制を監視および改善するための ID セキュリティ スコアも用意されています。  ID セキュリティ スコアでは、Microsoft 365 Defender や Microsoft Defender for Cloud と同じ方法で、改善処置および推奨事項を提供することで、Azure Active Directory における ID の全体的なセキュリティ態勢を改善できるようにしています。  このラボでは、この機能について説明します。 

#### <a name="estimated-time-15-minutes"></a>推定時間:15 分

### <a name="exercise-1---using-identity-secure-score-to-monitor-and-manage-identity-security-posture"></a>演習 1 - ID セキュリティ スコアを使用して ID セキュリティ態勢を監視および管理する

#### <a name="task-1---review-identity-secure-score-and-improvement-actions"></a>タスク 1 - ID のセキュリティ スコアと改善処置を確認する

1. グローバル管理者として [https://portal.azure.com](https://portal.azure.com) にサインインします。

1. **[Azure AD Identity Protection]** を検索してから選択します。

1. **[概要]** タイルには、 **[ID セキュリティ スコア]** が表示されます。

1. **[ID セキュリティ スコア]** を選択します。  これにより、[ID セキュリティ スコア] ダッシュボードが表示されます。

1. 下にスクロールして、 **[改善アクション]** を表示します。

1. これらの改善処置は、Microsoft Defender for Cloud および Microsoft 365 Defender での改善処置とは対照的であり、ID に固有のものとなります。  これにより、セキュリティ態勢管理に対する潜在的な処置に焦点を絞った一覧が提供されます。  この一覧から開始された改善処置は、テナントの全体的なセキュリティ態勢にも影響します。 

#### <a name="task-2---execute-an-improvement-action"></a>タスク 2 - 改善処置を実行する

1. ID セキュリティ態勢の 1 つの領域を改善するには、 **[サインイン リスク ポリシーを有効にする]** を選択します。

1. 開いたタイルで下にスクロールし、 **[はじめに]** を選択します。

1. **Identity Protection | サインイン リスク ポリシー**。新しいタブが開きます。

1. **[割り当て]** で **[すべてのユーザー]** を選択します。

1. **[サインイン リスク]** で、 **[中以上]** を選択します。

1. **[コントロール]** で **[許可]**  -  **[多要素認証を要求する]** を選択します。

1. **[ポリシーの適用]** を **[オン]** にし、 **[保存]** を選択します。

1. サインイン リスク ポリシーを作成済みですが、ここで、ID セキュリティ スコアを上げる必要が生じました。  これが ID セキュア スコアに影響を与えるようになるまで最大 24 時間かかります。

1. その他の改善処置と、それらを作成して有効にする手順を確認します。


