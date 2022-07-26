---
lab:
  title: 09 - ゲスト ユーザーをディレクトリに追加する
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: 9410e7a9c69431ece616a1af29ae52b76c7f38b7
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421424"
---
# <a name="lab-09-add-guest-users-to-the-directory"></a>ラボ 09: ゲスト ユーザーをディレクトリに追加する

## <a name="lab-scenario"></a>ラボのシナリオ

あなたの会社は多くのベンダーと協力していますが、場合によっては、ベンダーのアカウントをゲストとしてディレクトリに追加する必要があります。

#### <a name="estimated-time-5-minutes"></a>推定時間:5 分

### <a name="exercise-1---add-guest-users-to-the-directory"></a>演習 1 - ゲスト ユーザーをディレクトリに追加する

#### <a name="task---add-the-guest-user"></a>タスク - ゲスト ユーザーを追加する

1. 制限付き管理者ディレクトリ ロールまたはゲストの招待元ロールが割り当てられたユーザーとして、[https://portal.azure.com](https://portal.azure.com) にサインインします。

2. **[Azure Active Directory]** を選択します。

3. **[管理]** にある **[ユーザー]** を選択します。

4. **[新しいゲスト ユーザー]** を選択します。

    ![「新しいゲストユーザー」メニュー オプションが選択された「ユーザー」ブレードを表示する画面イメージ](./media/lp1-mod3-new-guest-user-menu-selection.png)

5. [新しいユーザー] ページで **[ユーザーの招待]** を選択し、ゲスト ユーザーの情報を追加します。

    **注** - グループのメール アドレスはサポートされていません。個人のメール アドレスを入力してください。 また、一部の電子メール プロバイダーでは、ユーザーはプラス記号 (+) と追加テキストを電子メール アドレスに付け加えて、受信ボックスのフィルター処理などに役立てることができます。 ただし、Azure AD では現在、電子メール アドレスのプラス記号はサポートされていません。 配信の問題を回避するために、プラス記号と、それに続く @ 記号より前の任意の文字を含めません。

6. 完了したら、 **[招待する]** を選択します。

7. [ユーザー] ブレードで、アカウントが一覧表示されていることを確認し、**[ユーザーの種類]** 列に **[ゲスト]** が表示されていることを確認します。

招待を送信すると、ユーザー アカウントがディレクトリにゲストとして自動的に追加されます。
