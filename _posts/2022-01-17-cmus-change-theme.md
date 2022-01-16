---
title: "CMUS - изменить тему оформления"
layout: post
categories: Linux
tags: [cmus, theme, music, linux]
share: true
---

После того, как [CMUS][1] успешно установлен, хорошо было бы - изменить тему оформления - с той, которая есть по умолчанию.

Это легко сделать. При установке CMUS - устанавливаются также дополнительные темы оформления. Находятся они по пути /usr/share/cmus и можно их посмотреть так:

{% highlight bash %}
ls /usr/share/cmus
{% endhighlight %}

Также список тем можно посмотреть в репозитории пакета, на GitHub - [https://github.com/cmus/cmus/tree/master/data](https://github.com/cmus/cmus/tree/master/data).

Изменить тему оформления можно командой:

{% highlight bash %}
:colorscheme gruvbox
{% endhighlight %}

... именно так - просто имя темы, без расширения. И все - можно пользоваться.

***
[1]: https://cmus.github.io/ "Сonsole music player for Unix-like operating systems"
