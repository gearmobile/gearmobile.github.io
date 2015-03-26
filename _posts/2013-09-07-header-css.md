---
layout: post
title: "Шапка сайта и навигационное меню с помощью CSS"
author: gearmobile
tags: [css, html]
---

Просматривал видеокурс по блочной верстке сайта от Андрей Морковина. Начал смотреть с чувством, что вот - сейчас научусь чему-то новому. Но терпения хватило досмотреть до девятой части. Устал наблюдать мучения автора по верстке шаблона, и в частности, то, как создавалась шапка. Автор зачем-то вырезал только часть фона с навигацией, вставлял изображение логотипа в html-каркас и обертывал его ссылкой, пытался угадать местоположение навигации с помощью абсолютного или относительного позиционирования. Я решил сам попробовать сделать шапку сайта так, как мне кажется более правильным.

В основу создания шапки я положил свойство вложенных слоев на div'ах. Кстати, с этим методом я только недавно познакомился в другом видеоуроке от Дмитрия Семенова. И сделал описание его своими словами в статье "[Раздвижной фон на CSS][1]". Далее, предполагается, что размеры всех фоновых изображений известны (*на практике так и происходит, при вырезании их из psd-макета*).

Для чистоты эксперимента приведу эти размеры: `bg-nav.gif - 300x70px`, `bg-header.gif - 800x50px`, `logo.gif - 30x30px`. В CSS-свойствах сделал для них подстановку с помощью фоновой заливки цветом, для подстраховки.

Итак, что я буду делать. Первый шаг стандартный. Создается обертка с помощью слоя `div id="wrap"`, которой прописываются свойства центрирования страницы и задания ей ширины:

{% highlight css %}
#wrap{
  width: 800px;
  height: 100%;
  margin: 0 auto;
  background: #c0c0c0;
}
{% endhighlight %}

Затем создается слой `div id="header"`, в котором будет располагаться шапка будущего сайта. Для нее прописываю совсем короткие свойства, с помощью которых гарантированно растягиваю шапку на всю ширину блока-родителя `div id="wrap"` и задаю ее высоту:

{% highlight css %}
#header{
  width: 100%;
  height: 70px;
}
{% endhighlight %}

Затем создаю слой `div id="nav"`, задача которого будет содержать в себе фоновое изображение для навигационного списка шапки. Высоту этого слоя устанавливаю равной высоте шапки, а сам фоновый рисунок позиционирую в правом углу блока. Высота его равна высоте шапки, поэтому достаточно сметить его по-горизонтали вправо, а по-вертикали оставляю как есть.

Рисунок короткий и будет занимать не всю ширину шапки, а только некоторую ее правую часть, как раз ровно настолько, чтобы вместить в себя навигационный список. CSS-код для этого слоя представлен ниже:

{% highlight css %}
#nav{
  background: url(i/bg-nav.gif) #b318cf 100% 0 no-repeat;
  height: 70px;
}
{% endhighlight %}

Теперь создаю еще один слой `div id="head"`, в котором будет размещено еще одно фоновое изображение. По высоте оно меньше, чем фоновое изображение слоя `div id="nav"` и будет располагаться поверх этого слоя, перекрывая его.

Поэтому фон слоя `div id="nav"` будет видет только частично, лишь его нижний краешек, для которого и отводится роль фона навигации. Для слоя `div id="head"` явно задаю его высоту. Код со свойствами приведен ниже:

{% highlight css %}
#head{
  background: url(i/bg-header.gif) #2b66c8 0 0 no-repeat;
  height: 50px;
}
{% endhighlight %}

Ну вот, задача практически и решена. При этом не было использовано ни абсолютного, ни относительного позиционирования. только смещение фона слоя. Осталось создать последний слой, который будет выполнять задачу логотипа сайта. Размещаю его поверх всех остальных слоев и делаю кликабельным на все его пространство.

При этом снова воспользуюсь фоновым изображение, которое вложу внутрь этого слоя. Никаких img в html-коде! Позиционировать или смещать его никуда не надо, так как он по-умолчанию расположится в левом верхнем углу блока (*как мною задумано для простоты эксперимента*). Только явно задам этому слою высоту и ширину, равную высоте и ширине фонового рисунка:

{% highlight css %}
#logo{
  background: url(i/logo.gif) #36cf18 0 0 no-repeat;
  width: 30px;
  height: 30px;
}
{% endhighlight %}

Чтобы сделать слой кликабельным, помещаю внутрь него ссылку. Так как изначально она является строчным элементом (inline), то ей невозможно задать правила, чтобы "растянуть" на всю высоту и ширину слоя-родителя `div id="logo"`.

Поэтому "превращаю" ссылку в блочный элемент с помощью свойства `display:block`. А вот теперь растяну ссылку, задав для нее ширину и высоту в процентах. Конечно, можно указать эти параметры и с помощью пикселей, так как размеры логотипа известны. Но лучше возложить эту задачу на плечи браузера - пусть сам вычисляет размеры блока-ссылки:

{% highlight css %}
#logo a{
  display: block;
  width: 100%;
  height: 100%;
}
{% endhighlight %}

Осталось создать навигационное меню шапки, которое должно располагаться поверх слоя `div id="nav"`. Создаю ненумерованный список, который помещаю внутрь слоя `div id="nav"`. Так как по коду слой `div id="head"` расположен выше и имеет фиксированную высоту, то список займет все оставшееся пространство под ним: `70px - 50px = 20px`.

Теперь достаточно сместить список вправо с помощью `float: right` и прописать для него обычные свойства, чтобы расположить горизонтально и стилизовать:

{% highlight css %}
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
{% endhighlight %}

Единственный момент, который вызвал у меня затруднения, это появившиеся еле заметные отступы между внешним блоком `ul` и внутренним элементом(ами) `li`. Первоначально для них я прописал свойство `display: inline`. Но после "наводки" Kray Storm с форума forum.htmlbook.ru проблема была решена. Для элементов `li` и я поменял свойство на `display: inline-block` и для я дополнительно задал высоту строки `line-height: 20px`, равную высоте блока `ul`. Зазоры пропали и пункты меню растянулись на всю высоту блока-родителя.

Все, шапка сайта готова. Если посмотреть на html-код, то видно, что он "правильный". То есть, он не замусорен всякими `img`. Разметка выполнена простыми свойствами CSS, который будут гарантировано работать почти во всех браузерах. При этом она никуда не "съедет". Ниже приведу полный код html-каркаса и CSS-кода.

HTML-код:

<figure id="attachment_371" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/09/header-karkas-600x256.png" alt="HTML каркас шапки сайта" width="600" height="256" class="size-medium wp-image-371" />][2]
  <figcaption class="wp-caption-text">HTML каркас шапки сайта</figcaption>
</figure>

CSS-код:

{% highlight css %}
/*  reset  */
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
{% endhighlight %}

Здесь я представлю нарисованную мною схему расположения всех блоков в шапке сайта:

<figure id="attachment_372" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/09/shema.png" alt="Блок-схема на div&#039;ах шапки сайта" width="600" height="400" class="size-full wp-image-372" />][3]
  <figcaption class="wp-caption-text">Блок-схема на div'ах шапки сайта</figcaption>
</figure>

И, наконец, результат всего - готовая шапка сайта:

<figure id="attachment_373" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/09/result-header-600x314.png" alt="Готовая шапка сайта" width="600" height="314" class="size-medium wp-image-373" />][4]
  <figcaption class="wp-caption-text">Готовая шапка сайта</figcaption>
</figure>

 [1]: http://localhost:7788/third/?p=187 "Раздвижной фон на CSS"
 [2]: http://localhost:7788/third/wp-content/uploads/2013/09/header-karkas.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/09/shema.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/09/result-header.png