---
title: Шапка сайта и навигационное меню с помощью CSS
author: gearmobile
layout: post
permalink: /%d1%88%d0%b0%d0%bf%d0%ba%d0%b0-%d1%81%d0%b0%d0%b9%d1%82%d0%b0-%d0%b8-%d0%bd%d0%b0%d0%b2%d0%b8%d0%b3%d0%b0%d1%86%d0%b8%d0%be%d0%bd%d0%bd%d0%be%d0%b5-%d0%bc%d0%b5%d0%bd%d1%8e-%d1%81-%d0%bf%d0%be%d0%bc/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 7
ratings_score:
  - 34
ratings_average:
  - 4.86
categories:
  - Статьи по CSS
tags:
  - css
---
Просматривал видеокурс по блочной верстке сайта от Андрей Морковина. Начал смотреть с чувством, что вот &#8211; сейчас научусь чему-то новому. Но терпения хватило досмотреть до девятой части. Устал наблюдать мучения автора по верстке шаблона, и в частности, то, как создавалась шапка. Автор зачем-то вырезал только часть фона с навигацией, вставлял изображение логотипа в html-каркас и обертывал его ссылкой, пытался угадать местоположение навигации с помощью абсолютного или относительного позиционирования. Я решил сам попробовать сделать шапку сайта так, как мне кажется более правильным.

В основу создания шапки я положил свойство вложенных слоев на div&#8217;ах. Кстати, с этим методом я только недавно познакомился в другом видеоуроке от Дмитрия Семенова. И сделал описание его своими словами в статье &#8220;[Раздвижной фон на CSS][1]&#8220;. Далее, предполагается, что размеры всех фоновых изображений известны (на практике так и происходит, при вырезании их из psd-макета). Для чистоты эксперимента приведу эти размеры: bg-nav.gif &#8211; 300x70px, bg-header.gif &#8211; 800x50px, logo.gif &#8211; 30x30px. В CSS-свойствах сделал для них подстановку с помощью фоновой заливки цветом, для подстраховки.

Итак, что я буду делать. Первый шаг стандартный. Создается обертка с помощью слоя div id=&#8221;wrap&#8221;, которой прописываются свойства центрирования страницы и задания ей ширины:

<pre>#wrap{
  width: 800px;
  height: 100%;
  margin: 0 auto;
  background: #c0c0c0;
  }
</pre>

Затем создается слой div id=&#8221;header&#8221;, в котором будет располагаться шапка будущего сайта. Для нее прописываю совсем короткие свойства, с помощью которых гарантированно растягиваю шапку на всю ширину блока-родителя div id=&#8221;wrap&#8221; и задаю ее высоту:

<pre>#header{
  width: 100%;
  height: 70px;
  }
</pre>

Затем создаю слой div id=&#8221;nav&#8221;, задача которого будет содержать в себе фоновое изображение для навигационного списка шапки. Высоту этого слоя устанавливаю равной высоте шапки, а сам фоновый рисунок позиционирую в правом углу блока. Высота его равна высоте шапки, поэтому достаточно сметить его по-горизонтали вправо, а по-вертикали оставляю как есть. Рисунок короткий и будет занимать не всю ширину шапки, а только некоторую ее правую часть, как раз ровно настолько, чтобы вместить в себя навигационный список. CSS-код для этого слоя представлен ниже:

<pre>#nav{
  background: url(i/bg-nav.gif) #b318cf 100% 0 no-repeat;
  height: 70px;
  }
  </pre>

Теперь создаю еще один слой div id=&#8221;head&#8221;, в котором будет размещено еще одно фоновое изображение. По высоте оно меньше, чем фоновое изображение слоя div id=&#8221;nav&#8221; и будет располагаться поверх этого слоя, перекрывая его. Поэтому фон слоя div id=&#8221;nav&#8221; будет видет только частично, лишь его нижний краешек, для которого и отводится роль фона навигации. Для слоя div id=&#8221;head&#8221; явно задаю его высоту. Код со свойствами приведен ниже:

<pre>#head{
  background: url(i/bg-header.gif) #2b66c8 0 0 no-repeat;
  height: 50px;
  }
</pre>

Ну вот, задача практически и решена. При этом не было использовано ни абсолютного, ни относительного позиционирования. только смещение фона слоя. Осталось создать последний слой, который будет выполнять задачу логотипа сайта. Размещаю его поверх всех остальных слоев и делаю кликабельным на все его пространство. При этом снова воспользуюсь фоновым изображение, которое вложу внутрь этого слоя. Никаких img в html-коде! Позиционировать или смещать его никуда не надо, так как он по-умолчанию расположится в левом верхнем углу блока (как мною задумано для простоты эксперимента). Только явно задам этому слою высоту и ширину, равную высоте и ширине фонового рисунка.

<pre>#logo{
  background: url(i/logo.gif) #36cf18 0 0 no-repeat;
  width: 30px;
  height: 30px;
  }
  </pre>

Чтобы сделать слой кликабельным, помещаю внутрь него ссылку. Так как изначально она является строчным элементом (inline), то ей невозможно задать правила, чтобы &#8220;растянуть&#8221; на всю высоту и ширину слоя-родителя div id=&#8221;logo&#8221;. Поэтому &#8220;превращаю&#8221; ссылку в блочный элемент с помощью свойства display:block. А вот теперь растяну ссылку, задав для нее ширину и высоту в процентах. Конечно, можно указать эти параметры и с помощью пикселей, так как размеры логотипа известны. Но лучше возложить эту задачу на плечи браузера &#8211; пусть сам вычисляет размеры блока-ссылки.

<pre>#logo a{
  display: block;
  width: 100%;
  height: 100%;
  }
  </pre>

Осталось создать навигационное меню шапки, которое должно располагаться поверх слоя div id=&#8221;nav&#8221;. Создаю ненумерованный список, который помещаю внутрь слоя div id=&#8221;nav&#8221;. Так как по коду слой div id=&#8221;head&#8221; расположен выше и имеет фиксированную высоту, то список займет все оставшееся пространство под ним: 70px &#8211; 50px = 20px. Теперь достаточно сместить список вправо с помощью float:right и прописать для него обычные свойства, чтобы расположить горизонтально и стилизовать:

<pre>#nav ul{
  list-style-type: none;
  float: right;
  }
    #nav li{
      display: inline-block;
    }
      #nav a{
        text-decoration: none;
        color: #fff;
        font-weight: bold;
        margin-right: 15px;
        line-height: 20px;
        display: inline-block;
      }
  </pre>

Единственный момент, который вызвал у меня затруднения, это появившиеся еле заметные отступы между внешним блоком ul и внутренним элементом(ами) li. Первоначально для них я прописал свойство display:inline. Но после &#8220;наводки&#8221; Kray Storm с форума forum.htmlbook.ru проблема была решена. Для элементов li и a поменял свойство на display: inline-block и для a дополнительно задал высоту строки line-height: 20px, равную высоте блока ul. Зазоры пропали и пункты меню растянулись на всю высоту блока-родителя.

Все, шапка сайта готова. Если посмотреть на html-код, то видно, что он &#8220;правильный&#8221;. То есть, он не замусорен всякими img. Разметка выполнена простыми свойствами CSS, который будут гарантировано работать почти во всех браузерах. При этом она никуда не &#8220;съедет&#8221;. Ниже приведу полный код html-каркаса и CSS-кода.

HTML-код:<figure id="attachment_371" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/header-karkas-600x256.png" alt="HTML каркас шапки сайта" width="600" height="256" class="size-medium wp-image-371" />][2]<figcaption class="wp-caption-text">HTML каркас шапки сайта</figcaption></figure> 

CSS-код:

<pre>/*  reset  */
  *{
    margin: 0;
    padding: 0;
  }

  /*  main */
  #wrap{
    width: 800px;
    height: 100%;
    margin: 0 auto;
    background: #c0c0c0;
  }
  #header{
    width: 100%;
    height: 70px;
  }
  #nav{
    background: url(i/bg-nav.gif) #b318cf 100% 0 no-repeat;
    height: 70px;
  }
    #nav ul{
      list-style-type: none;
      float: right;
    }
      #nav li{
        display: inline-block;
      }
        #nav a{
          text-decoration: none;
          color: #fff;
          font-weight: bold;
          margin-right: 15px;
          line-height: 20px;
          display: inline-block;
        }
  #head{
    background: url(i/bg-header.gif) #2b66c8 0 0 no-repeat;
    height: 50px;
  }
  #logo{
    background: url(i/logo.gif) #36cf18 0 0 no-repeat;
    width: 30px;
    height: 30px;
  }
    #logo a{
      display: block;
      width: 100%;
      height: 100%;
    }
  </pre>

Здесь я представлю нарисованную мною схему расположения всех блоков в шапке сайта:<figure id="attachment_372" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/shema.png" alt="Блок-схема на div&#039;ах шапки сайта" width="600" height="400" class="size-full wp-image-372" />][3]<figcaption class="wp-caption-text">Блок-схема на div&#8217;ах шапки сайта</figcaption></figure> 

И, наконец, результат всего &#8211; готовая шапка сайта:<figure id="attachment_373" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/result-header-600x314.png" alt="Готовая шапка сайта" width="600" height="314" class="size-medium wp-image-373" />][4]<figcaption class="wp-caption-text">Готовая шапка сайта</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-369" class="post-ratings" data-nonce="199c2676b2"><img id="rating_369_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(369, 1, '1 Star');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_369_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(369, 2, '2 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_369_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(369, 3, '3 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_369_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(369, 4, '4 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_369_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(369, 5, '5 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>7</strong> votes, average: <strong>4,86</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_369_text"></span></span><span id="post-ratings-369-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=187 "Раздвижной фон на CSS"
 [2]: http://localhost:7788/third/wp-content/uploads/2013/09/header-karkas.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/09/shema.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/09/result-header.png