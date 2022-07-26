---
lab:
  title: 19 - Azure AD Multi-Factor Authentication 登録ポリシーを構成する
  learning path: "02"
  module: Module 02 - Implement an Authentication and Access Management Solution
ms.openlocfilehash: 85aabb3ebb4f2b6a8261e6f804c536e7e6f5c3f9
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421325"
---
# <a name="lab-19---configure-an-azure-ad-multi-factor-authentication-registration-policy"></a>ラボ 19 - Azure AD Multi-Factor Authentication 登録ポリシーを構成する

## <a name="lab-scenario"></a>ラボのシナリオ

Azure AD Multi-Factor Authentication は、ユーザー名とパスワードに加えて、その他の要素を使用することでユーザーを確認する手段を提供します。 ユーザーのサインインに第 2 のセキュリティ層を提供します。ユーザーが MFA プロンプトに応答できるようにするには、まず Azure AD Multi-Factor Authentication に登録する必要があります。 Azure AD 組織の MFA 登録ポリシーがすべてのユーザーに割り当てられるように構成する必要があります。

#### <a name="estimated-time-5-minutes"></a>推定時間:5 分

### <a name="exercise-1---set-up-mfa-registration-policy"></a>演習 1 - MFA 登録ポリシーを設定する

#### <a name="task---policy-configuration"></a>タスク - ポリシーの構成

1. グローバル管理者アカウントを使用して、[https://portal.azure.com]( https://portal.azure.com) にサインインします。

2. ポータル メニューを開き、**[Azure Active Directory]** を選択します。

3. [Azure Active Directory] ブレードで、**[管理]** の下にある **[セキュリティ]** を選択します。

4. [セキュリティ] ブレードの左側のナビゲーションで **[ID 保護]** を選択します。

5. [ID 保護] ブレードの左側のナビゲーションで、**[MFA 登録ポリシー]** を選択します。

    ![参照パスが強調表示された [MFA 登録ポリシー] ページを表示する画面イメージ](./media/lp2-mod4-browse-to-mfa-registration-policy.png)

6. **[割り当て]** で:

7. **[割り当て]** で、**[すべてのユーザー]** を選択し、使用可能なオプションを確認します。

8. **[すべてのユーザー]** を選択するか、ロールアウトを制限する場合は **[個人と グループの選択]** を選択します。

9. また、ポリシーからユーザーを除外することもできます。

10. **[コントロール]** で、**[Require Azure AD MFA registration]\(Azure AD MFA の登録が必要\)** が選択されていて、変更できないことに注意してください。

11. **[ポリシーを適用する]** で、 **[オン]** を選択してから **[保存]** を選択します。
