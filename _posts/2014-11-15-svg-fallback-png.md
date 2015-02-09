---
title: SVG fallback с помощью PNG
author: gearmobile
excerpt: Четыре способа реализовать кросс-браузерную поддержку SVG-изображений с помощью отката fallback к изображениям формата PNG. Три метода из четырех используют библиотеку Modernizr. Четвертый способ реализован на чистом CSS. Ни в одном из способов не используется библиотека jQuery.
layout: post
permalink: /svg-fallback-png/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Web Development
tags:
  - png
  - svg fallback
---
**Примечание переводчика**: статья просто отличная и написана мастером своего дела Nick.

Немного лирики &#8220;для тех, кто в танке&#8221; &#8211; fallback можно в данном контексте перевести как &#8211; &#8220;откат&#8221;. То есть, если браузер по каким-то причинам **не поддерживает** SVG, то на web-странице выполняется &#8220;откат&#8221; &#8211; SVG-изображения **заменяются** на PNG-изображения.

В этом и заключается вся фишка данного способа. Но вот реализаций этого способа несколько и они рассмотрены ниже. Лично меня впечатлил **второй способ** (*впрочем, не только меня &#8211; можно почитать комментарии к [статье-оригиналу][1]*).

Далее &#8211; текст автора по имени Nick (*в вольном переводе*).

* * *

В следующих четырех сниппетах я рассмотрю применение метода SVG fallback c помощью PNG-изображений **четырьмя различными способами**. Все четыре способа направлены на одну цель &#8211; обеспечение **кросс-браузерной поддержки SVG** на web-странице.

Если вы еще не используете SVG в своих проектах, то вам следует уже начать это делать. SVG великолепен и является прекрасным способом минимизации и упрощения спрайтов; в частности, когда это касается таких вещей, как иконки. Если на создаваемом вами сайте все изображения сохранены в формате PNG, то для вас самое время перескочить на SVG-поезд.

Ниже показаны сниппеты, которые тремя различными путями осуществляют применение SVG, а также SVG fallback к изображениям формата PNG, если браузер не поддерживает SVG.

Что мы будем рассматривать:

  * SVG в качестве фонового изображения, fallback с помощью Modernizr
  * SVG в качестве фонового изображения, fallback с помощью CSS
  * SVG в качестве встраиваемого изображения (тег img), onerror fallback
  * SVG в качестве встраиваемого изображения (тег img), , fallback с помощью Modernizr

[Modernizr][2] является прекрасным инструментом для определения возможностей браузера. Она автоматически добавляет ко всем HTML-элементам в DOM классы в зависимости от того, поддерживает браузер ту или иную возможность или нет. В нашем случае, Modernizr будет добавлять класс `svg` или `no-svg` для всех элементов в DOM в зависимости от того, поддерживает ли браузер SVG.

### SVG в качестве фонового изображения, fallback с помощью Modernizr

Используя Modernizr, мы отпеределяем, поддерживает браузер SVG или нет. Если SVG используется в качестве фонового изображения, то тогда проще сохранить изображения для страницы в двух верысиях &#8211; SVG и PNG (прим. переводчика: например, IcoMoon умеет так делать). В таблице стилей CSS тогда нужно добавить дополнительный класс. При таком подходе исключается двойная загрузка файлов (SVG и PNG), так как класса `no-svg` просто не существует в DOM, если браузер поддерживает SVG, и наоборот.

<pre>// CSS

.tomato {
    background-image: url('img/tomato.svg');
}
.no-svg .tomato {
    background-image: url('img/tomato.png');
}
</pre>

### SVG в качестве фонового изображения, fallback с помощью CSS

Этот способ будет даже немного покруче, так как он не зависит от какой-либо библиотеки. Даже если библиотека Modernizr подключена у вас в проекте, в этом случае она уже не играет никакой роли. Но если вы подключили библиотеку Modernizr в проект только для того, чтобы реализовать откат (fallback) для фоновых изображений SVG, то вам лучше воспользоваться рассматриваемым методом.

Данный метод основан на маленькой хитрости, заключающейся в том, что поддержка множественных фоновых изображений (multiple background) в браузерах почти точно такая же, что и поддержка SVG. Другими словами, если браузер не поддерживает множественные фоны (multiple background), то он не будет поддерживать и SVG. В результате по коду произойдет откат (fallback) до первой строки, в которой прописано отображение PNG-версии файла.

<pre>// CSS

.tomato {
    background: url('img/tomato.png');
    background-image: url('img/tomato.svg'), none;
}
</pre>

### SVG в качестве встраиваемого изображения (тег img), onerror fallback

Для этого метода необходимо редактирование HTML-кода. Основан метод на использовании Javascript-функции `onerror`, которая встраивается внутрь HTML-тега `<img>`. Благодаря этой функции осуществляется откат (fallback), если браузер не смог загрузить изображение по пути, указанному в атрибуте `src`.

Однако, с етим методом нужно быть осторожным. Если отката (fallback) не произойдет, то некоторые браузеры могут &#8220;зависнуть&#8221; в бесконечном цикле. Это явно не хорошо.

<pre>// HTML

<img src="tomato.svg" onerror="this.src='tomato.png'" />
</pre>

Данный метод также может быть несколько трудоемким, если необходимо подключить к странице много SVG-изображений и при этом нет прямого доступа к исходному коду файла.

Однако, если у вас стоит именно такая задача, то вам можно воспользоваться четвертым способом, рассмотренным ниже.

Зависания браузера в бесконечном цикле можно избежать благодаря небольшой поправке, которую подсказал Roy Reed:

<pre>// HTML

<img src="tomato.svg" onerror="this.src='tomato.png'; this.onerror=null;" />
</pre>

### SVG в качестве встраиваемого изображения (тег img), , fallback с помощью Modernizr

Этому методу также нужна поддержка библиотеки Modernizr для определения возможностей. Как обычно, с помощью этой библиотеки определяем возможности конкретного пользовательского браузера.

Если браузер поддерживает SVG, то строку с тегом `img` отставляем &#8220;как есть&#8221;:

<pre>// HTML

<img src="tomato.svg" />
</pre>

Если же браузер пользователя не поддерживает SVG, то запускается мальнький скрипт, который отыскивает в DOM все img-элементы с атрибутом `src="*.svg"` и производит у файлов-изображений замену расширения с `svg` на `png`.

Чтобы метод сработал, необходимо иметь две версии (SVG и PNG) одного файла; имена файлов должны быть идентичными.

Ниже показан HTML и Javascript. Чтобы пример сработал, убедитесь, что подключили библиотеку Modernizr:

<pre>// HTML

<img src="tomato.svg" />
</pre>

<pre>// Javascript

if (!Modernizr.svg) {
    var imgs = document.getElementsByTagName('img');
    var svgExtension = /.*\.svg$/
    var l = imgs.length;
    for(var i = 0; i &lt; l; i++) {
        if(imgs[i].src.match(svgExtension)) {
            imgs[i].src = imgs[i].src.slice(0, -3) + 'png';
            console.log(imgs[i].src);
        }
    }
}
</pre>

### Заключение

Я считаю нужным сказать еще раз, что если на данный момент в своих проектах вы **не используете SVG**, то вам **следует перейти на его использование**.

Поддержка SVG на сегодня достаточно хорошая, а в скором времени этот формат будет использоваться повсеместно. Применение SVG в проекте имеет множество преимуществ.

Для новичков - вам мне стоит беспокоиться об версии PNG-изображений специально для Retina-дисплеев. SVG-изображения не зависят от разрешения экрана, поэтому с поддержкой адаптивных дизайнов у таких изображений проблем нет.

SVG-изображения могут быть встроены прямо в HTML-документ в качестве одного их его элементов; при этом отпадает необходимость в сохранении SVG-изображения в качестве отдельного файла.

Если открыть любой SVG-файл в редакторе кода, то можно увидеть SVG-код, на котором написан данный файл.

Возможности SVG очень велики, поэтому смело запрыгивайте на платформу SVG-поезда и не бойтесь его использовать на практике! SVG дружелюбен и приятен в обращении.

Оцените статью:  
<span id="post-ratings-2001" class="post-ratings" data-nonce="7dd163d556"><img id="rating_2001_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2001, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2001_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2001, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2001_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2001, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2001_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2001, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2001_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2001, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2001_text"></span></span><span id="post-ratings-2001-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://callmenick.com/2014/04/02/svg-fallback-with-png/ "SVG Fallback with PNG Images"
 [2]: http://localhost:7788/third/?p=1087 "Что такое библиотека Modernizr"