---
title: Создать зачеркнутый заголовок на CSS
author: gearmobile
layout: post
permalink: /css-side-lined-headline/
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
  - css
---
Создать заголовок с эффектом зачеркивания. Создается с помощью псевдо-элементов `:before` и `:after`. Оба псевдо-элемента применяются только к одному элементу &#8211; заголовку определенного уровня и дополнительной разметки не требуется, все семантично. Линии подчеркивания имеют фиксированную ширину с обеих сторон, что упрощает задачу. Положение линий по вертикали &#8211; точно по центру. CSS-код во многом похож на тот, который пишется при создании теней под углами блока &#8220;[Создание приподнятых теней (lifted shadow) с помощью CSS][1]&#8220;.

Создание такого эффекта выполняется простым кодом. Первоначально задаем HTML-разметку с использованием заголовка первого уровня `h1`:

<pre><h1>
  about me
</h1>
</pre>

И прописываем для него CSS-правила, чтобы привести его к тому виду, который нам необходим:

<pre>h1{
      width: 900px;
      margin: 100px auto;
      border: 1px solid #000;
      text-align: center;
      font-size: 40px;
      line-height: 60px;
      text-transform: uppercase;
      position: relative;
    }
</pre>

Выравнивание по центру, размер шрифта (кегль) и высота блока через интерлиньяж `line-height`, делаем все буквы заглавными &#8211; все стандартно. Но не забываем о позиционировании, которое устанавливаем относительным, ибо оно потребуется нам для псевдо-элементов `:before` и `:after`.

Теперь создаем общие правила для обоих псевдо-элементов `:before` и `:after`.

<pre>h1:before, h1:after{
    content: '';
    position: absolute;
    top: 50%;
    margin-top: -2px;
    left: 0;
    height: 4px;
    width: 320px;
    background-color: #000;
  }
</pre>

Единственным примечательным моментом в этом коде является свойство `top: 50%`, которое размещает линию точно по центру вертикали блочного элемента. В нашем случае таким блочным элементом является заголовок первого уровня `h1`. Кроме того, нужно установить еще одно правило &#8211; `margin-top: -2px`. Этим правилом мы поднимаем сгенерированные линии вверх на половину их высоты. Почему это нужно делать, можно догадаться и так. Но если догадка не приходит, то можно почитать статью &#8220;[CSS &#8211; разместить объект точно по центру блока][2]&#8220;.

Так как правила мы прописали для обоих элементов, то следуют переписать некоторые из них для элемента `:after`. Точнее &#8211; нам нужно только правило `right`, чтобы &#8220;сдвинуть&#8221; его вправо:

<pre>h1:after{
    right: 0;
    left: auto;
  }
</pre>

Результат работы кода показан на рисунке ниже. Граница для заголовка задана мною для наглядности:<figure id="attachment_120" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/header-stroke-600x228.jpg" alt="Зачеркнутый заголовок на CSS" width="600" height="228" class="size-medium wp-image-120" />][3]<figcaption class="wp-caption-text">Зачеркнутый заголовок на CSS</figcaption></figure> 

Полностью весь код для создания такого эффекта приведен ниже:

<pre>h1{
    width: 900px;
    margin: 100px auto;
    border: 1px solid #000;
    text-align: center;
    font-size: 40px;
    line-height: 60px;
    text-transform: uppercase;
    position: relative;
  }
  h1:before, h1:after{
    content: '';
    position: absolute;
    top: 50%;
    margin-top: -2px;
    left: 0;
    height: 4px;
    width: 320px;
    background-color: #000;
  }
  h1:after{
    right: 0;
    left: auto;
  }
</pre>

#### UPD 19\01\2014

Для быстроты, удобства и краткости можно воспользоваться готовым миксином из библиотеки Scut &#8211; [Side-Lined][4].

Оцените статью:  
<span id="post-ratings-118" class="post-ratings" data-nonce="00e4fd1d6a"><img id="rating_118_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(118, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_118_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(118, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_118_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(118, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_118_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(118, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_118_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(118, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_118_text"></span></span><span id="post-ratings-118-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=105 "Создание приподнятых теней (lifted shadow) с помощью CSS"
 [2]: http://localhost:7788/third/?p=122 "CSS - разместить объект точно по центру блока"
 [3]: http://localhost:7788/third/wp-content/uploads/2013/10/header-stroke.jpg
 [4]: http://davidtheclark.github.io/scut/side-lined.html