---
title: 'Псевдокласс :target  &#8211; стили для элемента-якоря в HTML-документе'
author: gearmobile
layout: post
permalink: /pseudo-class-target/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Статьи по CSS
tags:
  - target
---
Настала очередь изучить, что такое псевдо-класс `:target`. Вопрос достаточно интересный как с точки зрения теории, так еще больше &#8211; с точки зрения практики.

Начнем издалека и вспомним (*если кто читал*) одну из глав книги Энди Бадда &#8220;**Мастерская CSS**&#8220;. Глава называется &#8220;**Изменение стиля элемента при наведении указателя на отдаленный элемент**&#8221; и речь в ней идет о том, как сделать так, чтобы **управлять одним элементом с помощью другого**.

Техника, описанная в данной главе, представляла из себя следующее. В ссылку вкладывались несколько элементов, которые **позиционировались абсолютно** на странице и **размещались в любом ее месте**.

Визуально создается впечатление, что они никак не связаны между собой. Но на самом деле они находятся **внутри одного элемента** &#8211; ссылки (*ниже приведен кусок кода из этой главы в качестве примера*):

<pre>// HTML

<a title="Richard Rutter" href="http://www.clagnut.com/">
  <span class="link">» Richard Rutter</span>
</a>
</pre>

Способ достаточно хорош, за исключением того, что применяется **дополнительная разметка** и **нарушается семантика** HTML-документа. На момент написания этой книги это был единственный способ управления &#8220;отдаленными&#8221; элементами на странице.

Но на сегодняшний день существует еще один способ, более аккуратный и универсальный &#8211; **с помощью псевдо-класса** `:target`. Другое дело, что поддержка в браузерах этого CSS-свойства не полностью реализована и здесь можно смело показать пальцем в сторону браузера IE, в нем оно поддерживается, **начиная с 9-ой версии** &#8211; <a title="Can I Use - Target" href="http://caniuse.com/#search=target" target="_blank">Can I Use &#8211; Target</a>.<figure id="attachment_2078" style="width: 256px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/target.png" alt="target" width="256" height="256" class="size-full wp-image-2078" />][1]<figcaption class="wp-caption-text">Псевдо-класс target</figcaption></figure> 

С помощью этого псевдо-класса можно управлять абсолютно **любым элементом в документе**. При этом он не обязан располагаться в каком-то определенном месте, наоборот &#8211; он может находиться в нормальном потоке и не нарушать семантику.

Приведу в качестве примера кусок кода, демонстрирующий такой подход:

<pre>// HTML



<p>
  Lorem ipsum dolor sit amet, sed do eiusmod tempor
</p>


<p>
  Lorem ipsum dolor <a href="#example">Example</a> et dolore magna aliqua.
</p>


<p id="example">
  Lorem ipsum dolor sit amet, ut enim ad minim veniam
</p>


<p>
  Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut
</p>


<p>
  Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut
</p>
</pre>

Видим ссылку, помещенную в середине документа, обрамленную элементами `p`. У ссылки атрибут `href` имеет значение `#example`, который очень похож на ссылку на якорь. На самом деле это и есть ссылка на якорь, который назначен для одного из параграфов с идентификатором `id="example"`.

Вид ссылки может быть не обязательно таким, но и более длинным &#8211; `http://localhost:7788/third/#example`. Все, что располагается в ней после знака диез (#), называется *хэштег*.

Псевдо-класс `:target` как раз и служит для стилизации элемента с якорем, на который указывает такая ссылка. Давайте приступим к стилизации, чтобы воочию увидеть, как работает этот псевдо-элемент.

Для одного из параграфов мы уже назначили идентификатор, который является якорем. Пропишем для него немного правил:

<pre>// CSS

#example{
  font: 12px Georgia, serif;
  color: #778899;
  -webkit-transition: all .3s ease-in-out;
     -moz-transition: all .3s ease-in-out;
      -ms-transition: all .3s ease-in-out;
       -o-transition: all .3s ease-in-out;
          transition: all .3s ease-in-out;
}
</pre>

Мы изменили семейство **шрифтов**, **кегль** и **цвет**. Эти правила устанавливаются &#8220;как обычно&#8221;, то есть &#8211; как прописали, так они и отображаются в браузере. Теперь создадим немного стилей, которые первоначально себя никак не проявляют, а только по происшествии какого-то события.

В нашем случае это будет клик на ссылке. Для таких правил синтаксис следующий:

<pre>// CSS

#example:target{
  color: #bbddff;
  font-weight: bold;
  outline: 1px solid #ff0000;
  padding: 20px;
  text-shadow: 1px 1px 1px #667788;
}
</pre>

Откроем созданную нами страницу в браузере &#8211; и почти ничего не увидим. Точнее &#8211; только те правила, которые явно прописаны в первом куске кода. Но если кликнуть мышью на ссылке с текстом `Example`, то увидим достаточно занимательную трансформацию параграфа. Это псевдо-класс `:target` в действии!

Он применил прописанные для него правила только при совершении некоего события. И применены они были к обособленному участку HTML-кода (помеченному идентификатором `#example`), который почти никак не связан со ссылкой.

Можно немного усложнить пример и связать несколько параграфов между собой, то есть таким образом:

<pre>// CSS

#example:target + p{
  font-variant: small-caps;
  font-weight: bold;
  color: #0000ff;
  text-indent: 3em;
}
</pre>

Откроем вновь страницу в браузере и посмотрим результат. Все ОК.

Псевдо-класс `:target` может принимать любые CSS-свойства, в том числе скрытие\показ элементов с помощью правила `display`. Последнее довольно часто применяется при верстке различных блоков.

На странице сайта MDN приведен пример создания одного из таких блоков &#8211; [CSS LightBox][2]. Другим ярким примером использования этого элемента являются вкладки на чистом CSS, где необходима смена цвета вкладок и их содержимого при переключении.

Ниже привожу, как всегда, полный текст кода.

<pre>// HTML



<p>
  Lorem ipsum dolor sit amet, sed do eiusmod tempor
</p>


<p>
  Lorem ipsum dolor <a href="#example">Example</a> et dolore magna aliqua.
</p>


<p id="example">
  Lorem ipsum dolor sit amet, ut enim ad minim veniam
</p>


<p>
  Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut
</p>


<p>
  Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut
</p>
</pre>

<pre>// CSS

#example{
  font: 12px Georgia, serif;
  color: #778899;
  -webkit-transition: all .3s ease-in-out;
     -moz-transition: all .3s ease-in-out;
      -ms-transition: all .3s ease-in-out;
       -o-transition: all .3s ease-in-out;
          transition: all .3s ease-in-out;
}

#example:target{
  color: #bbddff;
  font-weight: bold;
  outline: 1px solid #ff0000;
  padding: 20px;
  text-shadow: 1px 1px 1px #667788;
}

#example:target + p{
  font-variant: small-caps;
  font-weight: bold;
  color: #0000ff;
  text-indent: 3em;
}
</pre>

В принципе, это и все, что можно сказать о псевдо-классе `:target`.

Оцените статью:  
<span id="post-ratings-151" class="post-ratings" data-nonce="9bbf63919b"><img id="rating_151_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(151, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_151_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(151, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_151_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(151, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_151_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(151, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_151_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(151, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_151_text"></span></span><span id="post-ratings-151-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/target.png
 [2]: https://developer.mozilla.org/en-US/docs/Web/CSS/:target "MDN LightBox Target"