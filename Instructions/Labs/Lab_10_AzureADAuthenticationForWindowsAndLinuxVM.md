---
lab:
  title: 10 - Windows および Linux Virtual Machines に対する Azure AD Authentication
  learning path: "02"
  module: Module 02 - Implement an Authentication and Access Management Solution
ms.openlocfilehash: 82dcb43bdae3df54a80625dc29134d4497207d8c
ms.sourcegitcommit: 80c5c0ef60c1d74fcc58c034fe6be67623013cc0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2022
ms.locfileid: "146823188"
---
# <a name="lab-10---azure-ad-authentication-for-windows-and-linux-virtual-machines"></a>ラボ 10 - Windows および Linux Virtual Machines に対する Azure AD Authentication

**注** - このラボでは Azure Pass が必要です。 手順については、ラボ 00 を参照してください。

## <a name="lab-scenario"></a>ラボのシナリオ

会社は、リモート アクセス用の仮想マシンへのログインに Azure Active Directory を使用することを決定しました。  このラボでは、Windows および Linux 仮想マシンに対してこれをセットアップする方法について示します。

#### <a name="estimated-time-30-minutes"></a>予想所要時間: 30 分

### <a name="exercise-1---login-to-windows-virtual-machines-in-azure-with-azure-ad"></a>演習 1 - Azure AD を使用して Azure の Windows Virtual Machines にログインする

#### <a name="task-1---create-a-windows-virtual-machine-with-azure-ad-login-enabled"></a>タスク 1 - Azure AD ログインを有効にして Windows 仮想マシンを作成する

1. [https://portal.azure.com](https://portal.azure.com) を参照します

1. **[+ リソースの作成]** を選択します。

1. [マーケットプレースを検索] 検索バーに「**Windows Server**」と入力します。

1. **[Windows Server]** を選択して、次に [ソフトウェア プランの選択] ドロップダウンから **[Windows Server 2019 Datacenter]** を選択します。

1. [基本] タブで VM 用の管理者ユーザー名とパスワードを作成する必要があります。

1. **[管理]** タブで、[Azure AD] セクションの [Azure AD でログインする] のチェックボックスをオンにします。

1. [ID] セクションの **[システム割り当てマネージド ID]** がチェックされていることを確認します。 Azure AD を使用してログインを有効にすると、この操作は自動的に行われます。

1. 仮想マシンの作成エクスペリエンスの残りの部分に移動します。 

1. [作成] を選択します。

#### <a name="task-2---azure-ad-login-for-existing-azure-virtual-machines"></a>タスク 2 - 既存の Azure Virtual Machines に対する Azure AD ログイン

1. [https://portal.azure.com](https://portal.azure.com) で **[Virtual Machines]** を参照します。

1. **[アクセス制御 (IAM)]** を選択します。

1. **[追加]** 、 **[ロールの割り当ての追加]** の順に選択して、[ロールの割り当ての追加] ページを開きます。

1. 次のロールを割り当てます。 
    - **ロール**:仮想マシンの管理者ログインまたは仮想マシンのユーザー ログイン
    - **アクセスの割り当て先**:ユーザー、グループ、サービス プリンシパル、またはマネージド ID

1. 詳細な手順については、「Azure portal を使用して Azure ロールを割り当てる」を参照してください。

### <a name="exercise-2---login-to-linux-virtual-machines-in-azure-with-azure-ad"></a>演習 2 - Azure AD を使用して Azure の Linux Virtual Machines にログインする

#### <a name="task-1---create-a-linux-vm-with-system-assigned-managed-identity"></a>タスク 1 - システム割り当てマネージド ID を使用して Linux VM を作成する

1. [https://portal.azure.com](https://portal.azure.com) を参照します

1. **[+ リソースの作成]** を選択します。

1. [人気] ビューの **[Ubuntu Server 18.04 LTS]** の下の **[作成]** を選びます。

1. **[管理]** タブで、チェック ボックスをオンにして、 **[Azure Active Directory でログインする (プレビュー)]** を有効にします。

1. **システム割り当てマネージド ID** がオンにされていることを確認します。

1. 仮想マシンの作成エクスペリエンスの残りの部分に移動します。 このプレビュー期間中は、ユーザー名とパスワードまたは SSH 公開キーで管理者アカウントを作成する必要があります。

#### <a name="task-2---azure-ad-login-for-existing-azure-virtual-machines"></a>タスク 2 - 既存の Azure Virtual Machines に対する Azure AD ログイン

1. [https://portal.azure.com](https://portal.azure.com) で **[Virtual Machines]** を参照します。

1. **[アクセス制御 (IAM)]** を選択します。

1. [追加] > [ロール割り当ての追加] を選択して、[ロール割り当ての追加] ページを開きます。

1. 次のロールを割り当てます。 
    - **ロール**:仮想マシンの管理者ログインまたは仮想マシンのユーザー ログイン
    - **アクセスの割り当て先**:ユーザー、グループ、サービス プリンシパル、またはマネージド ID

1. 詳細な手順については、「Azure portal を使用して Azure ロールを割り当てる」を参照してください。
