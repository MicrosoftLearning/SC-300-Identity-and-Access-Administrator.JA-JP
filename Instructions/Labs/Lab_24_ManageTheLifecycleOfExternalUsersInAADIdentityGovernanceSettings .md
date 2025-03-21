---
lab:
  title: 24 - Microsoft Entra ID ガバナンスの設定で外部ユーザーのライフサイクルを管理する
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# ラボ 24: Microsoft Entra ID ガバナンスの設定で外部ユーザーのライフサイクルを管理する

### ログインの種類 = Microsoft 365 管理

## ラボのシナリオ

アクセス パッケージ要求が承認されることでディレクトリに招待された外部ユーザーが、アクセス パッケージの割り当てを失ったときに行われる処理を選択できます。 これは、ユーザーがアクセス パッケージの割り当てをすべて放棄した場合、または最後のアクセス パッケージの割り当てが期限切れになった場合に、行われる可能性があります。 既定では、アクセス パッケージの割り当てをすべて失った外部ユーザーは、ディレクトリへのサインインをブロックされます。 30 日後に、ゲスト ユーザー アカウントがディレクトリから削除されます。

#### 推定時間:5 分

### 演習 1 - Microsoft Entra ID ガバナンスの設定

#### タスク 1 - Microsoft Entra ID ガバナンスの設定で外部ユーザーのライフサイクルを管理する

1. グローバル管理者として、 [https://entra.microsoft.com](https://entra.microsoft.com)  にサインインします。

2. [Microsoft Entra ID] 項目を開き、 **[Identity Governance]** を選択します。

3. 左側のナビゲーション メニューの **[エンタイトルメント管理]** で、**[設定]** を選択します。

4. 上部のメニューで、**[編集]** を選択します。

    ![[manage the lifecycle of external users](外部ユーザーのライフサイクルを管理する) が強調された Identity Governance の [設定] ページが表示されている画面イメージ。](./media/lp4-mod1-manage-lifcycle-of-ext-users.png)

5. **[Manage the lifecycle of external users](外部ユーザーのライフサイクルを管理する)** セクションで、外部ユーザーに対するさまざまな設定を確認します。

6. 外部ユーザーがアクセス パッケージへの最後の割り当てを失ったときに、そのユーザーによるこのディレクトリへのサインインをブロックする場合は、**[Block external user from signing in to this directory](外部ユーザーによるこのディレクトリへのサインインをブロックする)** を **[はい]** に設定します。

7. ディレクトリへのサインインをブロックされたユーザーは、アクセス パッケージを再要求したり、このディレクトリで追加のアクセス権を要求したりすることができません。 その後、これらのユーザーが他のアクセス パッケージへのアクセスを要求する必要がある場合は、サインインをブロックするように構成しないでください。

8. 外部ユーザーがアクセス パッケージへの最後の割り当てを失ったときに、このディレクトリ内のゲスト ユーザー アカウントを削除する場合は、 **[Remove external user](外部ユーザーを削除)** を **[はい]** に設定します。

    **注** - エンタイトルメント管理を使用すると、エンタイトルメント管理によって招待されたアカウントのみが削除されます。 また、ユーザーがこのディレクトリ内のアクセス パッケージの割り当てではないリソースに追加されていた場合でも、そのユーザーはサインインをブロックされ、このディレクトリから削除されることに注意してください。 アクセス パッケージの割り当てを受け取る前に、ゲストがこのディレクトリ内に存在していた場合は、そのまま残ります。 ただし、ゲストがアクセス パッケージの割り当てによって招待され、招待された後で OneDrive for Business または SharePoint Online サイトにも割り当てられた場合でも、そのゲストは削除されます。

9. このディレクトリ内のゲスト ユーザー アカウントを削除する場合は、削除するまでの日数を設定できます。 アクセス パッケージへの最後の割り当てが失われた直後にゲスト ユーザー アカウントを削除する場合は、 **[Number of days before removing external user from this directory](このディレクトリから外部ユーザーを削除するまでの日数)** を **0** に設定します。

10. 変更を行った場合は、**[保存]** を選択します。
