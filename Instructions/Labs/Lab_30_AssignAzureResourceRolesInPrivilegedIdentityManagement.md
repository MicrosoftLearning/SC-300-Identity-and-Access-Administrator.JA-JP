---
lab:
  title: オプション 30 - Privileged Identity Management で Azure リソース ロールを割り当てる演習を行う
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: 3baeb4982316d86e2717ca5c1f8cb8079c423585
ms.sourcegitcommit: a2dd8d3f669d7b7f1c97c87a5b01afd61eb36380
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2022
ms.locfileid: "141368739"
---
# <a name="lab-30---optional-assign-azure-resource-roles-in-privileged-identity-management"></a>ラボ 30 - オプション:Privileged Identity Management で Azure リソース ロールを割り当てる

## <a name="this-lab-requires-an-azure-pass-or-subscription-to-perform-which-is-currently-not-provided-with-the-course--apologies-for-any-incovenience--we-are-in-the-process-of-updating-the-labs-and-will-have-this-lab-reconfigured-in-the-next-few-weeks--thank-you-for-your-patience-and-understanding"></a>このラボを実行するには、Azure Pass またはサブスクリプションが必要ですが、現在のところはこのコースには含まれていません。  ご不便をおかけして申し訳ございません。  現在はラボの更新処理中であり、数週間以内にラボの再構成を完了する予定です。  何とぞご理解いただけますようお願い申し上げます。


## <a name="lab-scenario"></a>ラボのシナリオ

Azure Active Directory (Azure AD) Privileged Identity Management (PIM) では、組み込みの Azure リソース ロールと、以下を含むカスタム ロール (ただしこれらに限定されません) を管理できます。

- 所有者
- User Access Administrator
- Contributor
- セキュリティ管理者
- Security Manager

ユーザーを Azure リソース ロールの候補にする必要があります。

#### <a name="estimated-time-10-minutes"></a>推定時間:10 分

### <a name="exercise-1---pim-with-azure-resources"></a>演習 1 - Azure AD リソースを使用した PIM

#### <a name="task-1---assign-azure-resource-roles"></a>タスク 1 - Azure リソース ロールを割り当てる

1. 全体管理者アカウントを使用して、[https://portal.azure.com](https://portal.azure.com) にサインインします。

2. **[Azure AD Privileged Identity Management]** を検索してから選択します。

3. [Privileged Identity Management] ブレードの左側のナビゲーションで **[Azure リソース]** を選択します。

4. 上部のメニューで **[リソースの探索]** を選択します。

5. [Azure リソース - 検出] ブレードでサブスクリプションを選択し、上部のメニューで **[リソースの管理]** を選択します。

    ![サブスクリプションとリソースの管理が強調表示されている [Azure リソース - 検出] ブレードを表示している画面イメージ](./media/lp4-mod3-pim-azure-resource-management.png)

6. **[管理用に選択したリソースのオンボード]** ダイアログ ボックスで情報を確認し、**[OK]** を選択します。

7. オンボードが完了したら、[Azure リソース - 検出] ブレードを閉じます。

8. [Azure リソース] ブレードで、サブスクリプションを選びます。

    ![最近追加された Azure リソースを表示している画面イメージ](./media/lp4-mod3-pim-az-resource-overview.png)

9. 左側のナビゲーション メニューで、**[管理]** の下にある **[ロール]** を選択して、Azure リソースのロールの一覧を表示します。

10. 上部のメニューで **[+ 割り当ての追加]** を選択します。

11. [割り当ての追加] ブレードで、**[ロールの選択]** メニューを選択し、**[API Management サービス共同作成者]** を選択します。

12. **[メンバーの選択]** で **[メンバーが選択されていません]** を選択します。

13. ロールを割り当てる組織から **[Miriam Graham]** を選択します。  次に、**[選択]** を選択します。

14. **[次へ]** を選択します。

15. **[設定]** タブの **[割り当ての種類]** で **[対象]** を選択します。

    - **[対象]** 割り当ての場合、このロールのメンバーは、ロールを使用するにはアクションを実行する必要があります。 要求されるアクションには、多要素認証 (MFA) チェックの実行、業務上の妥当性の指定、指定された承認者に対する承認要求などがあります。

    - **アクティブ** 割り当てでは、メンバーがロールを使用するためのアクションを実行する必要はありません。 アクティブとして割り当てられたメンバーには常に、そのロールに割り当てられた特権があります。

16. 開始日時と終了日時を変更して割り当て期間を指定します。

17. 完了したら、 **[割り当て]** を選択します。

18. 新しいロールの割り当てが作成されると、状態の通知が表示されます。

#### <a name="task-2---update-or-remove-an-existing-resource-role-assignment"></a>タスク 2 - 既存のリソースのロールの割り当てを更新または削除する

既存のロールの割り当てを更新または削除するには、次の手順を実行します。

1. **[Azure AD Privileged Identity Management]** を開きます。

2. **[Azure リソース]** を選択します。

3. 管理するサブスクリプションを選択して、その概要ページを開きます。

4. **[管理]** で、 **[割り当て]** を選択します。

5. **[対象ロール]** タブの [操作] 列で、使用可能なオプションを確認します。

6. **[削除]** を選択します。

7. **[削除]** ダイアログ ボックスで情報を確認し、**[はい]** を選択します。
