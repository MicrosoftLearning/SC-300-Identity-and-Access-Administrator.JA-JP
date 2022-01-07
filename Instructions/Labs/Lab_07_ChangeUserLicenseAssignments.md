---
lab:
    title: '07 - ユーザー ライセンス割り当てを変更する'
    learning path: '01'
    module: 'モジュール 02 - ID の作成、構成、管理を行う'
---

# ラボ 07: ユーザー ライセンス割り当てを変更する

## ラボ シナリオ

組織内の一部のユーザー アカウントには、割り当てられたライセンスで利用可能なすべての製品が提供されない場合や、ライセンス割り当ての更新または追加が必要な場合があります。Azure AD でユーザー アカウントのライセンス割り当てを更新できるようにする必要があります。

#### 推定時間: 5 分

## 演習 1 - Windows 10 ライセンスをユーザー アカウントに追加する

### タスク1 - Azure Active Directory でライセンスのないユーザーを検索する

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を参照します。

2. 左側のナビゲーション メニューの **「管理」** で、**「ユーザー」** を選択します。

3. 「ユーザー」ブレードで、検索ボックスに **「Raul」** と入力します。

4. **「Raul Razo」** をクリックします
5. Raul のプロファイルを確認し、**利用場所** が設定されていることを確認します。

    **警告** - ユーザーにライセンスを割り当てるには、ユーザーに使用場所が割り当てられている必要があります。

6. 左側のメニューの **「ライセンス」** メニュー項目をクリックします。
7. Rual に "ライセンスの割り当てが見つかりません" と表示されていることを確認します。

### タスク2 - ユーザー ライセンスの割り当てを更新する

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を参照します。

2. 左側のナビゲーション メニューの **「管理」** で、**「ユーザー」** を選択します

3. 「ユーザー」ブレードで、**Raul Razo** を選択します。

4. 左側のナビゲーションで、**「ライセンス」** を選択します。

5. **「+ 割り当て」** ボタンを選択します。 

6. 「ライセンスの割り当ての更新」ブレードで、1 **Windows 10 Enterprise E3** ライセンスのチェック ボックスをオンにします。

    ![「ライセンスの割り当ての更新」ページとライセンス オプションが強調表示されている画面イメージ](./media/lp1-mod2-assign-user-license-options.png)

7. 完了したら、**「保存」** を選択します。
8. 画面の上部で、`Home > Contoso Marketing > User >` **「Raul Razo」** をクリックします
9. ライセンスが割り当てられていることに注目してください。
