---
lab:
  title: 07 - Azure AD Connect を使用してハイブリッド ID を追加する
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# ラボ 07: 省略可能 --- Azure AD Connect を使用してハイブリッド ID を追加する

**注** - このラボでは Azure Pass が必要です。 手順については、ラボ 00 を参照してください。

**注 2** - このラボには、省略可能というタイトルが付いています。  完了には少なくとも 1 時間かかります。ラボの手順で詳しく説明する必要があります。  時間の許す限り、自由に行ってください。  会社でハイブリッド構成を既に設定している場合、または Azure AD Connect を使用する予定がない場合は、このラボを飛ばしてください。

## ラボのシナリオ

会社にはオンプレミスの Active Directory Domain Services があります。  ID およびアクセス管理ソリューションとしてオンプレミスの Active Directory を引き続き使用したいと考えていますが、ユーザーが同じユーザー名とパスワードでクラウド アプリケーションにアクセスできるようにする必要もあります。

#### 予想所要時間: 60 分

### 演習 1 - オンプレミス インフラストラクチャを設定する

#### タスク 1 - オンプレミスの Active Directory インフラストラクチャを作成する

1. デプロイ テンプレートにはこのリンクからアクセスできます: [オンプレミスのテスト ラボ ガイド](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm)。

    **学習者と MCT への注意** - このテンプレートのデプロイには 30 分から 60 分かかる場合があるため、この手順で休憩を取るか、コースの講義セクションの前にデプロイを実行する準備をしてください。

    **ラボ プロバイダーへの注意** - 可能であれば、ラボ環境のセットアップの一部として完了してデプロイすることが学生に役立ちます。

2. **[TLG (テスト ラボ ガイド) - 3 VM 基本構成 (v1.0)]** ページで、 **[Azure へのデプロイ]** を選択します。

   **注** - 3 VM 基本構成では、指定したドメイン名を使用して DC1 という名前の Windows Server 2016 Active Directory ドメイン コントローラーと、Windows Server 2016 を実行している APP1 という名前のドメイン メンバー サーバーがプロビジョニングされます。 また、Windows 10 を実行しているクライアント VM をプロビジョニングするオプションも提供されますが、ラボでは使用しません (主に、Azure で VM Windows 10 を実行するときに適用されるライセンス要件が原因です)。 ドメイン メンバー サーバー (APP1) には、.NET 4.5 と IIS が自動的にインストールされています。  
   
   **注** - このラボに必要な VM は **DC1** です。  Azure Pass を使用している場合、VM は 2 台までに制限されるため、クライアント VM で失敗する可能性があります。  これはこのラボでは必要ありません。

3. **[カスタム デプロイ]** ページで、次の設定を指定し、 **[確認と作成]** を選択してから **[作成]** を選択します。

   -   [サブスクリプション]:ラボ環境の Azure VM をプロビジョニングするターゲット Azure サブスクリプションの名前。
   -   リソース グループ: (新規作成) **hybrididentity-RG**
   -   場所: ラボ環境の Azure VM をホストする Azure リージョンの名前。
   -   構成名:**TlgBaseConfig-01**
   -   ドメイン名: **corp.contoso.com**
   -   サーバー OS:**2016-Datacenter**
   -   管理者ユーザー: **demouser**
   -   管理パスワード: **覚えておく必要があるセキュリティで保護されたなパスワードを入力します**
   -   クライアント VM をデプロイする:"**いいえ**"
   -   クライアント VHD URI: **空白のままにします**
   -   VM サイズ:**Standard_D2s_v3**
   
   **注** - サブスクリプションで一覧表示されているサイズがサポートされていない場合は、同様の VM サイズを使用します。 ドキュメントは <https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes> にあります。

   -   DNS ラベル プレフィックス:**有効なグローバルに一意の DNS 名 (文字、数字、ハイフンで構成される一意の文字列。文字で始まり、最大 47 文字まで)。**

   -   _artifacts の保存先:"**既定値をそのまま使用します**"
   -   _アーティファクト ロケーション SAS トークン: **空白のままにする**

4. **[確認および作成]** を選択します。

5. 検証に合格したら、 **[作成]** を選択します。
    
6. デプロイが完了するまで待ちます。 これには 60 分ほどかかる場合があります。


### タスク 2 - ラボ環境の Azure VM を構成する

1. Azure portal が表示されているブラウザー ウィンドウで、**DC1** Azure VM に移動し、リモート デスクトップ経由で接続します。 サインインを求められたら、次の認証情報を使用してサインインします。

   -   ユーザー名: **demouser**
   -   パスワード: **タスク 1 で作成したセキュリティで保護されたパスワードを使用します**

2.  **DC1** へのリモート デスクトップ セッション内で、**Windows PowerShell ISE** を起動し、スクリプト ペインに次のスクリプトを追加し、それを実行して **DC1** と **APP1** の両方の Azure VM で Internet Explorer セキュリティ強化の構成とユーザー アクセス制御を無効にします。

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ConsentPromptBehaviorAdmin" -Value 00000000}
    ```

    **注:**  同じファイルで複数の PowerShell スクリプトを実行するために、特定のスクリプトを強調表示し、緑色の再生ボタンの横にある **[選択範囲の実行]** を選択できます。 

3.  **[Windows PowerShell ISE]** ウィンドウ内で、スクリプト ペインに次のスクリプトを追加し、それを実行して **DC1* と **APP1** の両方の Azure VM にリモート サーバー管理ツールをインストールします。

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Install-WindowsFeature RSAT -IncludeAllSubFeature} 
    ```

4.  **[Windows PowerShell ISE]** ウィンドウ内で、スクリプト ペインに次のスクリプトを追加し、それを実行して **DC1* と **APP1** の両方の Azure VM で TLS 1.2 を有効にします。

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force}
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value 1 –PropertyType DWORD}
    ```

5.  **[Windows PowerShell ISE]** ウィンドウ内で、次のスクリプトをスクリプト ペインに追加し、それを実行して**APP1** Azure VM でホストされている既定の Web サイトで Windows 統合認証を構成します。

    ```pwsh

    $vmNames = @('app1')
    Invoke-Command -ComputerName $vmNames {Enable-WindowsOptionalFeature -Online -FeatureName IIS-WindowsAuthentication}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/anonymousAuthentication" -Name Enabled -Value False -PSPath IIS:\ -Location "Default Web Site"}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/windowsAuthentication" -Name Enabled -Value True -PSPath IIS:\ -Location "Default Web Site"}
    ```

### タスク 3 - Azure VM を再起動する

1. **[Windows PowerShell ISE]** ウィンドウ内で、コンソール ペインから以下を実行して **APP1** を再起動します。

    ```pwsh

    Restart-Computer -ComputerName 'APP1'
    ```

2. **[Windows PowerShell ISE]** ウィンドウ内で、コンソール ペインから以下を実行して **DC1** を再起動します。

    ```pwsh
    Restart-Computer -ComputerName 'DC1'
    ```

### タスク 5 - ccontoso.local Active Directory を構成する

1. リモート デスクトップ経由で **DC1** Azure VM にもう一度接続します。 サインインを求められたら、次の認証情報を使用してサインインします。

    -   ユーザー名: **demouser**

    -   パスワード: **demo\@pass123**
       - **覚えておくことができる安全なパスワードを入力することを強くお勧めします。**

2.  **DC1** へのリモート デスクトップ セッション内で、Internet Explorer を起動して、以下のリンクに移動します。

    ```
    https://github.com/microsoft/MCW-Hybrid-identity/tree/main/Hands-on%20lab/studentfiles
    ```

3. **[Active Directory デモ/テスト環境のユーザー/グループの作成]** ページで、 **[CreateDemoUsers.ps1]** リンクを選択し、ライセンス条項に同意して、対応するスクリプトをローカル ファイル システムに保存します。

4. **[Active Directory デモ/テスト環境のユーザー/グループの作成]** ページで、 **[CreateDemoUsers.csv]** リンク (PowerShell コード セクションのすぐ上) を選択し、対応する csv ファイルを **CreateDemoUsers.ps1** ファイルと同じ場所に保存します。

5. **DC1** へのリモート デスクトップ セッション内で、エクスプローラーを起動し、両方のファイルをダウンロードしたフォルダーに移動し、ファイル **CreateDemoUsers.ps1** を右選択し、 **[プロパティ]** を選択し、 **[CreateDemoUsers.ps1 のプロパティ]** ダイアログ ボックスで **[ブロック解除]** チェックボックスをオンにして、 **[OK]** を選択します。

6. エクスプローラー ウィンドウ内で、もう一度ファイル **CreateDemoUsers.ps1** を右選択し、 **[編集]** を選択します。 

7. **[管理者:Windows PowerShell ISE]** ウィンドウで、**148** 行目を次のように変更します。

    ```pwsh
    $UserCount = 1000 #Up to 2500 can be created
    ```

   to
    ```pwsh
    $UserCount = 2500 #Up to 2500 can be created
    ```

8. **[Windows PowerShell ISE]** ウィンドウで、変更を保存し、**CreateDemoUsers.ps1** スクリプトを実行してラボ環境の組織単位階層を作成し、テスト ユーザー アカウントを設定します。 

9.  **[Windows PowerShell ISE]** ウィンドウ内で、次のスクリプトをスクリプト ペインに追加し、それを実行して、このラボで使用する AD ユーザー アカウントの設定を変更します。

    ```pwsh

    $adUser1 = Get-ADUser -Filter {samAccountName -eq "AGAyers"}
    $adUser1groups = $adUser1 | Get-ADPrincipalGroupMembership 
    $adUser1groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser1.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser1.DistinguishedName
    Move-ADObject -Identity $adUser1.DistinguishedName -TargetPath 'OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)

    $adUser2 = Get-ADUser -Filter {samAccountName -eq "TFBell"}
    $adUser2groups = $adUser2 | Get-ADPrincipalGroupMembership 
    $adUser2groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser2.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser2.DistinguishedName
    Move-ADObject -Identity $adUser2.DistinguishedName -TargetPath 'OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Bell\, Teresa,OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)
    Get-ADGroup -Identity 'Domain Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    Get-ADGroup -Identity 'Enterprise Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

10. **[Windows PowerShell ISE]** ウィンドウ内で、スクリプト ペインに次のスクリプトを追加し、それを実行して **Servers** と **Clients** という名前の追加の組織単位を作成し、**APP1** コンピューター アカウントを 1 つ目に移動します。

    ```pwsh

    New-ADOrganizationalUnit -Name 'Servers' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    New-ADOrganizationalUnit -Name 'Clients' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Move-ADObject -Identity 'CN=APP1,CN=Computers,DC=corp,DC=contoso,DC=com' -TargetPath 'OU=Servers,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

11. **DC1** からサインアウトします。

## 演習 2:Active Directory フォレストを Azure Active Directory テナントと統合する

### タスク 1:Azure Active Directory テナントを作成し、EMS E5 試用版をアクティブ化する

このタスクでは、次の設定で Azure Active Directory テナントを作成します。 

-   組織名:**Contoso**

-   初期ドメイン名:有効な一意のドメイン名。

-   国またはリージョン:**米国**

1. ラボ コンピューターから新しい Web ブラウザー ウィンドウを起動し、Azure portal (<https://portal.azure.com>) に移動します (まだの場合)。

2. メッセージが表示されたら、Before Hands-On Lab 演習でリソースをデプロイした Azure サブスクリプションにサインインします。

3. ラボ コンピューターで、Azure portal の **[+ リソースの作成]** を選択します。

4. **[新規]** ページの **[Marketplace の検索]** テキスト ボックスに 「**Azure Active Directory**」と入力し、結果のリストで **[Azure Active Directory]** を選択します。

5. **[Azure Active Directory]** ページで、 **[作成]** を選択します。

6. **[ディレクトリの作成]** ページで、次の設定を指定して、 **[作成]** を選択します。

[基本] タブ:
    -   テナントの種類を選択する: **[Azure Active Directory]** を選びます

[構成] タブ:
    -   組織名:**Contoso**

    -   初期ドメイン名:有効な一意のドメイン名。

    -   国またはリージョン:**米国**

7. 作成されたら、**Azure Active Directory** を開きます。

8. [概要] ページで、 **[テナントの管理]** を選びます。

9. 新しく作成したディレクトリにチェックを入れます。

10. ページの上部にある **[切り替え]** を選びます。

    >**注**:すべてが正しく表示されるまで数分かかる場合があります。

11. **[Contoso - 概要]** ページで、 **[ユーザー]** を選択します。

12. この新しいテナントには単一の ExternalAzureAD ユーザーしかいないことに注意してください。

### タスク 2: このディレクトリを管理するように Azure AD ユーザーを作成して構成する

1. ラボ コンピューターで、Azure portal の **[Contoso - 概要]** ページに戻ります。

2. **[Contoso - 概要]** ページで、左側のナビゲーションの **[管理]** の下にある **[ユーザー]** を選択します。

3. **[ユーザー すべてのユーザー]** ページで、ユーザー アカウントを表すエントリを選択します。

4. ユーザー アカウントの **[プロファイル]** ページで、 **[編集]** を選択します。

5. **[設定]** セクションの **[使用場所]** ドロップダウン リストで、 **[米国]** エントリを選び、 **[保存]** を選択します。

#### 新しい管理者を作成する

6. **[新しいユーザー]** ページで、 **[ユーザーの作成]** オプションがオンになっていることを確め、次の設定を指定して **[作成]** を選択します。

    - ユーザー名: **john.doe *@your Azure AD テナント ドメイン名***。ここで、***ご利用の Azure AD テナント ドメイン名***は、Contoso Azure AD テナントの作成時に指定したドメイン名です。

    - 名前: **john.doe**

    - 名:**John**

    - 姓:**Doe**
    
    - パスワード: **パスワードの自動生成**
    
    - パスワードの表示: **有効**にしてから、必ずパスワードをコピーしてください。

    - グループ:**グループは選択されていません**
    
    - ロール:**全体管理者**
    
    - サインインのブロック: **いいえ**
    
    - 利用場所:**米国**
    
    - 役職:**空白のままにします**
    
    - 部署:**空白のままにします**

    > **注**: **[ユーザー名]** と **[パスワード]** の値をメモ帳にコピーします。 これらは、このラボの後半で必要になります。


### タスク 5:Contoso Active Directory フォレストで DNS サフィックスを構成する

このタスクでは、新しく検証された Azure AD カスタム ドメイン名と一致するように、Contoso Active Directory フォレストの DNS サフィックスを構成します。

1. ラボ コンピューターの Azure portal で、Before Hands-On Lab 演習でリソースをデプロイした Azure サブスクリプションに関連付けられている Azure AD テナント (**既定のディレクトリ**) にサインインしていることを確認します。 そうでない場合は、Azure portal のツール バーにある **[ディレクトリ + サブスクリプション]** アイコン (**Cloud Shell** アイコンの右側) を選択して、その Azure AD テナントに切り替えます。 

2. Azure portal で、**DC1** 仮想マシンのページに移動します。

3. **DC1** 仮想マシン ページで、リモート デスクトップ経由で **DC1** に接続します。 サインインを求められたら、**demouser** 名と **demo\@pass123** パスワードを使用します。 

4. **DC1** へのリモート デスクトップ セッション内で、 **[サーバー マネージャー]** ウィンドウの **[ツール]** にある **[Active Directory ドメインと信頼関係]** コンソールを起動します。 

5. **[Active Directory ドメインと信頼関係]** コンソールで、左側の **[Active Directory ドメインと信頼関係 [DC1.corp.contoso.com]]** を右選択し、 **[プロパティ]** を選択します。

6. **[Active Directory ドメインと信頼関係 [DC1.corp.contoso.com]]** ウィンドウの **[UPN サフィックス]** タブで、 **[代替 UPN サフィックス]** テキストボックスに、前のタスクで検証したカスタム ドメインの名前を入力し、 **[追加]** を選択してから、 **[OK]** を選択します。

7. **DC1** へのリモート デスクトップ セッション内で、 **[サーバー マネージャー]** ウィンドウの **[ツール]** にある **[Active Directory ユーザーとコンピューター]** コンソールを起動します。 

8. **[Active Directory ユーザーとコンピューター]** コンソールで、左側の **[corp.contoso.com]** を展開し、ドメインの組織単位階層とドメイン グループのグループ メンバーシップを確認します。 

9.  **DC1** へのリモート デスクトップ セッション内で、Windows PowerShell ISE を起動し、[スクリプト] ペインで以下を実行して、 **[エンジニアリング]** グループのメンバーであるすべてのユーザーの UPN サフィックスを、Contoso Azure AD テナントのカスタムの検証済みドメイン名に一致するものに置き換えます (プレースホルダー `<custom_domain_name>` は、Contoso Azure AD テナントに割り当てたカスタムの検証済みドメイン名の実際の名前に置き換えます)。 

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {$_.objectClass -eq 'user'}

    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        $userName = $user.UserPrincipalName.Split('@')[0] 
        $upn = $userName + "@" + $domainName 
        $user | Set-ADUser -UserPrincipalName $upn
    }
    ```

### タスク 6:Azure AD Connect をインストールします。

このタスクでは、Azure AD Connect をインストールします。

1. **DC1** へのリモート デスクトップ セッション内で、[サーバー マネージャー] の **[ローカル サーバー]** を選択し、 **[IE セキュリティ強化の構成]** が無効になっていることを確かめます。 そうでない場合は、 **[IE セキュリティ強化の構成]** の横にある **[オン]** リンクを選択し、 **[管理者]** 設定を **[オフ]** に設定し、 **[OK]** を選択します。

2. **DC1** へのリモート デスクトップ セッション内で、 **[Windows PowerShell ISE]** ウィンドウを開き、このコマンドを実行して Chrome ブラウザーをインストールします。

    ```pwsh
    $LocalTempDir = $env:TEMP; $ChromeInstaller = "ChromeInstaller.exe"; (new-object System.Net.WebClient).DownloadFile('http://dl.google.com/chrome/install/375.126/chrome_installer.exe', "$LocalTempDir\$ChromeInstaller"); & "$LocalTempDir\$ChromeInstaller" /silent /install; $Process2Monitor = "ChromeInstaller"; Do { $ProcessesFound = Get-Process | ?{$Process2Monitor -contains $_.Name} | Select-Object -ExpandProperty Name; If ($ProcessesFound) { "Still running: $($ProcessesFound -join ', ')" | Write-Host; Start-Sleep -Seconds 2 } else { rm "$LocalTempDir\$ChromeInstaller" -ErrorAction SilentlyContinue -Verbose } } Until (!$ProcessesFound)
    ```

2. **DC1** へのリモート デスクトップ セッション内で、Chrome ブラウザーを起動し、Azure portal (<https://portal.azure.com>) に移動します。

3. サインインを求められたら、この演習で先ほどメモ帳にコピーした **john.doe** Azure AD ユーザー アカウントの資格情報を入力します。

4. メッセージが表示されたら、**john.doe** ユーザー アカウントのパスワードを変更します。 
  
    > **注**:''**同じパスワードがこれまでに何度も使われています。より推測されにくいパスワードをお選びください**'' というメッセージが表示されたら、受け入れられるほど十分に一意になるまでパスワードを変更する必要があります。

5. **サインインしたままにする**かどうかを確認するメッセージが表示された場合は、 **[いいえ]** を選択します。 Azure portal インターフェイスにリダイレクトされます。 

6. **[Microsoft Azure へようこそ]** ダイアログ ボックスが表示された場合は、 **[後で]** を選択します。 

7. Azure portal で、ポータルの左側のナビゲーションにある **[Azure Active Directory]** を選択し、 **[Contoso - 概要]** ページに移動します。

8. **[Contoso - 概要]** ページで、左側の **[管理]** の下にある **[Azure AD Connect]** を選択します。

9.  **[Azure AD Connect]** ページで、 **[Azure AD Connect をダウンロードする]** リンクを選択します。  その後、メニューから **[Connect 同期]** を選びます。

10. Microsoft ダウンロード サイトの **[Microsoft Azure Active Directory Connect]** Web ページで、 **[ダウンロード]** を選択します。

11. **AzureADConnect.msi** を実行するか保存するかを確認するメッセージが表示されたら、 **[実行]** を選択します。 これにより、ファイルがダウンロードされ、 **[Microsoft Azure Active Directory Connect]** ウィザードが自動的に起動します。 

12. **[Azure AD Connect へようこそ]** ページで、 **[ライセンス条項とプライバシーに関する声明に同意します]** ボックスをオンにし、 **[続行]** を選択します。

13. **[簡単設定]** ページで、 **[カスタマイズ]** ボタンを選択します。

14. **[必要なコンポーネントをインストールする]** ページで、オプションの構成オプションをすべて選択解除したままにして、 **[インストール]** を選択します。

15. **[ユーザー サインイン]** ページで、 **[パススルー認証]** オプションと **[シングル サインオンを有効にする]** チェック ボックスをオンにし、 **[次へ]** を選択します。

16. **[Azure AD に接続]** ページで、**john.doe** アカウントの資格情報を使用してサインインし、 **[次へ]** を選択します。

17. **[ディレクトリの接続]** ページで、**corp.contoso.com** エントリが **[フォレスト]** ドロップダウン リストに表示されていることを確めて、 **[ディレクトリの追加]** を選択します。 **[AD フォレスト アカウント]** で、 **[新しい AD アカウントの作成]** オプションがオンになっていることを確め、 **[エンタープライズ管理者ユーザー名]** テキストボックスに「**CORP.CONTOSO.COM\\demouser**」と入力し、 **[パスワード]** テキストボックスに「**demo\@pass123**」と入力して **[OK]** を選択します。


18. **[ディレクトリの接続]** ページに戻り、 **[次へ]** を選択します。

19. **[Azure AD サインイン構成]** ページで、カスタム ドメイン名が検証済みの **Active Directory UPN サフィックス**として一覧表示されていること、および **userPrincipalName** エントリが **[ユーザー プリンシパル名]** ドロップダウン リストに表示されていることを確めます。 **UPN サフィックスが検証済みのドメイン名と一致しない場合は、ユーザーがオンプレミスの資格情報を使用して Azure AD にサインインできない**ことを示す警告に注意してください。 **[一部の UPN サフィックスが検証済みドメインに一致していなくても続行する]** ボックスをオンにして、 **[次へ]** を選択します。 

    >**注**:一部のユーザーは **contoso.local** UPN サフィックスを使用してまだ構成されていますが、ルーティングできず、Azure AD テナントの検証済みカスタム ドメイン名として構成できないため、これは想定されることです。

20. **[ドメインと OU のフィルター処理]** ページで、 **[選択したドメインと OU の同期]** を選び、**DemoAccounts** OU とそのすべての子 OU のみが選択されていることを確かめて、 **[次へ]** を選択します。 


21. **[ユーザーを一意に識別]** ページで、既定の設定を受け入れ、 **[次へ]** を選択します。 


22. **[ユーザーとデバイスをフィルタリングする]** ページで、既定の設定を受け入れ、 **[次へ]** を選択します。 

23. **[オプション機能]** ページで、既定の設定を受け入れ、 **[次へ]** を選択します。

24. **[シングル サインオンを有効にする]** ページで、 **[資格情報の入力]** を選択し、 **[フォレストの資格情報]** ダイアログ ボックスで、**CORP\\demouser** ユーザー名と **demo\@pass123** パスワードでサインインし、 **[次へ]** を選択します。


25. **[構成の準備完了]** ページで、 **[構成が完了したら、同期プロセスを開始してください]** チェック ボックスがオンになって**いない**ことを確めて、 **[インストール]** を選択します。


   > **注**:同期プロセスを有効にする前に、属性レベルのフィルター処理を構成します。

   > **注**:インストールにはおよそ 2 分かかります。

26. **[構成が完了しました]** ページで、 **[終了]** を選択します。


### タスク 7:Active Directory のごみ箱を有効にする

このタスクでは、Contoso Active Directory ドメインでごみ箱を有効にします。 

1. **DC1** へのリモート デスクトップ セッション内で、[サーバー マネージャー] コンソールの [ツール] メニューにある **[Active Directory 管理センター]** を起動します。


2. **[Active Directory 管理センター]** コンソールで、左側の **[corp (ローカル)]** を右選択し、 **[ごみ箱を有効にする]** を選択します。 確認メッセージが表示されたら、**[OK]** を選択します。


3. AD 管理センターの更新を求められたら、 **[OK]** を選択します。

   > **注**:ハイブリッド シナリオでのごみ箱の利点については、<https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-recycle-bin> を参照してください

### タスク 8:Azure AD Connect 属性レベルのフィルター処理を構成する

このタスクでは、ユーザー アカウントの同期を、ターゲットの Azure AD テナントのカスタム ドメイン名と一致する UPN サフィックスを持つものに制限する Azure AD Connect 属性レベルのフィルター処理を構成します。

   > **注**:肯定のフィルター処理オプションには、少なくとも 2 つの同期規則が必要になります。 そのうちの 1 つで、同期対象のオブジェクトの正しいスコープが決定されます。 2 つ目の包括的な同期規則では、同期する必要があるオブジェクトとしてまだ識別されていないすべてのオブジェクトを除外します。

1. **DC1** へのリモート デスクトップ セッション内で、[スタート] メニューの **[Azure AD Connect]** の下にある **[同期ルール エディター]** を起動します。


2. [同期ルール エディター] ウィンドウの **[同期ルールの表示と管理]** ページで、 **[方向]** ドロップダウン リストに **[受信]** が表示されていることを確めて、 **[新しいルールの追加]** を選択します。 これにより、 **[受信方向の同期規則の作成]** ウィザードが起動します。


3. **[受信方向の同期規則の作成 - 説明]** ページで、次の設定を指定し、 **[次へ]** を選択します。

    - 名前: **Custom In from AD - UPN Filter**

    - 説明: **カスタム受信規則 - Azure AD カスタム ドメインに一致するように UPN が設定されたユーザーが含まれます**

    - 接続先システム: **corp.contoso.com**

    - 接続先システム オブジェクトの種類: **user**

    - メタバース オブジェクトの種類: **person**

    - リンクの種類: **join**

    - 優先順位:**50**

    - タグ:"**空のままにします**"

    - パスワードの同期を有効にする:"**空のままにします**"

    - 無効:"**空のままにします**"


4. **[受信スコープ フィルターの作成]** ページで、 **[グループの追加]** を選択し、 **[句の追加]** を選んで以下を指定し、 **[次へ]** を選択します。

    - 属性: **userPrincipalName**

    - 演算子:**ENDSWITH**

    - 値: **\@\<your custom domain name>**

5. **[結合規則]** ページで、 **[次へ]** を選択します。

6. **[変換]** ページで、 **[変換の追加]** を選択し、以下を指定して **[追加]** を選択します。

    - FlowType:**定数**

    - ターゲット属性: **cloudFiltered**

    - 出典:**False**

7. **次の同期サイクル中に完全インポートと完全同期が 'corp.contoso.com' で実行される**ことを示すメッセージを表示する **[警告]** ダイアログ ボックスが表示されたら、 **[OK]** を選択します。

   > **注**:これにより、新しいルールがルール リストの上部に一覧表示された、[同期ルールの表示と管理] インターフェイスに戻るはずです。 

8. **[同期ルール エディター]** ウィンドウに戻り、 **[同期ルールの表示と管理]** ページで、 **[方向]** ドロップダウン リストに **[受信]** が表示されていることを確め、 **[新しいルールの追加]** をもう一度選択します。 これにより、 **[受信方向の同期規則の作成]** ウィザードが起動します。

9. **[説明]** ページで、次の設定を指定して **[次へ]** を選択します。

    - 名前: **Custom In from AD - Catch-all Filter**

    - 説明: **カスタム受信規則 - UPN が Azure AD カスタム ドメインと一致するように設定されていないすべてのユーザーを除外します**

    - 接続先システム: **corp.contoso.com**

    - 接続先システム オブジェクトの種類: **user**

    - メタバース オブジェクトの種類: **person**

    - リンクの種類: **join**

    - 優先順位:**51**

    - タグ:"**空のままにします**"

    - パスワードの同期を有効にする:"**空のままにします**"

    - 無効:"**空のままにします**"


10. **[スコーピング ファイラー]** ページで、 **[次へ]** を選択します。

11. **[結合規則]** ページで、 **[次へ]** を選択します。

12. **[変換]** ページで、 **[変換の追加]** を選択し、以下を指定して **[追加]** を選択します。

    - FlowType:**定数**

    - ターゲット属性: **cloudFiltered**

    - 出典:**True** にします

13. **次の同期サイクル中に完全インポートと完全同期が 'corp.contoso.com' で実行される**ことを示すメッセージを表示する **[警告]** ダイアログ ボックスが表示されたら、 **[OK]** を選択します。

    >**注**:これにより、新しいルールがルール リストの上部に一覧表示された、 **[同期ルールの表示と管理]** インターフェイスに戻るはずです。 

### タスク 9:ディレクトリ同期を開始して確認する

1. **DC1** へのリモート デスクトップ セッション内で、 **[Azure AD Connect]** デスクトップ ショートカットをダブル選択します。

2. **[Azure AD Connect へようこそ]** ページで、 **[構成]** を選択します。 

3. **[追加のタスク]** ページで、 **[カスタマイズ同期オプション]** を選択し、 **[次へ]** を選択します。

4. **[Azure AD に接続]** ページで、**john.doe** アカウントの資格情報を使用してサインインし、 **[次へ]** を選択します。

5. **[ディレクトリの接続]** ページで、 **[次へ]** を選択します。

6. **[ドメインと OU のフィルタリング]** ページで、 **[次へ]** を選択します。 

7. **[オプション機能]** ページで、既定の設定を受け入れ、 **[次へ]** を選択します。

8. **[シングル サインオンを有効にする]** ページで、 **[次へ]** を選択します。

9. **[構成の準備完了]** ページで、 **[構成が完了したら、同期プロセスを開始してください]** チェック ボックスをオンにし、 **[構成]** を選択します。

10. **[構成が完了しました]** ページで、 **[終了]** を選択します。

11. **DC1** へのリモート デスクトップ セッション内で、Azure portal が表示されている Edge ブラウザー ウィンドウで、Contoso Azure AD テナントの **[ユーザー - すべてのユーザー]** ページに移動します。

12. **[ユーザー - すべてのユーザー]** ページで、ユーザー オブジェクトのリストには、Azure AD テナントのカスタム ドメイン名と一致する UPN サフィックスを持つすべてのユーザー アカウントが含まれていることに注意してください。 ページを更新するか、変更が表示されるまで数分待つ必要がある場合があります。

13. Azure portal で、Contoso Azure AD テナントの **[グループ - すべてのグループ]** ページに移動し、すべての corp.contoso.com ドメイン グループも同期されていることに注意してください。 

14. Azure portal で、 **[Contoso - Azure AD Connect]** ページに移動し、左側にある **[Azure AD Connect]** を選択します。 次のように設定されていることを確認します。 

    - Azure AD Connect 同期状態:**有効** 
  
    - 最後の同期:**これは何らかのタイムスタンプである必要があります**。 
  
    - パスワード ハッシュの同期:**Disabled** 
  
    - フェデレーション：**Disabled**
   
    - シームレスなシングル サインオン:**1 ドメインに対して有効** 
  
    - パススルー認証:**1 エージェントで有効**

   > **注**:運用環境では、冗長性のために追加のエージェントをインストールします。 詳細については、「<https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start>」を参照してください。

### タスク 10:ハイブリッド Azure AD 参加を構成する

このタスクでは、Azure AD Connect デバイス同期オプションを構成します。

1. **DC1** へのリモート デスクトップ セッション内で、 **[Azure AD Connect]** デスクトップ ショートカットをダブル選択します。

2. **[Azure AD Connect へようこそ]** ページで、 **[構成]** を選択します。 

3. **[追加のタスク]** ページで、 **[デバイス オプションの構成]** を選択し、 **[次へ]** を選択します。

4. **[概要]** ページで、**ハイブリッド Azure AD 参加**と**デバイスのライトバック**に関する情報を確認し、 **[次へ]** を選択します。

5. **[Azure AD に接続]** ページで、**john.doe** アカウントの資格情報を使用してサインインし、 **[次へ]** を選択します。

6. **[デバイス オプション]** ページで、 **[ハイブリッド Azure AD 参加の構成]** オプションがオンになっていることを確めて、 **[次へ]** を選択します。 

7. **[デバイスのオペレーティング システム]** ページで、 **[Windows 10 以降のドメインに参加しているデバイス]** と **[サポートされている Windows ダウンレベル ドメインに参加しているデバイス]** のチェック ボックスをオンにし、 **[次へ]** を選択します。 

   > **注**:マネージド ドメインのシームレスな SSO またはフェデレーション ドメインの AD FS などのフェデレーション サービスを使用している場合にのみ、Windows ダウンレベル デバイスはサポートされています。

8. **[SCP の構成]** ページで、**corp.contoso.com** Active Directory フォレスト ボックスをオンにし、 **[認証サービス]** ドロップダウン リストで **[Azure Active Directory]** エントリを選び、 **[追加]** を選択します。

9. corp.contoso.com のエンタープライズ管理者の資格情報の入力を求められたら、 **[Windows のセキュリティ]** ダイアログ ボックスで、**CORP\\demouser** ユーザー名と **demo\@pass123** パスワードでサインインします。

10. **[SCP 構成]** ページに戻り、 **[次へ]** を選択します。

11. **[構成の準備完了]** ページで、 **[構成]** を選択します。

12. **[構成が完了しました]** ページで、タスクが正常に完了したことを確認し、 **[終了]** を選択します。


### タスク 11:ハイブリッド Azure AD 参加を実行する

1. ラボ コンピューターの Azure portal で、Before Hands-On Lab 演習でリソースをデプロイした Azure サブスクリプションに関連付けられている Azure AD テナント (**既定のディレクトリ**) にサインインしていることを確認します。 そうでない場合は、Azure portal のツール バーにある **[ディレクトリ + サブスクリプション]** アイコン (**Cloud Shell** アイコンの右側) を選択して、その Azure AD テナントに切り替えます。 

2. Azure portal で、**APP1** 仮想マシンのページに移動します。

3. **APP1** 仮想マシン ページで、リモート デスクトップ経由で **APP1** に接続します。 サインインを求められたら、**AGAyers\@<custom_domain_name>** ユーザー名と **demo@pass123** パスワードを使用します (ここで **<custom_domain_name>** プレースホルダーは、この演習で先ほど Contoso Azure AD テナントに割り当てたカスタム DNS ドメイン名を表します)。

4. **APP1** へのリモート デスクトップ セッション内で、 **[サーバー マネージャー]** ウィンドウの **[ツール]** にある **[タスク スケジューラ]** を起動します。 


5. **[タスク スケジューラ]** コンソールで、 **[タスク スケジューラ ライブラリ]**  >  **[Microsoft]**  >  **[Windows]**  >  **[Workplace Join]** に移動します。 そこから、**Automatic-Device-Join** タスクを有効にして実行します。 


6. **DC1** へのリモート デスクトップ セッションに切り替え、Windows PowerShell ISE ウィンドウのコンソール ペインから、以下を実行して Azure AD Connect の差分同期を開始します。

   ```pwsh
   Import-Module -Name 'C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1'
   
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. **APP1** へのリモート デスクトップ セッションに戻り、**コマンド プロンプト**を起動します。

8. コマンド プロンプト ウィンドウで、以下を実行して APP1 の Azure AD 登録状態を確認します。 

   ```
   dsregcmd /status
   ```

9. コマンドの出力が次のようになっていることを確認します。

   ```
   +----------------------------------------------------------------------+
   | Device State                                                         |
   +----------------------------------------------------------------------+

        AzureAdJoined : YES
     EnterpriseJoined : NO
             DeviceId : 61eea2b8-efbe-43d9-b267-126433c8ee34
           Thumbprint : BBAAA0FB4A55E880388851BED955A2669A961A96
       KeyContainerId : 2eb75eb8-0a1d-437b-99d9-9dd161ca0d90
          KeyProvider : Microsoft Software Key Storage Provider
         TpmProtected : NO
         KeySignTest: : PASSED
                  Idp : login.windows.net
             TenantId : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
           TenantName : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
          AuthCodeUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/authorize
       AccessTokenUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/token
               MdmUrl :
            MdmTouUrl :
     MdmComplianceUrl :
          SettingsUrl :
       JoinSrvVersion : 1.0
           JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/
            JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net
        KeySrvVersion : 1.0
            KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/
             KeySrvId : urn:ms-drs:enterpriseregistration.windows.net
         DomainJoined : YES
           DomainName : CORP

   +----------------------------------------------------------------------+
   | User State                                                           |
   +----------------------------------------------------------------------+

               NgcSet : NO
      WorkplaceJoined : NO
        WamDefaultSet : NO
           AzureAdPrt : NO

   +----------------------------------------------------------------------+
   | Ngc Prerequisite Check                                               |
   +----------------------------------------------------------------------+

        IsUserAzureAD : NO
        PolicyEnabled : NO
       DeviceEligible : YES
   SessionIsNotRemote : NO
     X509CertRequired : NO
         PreReqResult : WillNotProvision

   ```
11. **DC1** へのリモート デスクトップ セッションに戻り、Azure portal が表示されている Edge ブラウザー ウィンドウで、Contoso Azure AD テナントの **[デバイス - すべてのデバイス]** ページに移動し、 **[結合の種類]** が **[Hybrid Azure AD joined]** に設定されている APP1 サーバーを表すエントリがあることを確認します。

   > **注**:Azure AD 登録の状態が正しく報告され、その Azure AD オブジェクトが Azure portal に表示されるまで待つ必要がある場合があります。


