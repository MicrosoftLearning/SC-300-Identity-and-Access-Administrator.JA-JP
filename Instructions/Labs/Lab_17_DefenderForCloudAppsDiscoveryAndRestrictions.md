---
lab:
  title: 17 - Defender for Cloud Apps アプリケーション検出と制限適用
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# ラボ 17 - Defender for Cloud Apps アプリケーション検出と制限適用

### ログインの種類 = Microsoft 365 管理

## ラボのシナリオ

Microsoft Defender for Cloud Apps では、ユーザーがアクセスしているアプリケーションを特定するため、ネットワーク トラフィックのログを活用します。オンプレミス ファイアウォールのトラフィック ログからは、最も一般的なアプリケーションとそれにアクセスしているユーザーに関するスナップショット レポートが提供されます。マネージド デバイスからのトラフィックが Microsoft Defender for Cloud Apps 検出の概要ダッシュボードに送信されます

#### 推定時間:10 分

### 演習 1 - Defender for Cloud Apps 検出

#### タスク 1 - Defender for Cloud Apps の検出アプリ

1. グローバル管理者アカウントを使用して、[https://security.microsoft.com](https://security.microsoft.com)  にサインインします。

1. 左側のメニューで、**Cloud Apps** という名前の見出しまでスクロールし、 **[クラウド アプリ カタログ]** をクリックします。

1. **[カテゴリ別に参照]** ペインで、 **[クラウド ストレージ]** を選択します。

1. アプリの一覧で、アプリ名の横にある **[リスク スコア]** をメモします。  

1. 別のブラウザー タブを開き、**www.dropbox.com** に移動します。

1. この Web サイトにアクセスできます。

1. Dropbox のタブを閉じます。

1. Defender for Cloud Apps 画面に戻り、Dropbox の右側にある 3 つのドットを選択します。

1. **[承認済み]** を選択し、**[次へ]** ボタンをクリックします。 

#### タスク 2 - Defender for Cloud Apps でアプリを制限する

1. **[検出されたアプリ]** タイルに戻り、Dropbox の **["承認されていない" としてタグ付けする]** を選択します。  **注**:これは丸で囲まれているチェック マークの横にあります。

1. **[保存]**

1. このプロセスでは、会社の方針で承認されないアプリケーションがブロックされるため、組織内でシャドウ IT が制限されます。

**注**: アプリケーションの承認および非承認の際には遅延があります。 最大 5 分待つ必要がある場合があります。

アプリケーションが承認されていないものとしてブロックされると、Microsoft Defender for Cloud Apps と統合された MDE (Microsoft Defender for Endpoint) にオンボードされているクライアントで、ブラウザー、非公開ブラウザー、ストア ダウンロードを介してアプリケーションにアクセスできなくなります。
