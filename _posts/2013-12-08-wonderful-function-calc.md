---
title: Замечательная функция calc()
author: gearmobile
layout: post
permalink: /wonderful-function-calc/
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
  - calc()
---
*Как всегда случайно набрел в просторах Интернет на интересный блог (http://webdesignernotebook.com/) одной девушки-дизайнера с не менее интересным именем Inayaili de León Persson. Более того, эта девушка португальского происхождения родом из Панамы, но родилась она в СССР! С 2008 года живет в Лондоне и работает ведущим веб-дизайнеров в Canonical (привет, Ubuntu!). Как все закручено! ))*

*Но это было лирическое вступление. Переходим к главному. Мне на глаза уже давно попадались описания функции calc() &#8211; на CSSTricks (еще не успел прочитать) и на htmlbook (успел прочитать). Последний источник как-то не впечатлил, из-за сухости изложения материала, наверное.*

*А вот на сайте девушки с таким необычным именем функция calc() описана кратко, но интересно, с примерами. И хоть написана статья была в далеком 2011 году, мне интересно было ее прочитать для себя (и фактически перевести). Оригинал статьи находиться в укороченной через Google ссылке &#8211; http://goo.gl/8KYN8y.*

## Что такое функция calc()

Функция calc() может быть использована для вычисления различных линейных размеров на странице. Например, с ее помощью можно рассчитывать значение границ, margins, paddings, кегля и многое другое. Вычисление ширины объектов может быть чрезвычайно сложной задачей, особенно если макет сайта резиновый; функция calc() уникальная, потому что она позволяет выполнять расчеты внутри самих таблиц стилей CSS.

Функция calc() умеет работать с простейшими математическими операторами:

  * сложением (+)
  * вычитанием (-)
  * умножением (*)
  * делением (/)

Давайте рассмотрим простейший пример работы функции calc():

<pre>div{
    width: calc(100% - 20px);
  }
</pre>

Очень просто, не правда ли? В одной функции может использоваться не один, а несколько математических операторов:

<pre>div{
    width: calc(100% - 20px + 2px*2);
  }
</pre>

В текущей спецификации говориться, что операции умножения и деления имеют приоритет над операциями сложения и вычитания. Это означает, что в примере выше сначала будет вычислено выражение `2px*2`, и только затем два оставшихся &#8211; сложение и вычитание. Также обратите внимание, что деление на 0 приведет (и должно привести) к ошибке.

Спецификация по функции calc() еще не завершена, но ее основы уже готовы.

### Простой пример использования

Для того, чтобы показать возможности функции calc(), была создана базовая разметка страницы с помощью этой функции.

Разметка состоит из основного контейнера `div id="main"` (расположенного слева), колонки справа `div id="accessory"` и подвала, помещенного внизу `div id="footer"`.

Ниже приведен код этой разметки:

<pre><div class="wrapper">
  <div id="main">
    <h1>
      Far far away…
    </h1>
          
    
    <p>
      Far far away, behind the word mountains…
    </p>
        
  </div>
  
      
  
  <div id="accessory">
    <ul>
      <li>
        <a href="#">Far far away…</a>
      </li>
              
      
      <li>
        <a href="#">Separated they live…</a>
      </li>
              
      
      <li>
        <a href="#">A small river named…</a>
      </li>
            
    </ul>
        
  </div>
  
      
  
  <div id="footer">
    Visit the article…
        
  </div>
  
    
</div>
</pre>

После применения не требующего объяснений (надо надеяться) простого сброса CSS-стилей (полный код CSS-сброса смотрите в исходном коде примера &#8211; http://webdesignernotebook.com/examples/calc-function.html), установки базового шрифта и внешнего вида ссылок, стилизуем элемент `body`:

<pre>body {
    background: #e8eadd;
    color: #3c323a;
    padding: 20px;
  }
</pre>

После этого я говорю, что основной контейнер `div.wrapper` должен занимать всю ширину своего контейнера (100%) за вычетом 40 пикселей и располагаться горизонтально, по центру:

<pre>.wrapper{
    width: 1024px; /* Откат для браузеров, которые не поддерживают функцию calc() */
    width: -moz-calc(100% - 40px);
    width: calc(100% - 40px);
    margin: auto;
  }
</pre>

В коде выше была добавлена строка отката для браузеров, которые не поддерживают работу с функцией calc(), а также браузерный префикс `-moz-` для браузера Firefox 4.

Затем устанавливается ширина, границы, плавание влево и margins для основного блока с контентом `div#main`:

<pre>#main{
    border: 8px solid #b8c172;
    float: left;
    margin: 0 20px 20px 0;
    padding: 20px;
    width: 704px; /* Откат для браузеров, которые не поддерживают функцию calc() */
    width: -moz-calc(75% - 20px*2 - 8px*2);
    width: calc(75% - 20px*2 - 8px*2);
  }
</pre>

Давайте разберемся с функцией calc() в этом примере кода. Здесь я хочу, чтобы ширина контейнера div#main равнялась 75% (75% от ширины контейнера-родителя, не забывайте об этом!). Но из этой ширины мне необходимо вычесть padding слева и справа от контейнера &#8211; `20px*2`, а также ширину границы с обоих сторон &#8211; `8px*2`.

Переходим к боковой панели `div#accessory` и говорим ей, что она должна занимать оставшуюся ширину контейнера-родителя в 25%. Но при этом также должны учитываться ширина границы этого блока, margin-right (20px) и padding. Блок будет &#8220;плавать&#8221; вправо:

<pre>#accessory{
    border: 8px solid #b8c172;
    float: right;
    padding: 10px;
    width: 208px; /* Откат для браузеров, которые не поддерживают функцию calc() */
    width: -moz-calc(25% - 10px*2 - 8px*2 -20px);
    width: calc(25% - 10px*2 - 8px*2 -20px);
  }
</pre>

Если более подробно разобрать выражение `calc(25% - 10px*2 - 8px*2 -20px)`, то увидим, что из первоначальной ширины 25% вычитается padding справа и слева `10px*2`, ширина правой и левой сторон границы этого блока `8px*2`, а также правый margin для блока-контейнера `div#main`.

Блок-подвал `footer` просто имеет ширину, равную всей ширине блока-родителя. Я думаю, что описывать стили для этого блока излишне.

Если уменьшать размер окна браузера, то при достижении им определенной величины ширина боковой панели `div#accessory` становиться слишком маленькой, что нарушает дизайн страницы. Поэтому в код ниже был добавлен простой media query, с помощью которого у блоков `div#main` и `div#accessory` убирается плавание влево-вправо и пересчитывается ширина обоих блоков так, чтобы они занимали 100% ширины блока-родителя за минусом ширины границ и соответствующих padding:

<pre>@media screen and (max-width: 768px){
    #main, #accessory{
      float: none;
    }
    #main{
      margin-right: 0;
      width: -moz-calc(100% - 20px*2 - 8px*2);
      width: calc(100% - 20px*2 - 8px*2);
    }
    #accessory{
      width: -moz-calc(100% - 20px*2 - 8px*2);
      width: calc(100% - 20px*2 - 8px*2);
    }
  }
</pre>

Приведенный выше пример разметки страницы является очень упрощенным. Но есть надежда, что он заинтересует вас и подтолкнет к дальнейшим экспериментам с замечательной функцией calc().

## Поддержка браузерами

Функция calc() поддерживается браузером IE9 и Firefox 4 (для которого необходимо указать браузерный префикс `-moz-calc()`). Я понимаю, однако, что применение этой функции в устаревших браузерах к таким вещам, как анимация, может быть большой проблемой. Но в тоже время, анимация не является жизненно важной необходимостью сайта.

Это не означает, что вы не должны пробовать эту функцию на практике. Ведь разработчики браузеров Firefox и IE предприняли усилия для того, чтобы внести поддержку данной функции в свои браузеры. Доля этих браузеров на мировом рынке самая большая, поэтому, я полагаю, что остальные производители браузеров не останутся долго в стороне.

В своих примерах я предпочла использовать откат в виде абсолютной величины (ширина блока) для браузеров, которые не поддерживают данную функцию.

&#8230;

*Дальше переводить не стал, ибо идет сплошная &#8220;вода&#8221; в виде заключения и всяческих пожеланий, не относящаяся к делу.*

Оцените статью:  
<span id="post-ratings-762" class="post-ratings" data-nonce="419a63844e"><img id="rating_762_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(762, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_762_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(762, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_762_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(762, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_762_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(762, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_762_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(762, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_762_text"></span></span><span id="post-ratings-762-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>