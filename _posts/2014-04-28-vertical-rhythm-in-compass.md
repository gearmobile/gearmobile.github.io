---
title: "Создание Vertical Rhythm в Compass"
layout: post
categories: css
tags: [vertical-rhythm, compass]
share: true
---

> Приступаем к интересной теме - вертикальному ритму "Vertical Rhythm" в веб-дизайне и способе его создания с помощью библиотеки Compass.

Первое, с чего стоит начать, это небольшой вводный курс - что такое вертикальный ритм и для чего он нужен.

Ну, во-первых, в Интернете на момент написания статьи не так уж и много материалов по этой тематике; в немногочисленных материалах сущность вопроса преподносится как нечто очень сложное.

На самом деле это не так. Все мы когда-то учились в школе и наверное, помним тетрадки в линейку по русскому языку, в которых строгие учительницы заставляли нас писать:

![Vertical Rhythm - Школьная тетрадь в линейку]({{site.url}}/images/uploads/2014/04/copybook.jpg)

Так вот - сами не зная об этом, мы уже тогда использовали вертикальный ритм (Vertical Rhythm) на практике! Слово вертикальный ритм говорит само за себя - текст или контент на странице должен размещаться в определенном ритме, по определенному правилу; а не хаотично.

В данном случае все строки на такой странице должны размещаться по нарисованным линейкам - это и есть суть пресловутого Vertical Rhythm.

В типографике вертикальный ритм применяется с незапамятных времен; и только с недавних пор о вертикальном ритме заговорили применительно к веб-дизайну. Использование вертикального ритма в веб-дизайне подразумевает применение CSS-свойств, управляющих вертикальными параметрами элементов страницы: размером шрифта (`font-size`), высотой строки(`line-height`), отступами (`padding` и `margin`), границами (`border`).

Основная цель вертикального ритма - сделать текст (контент - в общем случае) максимально читабельным. То есть, это когда посетитель заходит на страницу, читает что-либо на ней, и сам процесс не доставляет ему никаких неудобств. Напротив - ему приятно читать такой текст.

В библиотеке Compass имеется модуль "Vertical Rhythm", задача которого - максимально упростить создание и настройку вертикального ритма в проекте. Модуль Vertical Rhythm в Compass - это набор функций и миксинов, облегчающих вычисление высоты строк, вертикального `padding` и `margin`, толщины границ (`border`).

Вычисления основаны на базовой высоте строки `line-height` и базовом размере шрифта `font-size` с целью создания горизонтальной сетки. Давайте приступим к практике; то, что я не смог рассказать своими словами, думаю, будет наглядно показано на живых примерах.

Первое, что необходимо сделать - это установить (если еще не установлена) Compass версии `1.0.0 alpha 19`. Почему именно эту версию? В ней есть множество возможностей, которые отсутствуют в старой версии.

Установка Compass этой версии под Windows 7 на момент написания статьи является достаточно непростой задачей, поэтому рекомендую обратиться к статье "Медиа-запросы Breakpoint в Sass".

## Создаем и настраиваем проект в Compass

Создаем новый проект в командной строке с помощью Compass:

{% highlight powershell %}
compass create vertical_rhythm_example --bare
{% endhighlight %}

Ключ `--bare` используется здесь, чтобы создать "голый" экземпляр проекта под Sass/Compass, без лишних файлов `print.scss`, `ie.scss` и так далее.

Производим неодходимые настройки в файле `config.rb`, а также создаем файлы `sass/style.scss`, `css/style.css`, `index.html`.

HTML-файл наполним структурой вида:

{% highlight html %}
<div class="wrapper">
  <h1>header 1</h1>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, architecto laborum quas iste nam maxime tempora temporibus inventore? Rerum, obcaecati porro officiis temporibus assumenda dicta odit ullam dolore vero laborum!</p>
  <h2>header 2</h2>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Doloremque, accusantium, amet, molestiae quas dolore deleniti non aut quis inventore repudiandae nostrum porro alias dolor pariatur rem sequi ea consequatur perferendis.</p>
  <h3>header 3</h3>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequatur, iusto, iure, quia ipsum dolore ea exercitationem porro et nostrum nam cumque hic possimus dolorem deleniti distinctio incidunt magnam earum quis.</p>
  <h4>header 4</h4>
  <img src="http://placehold.it/700x300" />
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Tempora, omnis, ut, quis, nesciunt voluptatum rem dolor dolores amet vel sit error laboriosam quasi accusamus magnam neque sunt exercitationem molestias! Aperiam!</p>
  <h5>header 5</h5>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Atque, libero illum numquam sed quas. Assumenda, porro, suscipit, veniam, cum deleniti illo magnam harum ab earum obcaecati odit ad quo laudantium?</p>
  <img src="http://placehold.it/500x200" />
  <h6>header 6</h6>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid, consectetur quod saepe unde corrupti tenetur minus nesciunt obcaecati tempore ut facere iusto pariatur corporis itaque eius? Doloribus, quaerat modi nihil.</p>
</div>
{% endhighlight %}

То есть, для чистоты эксперимента, создаем заголовки с первого по шестой уровень, несколько параграфов и два изображения. В процессе работы с модулем вертикального ритма будем пользоваться официальной документацией по адресу - [Vertical Rhythm][3].

В файле `style.scss` подключаем сброс стилей Compass и модуль вертикального ритма:

{% highlight css %}
@import "compass/reset";
@import "compass/typography/vertical_rhythm";
{% endhighlight %}

Сделаем небольшую стилизацию для блока `.wrapper`, заголовков, параграфов и изображений, чтобы визуально было проще разобраться, что к чему:

{% highlight css %}
.wrapper{
  max-width: 960px;
  margin: 0 auto;
  background-color: hsla(240,100%,50%,.2);
}

h1,h2,h3,h4,h5,h6{
  font-weight: 700;
  text-transform: capitalize;
  background-color: hsla(120,100%,50%,.2);
}

p{
  background-color: hsla(0,100%,50%,.1);
}

img{
  max-width: 100%;
  margin: auto;
  display: block;
}
{% endhighlight %}

## Основные переменные в Vertical Rhythm

В модуле "Vertical Rhythm" библиотеки Compass имеется множество переменных, но среди них есть только две основные, которые необходимы для расчетов внутри этого модуля:

{% highlight css %}
$base-font-size: 22px;    // базовый размер шрифта
$base-line-height: 33px;  // базовое межстрочное расстояние
{% endhighlight %}

Значение переменной `$base-line-height` (как правило) равно выражению `$base-font-size * 1.5`, поэтому `22px * 1.5 = 33px`. Значение переменной `$base-font-size` в `22px` взято в качестве примера.

Помимо этого, есть еще две дополнительные переменные:

{% highlight css %}
$rhythm-unit: "rem";         // базовая единица измерения (по умолчанию em)
$rem-with-px-fallback: true; // откат к единицам измерения px в браузерах, которые не понимают единицу rem
{% endhighlight %}

## Включаем Vertical Rhythm

После ввода четырех вышеперечисленных переменных осталось только инициализировать модуль Vertical Rhythm" с помощью миксина:

{% highlight css %}
@include establish-baseline;
{% endhighlight %}

Миксин `establish-baseline` делает простые вещи - он устанавливает `font-size` и `line-height` для корневого тега `<html>`. Но делает он это с помощью относительных единиц измерения.

Допустим, в своем проекте мы установили размер шрифта `22px` и высоту строки `33px`. Если взглянуть на результат компиляции из SCSS в CSS, то увидим следующее:

{%  highlight css %}
html {
  font-size: 137.5%;
  line-height: 1.5em;
}
{% endhighlight %}

Размер шрифта `16px` является установленным по умолчанию в большинстве браузеров, поэтому `16px = 100%`. Следовательно, `22px = 137.5%`.

Относительная величина `line-height` всегда относительна к размеру шрифта `font-size` текущего элемента, поэтому в данном случае она равна 1.5em (`22px * 1.5 = 33px`).

Перезагрузим браузер с открытой страницей создаваемого проекта-примера и увидим, как резко изменилась картина! Вместо слепленных друг с другом строчек появилась более четкая и удобочитаемая структура. Видно, что каждая строка текста располагается внутри своей линии.

Чтобы еще более наглядно представить картину структурированного контента, воспользуемся миксином:

{% highlight css %}
body{
  @include debug-vertical-alignment;
}
{% endhighlight %}

Обрисовались строки, ну прямо как на школьном тетрадном листке! Хорошо видно, как все строки текста и изображение выстроились четко по линеечкам. Думаю, если читатель дошел до этого места, то ему стала понятна суть и принцип вертикального ритма без каких-либо объяснений!

## Margin и padding в Vertical Rhythm

Но строки, заголовки и изображения все равно тесно прижаты друг к другу. В модуле **Vertical Rhythm** имеются свои собственные инструменты для создания отступов у элементов контента, в основе которых лежит опять таки базовый размер шрифта (вот он - тот самый ритм!):

{% highlight css %}
$base-font-size * 1
{% endhighlight %}

Для элемента страницы можно задать `margin-top` или `padding-top`, `margin-bottom` или `padding-bottom`. Реализуется это с помощью специальных миксинов (на выбор, один из четырех):

{% highlight css %}
p{
  background-color: hsla(0,100%,50%,.1);

  @include margin-trailer;  // margin-bottom
  @include margin-leader;   // margin-top

  @include padding-trailer; // padding-bottom
  @include padding-leader;  // padding-top
}
{% endhighlight %}

Имеются универсальные миксины, которые являются сокращениями от вышеперечисленных. Таким миксинам передаются необходимые аргументы и на выходе получаем результат:

{% highlight css %}
p{
  background-color: hsla(0,100%,50%,.1);

  @include trailer($lines: 2, $property: margin); // margin-bottom на 2 строки
  @include trailer($lines: 2, $property: padding); // padding-bottom на 2 строки

  @include leader($lines: 2, $property: margin); // margin-top на 2 строки
  @include leader($lines:3, $property: padding); // padding-top на 3 строки
}
{% endhighlight %}

Одновременно задать `margin-top + margin-bottom` или `padding-top + padding-bottom` можно с помощью миксинов:

{% highlight css %}
p{
  background-color: hsla(0,100%,50%,.1);

  @include rhythm-margins; // margin-top + margin-bottom
  @include rhythm-padding; // padding-top + padding-bottom
}
{% endhighlight %}

Миксин `@include rhythm` является глобальным сокращением вышеназванных миксинов для создания отступов `margin` или `padding`.

## Создание границ в Vertical Rhythm

Отступы можно совмещать с границами `border`. То есть, можно (к примеру) создать верхний `padding` с верхней границей `border`.

Толщина границы и ее стиль управляются через переменные `$default-rhythm-border-width` и `$default-rhythm-border-style`. По умолчанию толщина границы равна `1px`, а ее стиль - `solid`.

{% highlight css %}
p{
  background-color: hsla(0,100%,50%,.1);

  @include leading-border; // padding-top + border-top
  @include trailing-border; // padding-bottom + border-bottom
  @include horizontal-borders; // padding-top + border-top и padding-bottom + border-bottom
  @include h-borders; // alias для horizontal-borders
}
{% endhighlight %}

Одновременно задать `padding` и `border` для всех четырех сторон можно через миксин:

{% highlight css %}
p{
  background-color: hsla(0,100%,50%,.1);
  @include rhythm-borders; // padding + border
}
{% endhighlight %}

Указать границу и отступ для какой-то одной стороны можно с помощью миксина:

{% highlight css %}
p{
  background-color: hsla(0,100%,50%,.1);
  @include apply-side-rhythm-border($side: left);
}
{% endhighlight %}

## Произвольный размер шрифта в Vertical Rhythm

Можно произвольно поменять размер шрифта любого элемента страницы, но делать это также нужно, исходя из ритма - с помощью соответствующего миксина `adjust-fonts-size-to`.

Давайте изменим размер заголовков таким образом, чтобы они отличались от основного текста (и были действительно заголовками):

{% highlight css %}
h1{
  @include adjust-font-size-to(2.074rem);
}

h2{
  @include adjust-font-size-to(1.728rem);
}

h3{
  @include adjust-font-size-to(1.44rem);
}

h4{
  @include adjust-font-size-to(1.2rem);
}

h5{
  @include adjust-font-size-to(1rem);
}

h6{
  @include adjust-font-size-to(0.833rem);
}
{% endhighlight %}

Или же, допустим, нужно установить для заголовка первого уровня `h1` размер шрифта в `42px`. Микcин будет выглядеть таким образом:

{% highlight css %}
h1{
  @include adjust-font-size-to(42px);
}
{% endhighlight %}

Первым делом, этот миксин делает размер шрифта элемента `h1` относительным к размеру шрифта элемента-контейнера. В нашем случае таковым является элемент `html`, поэтому размер шрифта равен `22px`. Соответственно, размер шрифта для `h1` получается (`42 / 22 = 1.90909`):

{% highlight css %}
font-size: 1.90909rem;
{% endhighlight %}

Вторым делом миксин заново вычисляет высоту строки для нашего заголовка `h1`. Делает он это таким образом:

{% highlight css %}
1.90909rem * 1.5 = 3rem (округленно)
22 * 3rem = 66px
{% endhighlight %}

Конечный результат показан ниже:

{% highlight css %}
h1 {
  font-size: 42px;
  font-size: 1.90909rem;
  line-height: 66px;
  line-height: 3rem;
}
{% endhighlight %}

Отлично, правда? Вся прелесть в том, что показанные выше расчеты можно с легкостью забыть - модуль "Vertical Rhythm" каждый раз будет вычислять размер шрифта и высоту строки сам, не "напрягая" нас.

Помимо указания размера шрифта в качестве аргумента, миксину `adjust-fonts-size-to` можно также передать количество линий, которое должен занимать заголовок. Например, так:

{% highlight css %}
h3{
  @include adjust-font-size-to(1.44rem,1);
}
{% endhighlight %}

Если вы попробуете у себя, то сразу увидите результат.

## Выравнивание изображений в Vertical Rhythm

Внимательный читатель должен заметить одну неточность, если он у себя повторил все шаги, описанные выше. Неточность заключается в том, что изображение не вписывается в вертикальный ритм, созданный нами на странице:

![Смещение в вертикальном ритме]({{site.url}}/images/uploads/2014/04/shift_in_vertical_rhythm.jpg)

А именно - первое изображение своим верхним краем совпадает с линией ритма. А вот нижняя граница не попадает на линию. Из-за этого весь дальнейший контент также смещается и вертикальный ритм нарушается.

Происходит это потому, что изображение мы сделали блочным элементом и присвоили ему фиксированные размеры в пикселях в HTML-коде:

{% highlight html %}
<img src="http://placehold.it/700x350" />
...
<img src="http://placehold.it/500x250" />
...
{% endhighlight %}

Исправить ситуацию можно с помощью плагина "Keep The Rhythm" под jQuery - [Keep The Rhythm][5]. Вдаваться в подробности работы этого плагина я не буду, а сразу покажу, как он подключается и результат его работы.

Получаем с GitHub библиотеку jQuery и сам плагин к ней:

{% highlight css %}
jquery-1.9.1.min.js
jquery.keeptherhythm.js
{% endhighlight %}

Подключаем к HTML-странице в ее конце. И затем создаем небольшой скрипт. Смотрим результат:

![Плагин Keep_The_Rhythm в действии]({{site.url}}/images/uploads/2014/04/keep_the_rhythm.jpg)

Все получилось! Однако, стоит заметить, что приведенный выше пример является упрощенным. Достаточно изменить масштаб страницы в окне браузера, и вертикальный ритм поломается.

Поэтому плагин "Keep The Rhythm" необходимо применять в связке с медиа-запросами для правильной его работы. По крайней мере, если возникнет вопрос по работе этого плагина, то документация на официальной странице всегда под рукой.

## Заключение

Основой для написания этой статьи послужили два материала (видео и статья):

* [Compass (Sass) — вертикальный ритм (vertical rhythm)][7]
* [Vertical Rhythm with Compass][8]

---

 [3]: http://beta.compass-style.org/reference/compass/typography/vertical_rhythm/ "Vertical Rhythm"
 [5]: http://www.gayadesign.com/diy/keep-the-rhythm-vertical-rhythm-on-objects-having-dynamic-heights/ "Keep The Rhythm"
 [7]: https://www.youtube.com/watch?v=Leert-TnSSg "Compass (Sass) — вертикальный ритм (vertical rhythm)"
 [8]: http://atendesigngroup.com/blog/vertical-rhythm-compass "Vertical Rhythm with Compass"