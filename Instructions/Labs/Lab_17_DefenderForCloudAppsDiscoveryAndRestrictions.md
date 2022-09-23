---
lab:
  title: 17 - Defender for Cloud Apps アプリケーション検出と制限適用
  learning path: "03"
  module: Module 03 - Implement Access Management for Apps
ms.openlocfilehash: 2810d72197e31241d7a3c30d85b40cc5682be0bf
ms.sourcegitcommit: fa8ae52be1e809ca81d07036fefeebffb54c1861
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2022
ms.locfileid: "147521461"
---
# <a name="lab-17---defender-for-cloud-apps-application-discovery-and-enforcing-restrictions"></a>ラボ 17 - Defender for Cloud Apps アプリケーション検出と制限適用

## <a name="lab-scenario"></a>ラボのシナリオ

Microsoft Defender for Cloud Apps では、ユーザーがアクセスしているアプリケーションを特定するため、ネットワーク トラフィックのログを活用します。  オンプレミス ファイアウォールのトラフィック ログからは、最も一般的なアプリケーションとそれにアクセスしているユーザーに関するスナップショット レポートが提供されます。  マネージド デバイスからのトラフィックが Microsoft Defender for Cloud Apps 検出の概要ダッシュボードに送信されます

#### <a name="estimated-time-10-minutes"></a>推定時間:10 分

### <a name="exercise-1---defender-for-cloud-apps-discovery"></a>演習 1 - Defender for Cloud Apps 検出

#### <a name="task-1---discovery-apps-in-defender-for-cloud-apps"></a>タスク 1 - Defender for Cloud Apps の検出アプリ

1. グローバル管理者アカウントを使用して、[https://security.microsoft.com](https://security.microsoft.com) にサインインします。

1. 左側のメニューで、一番下までスクロールし、 **[その他のリソース]** を選択します。

1. **[その他のリソース]** ウィンドウの **[Microsoft Defender for Cloud Apps]** で **[開く]** を見つけて選択します。  Microsoft 365 アカウント内で **Microsoft Defender for Cloud Apps** ポータルに異動します。

1. 左側のメニューで **[検出]** ドロップダウンを選択し、 **[クラウド アプリ カタログ]** を選択します。

1. **[カテゴリ別に参照]** で **[クラウド ストレージ]** を選択します。

1. アプリの一覧で、アプリ名の横にある **[リスク スコア]** をメモします。  

1. 別のブラウザー タブを開き、**Dropbox.com** に移動します。

1. この Web サイトにアクセスできます。


#### <a name="task-2---restrict-apps-in-defender-for-cloud-apps"></a>タスク 2 - Defender for Cloud Apps でアプリを制限する

1. **[検出されたアプリ]** タイルに戻り、Dropbox の **["承認されていない" としてタグ付けする]** を選択します。  **注**:これは丸で囲まれているチェック マークの横にあります。

1. このプロセスでは、会社の方針で承認されないアプリケーションがブロックされるため、組織内でシャドウ IT が制限されます。

**注**:アプリケーションを禁止してからそのアプリケーションがブロックされるまでの間、遅延があります。

1. アプリケーションが未承認としてブロックされると、ブラウザー、非公開ブラウザー、ストア ダウンロードでそのアプリケーションにアクセスできなくなります。



