---
lab:
  title: 01 - ユーザー ロールを管理する
  learning path: "01"
  module: Module 01 - Implement an Identity Management Solution
ms.openlocfilehash: 2f0c349fe65316fd9a3166d81603b2b88af20a8f
ms.sourcegitcommit: bc5c47a39782e94c249ec4bce01ba0da9249ec61
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2022
ms.locfileid: "146822634"
---
# <a name="lab-01-manage-user-roles"></a>ラボ 01: ユーザー ロールを管理する

## <a name="lab-scenario"></a>ラボのシナリオ

あなたの会社では最近、アプリケーション管理者として業務を遂行する新しい従業員を採用しました。 新しいユーザーを作成し、セキュリティ ロールを割り当てる必要があります。

#### <a name="estimated-time-30-minutes"></a>予想所要時間: 30 分

### <a name="exercise-1---create-a-new-user-and-test-their-application-admin-rights"></a>演習 1 - 新しいユーザーを作成し、アプリケーションの管理者権限をテストする

#### <a name="task-1---add-a-new-user"></a>タスク 1 - 新しいユーザーを追加する

1. グローバル管理者として [https://portal.azure.com](https://portal.azure.com) にサインインします

2. 「**Azure Active Directory**」を検索して選択します。

3. 左側のナビゲーション メニューの **[管理]** で、 **[ユーザー]** を選択し、 **[+ 新しいユーザー]** を選択します。

4. 「ユーザーの作成」が選択されていることを確認します。  次の情報を使用してユーザーを作成します。

    | **設定**| **Value**|
    | :--- | :--- |
    | ユーザー名| ChrisG|
    | 名前| Chris Green|
    | 名| Chris|
    | 姓| Green|

5. 「**自分でパスワードを作成する**」をマークします

6. パスワードを使用する - **覚えておくことができる安全なパスワードを入力します。**

     *このアカウントに最初にログインするときにパスワードを変更する必要があります*

7. **[作成]** を選択します。 これでユーザーが作成され、組織に登録されました。

#### <a name="task-2---login-and-try-to-create-an-app"></a>タスク 2 - ログインしてアプリを作成する

1. 新しい InPrivate ブラウザー ウィンドウを開きます。
2. Azure portal [https://portal.azure.com](https://portal.azure.com) を Chris Green として開きます。

    | **設定**| **Value**|
    | :--- | :--- |
    | ユーザー名| ChrisG@`your domain name.com`|
    | パスワード| Pass@word1|

3. パスワードを更新します。

    | **設定**| **Value**|
    | :--- | :--- |
    | 現在のパスワード| Pass@word1|
    | 新しいパスワード| Pa$$w.rd1234|
    | パスワードの確認| Pa$$w.rd1234|

4. **[Microsoft Azure ツアーへようこそ]** ダイアログが表示された場合は、 **[後で]** ボタンをクリックします。

5. 画面上部の検索ダイアログで「**エンタープライズ アプリケーション**」を検索して選択します。
7. **[新しいアプリケーション]** を選択します。 **[+ 独自のアプリケーションの作成]** は使用できないことに注意してください。

9. **[アプリケーション プロキシ]** 、 **[ユーザー設定]** などの他の設定をクリックして、**Chris Green** に権限がないことを確認してください。
10. 右上隅にある **ChrisG** の名前をクリックして、サインアウトします。


### <a name="exercise-2---assign-the-application-admin-role-and-create-an-app"></a>演習 2 - アプリケーション管理者のロールを割り当て、アプリを作成する

#### <a name="task-1---assign-a-role-to-a-user"></a>タスク1 - ユーザーにロールを割り当てる

Azure Active Directory (Azure AD) を使用して、特権が低いロールで ID のタスクを管理する限定された管理者を指定できます。 ユーザーの追加または変更、管理ロールの割り当て、ユーザーのパスワードのリセット、ユーザーのライセンスの管理、ドメイン名の管理などの目的で管理者を割り当てることができます。

1. グローバル管理者のロールとしてまだログインしていない場合は、Azure portal を開いてログインします。
2. Azure Active Directory に移動します。
3. メニューの [管理] セクションで **[ユーザー]** をクリックします。
4. **Chris Green** のアカウントを選択します。
5. 「管理」メニューから「**割り当てられたロール**」を選択します。
6. **[+ 割り当ての追加]** を選択し、`Application administrator` ロールをマークします。
7. **[追加]** を選択します

    ![[割り当てられたロール] ページ - 選択されたロールを表示中](./media/directory-role-select-role.png)

**注**: ラボ環境で既に Azure AD Premium P2 がアクティブ化されている場合は、Privileged Identity Management (PIM) が有効になり、 **[次へ]** を選択し、このユーザーに永続的なロールを割り当てる必要があります。

8. **[更新]** ボタンをクリックします。

**注 - 新しく割り当てられたアプリケーション管理者ロールが、ユーザーの [割り当てられたロール] ページに表示されます。**

#### <a name="task-2---check-application-permissions"></a>タスク 2 - アプリケーションのアクセス許可を確認する

1. 新しい InPrivate ブラウザー ウィンドウを開きます。
2. Azure portal [https://portal.azure.com](https://portal.azure.com) を Chris Green として開きます。

    | **設定**| **Value**|
    | :--- | :--- |
    | ユーザー名| ChrisG@`your domain name.com`|
    | パスワード| Pa$$w.rd1234|

3. **[Microsoft Azure ツアーへようこそ]** ダイアログが表示された場合は、 **[後で]** ボタンをクリックします。
4. 画面上部の検索ダイアログで「**エンタープライズ アプリケーション**」を検索して選択します。
5. 「 **+ 新しいアプリケーション**」が利用可能になったことに注意してください。
6. **[+ 新しいアプリケーション]** を選択します。

   **注 - このロールには、テナントにアプリケーションを追加する権限があります。この権限については、後のラボでさらに実験します。**

7. Azure portal の Chris Green のインスタンスからサインアウトし、ブラウザーを閉じます。

### <a name="exercise-3---remove-a-role-assignment"></a>演習3 - ロールの割り当てを削除する

#### <a name="task-1---remove-the-application-administrator-from-chris-green"></a>タスク 1 - Chris Green からアプリケーション管理者を削除する

このタスクでは、別の方法を使用して、割り当てられたロールを削除します。 Azure AD の「**ロールと管理者**」オプションを使用します。

1. グローバル管理者としてまだログインしていない場合は、Azure portal を起動して今すぐログインしてください。
2. 検索ボックスに「**Azure Active Directory**」と入力し、Azure AD を起動します。
3. **Azure Active Directory** で **[ロールと管理者]** を選択して、一覧から **[アプリケーション管理者]** ロールを選択します。

**注**: ラボ環境で既に Azure AD Premium P2 がアクティブ化されている場合は、Privileged Identity Management (PIM) が有効になり、 **[次へ]** を選択し、このユーザーに永続的なロールを割り当てる必要があります。

4. **[アプリケーション管理者 | 割り当て]** ページの一覧に Chris Green の名前が表示されます。
5. Chris Green の横にあるボックスにチェックを入れます。
6. ダイアログの上部にあるオプションから **[X 割り当ての削除]** をクリックします。
7. 確認ボックスが開いたら、「**はい**」と答えます。
8. 「Azure Active Directory」を閉じます。

### <a name="exercise-4---bulk-import-of-users"></a>演習 4 - ユーザーの一括インポート

#### <a name="task-1---bulk-operations-for-creating-users-with-a-csv-file"></a>タスク 1 - .csv ファイルを使用してユーザーを作成するための一括操作

1. Azure AD メニューの **[管理]** で **[ユーザー]** を選択します。

2. **[ユーザー |すべてのユーザー]** タイルで、 **[一括操作]** ドロップダウン矢印を選択し、 **[一括作成]** を選択します。

3. **[一括作成]** を選択すると、新しいタイルが開きます。 このタイルには、ユーザー情報を入力し、アップロードしてユーザーの一括作成を追加するために編集するテンプレート ファイルへの **[ダウンロード]** リンクが表示されます。

4. **[ダウンロード]** を選択して、.csv ファイルをダウンロードします。

5. .csv テンプレートには、ユーザー プロファイルに含まれるフィールドが用意されています。 これには、必要なユーザー名、表示名、初期パスワードが含まれます。 現時点では、部門や使用状況の場所などの省略可能なフィールドを入力することもできます。 次のスクリーンショットは、.csv ファイルを完了する方法の例です。 

    ![csv ファイル エントリを使用した一括インポート](./media/bulkimportexample.png)

6. 設定が完了したら、変更を保存してアップロードしてユーザーを追加します。

7. ファイルが正常にアップロードされたことが通知されます。  [送信] を選択してユーザーを追加します。 

ユーザーが作成されると、作成が成功したことを確認するメッセージが表示されます。  [ユーザーの一括作成] タイルを閉じると、 **[ユーザー | すべてのユーザー]** の一覧に新しいユーザーが設定されます。 

#### <a name="task-2---bulk-addition-of-users-using-powershell"></a>タスク 2 - PowerShell を使用したユーザーの一括追加

1. PowerShell を管理者として開きます。  これを行うには、Windows で PowerShell を検索し、[管理者として実行] を選択します。 

**注**: PowerShell ISE ではなく PowerShell を選択します。

2. 以前に使用していない場合は、Azure AD PowerShell モジュールを追加する必要があります。  次のコマンドを実行します。Install-Module AzureAD。  メッセージが表示されたら、Y キーを押して続行します。

    ```
    Install-Module AzureAD
    ```

3. 次のコマンドを実行して、モジュールが正しくインストールされていることを確認します。  

    ```
    Get-Module AzureAD 
    ```

4. 次に、次を実行して Azure にログインする必要があります。  

    ```
    Connect-AzureAD 
    ``` 

5. Azure AD にログインするための Microsoft ログイン ウィンドウが表示されます。  

6. 接続されていることを確認し、既存のユーザーを表示するには、次を実行します。  

    ``` 
    Get-AzureADUser 
    ```
    
7. すべての新しいユーザーに共通の一時パスワードを割り当てるには、次のコマンドを実行し、TempPW をユーザーに提供するパスワードに置き換えます。  

    ``` 
    $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
    ```

    ```
    $PasswordProfile.Password = "Pass@word1" 
    ```

8. これで、新しいユーザーの作成に取りかかることができます。  次のコマンドにユーザー情報が入力され、実行されます。  追加するユーザーが複数ある場合は、メモ帳の txt ファイルを使用してユーザー情報を追加し、PowerShell にコピーして貼り付けることができます。 

    ```
    New-AzureADUser -DisplayName "New User" -PasswordProfile $PasswordProfile -UserPrincipalName "NewUser@labtenantname.com" -AccountEnabled $true -MailNickName "Newuser"
    ```
**注**: **labtenantname.com** は、ラボ テナントによって割り当てられた **onmicrosoft.com** 名に置き換えます。

## <a name="experiment-with-managing-users"></a>ユーザーの管理を試す

Azure AD ページを使用して、ユーザーを追加および削除できます。  ただし、スクリプトを使用してユーザーを作成し、ロールを割り当てることができます。  スクリプトを使用して、Chris Green のユーザー アカウントに別のロールを与えてみます。 
 

### <a name="exercise-5---remove-a-user-from-azure-active-directory"></a>演習 5 - Azure Active Directory からユーザーを削除する

#### <a name="task-1---remove-a-user"></a>タスク 1 - ユーザーを削除する

アカウントを削除した後、復元する必要がある場合があります。 最近削除されたアカウントを復元できるかどうかを確認する必要があります。

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) にアクセスします。

2. 左側のナビゲーションの **[管理]** で、**[ユーザー]** を選択します。

3. **[ユーザー]** リストで、削除するユーザーのチェック ボックスをオンにします。 たとえば、**Chris Green** を選択します。

    **ヒント** - リストからユーザーを選択すると、複数のユーザーを同時に管理できます。 ユーザーを選択し、そのユーザーのページを開いている場合は、その個別のユーザーのみを管理します。

    ![1 つのユーザー チェック ボックスがオンになり、リストから複数のユーザーを選択する機能を示す別のチェック ボックスが強調表示された、[すべてのユーザー] ユーザー リストを表示した画面イメージ。](./media/lp1-mod2-remove-user.png)

4. ユーザー アカウントを選択した状態で、メニューの **[削除]** を選択します。

5. ダイアログ ボックスの情報を確認し、 **[はい]** を選択します。

#### <a name="task-2---restore-a-deleted-user"></a>タスク 2 - 削除済みユーザーを復元する

1. [ユーザー] ページの左側のナビゲーションで、**[削除済みのユーザー]** を選択します。

2. 削除されたユーザーの一覧を確認し、 **[Chris Green]** を選択します。

    **重要** - 既定では、削除されたユーザー アカウントは 30 日後に自動的に Azure Active Directory から完全に削除されます。

3. メニューで **[ユーザーの 復元]** を選択します。

4. ダイアログ ボックスを確認してから、**[OK]** を選択します。

5. 左側のナビゲーションで、**[すべてのユーザー]** を選択します。

6. ユーザーが復元されたことを確認します。


### <a name="exercise-6---add-a-windows-10-license-to-a-user-account"></a>演習 6 - Windows 10 ライセンスをユーザー アカウントに追加する

#### <a name="task-1---find-your-unlicensed-user-in-azure-active-directory"></a>タスク1 - Azure Active Directory でライセンスのないユーザーを検索する

組織内の一部のユーザー アカウントには、割り当てられたライセンスで利用可能なすべての製品が提供されない場合や、ライセンス割り当ての更新または追加が必要な場合があります。 Azure AD でユーザー アカウントのライセンス割り当てを更新できるようにする必要があります。

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) にアクセスします。

2. 左側のナビゲーション メニューの **「管理」** で、 **「ユーザー」** を選択します。

3. [ユーザー] ページで、検索ボックスに「**Raul**」と入力します。

4. **[Raul Razo]** をクリックします。

5. Raul のプロファイルを確認し、Usage Location が設定されていることを確認します。

    **警告** - ユーザーにライセンスを割り当てるには、ユーザーに使用場所が割り当てられている必要があります。

6. 左側のメニューの **[ライセンス]** メニュー項目を選択します。

7. Raul に "ライセンスの割り当てが見つかりません" と表示されていることを確認します。

8. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) にアクセスします。

9. 左側のナビゲーション メニューの **「管理」** で、 **「ユーザー」** を選択します

10. [ユーザー] ページで、 **[Raul Razo]** を選択します。

11. 左側のナビゲーションで、**[ライセンス]** を選択します。

12. **「+ 割り当て」** ボタンを選択します。 

13. [ライセンス割り当ての更新] ページで、**Windows 10/11 Enterprise E3** ライセンスのチェック ボックスをオンにします。

    ![「ライセンスの割り当ての更新」ページとライセンス オプションが強調表示されている画面イメージ](./media/lp1-mod2-assign-user-license-options.png)

14. 完了したら、**[保存]** を選択します。

15. 画面の上部にある **[ホーム]** を選択し、 **[Contoso]** を選択し、 **[ユーザー]** を選択し、 **[Raul Razo]** を選択します。

16. ライセンスが割り当てられていることに注目してください。
