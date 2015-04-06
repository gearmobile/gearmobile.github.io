---
title: "Hexagon на CSS"
layout: post
categories: css
tags: [css, hexagon]
share: true
---

> В этой статье будет детально рассмотрен вопрос создания фигуры шестиугольника (hexagon) на CSS.

Материал целиком основан на замечательной статье [CSS Hexagon Tutorial][1]. В Сети имеется хорошая статья по примерам создания различных видов фигур на CSS, и располагается эта статья на блоге известного CSS-гуру Chris Coyier [Shapes of CSS][2]. Среди прочих фигур там есть и желанный шестиугольник `hexagon` с готовым CSS-кодом что называется, "бери и пользуйся".

Но ведь такой подход для нас не интересен, правда? Это потом, когда мы изучим вопрос создания шестиугольника, мы будем делать так - нашел готовый код, скопировал к себе, подредактировал и готово! А сейчас мы пошагово пройдем весь путь, от начала и до конца - это даст нам понимание процесса.

## Как будем строить hexagon

Фигура hexagon изначально кажется неприступной - не понятно, с какого боку к ней подойди, чтобы начать постороение шестиугольника на CSS. Однако, если внимательно присмотреться, то hexagon можно разделить на три простые фигуры:

![Три части фигуры hexagon]({{site.url}}/images/uploads/2014/07/hexagon_origin.jpg)

Видно, что фигура состоит из двух одинаковых треугольников и одного прямоугольника. Построение треугольников на CSS выполняется очень просто - "CSS – почему треугольник это треугольник", прямоугольника - вообще в два движения.

Поэтому, построение шестиугольника hexagon на CSS сводится к двух задачам:

  * создать два треугольника
  * создать один прямоугольник

## Построение треугольников на CSS

Задачу создания треугольников на CSS начнем с построения обычного квадрата со стороной в `100px` и широкой границей `30px` определенного цвета `#789`:

{% highlight html %}
<div class="hexagon">
{% endhighlight %}

{% highlight css %}
.hexagon{
  width: 100px;
  height: 100px;
  border: 30px solid #789;
}
{% endhighlight %}

![Квадрат на CSS]({{site.url}}/images/uploads/2014/07/hexagon_square.jpg)

"Раскрасим" границы квадрата для того, чтобы можно было визуально отличать их друг от друга:

{% highlight html %}
<div class="hexagon hexagon_colors"></div>
{% endhighlight %}

{% highlight css %}
.hexagon_colors{
  border-top-color: lighten(#789, 5%);
  border-right-color: lighten(#789, 10%);
  border-bottom-color: darken(#789, 10%);
  border-left-color: darken(#789, 5%);
}
{% endhighlight %}

![Квадрат на CSS с границами разного цвета]({{site.url}}/images/uploads/2014/07/hexagon_square_colors.jpg)

Затем обнулим высоту `height` и ширину `width` нашего квадрата. Он "схлопнется", оставив для нас видимой только его широкую границу со всех четырех сторон:

{% highlight html %}
<div class="hexagon hexagon_colors hexagon_zero"></div>
{% endhighlight %}

{% highlight css %}
.hexagon_zero{
  width: 0;
  height: 0;
}
{% endhighlight %}

![Квадрат на CSS с нулевой высотой и шириной]({{site.url}}/images/uploads/2014/07/hexagon_square_zero.jpg)

Теперь превратим полученную фигуру в настоящий треугольник. Для этого обнулим (уберем) у нее верхнюю границу `border-top`, а обе боковые границы `border-left`, `border-right` сделаем прозрачного `transparent` цвета:

{% highlight html %}
<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up"></div>
{% endhighlight %}

{% highlight css %}
.hexagon_triangle_up{
  border-top-width: 0;
  border-right-color: transparent;
  border-left-color: transparent;
}
{% endhighlight %}

![Треугольник на CSS]({{site.url}}/images/uploads/2014/07/hexagon_square_to_triangle.jpg)

У получившегося треугольника все стороны равны - высота и ширина по 30px каждая. Нам же необходимо "растянуть" треугольник в ширину, чтобы он у него появился тупой угол. Для этого нужно увеличить ширину боковых границ `border-left`, `border-right` треугольника, а ширину нижней границы `border-bottom` оставить прежней:

{% highlight html %}
<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
{% endhighlight %}

{% highlight css %}
.hexagon_triangle_up_large{
  border-left-width: 52px;
  border-right-width: 52px;
}
{% endhighlight %}

![Удлиненный треугольник на CSS]({{site.url}}/images/uploads/2014/07/hexagon_square_to_triangle_large.jpg)

Задача создания треугольника нами выполнена. Теперь необходимо получить точно такой треугольник, только "направленный" вниз. Это просто - достаточно поменять нулевое значение между верхней и нижней границей фигуры. Все остальные значения останутся неизменными. Чуть не забыл сказать, что для "повернутого" треугольника придется создать в HTML-коде новый блок:

{% highlight html %}
<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
{% endhighlight %}

{% highlight css %}
...

.hexagon_triangle_down{
  border-bottom-width: 0;
  border-right-color: transparent;
  border-left-color: transparent;
}

.hexagon_triangle_down_large{
  border-left-width: 52px;
  border-right-width: 52px;
}
{% endhighlight %}

![Два треугольника на CSS]({{site.url}}/images/uploads/2014/07/hexagon_square_to_two_triangles.jpg)

Первый шаг по созданию шестиугольника hexagon на CSS выполнен - у нас есть два одинаковых разнонаправленных треугольника. Теперь нужно создать "тело" для шестиугольника - прямоугольник.

### Построение прямоугольника на CSS

Для создания прямоугольника на CSS достаточно прописать для нового блока три величины - высоту, ширину и фоновый цвет. Новый блок я размещу между двумя блоками-треугольниками.

А вот с размерами для прямоугольника нужно разобраться немного подробнее. У него ширина должна быть равна удвоенной ширине боковой границы треугольника:

{% highlight css %}
border-left-width: 52px + border-right-width: 52px = 104px
{% endhighlight %}

А высота должна быть равна удвоенной высоте треугольника (или ширине верхней\нижней границы - кому как нравиться):

{% highlight css %}
border-top: 30px * 2 = 60px
{% endhighlight %}

В результате код будет следующим:

{% highlight html %}
<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
<div class="inside"></div>
<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
{% endhighlight %}

{% highlight css %}
...

.inside{
  width: 104px;
  height: 60px;
  background-color: #789;
}
{% endhighlight %}

![Hexagon на CSS]({{site.url}}/images/uploads/2014/07/hexagon.jpg)

Все - задача построения шестиугольника hexagon на CSS выполнена - все оказалось достаточно просто!

## Создание сетки из hexagon

Теперь можно усложнить задачу и создать из фигур hexagon своеобразную сетку, а-ля пчелиные соты. Задача тривиальная и весь вопрос сводиться к нескольким CSS-свойствам: `float`, `overflow`, `margin`, `padding`.

Создаю первый ряд сетки:

{% highlight html %}
<div class="row">
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
</div>
<!--  end row  -->
{% endhighlight %}

{% highlight css %}
...

.inside{
  width: 104px;
  height: 60px;
  background-color: #778899;
}

.hexa{
  float: left;
  margin: 0 3px 0 0;
}

.row{
  overflow: hidden;
}
{% endhighlight %}

![Первый ряд сетки из hexagons]({{site.url}}/images/uploads/2014/07/hexagon_first_row.jpg)

Второй ряд сетки строиться аналогично, за тем лишь исключением, что его необходимо сдвинуть влево и вверх:

{% highlight html %}
<!--  ROW  -->
<div class="row left_padding top_margin">
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large"></div>
    <div class="inside"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large"></div>
  </div>
  <!--  end hexa  -->
</div>
<!--  end row  -->
{% endhighlight %}

{% highlight css %}
.left_padding{
  padding-left: 53px;
}

.top_margin{
  margin-top: -28px;
}
{% endhighlight %}


![Первый и второй ряды сетки из hexagons]({{site.url}}/images/uploads/2014/07/hexagon_first-second_rows.jpg)

Дальше продолжать не имеет смысла - все остальные ряды строятся аналогично. Нужно только управлять ими с помощью соотвествующих классов, смещая влево или вверх:

![Несколько рядов сетки из hexagons]({{site.url}}/images/uploads/2014/07/hexagon_full_stack.jpg)

Лучше перейдем к другому интересному вопросу - созданию такого же шестиугольника hexagon, но несколько иной формы, "повернутого". У которого углы развернуты по-горизонтали, а не по-вертикали.

### Построение повернутого hexagon на CSS

Задача создания развернутого hexagon почти ничем не отличается от задачи построения обычного шестиугольника. Только потребуется несколько дополнительных строчек кода.

Дело в том, что в этом случае нужны углы, которые будут располагаться горизонтально и "смотреть" влево или вправо. Помимо этого, понадобиться "плавание" влево `float: left;`.

Для блока - "тела" hexagon нужно будет изменить значения высоты или ширины на прямопротивоположные.

Но не буду голословным, а лучше создам один такой `hexagon`:

{% highlight html %}
<div class="hexa">
  <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left"></div>
  <div class="inside_rotate left"></div>
  <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left"></div>
</div>
<!--  end hexa  -->
{% endhighlight %}

{% highlight css %}
/*  LEFT ARROW  */

.hexagon_triangle_left{
  border-left-width: 0;
  border-top-color: transparent;
  border-bottom-color: transparent;
}

.hexagon_triangle_left_large{
  border-top-width: 52px;
  border-bottom-width: 52px;
}

/*  RIGHT ARROW  */

.hexagon_triangle_right{
  border-right-width: 0;
  border-top-color: transparent;
  border-bottom-color: transparent;
}

.hexagon_triangle_right_large{
  border-top-width: 52px;
  border-bottom-width: 52px;
}

.inside_rotate{
  width: 60px;
  height: 104px;
  background-color: #778899;
}

.left{
  float: left;
}
{% endhighlight %}

![Развернутый hexagon]({{site.url}}/images/uploads/2014/07/hexagon_rotated.jpg)

Добавлю несколько таких шестиугольников, чтобы получился полный ряд:

![Несколько развернутых hexagons в ряд]({{site.url}}/images/uploads/2014/07/hexagon_rotated_row.jpg)

Отлично! Теперь нужно добавить еще один ряд - нижний. При этом опять придется немного модифицировать код, чтобы произвести смещение фигур влево и вверх:

{% highlight html %}
<!--  ROW  -->
<div class="row top_margin_double">
  <div class="hexa left_padding_double_middle">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left"></div>
    <div class="inside_rotate left"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa left_padding_double">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left"></div>
    <div class="inside_rotate left"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left"></div>
  </div>
  <!--  end hexa  -->
  <div class="hexa left_padding_double">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left"></div>
    <div class="inside_rotate left"></div>
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left"></div>
  </div>
  <!--  end hexa  -->
</div>
<!--  end row  -->
{% endhighlight %}

{% highlight css %}
.left_padding_double{
  padding-left: 64px;
}

.left_padding_double_middle{
  padding-left: 94px;
}

.top_margin_double{
  margin-top: -50px;
}
{% endhighlight %}

![Развернутые hexagons в два ряда]({{site.url}}/images/uploads/2014/07/hexagon_rotated_several_rows.jpg)

Можно продолжать постороние рядов до бесконечности, получая сетку из hexagons все большего размера:

![Развернутые hexagons в несколько рядов]({{site.url}}/images/uploads/2014/07/hexagon_rotated_more_rows.jpg)

### 3D-проекция hexagons

Можно видоизменить внешний вид сетки из hexagons, воспользовавшись CSS3-свойством `transform`. Создаю отдельный класс, в котором прописываю такие свойстсва:

{% highlight css %}
.hexa_transform{
  -webkit-transform: perspective(600px) rotateX(60deg);
  -moz-transform: perspective(600px) rotateX(60deg);
  -ms-transform: perspective(600px) rotateX(60deg);
  -o-transform: perspective(600px) rotateX(60deg);
  transform: perspective(600px) rotateX(60deg);
}
{% endhighlight %}

... и проверяю в окне браузера:

![3D-проекция сетки из hexagons]({{site.url}}/images/uploads/2014/07/hexagon_rotated_transform.jpg)

## Hexagons с помощью псевдо-классов

Рассмотренный выше способ создания hexagons хорош, но имеет один недостаток - слишком много дополнительных блоков, одними из которых являются блоки для создания треугольников.

Можно (и нужно) значительно сократить код, воспользовавшись для этой цели псевдо-классами `:before` и `:after`. Давайте я так и поступлю, при этом возьму код из примера, не буду ничего выдумывать:

{% highlight css %}
.hex:before {
  content: - ";
  width: 0; height: 0;
  border-bottom: 30px solid #778899;
  border-left: 52px solid transparent;
  border-right: 52px solid transparent;
  position: absolute;
  top: -30px;
}

.hex {
  margin-top: 30px;
  width: 104px;
  height: 60px;
  background-color: #778899;
  position: relative;
  float: left;
}

.hex:after {
  content: "";
  width: 0;
  position: absolute;
  bottom: -30px;
  border-top: 30px solid #778899;
  border-left: 52px solid transparent;
  border-right: 52px solid transparent;
}
{% endhighlight %}

![Hexagon на CSS с помощью псевдо-классов :before и :after]({{site.url}}/images/uploads/2014/07/hexagon_pseudo.jpg)

## CSS Hexagon

Рассмотренный выше способ неплох, причем оба его варианта. Но для практического применения оба они достаточно трудоемкие. В Сети, помимо многих других подобного рода, имеется online CSS-генератор для создания hexagon в считанные минуты.

Адрес сервиса располагается здесь - [CSS Hexagon][3]. Помимо создания самого hexagon, там можно "прикрутить" к фигуре тень и границу, что просто великолепно!

Все - на этом обзор закончен.

---

 [1]: http://jtauber.github.io/articles/css-hexagon.html "CSS Hexagon Tutorial"
 [2]: http://css-tricks.com/examples/ShapesOfCSS/ "Shapes of CSS"
 [3]: http://csshexagon.com/ "CSS Hexagon"
