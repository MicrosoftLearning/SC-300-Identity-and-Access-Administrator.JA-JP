---
lab:
  title: 20 - アプリのアクセス管理を実装する
  learning path: "03"
  module: Module 03 - Implement Access Management for Apps
ms.openlocfilehash: aec13b1f1279cb8ca17885306ef97e20e337a97d
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421385"
---
# <a name="lab-20---implement-access-management-for-apps"></a>ラボ 20 - アプリのアクセス管理を実装する

## <a name="lab-scenario"></a>ラボのシナリオ

組織では、特定のユーザーまたはグループのみがエンタープライズ アプリケーションにアクセスできる必要があります。 ユーザーを特定のアプリケーションに割り当てる必要があります。

#### <a name="estimated-time-5-minutes"></a>推定時間:5 分

### <a name="exercise-1---configure-and-enterprise-app"></a>演習 1 - Enterprise アプリを構成する

#### <a name="task-1---add-an-app-to-your-azure-ad-tenant"></a>タスク 1 - Azure AD テナントにアプリを追加する

1. グローバル管理者アカウントを使用して、[https://portal.azure.com](https://portal.azure.com) にサインインします。

2. ポータル メニューを開き、**[Azure Active Directory]** を選択します。

3. [Azure Active Directory] ブレードの **[管理]** で **[エンタープライズ アプリケーション]** を選択します。

4. [エンタープライズ アプリケーション] ウィンドウで **[+ 新しいアプリケーション]** を選択します。

    ![「新しいアプリケーション」が強調表示された「エンタープライズ アプリケーション」ブレードが表示されている画面イメージ](./media/lp3-mod1-new-enterprise-application.png)

5. [Azure AD ギャラリー (プレビュー) の参照] ブレードの **[アプリケーションの検索]** ボックスに「**GitHub**」と入力します。

    ![検索ボックスが強調表示されている「Azure AD ギャラリーの参照 (プレビュー)」ブレードが表示されている画面イメージ](./media/lp3-mod1-azure-ad-gallery-search.png)

6. 結果から **[GitHub Enterprise Cloud - エンタープライズ アカウント]** を選択します。

7. **[GitHub Enterprise Cloud - エンタープライズ アカウント]** で設定を確認し、**[作成]** を選択します。

8. 作成されると、「GitHub Enterprise Cloud – エンタープライズ アカウント」ブレードにリダイレクトされます。

#### <a name="task-2---assign-users-to-an-app"></a>タスク 2 - アプリにユーザーを割り当てる

1. [GitHub Enterprise Cloud - エンタープライズ アカウント] ブレードの [概要] ページで、**[はじめに]** の下にある **[1.ユーザーとグループの割り当て]** を選択します。

2. または、左側のナビゲーションの **[管理]** で **[ユーザーとグループ]** を選択できます。

3. [ユーザーとグループ] ページで、メニューから **[+ ユーザー/グループの追加]** を選択します。

4. [Add Assignment (割り当ての追加)] ブレードで **[ユーザーとグループ]** を選択します。

5. 「ユーザーとグループ」ウィンドウで、管理者アカウント、 **「選択」** の順に選択します。

    ![「選択」ボタンが強調表示されている、アプリへのユーザー アカウント割り当ての追加を表示している画面イメージ ](./media/lp3-mod1-add-app-assignment.png)

6. **[割り当て]** を選択します。
