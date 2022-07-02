---
lab:
  title: 17 - Azure AD スマート ロックアウトの値を管理する
  learning path: "02"
  module: Module 02 - Implement an Authentication and Access Management Solution
ms.openlocfilehash: d293cb09758538fcaedeb06ff7c874efc2420679
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421439"
---
# <a name="lab-17---manage-azure-ad-smart-lockout-values"></a>ラボ 17 - Azure AD スマート ロックアウトの値を管理する

## <a name="lab-scenario"></a>ラボのシナリオ

組織の追加のパスワード保護設定を構成する必要があります。

#### <a name="estimated-time-5-minutes"></a>推定時間:5 分

### <a name="exercise-1---manage-azure-ad-smart-lockout-values"></a>演習 1 - Azure AD スマート ロックアウトの値を管理する

#### <a name="task---add-smart-lockouts"></a>タスク - スマート ロックアウトを追加する

組織の要件に基づいて、Azure AD スマート ロックアウトの値をカスタマイズできます。 スマート ロックアウト設定を組織固有の値にカスタマイズするには、ユーザーに Azure AD Premium P1 以上のライセンスが必要です。

1. ディレクトリのグローバル管理者アカウントを使用して、[https://portal.azure.com](https://portal.azure.com) にアクセスし、サインインします。

2. ポータル メニューを開き、**[Azure Active Directory]** を選択します。

3. [Azure Active Directory] ブレードで、**[管理]** の下にある **[セキュリティ]** を選択します。

4. [セキュリティ] ブレードの左側のナビゲーションで **[認証方法]** を選択します。

5. 左側のナビゲーションで、**[パスワード保護]** を選択します。

    ![[認証方法] ブレードと、[パスワード認証] を参照するために選択されて強調表示された項目を表示している画面イメージ](./media/lp2-mod3-browse-to-password-protection.png)

6. [パスワード保護] の設定の **[ロックアウト期間 (秒単位)]** ボックスで値を **[120]** に設定します。

7. **[モード]** で **[適用済み]** を選択します。

8. 変更を保存します。

    **注** - スマート ロックアウトのしきい値がトリガーされると、アカウントがロックされているときに次のメッセージが表示されます。
    - ご使用のアカウントは、不正使用を防ぐために一時的にロックされています。 後でもう一度お試しください。問題が解決しない場合は管理者にお問い合わせください。
