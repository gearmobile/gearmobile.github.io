---
title: "Установка Compass v1.0.0 под Linux Mint"
layout: post
categories:
tags: [compass, linux]
share: true
---

> До вчерашнего дня у меня на ноутбуке под Linux Mint "Qiana" стояли два незаменимых для меня пакета для кодинга - Sass + Compass.

Оба пакета были не самой свежей версии, но стабильной. Однако, с недавних пор к ним прибавилось еще два пакета - Susy 2 и Breakpoint. Но Susy 2 для своей работы требует фреймворк Compass версии 1.0.0.

Поэтому, пришла пора обновить Compass и под Linux Mint. Под Windows 7 у меня уже давно стоит Compass-1.0.0.alpha.19 + Sass-3.3.8 (Maptastic Maple) + Susy-2.1.2 + Breakpoint-2.4.2.

Под эту систему процесс инсталляции Compass v1.0.0 замудреный и описан в этой статье - "Медиа-запросы Breakpoint в Sass".

Но работать под Windows мне не нравиться, поэтому поставил для себя задачу перейти на Compass версии 1.0.0.alpha.19 на Linux.

На момент написания статьи Compass и Sass у меня под Linux Mint "Qiana" были следующих версий:

{% highlight powershell %}
$ sass -v
Sass 3.2.19 (Media Mark)
$ compass -v
Compass 0.12.6 (Alnilam)
{% endhighlight %}

Произвожу "зачистку" системы командами:

{% highlight powershell %}
$ gem uninstall compass
$ gem uninstall sass
{% endhighlight %}

Установка Compass alpha-версии производится командой:

{% highlight powershell %}
$ gem install compass --pre
{% endhighlight %}

Но вот беда, под Linux Mint "Qiana" эта команда выдает ошибку:

{% highlight powershell %}...
Unable to install gem - Failed to build gem native extension - cannot load such file — mkmf (LoadError)
...
{% endhighlight %}

По своему прошлому опыту линуксоида зная, что почти всякая ошибка в Linux приводит к тому, что для ее решения приходится изрядно потанцевать с бубном, я приуныл. Но все-же решил погуглить - может кто-то уже сталкивался с такой проблемой и успел ее решить?

И о чудо - на StackOverflow нашелся такой вопрос и [готовое решение][1] на него. Правда, вопрос там относился к проблеме запуска Ruby определенной версии - `v 3.2.9` под Ubuntu 12.04, но это дела не меняет. Ошибка одна и таже и решение мне подошло однозначно.

На удивление, решение оказалось простым - нужно всего лишь установить в системе developer-версию Ruby - `ruby1.9.1-dev`.

На момент установки Compass версии `alpha.19` у меня имелся следующий Ruby:

{% highlight powershell %}
$ ruby -v
ruby 1.9.3p194 (2012-04-20 revision 35410) [i686-linux]
{% endhighlight %}

Ставлю developer-версию Ruby (вот оно - решение!):

{% highlight powershell %}
$ sudo apt-get install ruby1.9.1-dev
{% endhighlight %}

И затем снова пробую установить Compass alpha-версии:

{% highlight powershell %}
$ sudo gem install compass --pre
Building native extensions.  This could take a while...
Fetching: rb-inotify-0.9.5.gem (100%)
Fetching: rb-kqueue-0.2.3.gem (100%)
Fetching: listen-1.1.6.gem (100%)
Fetching: json-1.8.1.gem (100%)
Building native extensions.  This could take a while...
Fetching: compass-1.0.0.alpha.19.gem (100%)
...
{% endhighlight %}

На этот раз установка пошла успешно и Compass 1.0.0.alpha.19 появился в моей системе:

{% highlight powershell %}
$ sudo compass -v
Compass 1.0.0.alpha.19
{% endhighlight %}

Препроцессор Sass подтянулся автоматом, в качестве зависимости:

{% highlight powershell %}
$ sass -v
Sass 3.3.8 (Maptastic Maple)
{% endhighlight %}

Отлично! Теперь настала очередь сладкой парочки Susy 2 + Breakpoint:

{% highlight powershell %}
$ sudo gem install susy
Fetching: susy-2.1.2.gem (100%)
Successfully installed susy-2.1.2
...
$ sudo gem install breakpoint
Fetching: sassy-maps-0.4.0.gem (100%)
Fetching: breakpoint-2.4.2.gem (100%)
Successfully installed sassy-maps-0.4.0
Successfully installed breakpoint-2.4.2
...
{% endhighlight %}

Ну вот и все, проблема установки Compass 1.0.0.alpha.19 под Linux Mint "Qiana" успешно решена! Можно продолжать с удобством кодить под Linux.

Для полного счастья нужно еще разобраться с установкой Photoshop под Linux - тогда жизнь будет полной.

Удачного кодинга!

---

[1]: http://stackoverflow.com/questions/18316667/failed-to-build-gem-native-extension-mkmf-loaderror-ubuntu-12-04 "StackOverflow"