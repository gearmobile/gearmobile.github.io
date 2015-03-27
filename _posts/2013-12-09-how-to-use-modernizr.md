---
title: Как использовать Modernizr
author: gearmobile
layout: post
permalink: /how-to-use-modernizr/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 10
ratings_score:
  - 44
ratings_average:
  - 4.4
categories:
  - 'Javascript &amp; jQuery'
tags:
  - modernizr
---
Инструмент, который призван сделать жизнь прогрессивных веб-дизайнеров немного легче, это Modernizr. Короткий мануал, задача которого показать, каким образом можно применять этот полезный скрипт с максимальным эффектом для своих рабочих проектов.

### Обзор

Несмотря на то, что возможности CSS3 используются веб-дизайнерами все больше и больше, поддержка этих возможностей браузерами значительно отстает.

В последнее время я использую Modernizr практически постоянно для того, чтобы выделить те браузеры, которые не поддерживают специфические свойства стандарта CSS3.

### Как работает Modernizr

Для того, чтобы установить Modernizr, сначала скачайте его с этой страницы &#8211; http://www.modernizr.com/. Затем внутри тега `head` html-страницы подключите распакованный из архива файл `modernizr-1.0.min.js`:

<pre></pre>

Вторым шагом будет подключение класса `no-js` для корневого элемента html:

<pre>
</pre>


<p>
  <strong>Для чего необходимо подключать класс <code>no-js</code> к элементу html?</strong><br />
  Потому что элемент html с классом <code>no-js</code> будет <strong>состоянием страницы по-умолчанию</strong>. Если JavaScript (<code>js</code>) на странице отключен, то скрипт Modernizr также не будет работать (совместно со всеми остальными функциями страницы, завязанными на этом языке), поэтому было бы хорошо, если у нас будет возможность отката (fallback) для этого случая.
</p>


<blockquote>
  <p>
    Прим. переводчика: попробую от себя объяснить в двух словах, но иначе (если вдруг непонятно) что хотела сказать прекрасная девушка, автор статьи. Если на сайте отключена поддержка JavaScript, то класс <code>no-js</code> для элемента html &#8211; это та &#8220;зацепка&#8221;, на которую можно повесить все CSS-fallback&#8217;и для этого случая.
  </p>
  
</blockquote>


<p>
  Если же поддержка JavaScript в браузере включена, то <strong>произойдет динамическая подмена класса <code>no-js</code> для элемента html на целую группу других классов</strong>. В результате исходный код страницы может выглядеть примерно так:
</p>


<pre>
  
</pre>


<p>
  Впечатляет, не правда ли? Но что означают все эти классы? Давайте разберемся.
</p>


<p>
  В данном случае, страница была открыта в браузере Firefox 3.5. Этот браузер (к сожалению) не поддерживает множественные фоны на CSS, CSS-градиенты и CSS-трансформации. Скрипт Modernizr умеет автоматически определять возможности браузера, в котором открыта текущая веб-страница. Для каждого из CSS-свойств в скрипте Modernizr имеются свои собственные классы для их обозначения. Например, множественные фоны на CSS &#8220;обозначены&#8221; как <code>multipebgs</code>, CSS-градиенты как <code>cssgradients</code>, CSS-трансформации как <code>csstransforms</code> и так далее.
</p>


<p>
  Когда Modernizr определит, какие CSS-свойства данный браузер поддерживает, а какие нет, он создаст своеобразный отчет &#8211; список классов, по которому можно точно узнать, что браузер &#8220;умеет&#8221;, а что &#8211; нет. Если браузер поддерживает CSS-свойство трансформации, то на элемент html скрипт Modernizr &#8220;подцепит&#8221; класс <code>csstransforms</code>. А если браузер не поддерживает это свойство, то Modernizr добавит для имени класса <code>csstransforms</code> префикс <code>no-</code> и также &#8220;повесит&#8221; этот класс на элемент html, но в виде <code>no-csstransforms</code>. И так далее&#8230;
</p>


<p>
  Пример такого списка-отчета и был показан выше.
</p>


<h3>
  Что мне даст эта (ценная) информация?
</h3>


<p>
  Логичный вопрос &#8211; &#8220;а что мы можем делать с этой информацией?&#8221;. Хорошо, давайте рассмотрим простой пример.
</p>


<h4>
  Множественные фоны на CSS
</h4>


<p>
  Фон вашего сайта тщательным образом отстроен и вы используете множественные фоны для того, чтобы сделать его более простым и быстрым с помощью CSS-кода.
</p>


<p>
  Ваш CSS выглядит следующим образом:
</p>


<pre>
  #nice {
    background: url(background-one.png) top left repeat-x,
    url(background-two.png) bottom left repeat-x;
  }
</pre>


<p>
  И браузер генерирует этот прекрасный (ведь не даром же идентификатор имеет имя nice )) ) фон так:
</p>
<figure id="attachment_778" style="width: 241px;" class="wp-caption aligncenter">

<a href="http://localhost:7788/third/wp-content/uploads/2013/12/modernizr-safari.jpg"><img src="http://localhost:7788/third/wp-content/uploads/2013/12/modernizr-safari.jpg" alt="Множественные фоны" width="241" height="342" class="size-full wp-image-778" /></a><figcaption class="wp-caption-text">Множественные фоны</figcaption></figure>


<p>
  При использовании библиотеки Modernizr ваш код CSS должен быть преобразован в такой вид:
</p>


<pre>
  #nice {
    background: url(background-one.png) top left repeat-x;
  }
  .multiplebgs #nice {
    background: url(background-one.png) top left repeat-x,
    url(background-two.png) bottom left repeat-x;
  }
</pre>


<p>
  И вот что увидят посетители сайта в зависимости от того, каким браузером (<em>понимает он множественный фон или нет</em>) они пользуются:
</p>
<figure id="attachment_778" style="width: 241px;" class="wp-caption aligncenter">

<a href="http://localhost:7788/third/wp-content/uploads/2013/12/modernizr-safari.jpg"><img src="http://localhost:7788/third/wp-content/uploads/2013/12/modernizr-safari.jpg" alt="Множественный фон с Modernizr в Safari" width="241" height="342" class="size-full wp-image-778" /></a><figcaption class="wp-caption-text">Множественный фон с Modernizr в Safari</figcaption></figure>
<figure id="attachment_780" style="width: 241px;" class="wp-caption aligncenter"><a href="http://localhost:7788/third/wp-content/uploads/2013/12/modernizr-opera.jpg"><img src="http://localhost:7788/third/wp-content/uploads/2013/12/modernizr-opera.jpg" alt="Множественный фон с Modernizr в Opera" width="241" height="342" class="size-full wp-image-780" /></a><figcaption class="wp-caption-text">Множественный фон с Modernizr в Opera</figcaption></figure>


<p>
  Это очень простой пример использования скрипта Modernizr, но он должен послужит образцом того, что можно сделать с помощью данной библиотеки.
</p>


<h4>
  HTML5
</h4>


<p>
  Библиотека Modernizr также позволяет использовать новые элементы, доступные в HTML5 &#8211; header, footer, section, hgroup, video и так далее и стилизовать их.
</p>


<p>
  Однако, это не означает,  что все эти элементы можно использовать также в браузере IE. Но вы можете стилизовать эти элементы и тогда IE &#8220;поймет&#8221; их и не сможет игнорировать.
</p>


<blockquote>
  <p>
    Прим. переводчика: загадочная фраза, которая лично мне ни о чем не говорит. Требует дальнейшего изучения &#8230; ))
  </p>
  
</blockquote>


<h4>
  JavaScript
</h4>


<p>
  Вы также можете анализировать в вашем собственном JavaScript возможности, которые поддерживает Modernizr, используя пример следующего синтаксиса:
</p>


<pre>
  if (Modernizr.geolocation) {
  }
</pre>


<h4>
  Заключение
</h4>


<p>
  Надеюсь, мне удалось объяснить, для чего нужен Modernizr и насколько он полезен в повседневной работе. Так как мы не можем полностью полагаться на тот факт, что браузеры поддерживают все свойства, которые мы хотим использовать, то библиотека Modernizr является лучшим средством для того, чтобы объединить два мира &#8211; один, где все возможно, и другой, где все возможно лишь частично.
</p>


<p>
  Оригинал статьи &#8211; &#8220;How to use Modernizr&#8221; (http://webdesignernotebook.com/css/how-to-use-modernizr/)
</p>


<p>
  Оцените статью:<br />
  <span id="post-ratings-777" class="post-ratings" data-nonce="60cd3820b0"><img id="rating_777_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(777, 1, '1 Star');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_777_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(777, 2, '2 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_777_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(777, 3, '3 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_777_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(777, 4, '4 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_777_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(777, 5, '5 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>10</strong> votes, average: <strong>4,40</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_777_text"></span></span><span id="post-ratings-777-loading" class="post-ratings-loading">
  			<img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>
</p>