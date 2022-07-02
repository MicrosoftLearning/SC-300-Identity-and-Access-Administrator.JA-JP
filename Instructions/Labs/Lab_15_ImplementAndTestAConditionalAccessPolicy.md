---
lab:
  title: 15 - 条件付きアクセス ポリシーの実装とテストを行う
  learning path: "02"
  module: Module 02 - Implement an Authentication and Access Management Solution
ms.openlocfilehash: bbfa7210165481c0a36802153635a23741a92d0b
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421304"
---
# <a name="lab-15---implement-and-test-a-conditional-access-policy"></a>ラボ 15 - 条件付きアクセス ポリシーの実装とテストを行う

## <a name="lab-scenario"></a>ラボのシナリオ

組織では、内部アプリケーションへのユーザーのアクセスを制限する必要があります。 Azure Active Directory 条件付きアクセス ポリシーをデプロイする必要があります。

#### <a name="estimated-time-12-minutes"></a>推定時間:12 分

### <a name="exercise-1---set-a-conditional-access-policy-to-block-debrab-from-accessing-yammer"></a>演習 1 - DebraB が Yammer にアクセスするのをブロックする条件付きアクセス ポリシーを設定する

#### <a name="task-1----confirm-debrab-has-access-to-yammer"></a>タスク 1 - DebraB が Yammer にアクセスできることを確認する

1. 新しい InPrivate ブラウザー ウィンドウを開きます。
2. [https://www.office.com](https://www.office.com) に接続します 
3. プロンプトが表示されたら、DebraB としてログインします。

    | 設定 | 値 |
    | :--- | :--- |
    | ユーザー名 | **DebraB@** `<<your lab domain>>.onmicrosoft.com` |
    | パスワード | テナント管理者のパスワードを入力します (テナントの管理者のパスワードを取得するには、[ラボ リソース] タブを参照してください)。 |
    
4. Yammer アイコンをクリックして、正しく読み込まれることを確認します。

#### <a name="task-2----create-a-conditional-access-policy"></a>タスク 2 - 条件付きアクセスポリシーを作成する

Azure Active Directory 条件付きアクセスは Azure AD の高度な機能です。これにより、どのユーザーがリソースにアクセスできるかを制御する詳細なポリシーを指定できます。 条件付きアクセスを使用すると、グループ、デバイスの種類、場所、ロールなどに基づいてユーザーのアクセスを制限することでアプリケーションを保護できます。

1. ディレクトリのグローバル管理者アカウントを使用して、[https://portal.azure.com](https://portal.azure.com) にアクセスし、サインインします。

2. ポータル メニューを開き、**[Azure Active Directory]** を選択します。

3. [Azure Active Directory] ブレードで、**[管理]** の下にある **[セキュリティ]** を選択します。

4. [セキュリティ] ブレードの左側のナビゲーションで **[条件付きアクセス]** を選択します。

5. 上部のメニューで、ドロップダウンから **[+ 新しいポリシー]** を選択し、 **[新しいポリシーの作成]** を選択します。

    ![[新しいポリシー] が強調表示されている [条件付きアクセス] ブレードを表示している画面イメージ](./media/lp2-mod1-conditional-access-new-policy.png)

6. **[名前]** ボックスに「**Block Yammer for DebraB**」と入力します。

    **注** - この命名を使用すると、ポリシーとその機能をすばやく認識できます。

7. **[割り当て]** で、 **[ユーザーまたはワークロード ID]** を選択します。

8. [含める] タブで **[ユーザーとグループ]** チェックボックスをオンにします。

9. [選択] ウィンドウで **DebraB** アカウントを選択してから、**[選択]** を選択します。

10. **[クラウド アプリまたは操作]** を選択します。

11. **[クラウド アプリ]** が選択されていることを確認し、**[アプリの選択]** を選択します。

12. [選択] ウィンドウで **[Yammer]** を検索し、**[Office 365 Yammer]** を選択してから、**[選択]** を選択します。

13. **[アクセス制御]** で **[許可]** を選択します。

14. [許可] ウィンドウで **[アクセスのブロック]** を選択し、**[選択]** を選択します。

    **注** - このポリシーは、演習用にのみ構成されており、条件付きアクセス ポリシーを迅速に実証するために使用されます。

15. **[ポリシーを有効にする]** で、 **[オン]** を選択してから **[作成]** を選びます。

    ![ポリシー設定が強調表示された新しい条件付きアクセス ポリシーを表示している画面イメージ](./media/lp2-mod3-create-conditional-access-policy.png)

#### <a name="task-3---test-the-conditional-access-policy"></a>タスク 3 - 条件付きアクセス ポリシーをテストする

条件付きアクセス ポリシーをテストして、想定どおりに動作することを確認する必要があります。

1. 新しい [Inprivate] ブラウザー タブを開いて、[https://www.yammer.com/office365](https://www.yammer.com/office365) に移動します。
     - プロンプトが表示されたら、DebraB としてログインします。

    | 設定 | 値 |
    | :--- | :--- |
    | ユーザー名 | **DebraB@** `<<your lab domain>>.onmicrosoft.com` |
    | パスワード | テナント管理者のパスワードを入力します (テナントの管理者のパスワードを取得するには、[ラボ リソース] タブを参照してください)。 |
      
2. Microsoft Yammer に正常にアクセスできないことを確認します。

    ![条件付きアクセス ポリシーが有効になっているために、リソースへのアクセスがブロックされたことを表示している画面イメージ](./media/lp2-mod3-test-conditional-access-policy.png)

3. サインインしている場合は、タブを閉じ、1 分待ってから、もう一度やり直してください。
    
     **注** - DebraB として Yammer に自動ログインしている場合は、手動でログアウトする必要があります。資格情報/アクセスはキャッシュされました。  ログアウトしてサインインすると、Yammer セッションはアクセスを拒否するはずです。

4. タブを閉じ、[条件付きアクセス] ブレードに戻ります。

5. **[Yammer 条件付きアクセス]** ポリシーを選択します。

6. **[ポリシーを有効にする]** で **[オン]** を選択し、**[保存]** を選択します。
