---
lab:
  title: 05 - Azure AD にグループを追加する
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 192cb3bc35b573ed3b4799cfb3872038874cb521
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421445"
---
# <a name="lab-05-adding-groups-to-azure-ad"></a>ラボ 05: Azure AD にグループを追加する

## <a name="lab-scenario"></a>ラボのシナリオ

Azure AD 管理者としての職務の一環として、さまざまな種類のグループを作成することがあります。 組織の営業部門用に新しい Microsoft 365 グループを作成する必要があります。

#### <a name="estimated-time-5-minutes"></a>推定時間:5 分

### <a name="exercise-1---create-an-microsoft-365-group-in-azure-active-directory"></a>演習 1 - Azure Active Directory で Microsoft 365 グループを作成する

#### <a name="task-1---create-the-group"></a>タスク 1 - グループを作成する

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) にアクセスします。

2. 左側のナビゲーション メニューの **[管理]** で、**[グループ]** を選択します。

3. [グループ] ブレードのメニューで、**[新しいグループ]** を選択します。

4. 次の情報を使用して、グループを作成します。

    | **設定**| **Value**|
    | :--- | :--- |
    | グループの種類| Microsoft 365|
    | グループ名| Northwest Sales|
    | メンバーシップの種類| 割り当て済み|
    | 所有者| *自分の管理者アカウントをグループの所有者として割り当てる*|
    | メンバー| **Alex Wilber** と **Bianca Pisani**|

    ![[グループの種類]、[グループ名]、[所有者]、[メンバー] が強調表示された [新しいグループ] ブレードが表示されている画面イメージ](./media/lp1-mod2-create-o365-group.png)

5. 完了したら、**Northwest sales** という名前のグループが **[すべてのグループ]** リストに表示されていることを確認します。
