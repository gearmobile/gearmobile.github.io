---
title: 'Функции работы с цветом в Sass и Compass'
layout: post
categories: css
tags: [compass, sass]
share: true
---

> Приступаем к очередной интересной и обширной теме - как с помощью Sass/Compass облегчить себе жизнь при работе с цветами во время верстки.

Каждый верстальщик хорошо знает, как часто ему приходиться при верстке определять и манипулировать цветами в CSS-коде. Препроцессор Sass и его библиотека Compass обладают богатым набором функций, предназначеных для всевозможных операций с цветом в SCSS-коде.

Эта статья посвящена обзору функций Sass и Compass для работы с цветом. Начнем, как обычно, с самой простой функции и будем плавно продвигаться от простого к сложному.

## Первоначальная настройка проекта Compass

Для начала создадим пустой проект Compass и настроим его. Инициализируем несколько переменных _\$color_ и _\$color1_, которым определим цвет. Эти переменные понадобятся нам в дальнейшем.

{% highlight css %}
@import "compass/reset";

$color: hsla(120,100%,50%,.5);
$color1: hsla(240,100%,50%,.5);
\$unit: 180px;

div{
height: $unit;
  width: $unit;
border: 1px solid #000;
margin: 10px;
float: left;
text-align: center;
font-weight: bold;
font-size: 1.3rem;
color: darken($color,80%);
  line-height: $unit;
}
.origin{
background-color: \$color;
}
{% endhighlight %}

## Фунции lighten и darken

Начнем с самых простых функций - _lighten_ и _darken_. Кто маломальски знаком с английским языком, должен сам догадаться о их предназначении. Функция *lighten* осветляет исходный цвет, а функция *darken* затемняет его.

Синтаксис функций *lighten* и *darken* одинаков. Первым аргументом задается начальное значение цвета - передадим его функции в виде переменной *$color*. Вторым аргументом является значение в процентах, на которое нужно осветлить или затемнить исходный цвет:

{% highlight css %}
.lighten{
background-color: lighten(\$color,10%);
}

.darken{
background-color: darken(\$color,10%);
}
{% endhighlight %}

![Функции lighten и darken]({{site.url}}/images/uploads/2014/05/sass_colors-lighten_darken.png)

Функции lighten и darken могут использоваться в любом месте SCSS-кода - везде, где применяется цвет. Например, видоизменим показанный выше пример. Применим функции lighten и darken для изменения цвета шрифта, границы и фона:

{% highlight css %}
.mixin{
font-size: .95rem;
background-color: lighten($color,20%);
  border: 1px solid darken($color,30%);
color: darken(\$color,60%);
}
{% endhighlight %}

![Функции lighten и darken для цвета шрифта и границы]({{site.url}}/images/uploads/2014/05/sass_colors-mixin.png)

## Функции complement и invert

Переходим к функциям обратного преобразования цвета. Первая функция *complement* преобразует исходный цвет на прямо противоположный. Допустим, у нас имеется переменная *$color* c заданным в ней цветом. Передадим эту переменную функции *complement* в качестве аргумента:

{% highlight css %}
.complement{
background-color: complement(\$color);
}
{% endhighlight %}

В результате на выходе получим цвет, расположенный на 180 градусов по отношению к исходному цвету. Чтобы было понятнее, посмотрим на "HSLA wheel":

![HSLA wheel]({{site.url}}/images/uploads/2014/05/hsl-color-wheel.png)

Исходным цветом у нас является *hsla(120,100%,50%,.5)*. На 180 градусов по отношению к исходному цвету расположен *hsla(300,100%,50%,.5)*, иначе называемый Magenta. Вот его и получаем от функции *complement*.

Функция *invert* практичеси аналогична функции *complement*. Она также производит инвертирование цвета от исходного. Но функция *invert* отличается от функции *complement* тем, что с помощью нее производится инвертирование цветов (красного, зеленого, синего), но прозрачность *opacity* остается неизменной.

{% highlight css %}
.invert{
background-color: invert(\$color);
}
{% endhighlight %}

![Функции complement и invert]({{site.url}}/images/uploads/2014/05/sass_colors-complement_invert.png)

## Функция adjust-hue

Функция *adjust-hue* практически аналогична функции *complement* - она инвертирует исходный цвет. Но в отличие от последней обладает большей гибкостью. Если функция *complement* возвращает цвет, расположенный точно на 180 градусов от исходного (противоположный), то функция *adjust-hue* может управлять градусом расположения "выходного цвета."

Другими словами, можно задать угол, отличный от 180 градусов. Кроме того, значение угла может быть как положительным, так и отрицательным:

{% highlight css %}
.adjusthue_plus{
background-color: adjust-hue(\$color,80deg);
}

.adjusthue_minus{
background-color: adjust-hue(\$color,-80deg);
}
{% endhighlight %}

![Функция adjust-hue]({{site.url}}/images/uploads/2014/05/sass_colors-adjust-hue.png)

## Функции saturate и desaturate

В препроцессоре Sass имеется пара функций для управления насыщеностью цвета.

Функция *saturate()*:

{% highlight css %}
.saturate{
background-color: saturate(\$color,80%);
}
{% endhighlight %}

... увеличивает насыщенность цвета от исходного.

А функция *desaturate()*:

{% highlight css %}
.desaturate{
background-color: desaturate(\$color,80%);
}
{% endhighlight %}

... наоборот, уменьшает насыщенность цвета от исходного.

![Функции saturate и desaturate]({{site.url}}/images/uploads/2014/05/sass_colors-saturate_desaturate.png)

## Функции transparentize и fade-out

Функция *transparentize* добавляет к исходному цвету альфа-канал и, тем самым, управляет прозрачностью исходного цвета. Особая прелесть этой функции заключается в том, что даже если исходный цвет не имеет альфа-канала, то на выходе к этому цвету будет добавлен альфа-канал с заданым уровнем прозрачности. То есть, будет выполнено преобразование в формат RGBA.

Значение прозрачности может находиться в диапазоне от 0 (полностью прозрачный) до 1 (полностью непрозрачный):

{% highlight css %}
.transparentize{
background-color: transparentize(\$color,.2);
}
{% endhighlight %}

Функция *fade-out* аналогична функции *transparentize*:

{% highlight css %}
.fadeout{
background-color: fade-out(\$color,.2);
}
{% endhighlight %}

![Функции transparentize и fade-out]({{site.url}}/images/uploads/2014/05/sass_colors-transparentize_fade-out.png)

## Функции opacify и fade-in

Функции *opacify* и *fade-in* являются прямой противоположностью функций *transparentize* и *fade-out*. В помощью этих функций цвет делается менее прозрачным:

{% highlight css %}
.opacify{
background-color: opacify(\$color,.3);
}

.fadein{
background-color: fade-in(\$color,.3);
}
{% endhighlight %}

![Функции opacify и fade-in]({{site.url}}/images/uploads/2014/05/sass_colors-opacify_fade-in.png)

## Функция grayscale

Функция преобразования исходного цвета в оттенки серого чрезвычайно проста в использовании. В принципе, тут и рассказывать особенно нечего:

{% highlight css %}
.grayscale{
background-color: grayscale(\$color);
}
{% endhighlight %}

![Функция grayscale]({{site.url}}/images/uploads/2014/05/sass_colors-grayscale.png)

## Функция rgba

Если стоит задача преобразования исходного цвета (заданного в виде переменной, в формате HEX или HSLA) в формат RGBA, в этом случае на помощь придет функция *rgba*. При этом к выходному цвету добавляется альфа-канал для задания прозрачности цвета:

{% highlight css %}
.rgba{
background-color: rgba(\$color,.2);
}
{% endhighlight %}

![Функция rgba]({{site.url}}/images/uploads/2014/05/sass_colors-rgba.png)

С практической точки зрения функция rgba равносильна функции transparentize/fade-out или opacify/fade-in.

## Функция mix

В препроцессоре Sass имеется функция смешивания цветов для получения на выходе одного, результирующего цвета. Другими словами, у нас имеются два цвета, представленные переменными *$color* и *$color1*. C помощью функции *mix* можно смешать эти два цвета в определенной пропорции, чтобы получить на выходе один результирующий цвет.

{% highlight css %}
.mix{
background-color: mix($color,$color1,70%);
}
{% endhighlight %}

В показанном выше примере у функции *mix* имеются два аргумента в виде переменных (два цвета). Последний третий аргумент в виде процентов задает пропорцию, в которой один цвет будет смешан с другим. В нашем случае цвет *$color* смешан с цветом *$color1* в пропорции - 70% от первого цвета *$color* добавляется ко второму цвету *$color1*.

![Функция mix]({{site.url}}/images/uploads/2014/05/sass_colors-mix.png)

## Функция adjust-color

Вот мы и подошли к более сложным функциям препроцессора Sass. Первой из таких функций является *adjust-color*, c помощью которой можно управлять любым значением цвета - красным, зеленым, синим (для цветовой модели RGB) или же цветом, насыщеностью и светлотой (для цветовой модели HSL). Функции *adjust-color* также доступно управление альфа-каналом (прозрачностью) цвета.

Функция *adjust-color* достаточно сложная, но с помощью нее можно управлять практически всем, что относится к цвету в SCSS-коде. Давайте последовательно разберемся во всех ее возможностях.

Каждому цвету в этой функции соответствует одноименный аргумент:

- *$red*, *$green*, *$blue* - значения красного, зеленого и синего цветов в диапазоне от 0 до 255;
- *$hue* - значение от 0 до 359 градусов, обозначающих цвет на HSL-диаграме; значение может быть как положительным, так и отрицательным;
- *$saturation*, *$lightness* - значения насыщенности и светлоты для цветовой модели HSL; находятся в диапазоне от 0 до 100%; могут быть отрицательными или положительными;
- *$alpha* - значение альфа-канала в диапазоне от 0 до 1.

Хватит теории, давайте рассмотрим работу функции adjust-color на примерах.

1. Изменение цвета от исходного *$color* для цветовой модели HSLA. Первым аргументом передается цвет в виде переменной *$color*; вторым аргументом задается изменение цвета через переменную *$hue*:

{% highlight css %}
.adjustColorHue{
background-color: adjust-color($color,$hue:40);
}
{% endhighlight %}

![Функция adjust-color с аргументом $hue]({{site.url}}/images/uploads/2014/05/sass_colors-adjust-color_hue.png)

1. Изменение цвета и светлоты одновременно. Первым аргументом $color задается исходный цвет, вторым аргументом устанавливается цвет $hue, третьим аргументом задается изменение светлоты \$lightness:

{% highlight css %}
.adjustColorHueLightness{
background-color: adjust-color($color,$hue:40,\$lightness:30);
}
{% endhighlight %}

![Функция adjust-color с аргументом $hue и $lightness]({{site.url}}/images/uploads/2014/05/sass_colors-adjust-color_hue_lightness.png)

1. Изменение двух каналов цвета одновременно для цветовой модели RGB. Функции *adjust-color* передаются три аргумента: исходный цвет *$color*, канал красного цвета *$red*, канал зеленого цвета *$green*:

{% highlight css %}
.adjustColorRedGreen{
background-color: adjust-color($color,$red:40,\$green:30);
}
{% endhighlight %}

![Функция adjust-color с аргументом $red и $green]({{site.url}}/images/uploads/2014/05/sass_colors-adjust-color_red_green.png)

1. Смешивание аргументов цветовых моделей RGB и HSL в функции adjust-color. Передадим функции adjust-color аргументы исходного цвета $color, аргумент красного канала $red модели RGB и аргумент \$hue модели HSL:

{% highlight css %}
.adjustColorError{
background-color: adjust-color($color,$red:40,\$hue:20);
}
{% endhighlight %}

В результате компиляции данного кода в CSS получим такую ошибку:

{% highlight css %}
Syntax error: Cannot specify HSL and RGB values for a color at the same time for 'adjust-color'
on line 38 of .../sass/style.scss
{% endhighlight %}

... которая говорит о том, что в функции *adjust-color* недопустимо смешивание аргументов разных цветовых моделей - RGB и HSL.

Поэтому нужно быть внимательным при работе с функцией adjust-color и не допускать одновременной передачи функции аргументов разных цветовых моделей RGB и HSL.

## Функция scale-color

Рассмотренная выше функция *adjust-color* производила изменение цвета на основе занчений передаваемых ей аргументов. Функция *scale-color* работает несколько иначе - она изменяет цвет на основе исходного цвета. Чтобы было сразу понятно, о чем идет речь, давайте рассмотрим несколько примеров:

{% highlight css %}
.origin{
background-color: \$color;
}

.adjustcolor{
background-color: adjust-color($color,$lightness:-20%);
}

.scalecolor{
background-color: scale-color($color,$lightness:-20%);
}
{% endhighlight %}

![Разница между функциями adjust-color и scale-color]({{site.url}}/images/uploads/2014/05/sass_colors-adjust-color_scale-color.png)

В данном примере функция *adjust-color* берет за основу цвет в переменной *$color* и делает его светлее на фиксированные *20%*. Функция *scale-color*, c другой стороны, поступает несколько иначе. Ею строиться шкала светлоты от 1 до 100%, в которой 1 соответствует светлоте цвета, заданной в переменной *$color*. Значение *100%* соответствует полной прозрачности. И на основе этой шкалы функция *scale-color* вычисляет светлоту в *20%*.

Неудивительно, что в показанном выше примере результат функции *scale-color* оказался светлее, чем результат функции *adjust-color*.

## Функции shade и tint

Фреймворк Сompass также, как и препроцессор Sass, имеет в своем составе некоторое количество функций для работы с цветом. Наиболее интересными среди них могу показаться две функции - *shade* и *tint*.

Функция *shade* выполняет смешивание заданного цвета с черным цветом в указанной пропорции. Пропорция указывется в процентах от черного цвета:

{% highlight css %}
.shade{
background-color: shade(\$color,40%);
}
{% endhighlight %}

![Результат работы функции shade]({{site.url}}/images/uploads/2014/05/sass_colors-shade.png)

Функция *tint*, напротив, выполняет смешивание исходного цвета с белым цветом в заданном соотношении. Код ниже создаст цвет на основе смешения цвета в переменной *$color* и *30%* белого цвета:

{% highlight css %}
.tint{
background-color: tint(\$color,30%);
}
{% endhighlight %}

![Результат работы функции tint]({{site.url}}/images/uploads/2014/05/sass_colors-tint.png)

## Заключение

На этом обзор "цветовых" функций препроцессора Sass и библиотеки Compass можно считать завершенным. В качестве вывода можно сказать, что благодаря подобным функциям упрощается и убыстряется работа при верстке дизайна сайта.

Более того, с помощью данных функций, имея в качестве входного значения всего один цвет, можно создать отличный дизайн в профессиональной цветовой палитре. И не прибегнуть ни к одному из графических инструментов.

Помимо использования рассмотренных выше цветовых функций каждой по отдельности, можно комбинировать их в одном выражении, создавая достаточно сложные конструкции.

Данная статья является вольным переводом главы "Manipulate Color with Ease" замечательной книги "Sass and Compass for Designers" автора Ben Frain.

---
