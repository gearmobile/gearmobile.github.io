---
title: Создаем вертикальное меню на CSS
author: gearmobile
layout: post
permalink: /css-vertical-dropdown-menu/
ratings_users:
  - 3
ratings_score:
  - 6
ratings_average:
  - 2
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - css
---
Продолжаем изучение CSS и сегодня приступим к построению вертикального меню. Такие меню очень популярны и без них не обходится каждый второй сайт. Статей по созданию подобной навигации написано немало, но меня данный факт волнует мало. Моя задача &#8211; разобраться в принципе построения подобного меню и возможность сделать его самому, на коленках за пару минут. В действительности все просто, даже очень просто.

Созданное в этой статье вертикальное меню будет далеко по своим внешним эстетическим данным от совершенства. Но это и неважно &#8211; важен сам принцип, механизм построения и функционирования подобной навигации. А всякие фантики-бантики можно навесить всегда, было бы желание. Механизм действия и построения такого меню основан на одном единственном CSS-свойстве &#8211; `display`, а точнее на его значениях &#8211; `display: block` и `display: none`.

В этой статье будет создаваться простое вертикальное меню, в котором подменю размещается сбоку от основного меню. Существует более сложный вариант вертикального меню, в котором подменю размещается внутри основного. Такая навигация называется `меню-аккордеон` и принцип его создания будет рассмотрен позже.

C чего же мы начнем? С построения обычного маркированного списка, пунктами которого будут ссылки. Списку зададим класс с именем `menu`, так как он нам понадобиться в дальнейшем:

<pre><ul class="menu">
  <li>
    <a href="#">Punkt 1</a>
  </li>
      
  
  <li>
    <a href="#">Punkt 2</a>
  </li>
      
  
  <li>
    <a href="#">Punkt 3</a>
  </li>
      
  
  <li>
    <a href="#">Punkt 4</a>
  </li>
      
  
  <li>
    <a href="#">Punkt 5</a>
  </li>
    
</ul>
</pre>

Созданное только что меню будет внешним, а внутри него (точнее внутри его пунктов) мы поместим еще одно меню. Получиться одно меню, вложенное в другое (помните уроки HTML?). То есть, у нас есть пять пунктов внешнего меню &#8211; вот мы и вложим в каждый из них еще одно меню, перед ссылкой. Ссылка будет исполнять роль переключателя, который будет переводить значение свойства `display` из none в `block` и наоборот. В итоге получиться пять подменю, для каждого из которых мы пропишем один класс &#8211; `sub-menu`. Этот класс нам также потребуется в дальнейшем:

<pre><ul class="menu">
  <li>
    <a href="#">Punkt 1</a>
          <ul class="sub-menu">
      <li>
        <a href="#">Punkt 1-1</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 1-2</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 1-3</a>
      </li>
            
    </ul>
        
  </li>
      
  
  <li>
    <a href="#">Punkt 2</a>
          <ul class="sub-menu">
      <li>
        <a href="#">Punkt 2-1</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 2-2</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 2-3</a>
      </li>
            
    </ul>
        
  </li>
      
  
  <li>
    <a href="#">Punkt 3</a>
          <ul class="sub-menu">
      <li>
        <a href="#">Punkt 3-1</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 3-2</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 3-3</a>
      </li>
            
    </ul>
        
  </li>
      
  
  <li>
    <a href="#">Punkt 4</a>
          <ul class="sub-menu">
      <li>
        <a href="#">Punkt 4-1</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 4-2</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 4-3</a>
      </li>
            
    </ul>
        
  </li>
      
  
  <li>
    <a href="#">Punkt 5</a>
          <ul class="sub-menu">
      <li>
        <a href="#">Punkt 5-1</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 5-2</a>
      </li>
              
      
      <li>
        <a href="#">Punkt 5-3</a>
      </li>
            
    </ul>
        
  </li>
    
</ul>
</pre>

Все &#8211; каркас будущего вертикального меню готов и больше мы его трогать не будем. Остальные действия будем выполнять только с помощью CSS. Для начала создадим базовые стили, чтобы придать нашему меню хоть какой-то вид:

<pre>*{
    margin: 0;
    padding: 0;
  }
  a{
    text-decoration: none;
  }
  ul{
    list-style-type: none;
  }
  .menu{
    margin: 30px 0 0 30px;
    width: 100px;
  }
</pre>

Здесь мы обнуляем `margin` и `padding` для всех элементов, в том числе и `ul`; убираем маркер у пунктов меню; убираем подчеркивание у ссылок. Для внешнего списка с классом menu задаем отступ сверху и слева, чтобы не прилипал к границам окна браузера и устанавливаем фиксированную ширину в 100px.

Дальше форматируем пункты меню:

<pre>.menu li{
    position: relative;
    line-height: 20px;
    background-color: #ccc;
    margin-bottom: 1px;
  }
</pre>

Ставим высоту каждого элемента li равной 20px и выравниваем текст внутри него по центру вертикали; задаем фоновый цвет для них же, чтобы можно было различать каждый из пунктов на фоне окна браузера; делаем нижний `margin` в 1px, чтобы элементы li не сливались между собой и были похожи на пункты меню. Последний шаг &#8211; устанавливаем для li относительное позиционирование, так как в дальнейшем будем размещать подменю относительно этого элемента.

Далее чисто косметические правила для ссылок, находящихся внутри внешнего меню &#8211; размер шрифта (кегль) и цвет текста:

<pre>.menu li a{
    font-size: 16px;
    color: #000;
  }
</pre>

Теперь приступаем к самому интересному &#8211; стилизации подменю. Для начала зададим его ширину (пусть будет чуть меньше ширины внешнего списка):

<pre>.sub-menu{
    width: 90px;
  }
</pre>

Затем установим для подменю абсолютное позиционирование для того, чтобы сместить его вправо на значение, равное ширине внешнего списка, и &#8220;прилепить&#8221; кверху каждого из элементов li. И самое главное &#8211; скроем его отображение в браузере через правило `display: none`. В результате код будет выглядеть следующим образом:

<pre>.sub-menu{
    width: 90px;
    position: absolute;
    left: 100px;
    top: 0;
    display: none;
  }
</pre>

Немного стилизуем пункты меню и ссылки в подменю. Для каждого пункта подменю устанавливаем цвет фона, чтобы отличать подменю от основного меню. И цвет ссылок по той же причине:

<pre>.sub-menu li{
    background-color: #aaa;
  }
    .sub-menu li a{
      color: #fff;
    }
</pre>

Заключительный код, который заставляет наше меню работать именно так, как задумано. То есть, этим мы говорим браузеру присвоить свойству `display` значение `block` при наведении мыши на ссылку во внешнем списке:

<pre>.menu li:hover .sub-menu{
    display: block;
  }
</pre>

В результате подменю отобразиться (браузер сгенерирует его). Изначально в коде было прописано для него display: none. То есть, для браузера такого подменю не существовало и в DOM-модели документа элемент ul с классом `sub-menu` отсутствовал. Так как этому подменю задано абсолютное позиционирование со смещением вправо на 100px и вверх на 0px, то оно поместиться точно справа вверху от своего родителя &#8211; пункта меню внешнего списка.

В принципе, на этом уже все сказано. Основной принцип вертикального меню показан и создан. Остальное &#8211; уже дело техники, если нужно придать ему нужный вид. На закуску пример нашего меню в обычном состоянии:<figure id="attachment_110" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-vertical-menu-600x316.jpg" alt="Вертикальное меню на CSS" width="600" height="316" class="size-medium wp-image-110" />][1]<figcaption class="wp-caption-text">Вертикальное меню на CSS</figcaption></figure> 

И меню, когда наведена мышка на один из пунктов меню и справа появляется подменю, соответствующее этому пункту:<figure id="attachment_111" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/css-vertical-menu-expand-600x316.jpg" alt="Вертикальное меню на CSS с подменю" width="600" height="316" class="size-medium wp-image-111" />][2]<figcaption class="wp-caption-text">Вертикальное меню на CSS с подменю</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-109" class="post-ratings" data-nonce="c186724080"><img id="rating_109_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(109, 1, '1 Star');" onmouseout="ratings_off(2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_109_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(109, 2, '2 Stars');" onmouseout="ratings_off(2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_109_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(109, 3, '3 Stars');" onmouseout="ratings_off(2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_109_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(109, 4, '4 Stars');" onmouseout="ratings_off(2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_109_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(109, 5, '5 Stars');" onmouseout="ratings_off(2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>2,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_109_text"></span></span><span id="post-ratings-109-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/css-vertical-menu.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/css-vertical-menu-expand.jpg