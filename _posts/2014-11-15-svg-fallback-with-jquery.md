---
title: 'SVG fallback  с помощью jQuery'
author: gearmobile
excerpt: 'Реализация кросс-браузерной поддержки SVG с помощью плагинов под jQuery. Плагины SVGMagic и SVGeezy помогут облегчить задачу  SVG fallback на web-странице.'
layout: post
permalink: /svg-fallback-with-jquery/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 6
ratings_average:
  - 3
categories:
  - Web Development
tags:
  - jquery
  - svg fallback
---
Краткая статья, посвященная тому же вопросу &#8211; как реализовать кросс-браузерную поддержку SVG в браузерах. В предыдущей статье &#8220;[SVG fallback с помощью PNG][1]&#8221; было показано **четыре очень интересных способа** реализации такой задачи.

В этой статье будут показаны также несколько способов решения, но уже **с помощью библиотеки jQuery** .

В начале статьи автор рассказывает о преимуществах использования формата графики SVG. Думаю, что многие уже устали читать деферамбы о пользе SVG. Мне, как переводчику, тем более надоело переводить всю эту &#8220;воду&#8221;, поэтому смело ее опускаю и перехожу к главному.

* * *

### jQuery и Modernizr

Для реализации этого способа понадобиться библиотека Modernizr. Код реализации должен выглядеть таким образом:

<pre>// Javascript

if (Modernizr.svg) {
 // Supports SVG
} else {
 // Doesn't support SVG (Fallback)
}
 </pre>

Если Modernizr обнаружит, что пользовательский браузер не поддерживает SVG, то запуститься простой jQuery-скрипт, который произведет замену расширения `svg` на `png` у всех файлов-изображений:

<pre>// Javascript

 if (!Modernizr.svg) {
    $('img[src*="svg"]').attr('src', function() {
       return $(this).attr('src').replace('.svg', '.png');
    });
 }
 </pre>

Данный способ имет точно такие же ограничения, что и скрипт из предыдущей статьи &#8211; &#8220;[SVG fallback с помощью PNG][1]&#8220;. То есть, нужно иметь два комплекта файлов &#8211; один в SVG-формате, другой в PNG-формате. Имена файлов должны быть идентичными.

### SVGMagic &#8211; плагин под jQuery

[SVGMagic][2] &#8211; это простой плагин под библиотеку jQuery, который отыскивает в HTML-документе все SVG-изображения (в том числе и фоновые SVG-изображения). А затем им создаются PNG-копии всех найденных SVG-изображений, если браузер пользователя не поддерживает SVG.

Для работы с плагином SVGMagic достаточно установить его в проект и запустить инициализацию через jQuery:

<pre>// jQuery

 $(document).ready(function(){
    $('img').svgmagic();
 });
 </pre>

Работа плагина SVGMagic строится следующим образом. Проверяется возможность браузером пользователя отображения SVG-изображений. Если такой поддержки нет, то плагин выполняет полную проверку всего HTML-документа и собирает коллекцию всех URL на SVG-файлы, размещенные внутри этого документа.

Затем эта коллекция URL отправляется на сервер плагина. Сервер производит скачивание всех SVG-изображений по этим URL. Затем производиться конвертирование SVG в PNG.

На страницу клиента отправляется новая коллекция URL, которые теперь указывают на файлы формата PNG. Браузер посетителя загружает по этим ссылкам новые PNG-файлы и внешний вид страницы не нарушается.

### SVGeezy &#8211; еще один плагин jQuery

[SVGeezy][3] является fallback-плагином в полном смысле этого слова. Плагин проверяет поддержку SVG в браузере пользователя. Если таковой нет, то выполняется замена значения в атрибуте `src` на то, в котором указывается на путь PNG-файла.

Для работы с плагином нужно подключить его в проект и инициализировать:

<pre>// jQuery

 svgeezy.init(false, 'png');
 </pre>

Первый параметр плагина SVGeezy &#8220;говорит&#8221; ему &#8211; **не выполнять** или **выполнять** проверку. Если необходима проверка плагином SVGeezy браузера и замена изображений, то нужно оставить значение в `false`. Этот параметр может понадобиться в случае, когда нет необходимости в работе плагина на каких-то страницах.

Второй параметр &#8211; это **тип файла**, который будет заменять SVG на странице. Тип файла **может быть любым**; только нужно удостовериться, что файлы с таким расширением существуют.

Например, файл по пути `/images/logo.svg` будет заменен файлом по пути `/images/logo.png`.

* * *

На этом самая интересная часть статьи &#8220;[How to fallback to PNG if SVG not supported?][4]&#8221; завершается. Как лично мне кажется, в данной статье заслуживают внимания только **первый** и **последний** способы реализации SVG fallback.

Оцените статью:  
<span id="post-ratings-2010" class="post-ratings" data-nonce="8b515de1e6"><img id="rating_2010_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2010, 1, '1 Star');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2010_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2010, 2, '2 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2010_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2010, 3, '3 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2010_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2010, 4, '4 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2010_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2010, 5, '5 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>3,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2010_text"></span></span><span id="post-ratings-2010-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=2001 "SVG fallback с помощью PNG"
 [2]: https://dirkgroenen.github.io/SVGMagic/index.html "SVGMagic"
 [3]: http://benhowdle.im/svgeezy/ "SVGeezy"
 [4]: http://www.jquerybyexample.net/2014/09/how-to-svg-fallback-with-png-jquery.html "How to fallback to PNG if SVG not supported?"