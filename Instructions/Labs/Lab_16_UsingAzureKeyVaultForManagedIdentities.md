---
lab:
  title: 16 - マネージド ID に Azure Key Vault を使用する
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# ラボ 16 - マネージド ID に Azure Key Vault を使用する

**注** - このラボでは Azure Pass が必要です。 手順については、ラボ 00 を参照してください。

## ラボのシナリオ

Azure リソースのマネージド ID を使用するとき、Azure AD 認証をサポートするリソースに対して認証するためのアクセス トークンをコードで取得できます。ただし、すべての Azure サービスが Azure AD 認証をサポートしているわけではありません。 Azure リソースのマネージド ID をこれらのサービスと共に使用するには、Azure Key Vault にサービス資格情報を保存し、マネージド ID を使用して Key Vault にアクセスして、資格情報を取得します。

#### 推定時間:20 分

### 演習 1 - Azure Key Vault を使用して仮想マシン ID を管理する

#### タスク 1 - Windows 仮想マシンを作成する

1. [https://portal.azure.com](https://portal.azure.com) を参照します

1. **[+ リソースの作成]** を選択します。

1. [マーケットプレースを検索] 検索バーに「**Windows クライアント**」と入力します。

1. **[Windows クライアント]** を選び、プランのドロップダウンから **[Windows 10 Enterprise、バージョン 22H2 - x64 Gen 1]** を選びます。 次に、 **[作成]** を選択します。

1. [基本] タブで VM 用の管理者ユーザー名とパスワードを作成する必要があります。

1. **[管理]** タブで、 **[システム割り当てマネージド ID を有効にする]** ボックスをオンにします。

1. 仮想マシンの作成エクスペリエンスの残りの部分に移動します。 

1. [作成] を選択します。

#### タスク 2: キー コンテナーを作成する

1. グローバル管理者アカウントを使用して、[https://portal.azure.com]( https://portal.azure.com) にサインインします。

1. 左側のナビゲーション バーの上部で、 [リソースの作成] を選択します。

1. [Marketplace を検索] ボックスに「**Key Vault**」と入力します。  

1. 結果から **[Key Vault]** を選択します。

1. **［作成］** を選択します

1. 次に示すように、必要なすべての情報を入力します。 このラボで使用しているサブスクリプションを選択していることを確認してください。
    **注** キー コンテナー名は一意である必要があります。 フィールドの右側にある緑色のチェックマークを探します。

 - **リソース グループ** - sc300KeyVaultrg
 - **キー コンテナー名** - *anyuniquevalue*
 - **[アクセスの構成]** ページで、 **[Vault Access Policy] (コンテナーのアクセス ポリシー)** ラジオ ボタンをオンにします。
1. **[確認と作成]** を選択します。

1. **［作成］** を選択します


#### タスク 3 - シークレットを作成する

1. 新しく作成した Key Vault に移動します。

1. **[Secrets](シークレット)** を選択します。

1. **[生成/インポート]** を選択します。

1. [シークレットの作成] 画面の [アップロード オプション] で、 **[手動]** を選択したままにします。

1. シークレットの名前と値を指定します。  値は任意のものを指定できます。 

1. アクティブ化した日付と有効期限の日付をクリアのままにし、[有効] を [はい] のままにします。 

1. **[作成]** を選択して、シークレットを作成します。

#### タスク 4 - Key Vault へのアクセス許可を付与する

1. 新しく作成した Key Vault に移動します。

1. 左側のメニューで、 **[アクセス ポリシー]** を選択します。

1. **[+ 作成]** を選択します。

1. [アクセス ポリシーの追加] セクションで、[テンプレートからの構成 (省略可能)] のプルダウン メニューから [シークレットの管理] を選択します。

1. **[プリンシパルの選択]** で、 **[なし]** を選択して、選択するプリンシパルの一覧を開きます。 検索フィールドで、タスク 2 で作成した VM の名前を入力します。  結果一覧で VM を選択し、 [選択] を選択します。

1. **[追加]** を選択します。

1. **[保存]** を選択します。

#### タスク 5 - PowerShell を使用して Key Vault シークレットを使用してデータにアクセスする

1. ラボの仮想マシンから PowerShell を開きます。  

1. PowerShell では、テナント上で Web 要求を呼び出し、VM の特定のポートでローカル ホストのトークンを取得します。  

    ```
    $Response = Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -Method GET -Headers @{Metadata="true"}
    ```

1. 次に、アクセス トークンを応答から抽出します。  

    ```
    $KeyVaultToken = $Response.access_token
    ```

1. PowerShell の Invoke-WebRequest コマンドを使用して、Key Vault で以前に作成したシークレットを取得し、Authorization ヘッダーにアクセス トークンを渡します。  Key Vault の [概要] ページの [要点] セクションにある Key Vault の URL が必要です。  リマインダー - Key Vault の URI は、[概要] タブにあります。

    ```
    Invoke-RestMethod -Uri https://<your-key-vault-URI>/secrets/<secret-name>?api-version=2016-10-01 -Method GET -Headers @{Authorization="Bearer $KeyVaultToken"}
    ```
1. 次のような応答を受け取ります。 
    ```
    'My Secret' https://mi-lab-vault.vault.azure.net/secrets/mi-test/50644e90b13249b584c44b9f712f2e51 @{enabled=True; created=16…
    ```
1. このシークレットは、名前とパスワードを必要とするサービスに対する認証に使用できます。
