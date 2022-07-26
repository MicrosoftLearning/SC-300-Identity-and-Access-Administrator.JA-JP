---
lab:
  title: 28 - Azure AD ロール用に Privileged Identity Management を構成する
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: 533faf01ba4aab1bd40c76cb9e787c8a731be0ac
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421316"
---
# <a name="lab-28-configure-privileged-identity-management-for-azure-ad-roles"></a>ラボ 28:Azure AD ロール用に Privileged Identity Management を構成する

## <a name="lab-scenario"></a>ラボのシナリオ

特権ロール管理者は、ロール候補の割り当てをアクティブ化しているユーザーの操作性を変更するなど、Azure Active Directory (Azure AD) 組織の Privileged Identity Management (PIM) をカスタマイズできます。 PIM の構成について理解する必要があります。

#### <a name="estimated-time-15-minutes"></a>推定時間:15 分

### <a name="exercise-1---configure-azure-ad-role-settings"></a>演習 1 - Azure AD ロールの設定を構成する

#### <a name="task-1---open-role-settings"></a>タスク 1 - ロールの設定を開く

次の手順を実行して、Azure AD ロールの設定を開きます。

1. [https://portal.azure.com](https://portal.azure.com) にグローバル管理者としてサインインします。

2. **[Azure AD Privileged Identity Management]** を検索してから選択します。

3. [Privileged Identity Management] ブレードの左側のナビゲーションで **[Azure AD ロール]** を選択します。

4. [クイック スタート] ページの左側のナビゲーションで **[設定]** を選択します。

    ![[設定] メニューが強調表示された [Azure AD ロール] ページを表示している画面イメージ](./media/lp3-mod3-pim-ad-roles-settings.png)

5. ロールの一覧を確認してから、**[ロール名で検索]** に「**コンプライアンス**」と入力します。

6. 結果から **[コンプライアンス管理者]** を選択します。

7. ロール設定の詳細情報を確認します。

#### <a name="task-2---require-approval-to-activate"></a>タスク 2 - 有効化の承認を要件とする

複数の承認者を設定した場合、承認は、承認者が 1 人でも承認または拒否すると直ちに完了します。 2 人以上のユーザーからの承認を要求することはできません。 ロールをアクティブ化するために承認を必須にする場合は、次の手順を実行します。

1. [ロール設定の詳細] ページの上部のメニューで **[編集]** を選択します。

    ![[ロール設定の詳細 - コンプライアンス管理者] ページの上部の [編集] が強調表示されている画面イメージ](./media/lp4-mod3-pim-edit-compliance-role.png)

2. [ロール設定の編集 - コンプライアンス管理者] ブレードで **[アクティブ化には承認が必要です]** チェックボックスをオンにします。

3. **[承認者の選択]** を選択します。

4. [メンバーの選択] ウィンドウで管理者アカウントを選択し、**[選択]** を選択します。

    ![[ロール設定の編集] ブレードと、選択したメンバーが強調表示された [メンバーの選択] ウィンドウを表示している画面イメージ](./media/lp4-mod3-pim-add-approver.png)

5. ロール設定を構成したら、 **[更新]** を選択して変更を保存します。
