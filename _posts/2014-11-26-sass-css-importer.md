---
title: Плагин Sass CSS Importer
author: gearmobile
excerpt: Плагин Sass CSS Importer для импортирования файлов формата CSS в Sass-файлы. Необходим, когда нужно готовые CSS-файлы добавить к файлам формата Sass (SCSS).
layout: post
permalink: /sass-css-importer/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 16
ratings_average:
  - 4
categories:
  - Web Development
tags:
  - sass css importer
---
Краткий обзор плагина Sass CSS Importer для импортирования файлов CSS в файлы Sass.

В чем заключается вопрос? Как хорошо известно всем, кто постоянно работает с Sass [<sup>1</sup>][1]{#return-note-2082-1.simple-footnote}, с помощью директивы `@import` можно подключать одни Sass-файлы в другие Sass-файлы.

Например, подключить файл `typography.scss` в файл `main.scss` можно так:

<pre>@import “_typography”;
</pre>

Оба файла `main.scss` и `typography.scss` будут объединены препроцессором в один файл `main.scss`, который уже будет компилироваться в файл `main.css`.

Знак подчеркивания в данном случае является **дополнительной опцией**. Этим знаком препроцессору Sass указывается не выполнять **предварительную компиляцию** файла `typography.scss` в файл `typography.css` перед его подключением в `main.scss`.

Но что, если стоит задача подключения файлов формата CSS в файлы формата Sass? Директива `@import` в этом случае помочь не может. CSS-файл **нельзя просто так подключить** в Sass-файл.

Задача подключения CSS-файлов в Sass-файлы наиболее часто может возникнуть в случае использования различных готовых слайдеров или каруселей, которые зачастую идут “в комплекте” с минимальными правилами на CSS.

Что же делать?

### Плагин Sass CSS Importer

Совсем недавно (*17 июля сего года*) Chris Eppstein [<sup>2</sup>][2]{#return-note-2082-2.simple-footnote} выпустил специальный плагин, задачей которого и является **импортирование CSS-файлов** в Sass-файлы. Страничка с официальной документацией по плагину Sass CSS Importer расположена на GitHub &#8211; [Sass CSS Importer Plugin][3].

Там все описано кратко и предельно ясно. Однако, я был так доволен тем фактом, что теперь могу свободно подключать CSS в Sass, что решил потратить часть своего времени, чтобы описать его своими словами, по-русски.

### Установка Sass CSS Importer

Установка плагина выполняется как обычно, через менеджер пакетов `gem`:

<pre>$ sudo gem install --pre sass-css-importer
</pre>

### Подключение Sass CSS Importer

При использовании фреймворка Compass нужно добавить строку в конфигурационный файл `config.rb` своего текущего проекта:

<pre>require 'sass-css-importer'
</pre>

### Импортирование CSS в Sass

Теперь, чтобы импортировать CSS в Sass, нужно воспользоваться все той же директивой `@import`, но **со специальным синтаксисом**.

В общем случае этот синтаксис выглядит таким образом:

<pre>@import "CSS:имя_директории/имя_css_файла”;
</pre>

В частном случае синтаксис будет выглядеть таким образом:

<pre>@import "CSS:carousel";
</pre>

> Обратите внимание на важный момент: имя CSS-файла нужно указывать **без расширения**!

Можно запустить процесс компиляции через командную строку:

<pre>$ compass watch
</pre>

&#8230; и проверить, что CSS-файл будет включен в общий вывод.<figure id="attachment_2086" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-2086" src="http://localhost:7788/third/wp-content/uploads/2014/11/sass-css-importer-600x312.png" alt="Плагин Sass CSS Importer" width="600" height="312" />][4]<figcaption class="wp-caption-text">Плагин Sass CSS Importer</figcaption></figure> 

### Заключение

В принципе, вот и все, что можно сказать о Sass CSS Importer.

Оцените статью:  
<span id="post-ratings-2082" class="post-ratings" data-nonce="9049352bc1"><img id="rating_2082_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2082, 1, '1 Star');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2082_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2082, 2, '2 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2082_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2082, 3, '3 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2082_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2082, 4, '4 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2082_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2082, 5, '5 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>4,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2082_text"></span></span><span id="post-ratings-2082-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

<div class="simple-footnotes">
  <p class="notes">
    Notes:
  </p>
  
  <ol>
    <li id="note-2082-1">
      <a href="http://sass-lang.com/" title="Sass">Sass</a> &#8211; мощный препроцессор для CSS <a href="#return-note-2082-1">&#8617;</a>
    </li>
    <li id="note-2082-2">
      <a href="https://github.com/chriseppstein" title="Chris Eppstein">Chris Eppstein</a> &#8211; один из двух создателей <a href="http://compass-style.org" title="Compass">Compass</a> <a href="#return-note-2082-2">&#8617;</a>
    </li>
  </ol>
</div>

 [1]: #note-2082-1 "Sass &#8211; мощный препроцессор для CSS"
 [2]: #note-2082-2 "Chris Eppstein &#8211; один из двух создателей Compass"
 [3]: https://github.com/chriseppstein/sass-css-importer "Sass CSS Importer"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/11/sass-css-importer.png