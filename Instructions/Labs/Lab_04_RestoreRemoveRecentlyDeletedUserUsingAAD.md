---
lab:
  title: 04 - 削除済みユーザーを復元する
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 9ec368f11cce9ad63fbc297149a68582e1773358
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421311"
---
# <a name="lab-04-restore-a-deleted-user"></a>ラボ 04:削除済みユーザーの復元

## <a name="lab-scenario"></a>ラボのシナリオ

アカウントを削除した後、復元する必要がある場合があります。 最近削除されたアカウントを復元できるかどうかを確認する必要があります。

#### <a name="estimated-time-5-minutes"></a>推定時間:5 分

### <a name="exercise-1---remove-a-user-from-azure-active-directory"></a>演習 1 - Azure Active Directory からユーザーを削除する

#### <a name="task-1---remove-a-user"></a>タスク 1 - ユーザーを削除する

1. [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) にアクセスします。

2. 左側のナビゲーション メニューの **[管理]** で、**[ユーザー]** を選択します。

3. **[ユーザー]** リストで、削除するユーザーのチェック ボックスをオンにします。 たとえば、**Chris Green** を選択します。

    **ヒント** - リストからユーザーを選択すると、複数のユーザーを同時に管理できます。 ユーザーを選択してそのユーザーのブレードを開いた場合は、その個々のユーザーのみを管理します。

    ![リストから複数のユーザーを選択する機能を示した、1 つのユーザー チェック ボックスがオンになり、別のチェック ボックスが強調表示された、[すべてのユーザー] ユーザー リストを表示した画面イメージ。](./media/lp1-mod2-remove-user.png)

4. ユーザー アカウントを選択した状態で、メニューの **[ユーザーの削除]** を選択します。

5. ダイアログ ボックスを確認してから、**[OK]** を選択します。

#### <a name="task-2---restore-a-deleted-user"></a>タスク 2 - 削除済みユーザーを復元する

1. [ユーザー] ブレードの左側のナビゲーションで、**[削除済みのユーザー]** を選択します。

2. 削除したユーザーのリストを確認し、削除したばかりのユーザーを選択します。

    **重要** - 既定では、削除されたユーザー アカウントは 30 日後に自動的に Azure Active Directory から完全に削除されます。

3. メニューで **[ユーザーの 復元]** を選択します。

4. ダイアログ ボックスを確認してから、**[OK]** を選択します。

5. 左側のナビゲーション バーで、**[すべてのユーザー]** を選択します。

6. ユーザーが復元されたことを確認します。
