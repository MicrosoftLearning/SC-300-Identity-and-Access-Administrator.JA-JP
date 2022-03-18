---
lab:
  title: 03 - グループ メンバーシップを使用してライセンスを割り当てる
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 9ecd9c244867c5c995a5e6dc39bbdc47f48ad5c7
ms.sourcegitcommit: fbe0a16b7c6a9a2ac2c2ea3b3f707faa0afe23a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2022
ms.locfileid: "139258491"
---
# <a name="lab-03-assigning-licenses-using-group-membership"></a>ラボ 03:グループ メンバーシップを使用してライセンスを割り当てる

## <a name="lab-scenario"></a>ラボのシナリオ

あなたの組織は Azure AD のセキュリティ グループを使用してライセンスを管理することに決めました。 新しいセキュリティ グループを設定し、そのグループにライセンスを割り当て、グループ メンバーのライセンスが更新されたことを確認する必要があります。

#### <a name="estimated-time-10-minutes"></a>推定時間:10 分

### <a name="exercise-1---create-a-security-group-and-add-a-user"></a>演習 1 - セキュリティ グループを作成してユーザーを追加する

#### <a name="task-1---check-to-see-if-delia-dennis-has-access-to-office-365"></a>タスク 1 - Delia Dennis が Office 365 にアクセスできるかどうかを確認する

1. 新しい InPrivate ブラウザー ウィンドウを開きます。
2. [https://www.office.com](https://www.office.com) に接続します。
3. [サインイン] をクリックして、Delia Dennis として接続します。

    | **設定**| **Value**|
    | :--- | :--- |
    | ユーザー名 | DeliaD@`your domain name.com`|
    | Password| リソースからグローバル管理者のパスワードを入力します|

4. Office.com の Web サイトに接続する必要がありますが、ライセンスがないことを示すメッセージが表示されます。

    ![画面イメージ: Delia Dennis がログインしている Office.com の Web サイト。ライセンスが割り当てられていないため、Office アプリケーションは利用できません。](./media/delia-no-office-license.png)
    
5. ブラウザー ウィンドウを閉じます。

#### <a name="task-2----create-a-security-group-in-azure-active-directory"></a>タスク2 - Azure Active Directory でセキュリティ グループを作成する

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を参照します。

2. 左側のナビゲーション メニューの **[管理]** で、**[グループ]** を選択します。
3. [グループ] ブレードのメニューで、**[新しいグループ]** を選択します。
4. 次の情報を使用して、グループを作成します。

    | **設定**| **Value**|
    | :--- | :--- |
    | グループの種類| セキュリティ|
    | グループ名| sg-SC300-O365|
    | メンバーシップの種類| 割り当て済み|
    | 所有者| *自分の管理者アカウントをグループの所有者として割り当てる*|

5. 「メンバー」の下の「**メンバーを選択していません**」テキストをクリックします。
6. ユーザーの一覧から、 **「Delia Dennis」** を選択します。
7. **[選択]** ボタンをクリックします。

    ![「グループの種類」、「グループ名」、「所有者」、「メンバー」が強調表示された「新しいグループ」ブレードが表示されている画面イメージ](./media/lp1-mod2-create-group.png)

8. **[作成]** ボタンをクリックします。
9. 完了したら、**sg-SC300-O365** という名前のグループが **「すべてのグループ」** リストに表示されていることを確認します。

#### <a name="task-3---assign-a-license-to-a-group"></a>タスク3 - グループにライセンスを割り当てる

1. **「すべてのグループ」** リストで **sg-SC300-O365** を選択します。
2. [マーケティング] ブレードの **[管理]** で **[ライセンス]** を選択します。
3. メニューで **「+ 割り当て」** を選択します。
4. 「ライセンス割り当ての更新」ブレードの **「ライセンスの選択」** で、使用可能なライセンスのリストを確認し、**Office 365 E3** のチェック ボックスをオンにします。

    **ヒント** - 複数のライセンスが選択されている場合は、[ライセンス条項の確認] オプション メニューを使用して特定のライセンスを選択し、そのライセンスのライセンス オプションを表示できます。

    ![選択され、グループに割り当てられているライセンスを表示した画面イメージ。 [Review license] (ライセンスの確認) メニューも選択され、複数選択オプションが表示されます。](./media/lp1-mod2-assign-license-group.png)

6. **[保存]** を選択します。

#### <a name="taks-4---confirm-the-office-365-license"></a>タスク 4 - Office 365 ライセンスを確認する

1. 新しい InPrivate ブラウザー ウィンドウを開きます。
2. [https://www.office.com](https://www.office.com) に接続します。
3. [サインイン] をクリックして、Delia Dennis として接続します。

    | **設定**| **Value**|
    | :--- | :--- |
    | ユーザー名 | DeliaD@`your domain name.com`|
    | Password| リソースからグローバル管理者のパスワードを入力します|

4. Office.com Web サイトに接続すると、ライセンスに関するメッセージは表示されません。 左側にあるすべての Office アプリケーションを利用できます。

    ![画面イメージ: Delia Dennis がログインしている Office.com の Web サイト。ライセンスが割り当てられているため、Office アプリケーションが利用できます。](./media/delia-office-license.png)
    
5. ブラウザー ウィンドウを閉じます。
    
