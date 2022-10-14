---
lab:
  title: 25 - Azure AD エンタイトルメント管理でリソースのカタログを作成して管理する
  learning path: "04"
  module: Module 04 - Plan and Implement and Identity Governance Strategy
ms.openlocfilehash: c942d11da6bb857c7287c6407f8a31ae7329b3d4
ms.sourcegitcommit: 448f935ad266989a6f0086019e0c0e0785ad162b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "138421322"
---
# <a name="lab-25-create-and-manage-a-catalog-of-resources-in-azure-ad-entitlement-management"></a>ラボ 25:Azure AD エンタイトルメント管理でリソースのカタログを作成して管理する

## <a name="lab-scenario"></a>ラボのシナリオ

カタログは、リソースとアクセス パッケージのコンテナーです。 関連するリソースとアクセス パッケージをグループ化するときは、カタログを作成します。 どのユーザーでも、カタログを作成すると、最初のカタログ所有者になります。 カタログ所有者は、別のカタログ所有者を追加できます。 組織では、カタログを作成して構成する必要があります。

#### <a name="estimated-time-15-minutes"></a>推定時間:15 分

### <a name="exercise-1---building-out-resources-in-entitlement-management"></a>演習 1 - エンタイトルメント管理でのリソースの構築

#### <a name="task-1---create-a-catalog"></a>タスク 1: カタログを作成する

1. グローバル管理者アカウントを使用して、[https://portal.azure.com](https://portal.azure.com) にサインインします。

    **重要** - Azure AD の使用条件を使用および構成するには、以下が必要です。
    - Azure AD Premium P1、P2、EMS E3、EMS E5 のいずれかのサブスクリプション。
    - これらのサブスクリプションをお持ちでない場合は、Azure AD Premium を入手するか、Azure AD Premium 試用版を有効にすることができます。
    - 構成するディレクトリに対する次のいずれかの管理者アカウント。
        - グローバル管理者
        - セキュリティ管理者
        - 条件付きアクセス管理者

2. **[Azure Active Directory]** を開き、**[Identity Governance]** を選択します。

3. 左側のメニューの **[エンタイトルメント管理]** で、**[カタログ]** を選択します。

4. 上部のメニューで **[+ 新しいカタログ]** を選択します。

    ![[新しいカタログ] メニューが強調表示された Identity Governance カタログ ページが表示されている画面イメージ  ](./media/lp4-mod1-identity-governance-new-catalog.png)

5. [新しいカタログ] ペインで、**[名前]** ボックスに「**Marketing**」と入力します。

6. **[説明]** ボックスに「**マーケティング部門ユーザー**」と入力します。 この情報は、アクセス パッケージの詳細に表示されます。

7. **[Enabled for external users]\(外部ユーザーに対して有効\)** を指定すると、選択した外部ディレクトリのユーザーが、このカタログのアクセス パッケージを要求できるようになります。 この設定は変更されません。

8. **[有効] で [いいえ] を選択** します。

9. カタログをステージするか、必要になるまで無効にしておくかにより、カタログの即時使用を有効または無効にできます。 この演習では、カタログを有効にする必要はありません。

    ![[名前]、[説明]、[有効]、[作成] オプションが強調された [新しいカタログ] ペインが表示されている画面イメージ](./media/lp4-mod1-new-catalog-marketing.png)

10. [作成] を選択します。

#### <a name="task-2---add-resources-to-a-catalog"></a>タスク 2 - カタログにリソースを追加する

アクセス パッケージにリソースを含めるには、リソースがカタログ内に存在している必要があります。 追加できるリソースの種類は、グループ、アプリケーション、および SharePoint Online サイトです。 追加できるグループは、クラウドで作成された Microsoft 365 グループ、またはクラウドで作成された Azure AD セキュリティ グループです。 追加できるアプリケーションは Azure AD エンタープライズ アプリケーションで、これには SaaS アプリケーションと、Azure AD にフェデレーションされた独自アプリケーションの両方が含まれます。 追加できるサイトは、SharePoint Online サイトまたは SharePoint Online サイト コレクションです。

1. [Identity Governance] ブレードで、必要に応じて **[カタログ]** を選択します。

2. **[カタログ]** の一覧で **Marketing** を選択します。

3. 左側のナビゲーション メニューの **[管理]** で、**[リソース]** を選択します。

4. メニューで、**[+ リソースの追加]** を選択します。

5. [Add resources to catalog]\(カタログへのリソースの追加\) ブレードで、使用可能なオプションを確認します。  次の項目を追加します。

| リソースの種類 | 値 |
| :------------- | :---------- |
|  **グループとチーム** | Retail |
|  **アプリケーション** | Box |
|  **アプリケーション** | Salesforce |
|  **SharePoint サイト** | Brand <<< 利用可能な SharePoint サイトの一覧から選択 |

6. [Groups and Teams]\(グループとチーム\)、[アプリケーション]、または [SharePoint サイト] にはリソースがないかもしれません。 任意のリソース カテゴリを選択し、そのカテゴリからリソースを選択します。

7. この演習では、使用可能などのリソースを選択してもかまいません。

    ![カタログにリソースを追加する](./media/catalog-add-resources.png)

8. 作業が終了したら、 **[追加]** をクリックします。 これらのリソースをカタログ内のアクセス パッケージに含めることができるようになりました。

#### <a name="task-3---add-additional-catalog-owners"></a>タスク 3 - カタログ所有者をさらに追加する

カタログを作成したユーザーは最初のカタログ所有者になります。 カタログの管理を委任するには、カタログ所有者ロールにユーザーを追加します。 これは、カタログの管理責任を共有するのに役立ちます。

1. 必要に応じて、Azure portal で **[Azure Active Directory]** > **[Identity Governance] > [カタログ]** に移動し、**Marketing** を選択します。

2. Marketing カタログのブレードの左側のナビゲーション メニューで、[ロールと管理者] を選択します。

    ![Marketing カタログの [ロールと管理者] ページが表示されている画面イメージ](./media/lp4-mod1-catalog-roles-and-admins.png)

3. 上部のメニューで、利用可能なロールを確認し、 **「+ カタログ所有者の追加」** を選択します。

4. 「メンバーの選択」ウィンドウで、 **「Adele Vance」** を選択してから、 **「選択」** を選択します。

5. [ロールと管理者] の一覧で、新しく追加したロールを確認します。

#### <a name="task-4---edit-a-catalog"></a>タスク 4 - カタログを編集する

カタログの名前と説明を編集できます。 この情報は、アクセス パッケージの詳細に表示されます。

1. Marketing のブレードの左側のナビゲーションで、**[概要]** を選択します。

2. 上部のメニューで、**[編集]** を選択します。

3. 設定を確認し、**[プロパティ]** > **[有効]** で **[はい]** を選択します。

    ![有効なプロパティが表示されている画面イメージ。](./media/lp4-mod1-edit-marketing-catalog.png)

4. **[保存]** を選択します。

#### <a name="task-5---delete-a-catalog"></a>タスク 5 - カタログを削除する

カタログを削除できるのは、そのカタログにどのアクセス パッケージも含まれていない場合に限られます。

1. Marketing カタログの [概要] ページで、上部のメニューの [削除] を選択します。

2. 「削除」ダイアログ ボックスで情報を確認し、 **「いいえ」** を選択します。

    **注** - 次のラボで使用するためにカタログを保管しています。