---
lab:
  title: 06 - フェデレーション ID プロバイダーを追加する
  learning path: "01"
  module: Module 01 - Implement an identity management solution
ms.openlocfilehash: da25fe1a291e37a641448b8e4587352989993c96
ms.sourcegitcommit: 80c5c0ef60c1d74fcc58c034fe6be67623013cc0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2022
ms.locfileid: "146823197"
---
# <a name="lab-06-add-a-federated-identity-provider"></a>ラボ 06:フェデレーション ID プロバイダーを追加する

## <a name="lab-scenario"></a>ラボのシナリオ

あなたの会社は多くの仕入れ先と提携しており、時折、いくつかの仕入れ先のアカウントをゲストとしてディレクトリに追加し、サインインに Google アカウントの使用を許可する必要があります。

#### <a name="estimated-time-25-minutes"></a>推定時間: 25 分

### <a name="exercise-1---configure-identity-providers"></a>演習 1 - ID プロバイダーを構成する

#### <a name="task-1---configure-google-to-be-used-as-an-identity-provider"></a>タスク 1 - ID プロバイダーとして使用するように Google を構成する

**注** - この演習には、Google の Gmail アカウントが必要です。 新しい Google アカウントを作成し、演習の手順に従ってください。

1. https://console.developers.google.com で Google API に移動し、Google アカウントでサインインします。 共有のチーム Google アカウントを使用することをお勧めします。

1. サービスの使用条件への同意を求めるメッセージが表示されたらそのようにします。

1. 新しいプロジェクトを作成する: ページの上部にあるプロジェクト メニューを選択して、[プロジェクトの選択] ページを開きます。 [新しいプロジェクト] を選択します。  残りのフィールドは既定の設定のままにします。

1. [新しいプロジェクト] ページで、プロジェクトに名前 (**MyB2BApp** など) を付け、 **[作成]** を選択します。

1. [通知] メッセージ ボックスでリンクを選択するか、ページの上部にあるプロジェクト メニューを使用して、新しいプロジェクトを開きます。

1. 次に、 **[API とサービス]** で、 **[OAuth 同意画面]** を選択します。

1. [ユーザーの種類] で、 **[外部]** を選択し、 **[作成]** を選択します。

1. **[OAuth 同意画面]** の [アプリ情報] で、アプリケーション名 (**Azure AD** など) を入力します。

1. [User support email] (ユーザー サポートのメール) でメール アドレスを選択します。 これには、Google へのログインに使用したメール アドレスが含まれている必要があります。

1. [承認済みドメイン] の **[ドメインの追加]** を選択してから microsoftonline.com ドメインを追加します。

   ```
   microsoftonline.com
   ```

1. [開発者の連絡先情報] で、ポータルへのサインインに使用したラボ アカウントのメール アドレスを入力します。

1. **[Save and continue]** (保存して続行) を選択します。

1. 左側のメニューで、**[Credentials] (認証情報)** を選択します。

1. **[認証情報の作成]** を選択してから、 **[OAuth クライアント ID]** を選択します。

1. [アプリケーションの種類] メニューの [Web アプリケーション] を選択します。 アプリケーションの適切な名前を指定します (Azure AD B2B など)。 **[Authorized redirect URIs](承認されたリダイレクト URI)** に、次の URI を追加します。

   ```
       - https://login.microsoftonline.com
       - https://login.microsoftonline.com/te/**tenant ID**/oauth2/authresp
       (where <tenant ID> is your tenant ID)
       - https://login.microsoftonline.com/te/**tenant name**.onmicrosoft.com/oauth2/authresp
       (where <tenant name> is your tenant name)
   ```

1. [作成] を選択します。 ご自分の **クライアント ID** と **クライアント シークレット** をコピーします。 これらは、Azure portal で ID プロバイダーを追加するときに使用します。

1. テストの発行ステータスでプロジェクトを終了し、OAuth 同意画面にテスト ユーザーを追加することができます。 または、OAuth の同意画面 で [アプリの発行] ボタンを選択して、Google アカウントを持つ任意のユーザーがアプリを使用できます。

#### <a name="task-2---configure-azure-ad-for-google-federation"></a>タスク 2 - Google フェデレーション用に Azure AD を構成する

1. 制限付き管理者ディレクトリ ロールまたはゲストの招待元ロールが割り当てられたユーザーとして、[https://portal.azure.com](https://portal.azure.com) にサインインします。

1. **[Azure Active Directory]** を選択します。

1. **[管理]** で、 **[External Identities]** を選択します。

1. Microsoft では、ID プロバイダーとしての **Google** 向けに直接フェデレーションを提供しています。  これは、 **[External Identities | すべての ID プロバイダー]** ページから **[+ Google]** を選択して開始できます
 
1. [+ Google] を選択すると、別のページが開き、ID プロバイダーとして Google を構成するために必要な追加情報が表示されます。  

1. 前に取得したクライアント ID とクライアント シークレットを入力します。 [保存] を選択します。

1. これにより、ID プロバイダーとしての Google の構成が完了します。

**注** - Google をソーシャル ID プロバイダーとして追加できなかったというメッセージを受け取る場合があります。  その画面から移動し、[External Identities] に戻ると、Google がリストから利用できるようになります。

1. 既存の Gmail アカウントを使用している場合は、忘れずに、 **[External Identities | すべての ID プロバイダー]** でアカウントを削除してください。 Google 開発者コンソールに戻り、作成したプロジェクトを削除することもできます。

   **注** - このリンクを使用して、Google クライアント ID とクライアント シークレットを検索する手順を完了します。
   https://docs.microsoft.com/azure/active-directory/external-identities/google-federation

   **注** - Facebook も ID プロバイダーとして簡単に構成することもできます。 その手順は以下からアクセスできます。 https://docs.microsoft.com/azure/active-directory/external-identities/facebook-federation この演習で Google ではなく Facebook アカウントを使用する場合は、このオプションを完了します。

1. セットアップが完了したら、プライベート ブラウザーを開き、次の Web アドレスを入力します。

   ```
   login.microsoftonline.com
   ```

1. 作成した **Google** のメール アドレスとパスワードを入力します。  次に、アプリにアクセスするために Microsoft オンライン ポータルに入る必要があります。
