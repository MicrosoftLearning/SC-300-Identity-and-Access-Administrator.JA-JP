---
lab:
  title: 17 - Defender for Cloud Apps アプリケーション検出と制限適用
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
  description: Microsoft Defender for Cloud Apps を使って承認されていないアプリをブロックします。 Defender ポータルの機能と使用方法を調べます。
  duration: 10 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Defender for Cloud Apps
    - Microsoft Entra
---

# ラボ 17 - Defender for Cloud Apps アプリケーション検出と制限適用

### ログインの種類 = Microsoft 365 管理

## ラボのシナリオ

Microsoft Defender for Cloud Apps では、ユーザーがアクセスしているアプリケーションを特定するため、ネットワーク トラフィックのログを活用します。オンプレミス ファイアウォールのトラフィック ログからは、最も一般的なアプリケーションとそれにアクセスしているユーザーに関するスナップショット レポートが提供されます。マネージド デバイスからのトラフィックが Microsoft Defender for Cloud Apps 検出の概要ダッシュボードに送信されます

#### 推定時間:10 分

### 演習 1 - Defender for Cloud Apps 検出

#### タスク 1 - Defender for Cloud Apps の検出アプリ

1. `https://security.microsoft.com` で全体管理者アカウントを使用して **Microsoft Defender ポータル**にサインインします。

    > **注:** サインイン中に多要素認証 (MFA) を完了するように求められる場合があります。 続行する前に、プロンプトに従って認証方法を構成または確認します。

1. **Microsoft Defender ポータル**の左側のナビゲーション メニューで、**[クラウド アプリ]** を展開し、**[クラウド アプリ カタログ]** を選択します。

1. フィルター バーで、**[カテゴリ]** を **[クラウド ストレージ]** に設定します。

1. アプリの一覧から **[Dropbox]** を選択します。

1. アプリの詳細ペインで、**[概要]** タブの下に表示される **[リスク スコア]** を確認します。

1. 新しいブラウザー タブを開き、**Dropbox** (`https://www.dropbox.com`) に移動します。

1. この Web サイトにアクセスできます。

1. Dropbox のタブを閉じます。

1. Defender for Cloud Apps の画面に戻ります。

1. **[Dropbox]** 詳細ペインで、**[承認]** を選択します。

#### タスク 2 - Defender for Cloud Apps でアプリを制限する

1. Microsoft Defender ポータルの **[クラウド アプリ カタログ]** に戻ります。

1. アプリの一覧で **[Dropbox]** を見つけます。

1. **[Dropbox]** 詳細ペインで、**[非承認]** を選択します。

1. **[保存]** をクリックして変更を適用します。

> **注:** アプリケーションの承認または非承認には遅延が生じる場合があります。 変更が有効になるまでに最大 5 分かかる場合があります。

アプリケーションが **非承認**としてマークされると、**Microsoft Defender for Endpoint** にオンボーディングされ、**Microsoft Defender for Cloud Apps** と統合されているデバイスでは、次のようなアプリへのアクセスがブロックされます。
- ブラウザー アクセス
- InPrivate または Incognito ブラウザー セッション
- ストアからのアプリのダウンロード

### 演習の概要

この演習では、Cloud App Discovery のデータを確認し、Microsoft Defender for Cloud Apps でアプリの制限を構成しました。 この演習では、組織内のシャドウ IT を特定および管理する方法を示しました。
