---
title: オンラインでホストされている手順
permalink: index.html
layout: home
ms.openlocfilehash: 3f1d9eb9d23b41f212641797985d518792859159
ms.sourcegitcommit: 317faec6fdf204c92dfe1461d4a30f5b8d8ea950
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2022
ms.locfileid: "138357270"
---
# <a name="content-directory"></a>コンテンツ ディレクトリ

必要なラボ ファイルは、[こちらからダウンロード](https://github.com/MicrosoftLearning/SC-300-Identity-and-Access-Administrator/archive/master.zip)できます

各ラボの演習とデモへのハイパーリンクを以下に示します。

## <a name="labs"></a>ラボ

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| モジュール | ラボ |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
