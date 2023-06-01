---
lab:
  title: 15 - Azure AD の多要素認証登録ポリシーを構成する
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# ラボ 15 - Azure AD の多要素認証登録ポリシーを構成する

## ラボのシナリオ

Azure AD Multi-Factor Authentication は、ユーザー名とパスワードに加えて、その他の要素を使用することでユーザーを確認する手段を提供します。 ユーザーのサインインに第 2 のセキュリティ層を提供します。ユーザーが MFA プロンプトに応答できるようにするには、まず Azure AD Multi-Factor Authentication に登録する必要があります。 Azure AD 組織の MFA 登録ポリシーがすべてのユーザーに割り当てられるように構成する必要があります。

#### 推定時間:10 分

### 演習 1 - MFA 登録ポリシーを設定する

#### タスク 1 - ポリシーの構成

1. グローバル管理者アカウントを使用して、[https://portal.azure.com]( https://portal.azure.com) にサインインします。

2. ポータル メニューを開いてから、 **[Azure Active Directory]** を選択します。

3. [Azure Active Directory] ページで、 **[管理]** の下にある **[セキュリティ]** を選択します。

4. [セキュリティ] ページの左側のナビゲーションで **[Identity Protection]** を選択します。

5. [Identity Protection] ページの左側のナビゲーションで、 **[保護]** の下にある **[多要素認証登録ポリシー]** を選択します。

    ![参照パスが強調表示された [MFA 登録ポリシー] ページを表示する画面イメージ](./media/lp2-mod4-browse-to-mfa-registration-policy.png)

6. **[割り当て]** で:

7. **[割り当て]** で、**[すべてのユーザー]** を選択し、使用可能なオプションを確認します。

8. **[すべてのユーザー]** を選択するか、ロールアウトを制限する場合は **[個人と グループの選択]** を選択します。

9. また、ポリシーからユーザーを除外することもできます。

10. **[コントロール]** で、**[Require Azure AD MFA registration](Azure AD MFA の登録が必要)** が選択されていて、変更できないことに注意してください。


#### タスク 2 - MFA 登録用に Azure AD Identity Protection ポリシーを構成する

**注**:Azure AD Identity Protection では、Azure AD Premium P2 をアクティブにする必要があります。 

1. Azure portal で、検索バーで **[Azure AD Identity Protection]** に移動します。

1. メニューの **[保護]** で、 **[MFA 登録ポリシー]** を選択します。

1. **[割り当て]** で、[ユーザー] の下にある **[すべてのユーザー]** を選択し、MFA を適用するユーザーを選択します。

1. **[ポリシーの適用]** を **[オフ]** から **[オン]** に変更します。

1. **[保存]** を選択します。

これにより、ユーザーは次回ログインしようとしたときに MFA 登録を完了する必要があります。

1. プライベート ブラウザーから、`https://login.microsoftonline.com` に移動します。 テナントでユーザー名とパスワードを入力します。  ユーザーが入力を求められる追加のセキュリティ情報要件に注意してください。
