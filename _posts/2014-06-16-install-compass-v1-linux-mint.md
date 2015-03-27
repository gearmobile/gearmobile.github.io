---
title: Установка Compass v1.0.0 под Linux Mint
author: gearmobile
excerpt: 'До вчерашнего дня у меня на ноутбуке под Linux Mint "Qiana" стояли два незаменимых для меня пакета для кодинга - Sass + Compass. Оба пакета были не самой свежей версии, но стабильной. Однако, с недавних пор к ним прибавилось еще два пакета - Susy 2 и Breakpoint. Но Susy 2 для своей работы требует фреймворк Compass версии 1.0.0.'
layout: post
permalink: /install-compass-v1-linux-mint/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - OS Linux
tags:
  - compass
  - linux
---
До вчерашнего дня у меня на ноутбуке под Linux Mint &#8220;Qiana&#8221; стояли два незаменимых для меня пакета для кодинга &#8211; Sass + Compass. Оба пакета были не самой свежей версии, но стабильной. Однако, с недавних пор к ним прибавилось еще два пакета &#8211; Susy 2 и Breakpoint. Но Susy 2 для своей работы требует фреймворк Compass версии 1.0.0.

Поэтому, пришла пора обновить Compass и под Linux Mint. Под Windows 7 у меня уже давно стоит Compass-1.0.0.alpha.19 + Sass-3.3.8 (Maptastic Maple) + Susy-2.1.2 + Breakpoint-2.4.2. Под эту систему процесс инсталляции Compass v1.0.0 замудреный и описан в этой статье &#8211; [Медиа-запросы Breakpoint в Sass][1] . Но работать под Windows мне не нравиться, поэтому поставил для себя задачу перейти на Compass версии 1.0.0.alpha.19 на Linux.

На момент написания статьи Compass и Sass у меня под Linux Mint &#8220;Qiana&#8221; были следующих версий:

<pre>$ sass -v
Sass 3.2.19 (Media Mark)
$ compass -v
Compass 0.12.6 (Alnilam)
</pre>

Произвожу &#8220;зачистку&#8221; системы командами:

<pre>$ gem uninstall compass
$ gem uninstall sass
</pre>

Установка Compass alpha-версии производится командой:

<pre>$ gem install compass --pre
</pre>

Но вот беда, под Linux Mint &#8220;Qiana&#8221; эта команда выдает ошибку:

<pre>...
Unable to install gem - Failed to build gem native extension - cannot load such file — mkmf (LoadError)
...
</pre>

По своему прошлому опыту линуксоида зная, что почти всякая ошибка в Linux приводит к тому, что для ее решения приходится изрядно потанцевать с бубном, я приуныл. Но все-же решил погуглить &#8211; может кто-то уже сталкивался с такой проблемой и успел ее решить? И о чудо &#8211; на StackOverflow нашелся такой вопрос и <a href="http://stackoverflow.com/questions/18316667/failed-to-build-gem-native-extension-mkmf-loaderror-ubuntu-12-04" title="StackOverflow" target="_blank">готовое решение</a> на него. Правда, вопрос там относился к проблеме запуска Ruby определенной версии &#8211; `v 3.2.9` под Ubuntu 12.04, но это дела не меняет. Ошибка одна и таже и решение мне подошло однозначно.

На удивление, решение оказалось простым &#8211; нужно всего лишь установить в системе developer-версию Ruby &#8211; `ruby1.9.1-dev`.

На момент установки Compass версии alpha.19 у меня имелся следующий Ruby:

<pre>$ ruby -v
ruby 1.9.3p194 (2012-04-20 revision 35410) [i686-linux]
</pre>

Ставлю developer-версию Ruby (вот оно &#8211; решение!):

<pre>$ sudo apt-get install ruby1.9.1-dev
</pre>

И затем снова пробую установить Compass alpha-версии:

<pre>$ sudo gem install compass --pre
Building native extensions.  This could take a while...
Fetching: rb-inotify-0.9.5.gem (100%)
Fetching: rb-kqueue-0.2.3.gem (100%)
Fetching: listen-1.1.6.gem (100%)
Fetching: json-1.8.1.gem (100%)
Building native extensions.  This could take a while...
Fetching: compass-1.0.0.alpha.19.gem (100%)
...
</pre>

На этот раз установка пошла успешно и Compass 1.0.0.alpha.19 появился в моей системе:

<pre>$ sudo compass -v
Compass 1.0.0.alpha.19
</pre>

Препроцессор Sass подтянулся автоматом, в качестве зависимости:

<pre>$ sass -v
Sass 3.3.8 (Maptastic Maple)
</pre>

Отлично! Теперь настала очередь сладкой парочки Susy 2 + Breakpoint:

<pre>$ sudo gem install susy
Fetching: susy-2.1.2.gem (100%)
Successfully installed susy-2.1.2
...
$ sudo gem install breakpoint
Fetching: sassy-maps-0.4.0.gem (100%)
Fetching: breakpoint-2.4.2.gem (100%)
Successfully installed sassy-maps-0.4.0
Successfully installed breakpoint-2.4.2
...
</pre>

Ну вот и все, проблема установки Compass 1.0.0.alpha.19 под Linux Mint &#8220;Qiana&#8221; успешно решена! Можно продолжать с удобством кодить под Linux.

Для полного счастья нужно еще разобраться с установкой Photoshop под Linux &#8211; тогда жизнь будет полной.

Удачного кодинга!

Оцените статью:

<span id="post-ratings-1347" class="post-ratings" data-nonce="b1c7d619cb"><img id="rating_1347_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1347, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1347_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1347, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1347_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1347, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1347_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1347, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1347_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1347, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1347_text"></span></span><span id="post-ratings-1347-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1065 "Медиа-запросы Breakpoint в Sass"