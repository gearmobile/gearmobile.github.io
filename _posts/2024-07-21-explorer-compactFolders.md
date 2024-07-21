---
title: "VSC - explorer.compactFolders"
layout: post
categories: Development
tags: [visual studio code, vsc, vscode]
share: true
---

В Visual Studio Code по умолчанию стоит настройка, которая отображает на владке Explorer вложенные папки таким образом:

![VSC - Default View]({{site.url}}/images/uploads/2024/07/default_view.png "VSC - Default View")

Не знаю, чем руководствовались разработчики VSC, когда устанавливали такую настройку, но мне она кажется крайне неудачной и неудобной. Я предпочитаю "классическое" отображение вложенности папок в файловой системе.

В VSC практически все поддается настройкам и этот момент также легко исправить. В Settings редактора переводим отображение настроек в режим JSON и добавляем строку:

{% highlight javascript %}
"explorer.compactFolders: false
{% endhighlight %}

... вот так:

![VSC - Custom View Settings]({{site.url}}/images/uploads/2024/07/custom_view_settings.png "VSC - Custom View Settings")

... и тогда вложенные папки принимают удобочитаемый вид:

![VSC - Custom View]({{site.url}}/images/uploads/2024/07/custom_view.png "VSC - Custom View")

---