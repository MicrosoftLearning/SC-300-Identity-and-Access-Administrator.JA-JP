---
lab:
    title: '05 - Azure AD にグループを追加する'
    learning path: '01'
    module: 'モジュール 02 - ID の作成、構成、管理を行う'
---

# ラボ 05: Azure AD にグループを追加する

## ラボ シナリオ

Azure AD 管理者としての職務の一環として、さまざまな種類のグループを作成することがあります。組織の営業部門用に新しい Microsoft 365 グループを作成する必要があります。

#### 推定時間: 5 分

## Azure Active Directory で Microsoft 365 グループを作成する

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を参照します。

1. 左側のナビゲーション メニューの **「管理」** で、**「グループ」** を選択します。

1. 「グループ」ブレードのメニューで、**「新しいグループ」** を選択します。

1. 次の情報を使用して、グループを作成します。

    | **設定**| **値**|
    | :--- | :--- |
    | グループの種類| Microsoft 365|
    | グループ名| Northwest Sales|
    | メンバーシップの種類| 割り当て済み|
    | 所有者| *現在の管理者アカウント*|
    | メンバー| **Alex Wilber** と **Bianca Pisani**|

    ![「グループの種類」、「グループ名」、「所有者」、「メンバー」が強調表示された「新しいグループ」ブレードが表示されている画面イメージ](./media/lp1-mod2-create-o365-group.png)

1. 完了したら、**Northwest sales** という名前のグループが **「すべてのグループ」** リストに表示されていることを確認します。
