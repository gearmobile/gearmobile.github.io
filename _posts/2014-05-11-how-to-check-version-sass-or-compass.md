---
title: Как узнать версию Sass и Compass
author: gearmobile
layout: post
permalink: /how-to-check-version-sass-or-compass/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - compass
  - sass
---
Так как в Sass и Compass периодически добавляются новые возможности, жизненно важным для работы веб-разработчика становиться умение проверять, какая версия Sass или Compass установлены на его локальной машине.

Так как Sass и Compass не имеют графического интерфейса, то вся работа будет выполняться в командной строке (*или терминале, кому как нравиться*). К слову стоит от себя сказать, что лично я предпочитаю работать в командной строке OS Linux, так как терминал Windows для меня &#8211; испытание не для моих слабых нервов.

Узнать текущую версию Sass можно командой:

<pre>$ sudo  sass -v
Sass 3.2.19 (Media Mark)
</pre>

Проверить текущую версию Compass можно аналогичной командой:

<pre>$ sudo  compass -v
Compass 0.12.6 (Alnilam)
...
</pre>

### Проверить доступные версии Sass и Compass

Конечно, можно проверить наличие новых версий Sass или Compass на официальных сайтах этих проектов. Однако, это занятие достаточно времязатратное и, прямо скажем, не &#8220;*кошерное*&#8221; для истинного веб-разработчика. Так как такую же задачу можно решить гораздо быстрее, с помощью командной строки.

Например, запуск команды:

<pre>$ sudo gem list sass -a -r
</pre>

&#8230; заставит Ruby вывести список пакетов (`gem`), содержащих в своем имени слово `sass`; ключ `-a` скажет Ruby, что нужно вывести список всех (`all`) пакетов; ключ `-r` скажет Ruby, что этот список нужно получить удаленно, из репозитория.

Для Compass команда будет выглядеть аналогично, за исключением ключевого слова `compass`:

<pre>$ sudo gem list compass -a -r
</pre>

Проверю наличие такого списка из своей собственной локальной машины:

<pre>$ sudo gem list sass -a -r

*** REMOTE GEMS ***

sass (3.3.7, 3.3.6, 3.3.5, 3.3.4, 3.3.3, 3.3.2, 3.3.1, 3.3.0, 3.2.19, 3.2.18, 3.2.17, 3.2.16, 3.2.15, 3.2.14, 3.2.13, 3.2.12, 3.2.11, 3.2.10, 3.2.9, 3.2.8, 3.2.7, 3.2.6, 3.2.5, 3.2.4, 3.2.3, 3.2.2, 3.2.1, 3.2.0, 3.1.21, 3.1.20, 3.1.19, 3.1.18, 3.1.17, 3.1.16, 3.1.15, 3.1.14, 3.1.13, 3.1.12, 3.1.11, 3.1.10, 3.1.9, 3.1.8, 3.1.7, 3.1.6, 3.1.5, 3.1.4, 3.1.3, 3.1.2, 3.1.1, 3.1.0)
...
</pre>

<pre>$ sudo gem list compass -a -r

*** REMOTE GEMS ***

compass (0.12.6, 0.12.5, 0.12.4, 0.12.3, 0.12.2, 0.12.1, 0.12.0, 0.11.7, 0.11.6, 0.11.5, 0.11.4, 0.11.3, 0.11.2, 0.11.1, 0.11.0, 0.10.6, 0.10.5, 0.10.4, 0.10.3, 0.10.2, 0.10.1, 0.10.0, 0.8.17, 0.8.16)
...
</pre>

Стоит сразу оговориться, что показанными выше командами проверяется наличие всех версий Sass или Compass, которые являются **стабильными версиями**.

Узнать наличие и номера **нестабильных версий** пакетов Sass и Compass можно с помощью команд:

<pre>$ sudo gem list compass --pre -r
</pre>

<pre>$ sudo gem list sass --pre -r
</pre>

### Установить нестабильные (prerelease) версии Sass и Compass

Чтобы установить самую последнюю стабильную версию Sass, нужно выполнить команду:

<pre>$ sudo gem install sass
</pre>

Если же в нестабильной (*разрабатываемой*) версии Sass есть фичи, которые необходимы вам на данный момент, то можно установить **prerelease** версию с помощью команды:

<pre>$ sudo gem install sass --pre
</pre>

Аналогично можно поступить с Compass. Последняя стабильная версия этого пакета устанавливается командой:

<pre>$ sudo gem install compass
</pre>

&#8230; а нестабильная версия пакета устанавливается командой:

<pre>$ sudo gem install compass --pre
</pre>

Один момент по установке нестабильных версий пакетов Sass или Compass. Так как версии являются нестабильными, то возможны ошибки или сбои в их работе. Их установка и работа выполняется на ваш страх и риск, как говориться.

### Удаление определенной версии Sass или Compass

Чтобы деинсталлировать определенную версию пакета Sass или Compass, нужно выполнить команду:

<pre>$ sudo gem uninstall sass --version version_number
</pre>

&#8230; или:

<pre>$ sudo gem uninstall compass --version version_number
</pre>

&#8230; где `version_number` &#8211; это номер версии удаляемого пакета; ключ `--version` говорит Ruby, что необходимо производить деинсталляцию по номеру версии пакета.

Оцените статью:  
<span id="post-ratings-1184" class="post-ratings" data-nonce="45e8c18527"><img id="rating_1184_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1184, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1184_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1184, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1184_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1184, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1184_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1184, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1184_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1184, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1184_text"></span></span><span id="post-ratings-1184-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>