---
lab:
  title: 06 - グループ ライセンス割り当てを変更する
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 43274c8456dd760022efd09fc7cbb0efcac1037f
ms.sourcegitcommit: 533d012d39c31518af43d4a1d4bc091ea485d27c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2022
ms.locfileid: "138690103"
---
# <a name="lab-06-change-group-license-assignments"></a>ラボ 06:グループ ライセンス割り当てを変更する

## <a name="lab-scenario"></a>ラボのシナリオ

時折、Azure AD セキュリティ グループで使用されているライセンスの割り当てを変更する必要があります。 グループのライセンス割り当てを変更する手順を確実に理解しておく必要があります。

#### <a name="estimated-time-5-minutes"></a>推定時間:5 分

### <a name="exercise-1---change-group-license-assignments"></a>演習 1 - グループ ライセンスの割り当てを変更する

#### <a name="task---use-azure-ad-portal-to-make-changes"></a>タスク - Azure AD ポータルを使って変更する

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を参照します。

2. 左側のナビゲーション メニューの **[管理]** で、**[グループ]** を選択します。

3. **sg-Finance** グループを選びます。

4. 左側のナビゲーション メニューの **[管理]** で、**[ライセンス]** を選択します。

5. 現在の割り当てを確認し、メニューの **[+ 割り当て]** を選択します。

    ![現在のライセンスと「割り当て」メニューオプションが強調表示されている、選択されたグループ ライセンス オプションを表示した画面イメージ](./media/lp1-mod2-change-group-license.png)

6. 「ライセンスの割り当ての更新」ブレードで、**Windows 10 Enterprise E3** ライセンスを選択するか、既存のライセンスの選択を解除するか、ライセンス オプションを追加または削除します。これらを組み合わせることもできます。

7. 完了したら、**[保存]** を選択します。

8. グループの [ライセンス] ページで、変更を確認します。
