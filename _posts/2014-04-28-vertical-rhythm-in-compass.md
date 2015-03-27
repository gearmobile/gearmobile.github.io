---
title: Создание Vertical Rhythm в Compass
author: gearmobile
layout: post
permalink: /vertical-rhythm-in-compass/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - vertical rhythm
---
Приступаем к интересной теме &#8211; вертикальному ритму (**Vertical Rhythm**) в веб-дизайне и способе его создания с помощью библиотеки Compass.

Первое, с чего стоит начать, это небольшой вводный курс &#8211; что такое вертикальный ритм и для чего он нужен. Ну, во-первых, в Интернете на момент написания статьи не так уж и много материалов по этой тематике; в немногочисленных материалах сущность вопроса преподносится как нечто очень сложное. На самом деле это не так. Все мы когда-то учились в школе и наверное, помним тетрадки в линейку по русскому языку, в которых строгие учительницы заставляли нас писать:<figure id="attachment_1129" style="width: 528px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/copybook-528x600.jpg" alt="Vertical Rhythm - Школьная тетрадь в линейку" width="528" height="600" class="size-medium wp-image-1129" />][1]<figcaption class="wp-caption-text">Vertical Rhythm &#8211; Школьная тетрадь в линейку</figcaption></figure> 

Так вот &#8211; сами не зная об этом, мы уже тогда **использовали вертикальный ритм (Vertical Rhythm) на практике**! Слово вертикальный ритм говорит само за себя &#8211; текст или контент на странице должен размещаться в определенном ритме, по определенному правилу; а не хаотично. В данном случае все строки на такой странице должны размещаться по нарисованным линейкам &#8211; это и есть суть пресловутого Vertical Rhythm.

В типографике вертикальный ритм применяется с незапамятных времен; и только с недавних пор о вертикальном ритме заговорили применительно к веб-дизайну. Использование вертикального ритма в веб-дизайне подразумевает применение CSS-свойств, управляющих вертикальными параметрами элементов страницы: размером шрифта (`font-size`), высотой строки(`line-height`), отступами (`padding` и `margin`), границами (`border`).

Основная цель вертикального ритма &#8211; сделать текст (контент &#8211; в общем случае) максимально читабельным. То есть, это когда посетитель заходит на страницу, читает что-либо на ней, и сам процесс не доставляет ему никаких неудобств. Напротив &#8211; ему приятно читать такой текст.

В библиотеке Compass имеется модуль **Vertical Rhythm**, задача которого &#8211; максимально упростить создание и настройку вертикального ритма в проекте. Модуль Vertical Rhythm в Compass &#8211; это набор функций и миксинов, облегчающих вычисление высоты строк, вертикального `padding` и `margin`, толщины границ (`border`). Вычисления основаны на базовой высоте строки `line-height` и базовом размере шрифта `font-size` с целью создания горизонтальной сетки. Давайте приступим к практике; то, что я не смог рассказать своими словами, думаю, будет наглядно показано на живых примерах.

Первое, что необходимо сделать &#8211; это установить (если еще не установлена) Compass версии `1.0.0 alpha 19`. Почему именно эту версию? В ней есть множество возможностей, которые отсутствуют в старой версии. Установка Compass этой версии под Windows 7 на момент написания статьи является достаточно непростой задачей, поэтому рекомендую обратиться к статье [Медиа-запросы Breakpoint в Sass][2].

### Создаем и настраиваем проект в Compass

Создаем новый проект в командной строке с помощью Compass:

<pre>compass create vertical_rhythm_example --bare</pre>

Ключ `--bare` используется здесь, чтобы создать &#8220;голый&#8221; экземпляр проекта под Sass/Compass, без лишних файлов `print.scss`, `ie.scss` и так далее. Производим неодходимые настройки в файле `config.rb`, а также создаем файлы `sass/style.scss`, `css/style.css`, `index.html`.

HTML-файл наполним структурой вида:

<pre><div class="wrapper">
  <h1>
    header 1
  </h1>
  
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, architecto laborum quas iste nam maxime tempora temporibus inventore? Rerum, obcaecati porro officiis temporibus assumenda dicta odit ullam dolore vero laborum!
  </p>
  
  
  
  <h2>
    header 2
  </h2>
  
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Doloremque, accusantium, amet, molestiae quas dolore deleniti non aut quis inventore repudiandae nostrum porro alias dolor pariatur rem sequi ea consequatur perferendis.
  </p>
  
  
  
  <h3>
    header 3
  </h3>
  
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequatur, iusto, iure, quia ipsum dolore ea exercitationem porro et nostrum nam cumque hic possimus dolorem deleniti distinctio incidunt magnam earum quis.
  </p>
  
  
  
  <h4>
    header 4
  </h4>
  
  
  
  <img src="http://placehold.it/700x300" />
  
  
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Tempora, omnis, ut, quis, nesciunt voluptatum rem dolor dolores amet vel sit error laboriosam quasi accusamus magnam neque sunt exercitationem molestias! Aperiam!
  </p>
  
  
  
  <h5>
    header 5
  </h5>
  
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Atque, libero illum numquam sed quas. Assumenda, porro, suscipit, veniam, cum deleniti illo magnam harum ab earum obcaecati odit ad quo laudantium?
  </p>
  
  
  
  <img src="http://placehold.it/500x200" />
  
  
  
  <h6>
    header 6
  </h6>
  
  
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid, consectetur quod saepe unde corrupti tenetur minus nesciunt obcaecati tempore ut facere iusto pariatur corporis itaque eius? Doloribus, quaerat modi nihil.
  </p>
  
  
</div>
</pre>

То есть, для чистоты эксперимента, создаем заголовки с первого по шестой уровень, несколько параграфов и два изображения. В процессе работы с модулем вертикального ритма будем пользоваться официальной документацией по адресу &#8211; [Vertical Rhythm][3].

В файле `style.scss` подключаем сброс стилей Compass и модуль вертикального ритма:

<pre>@import "compass/reset";
@import "compass/typography/vertical_rhythm";
</pre>

Сделаем небольшую стилизацию для блока `.wrapper`, заголовков, параграфов и изображений, чтобы визуально было проще разобраться, что к чему:

<pre>.wrapper{
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
&lt;/code></pre>

### Основные переменные в Vertical Rhythm

В модуле **Vertical Rhythm** библиотеки Compass имеется множество переменных, но среди них есть **только две основные**, которые необходимы для расчетов внутри этого модуля:

<pre>$base-font-size: 22px;    // базовый размер шрифта
$base-line-height: 33px;  // базовое межстрочное расстояние
</pre>

Значение переменной `$base-line-height` (*как правило*) равно выражению `$base-font-size * 1.5`, поэтому `22px * 1.5 = 33px`. Значение переменной `$base-font-size` в 22px взято в качестве примера.

Помимо этого, есть еще **две дополнительные переменные**:

<pre>$rhythm-unit: "rem";         // базовая единица измерения (по умолчанию em)
$rem-with-px-fallback: true; // откат к единицам измерения px в браузерах, которые не понимают единицу rem
</pre>

### Включаем Vertical Rhythm

После ввода четырех вышеперечисленных переменных осталось только инициализировать модуль **Vertical Rhythm** с помощью миксина:

<pre>@include establish-baseline;</pre>

Миксин `establish-baseline` делает простые вещи &#8211; он устанавливает `font-size` и `line-height` для корневого тега `<html>`. Но делает он это с помощью относительных единиц измерения. Допустим, в своем проекте мы установили размер шрифта `22px` и высоту строки `33px`. Если взглянуть на результат компиляции из SCSS в CSS, то увидим следующее:

<pre>html {
  font-size: 137.5%;
  line-height: 1.5em;
}
</pre>

Размер шрифта `16px` является установленным по умолчанию в большинстве браузеров, поэтому `16px = 100%`. Следовательно, `22px = 137.5%`. Относительная величина `line-height` всегда относительна к размеру шрифта `font-size` текущего элемента, поэтому в данном случае она равна 1.5em (`22px * 1.5 = 33px`).

Перезагрузим браузер с открытой страницей создаваемого проекта-примера и увидим, как резко изменилась картина! Вместо слепленных друг с другом строчек появилась более четкая и удобочитаемая структура. Видно, что каждая строка текста располагается внутри своей линии. Чтобы еще более наглядно представить картину структурированного контента, воспользуемся миксином:

<pre>body{
  @include debug-vertical-alignment;
}
</pre>

Обрисовались строки, ну прямо как на школьном тетрадном листке! Хорошо видно, как все строки текста и изображение выстроились четко по линеечкам. Думаю, если читатель дошел до этого места, то ему стала понятна суть и принцип вертикального ритма без каких-либо объяснений!

### Margin и padding в Vertical Rhythm

Но строки, заголовки и изображения все равно тесно прижаты друг к другу. В модуле **Vertical Rhythm** имеются свои собственные инструменты для создания отступов у элементов контента, в основе которых лежит опять таки базовый размер шрифта (вот он &#8211; тот самый ритм!):

<pre>$base-font-size * 1</pre>

Для элемента страницы можно задать `margin-top` или `padding-top`, `margin-bottom` или `padding-bottom`. Реализуется это с помощью специальных миксинов (на выбор, один из четырех):

<pre>p{
  background-color: hsla(0,100%,50%,.1);

  @include margin-trailer;  // margin-bottom
  @include margin-leader;   // margin-top

  @include padding-trailer; // padding-bottom
  @include padding-leader;  // padding-top
}
</pre>

Имеются универсальные миксины, которые являются сокращениями от вышеперечисленных. Таким миксинам передаются необходимые аргументы и на выходе получаем результат:

<pre>p{
  background-color: hsla(0,100%,50%,.1);

  @include trailer($lines: 2, $property: margin); // margin-bottom на 2 строки
  @include trailer($lines: 2, $property: padding); // padding-bottom на 2 строки

  @include leader($lines: 2, $property: margin); // margin-top на 2 строки
  @include leader($lines:3, $property: padding); // padding-top на 3 строки
}
</pre>

Одновременно задать `margin-top + margin-bottom` или `padding-top + padding-bottom` можно с помощью миксинов:

<pre>p{
  background-color: hsla(0,100%,50%,.1);

  @include rhythm-margins; // margin-top + margin-bottom
  @include rhythm-padding; // padding-top + padding-bottom
}
</pre>

Миксин `@include rhythm` является глобальным сокращением вышеназванных миксинов для создания отступов `margin` или `padding`.

### Создание границ в Vertical Rhythm

Отступы можно совмещать с границами `border`. То есть, можно (к примеру) создать верхний `padding` с верхней границей `border`. Толщина границы и ее стиль управляются через переменные `$default-rhythm-border-width` и `$default-rhythm-border-style`. По умолчанию толщина границы равна `1px`, а ее стиль &#8211; `solid`.

<pre>p{
  background-color: hsla(0,100%,50%,.1);

  @include leading-border; // padding-top + border-top
  @include trailing-border; // padding-bottom + border-bottom
  @include horizontal-borders; // padding-top + border-top и padding-bottom + border-bottom
  @include h-borders; // alias для horizontal-borders
}
</pre>

Одновременно задать `padding` и `border` для всех четырех сторон можно через миксин:

<pre>p{
  background-color: hsla(0,100%,50%,.1);
  @include rhythm-borders; // padding + border
}
</pre>

Указать границу и отступ для какой-то одной стороны можно с помощью миксина:

<pre>p{
  background-color: hsla(0,100%,50%,.1);
  @include apply-side-rhythm-border($side: left);
}
</pre>

### Произвольный размер шрифта в Vertical Rhythm

Можно произвольно поменять размер шрифта любого элемента страницы, но делать это также нужно, исходя из ритма &#8211; с помощью соответствующего миксина `adjust-fonts-size-to`. Давайте изменим размер заголовков таким образом, чтобы они отличались от основного текста (и были действительно заголовками):

<pre>h1{
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
</pre>

Или же, допустим, нужно установить для заголовка первого уровня `h1` размер шрифта в `42px`. Микcин будет выглядеть таким образом:

<pre>h1{
  @include adjust-font-size-to(42px);
}
</pre>

Первым делом, этот миксин делает размер шрифта элемента `h1` относительным к размеру шрифта элемента-контейнера. В нашем случае таковым является элемент `html`, поэтому размер шрифта равен `22px`. Соответственно, размер шрифта для `h1` получается (`42 / 22 = 1.90909`):

<pre>font-size: 1.90909rem;</pre>

Вторым делом миксин заново вычисляет высоту строки для нашего заголовка `h1`. Делает он это таким образом:

<pre>1.90909rem * 1.5 = 3rem (округленно)
22 * 3rem = 66px
</pre>

Конечный результат показан ниже:

<pre>h1 {
  font-size: 42px;
  font-size: 1.90909rem;
  line-height: 66px;
  line-height: 3rem;
}
</pre>

Отлично, правда? Вся прелесть в том, что показанные выше расчеты можно с легкостью забыть &#8211; модуль **Vertical Rhythm** каждый раз будет вычислять размер шрифта и высоту строки сам, не &#8220;напрягая&#8221; нас.

Помимо указания размера шрифта в качестве аргумента, миксину `adjust-fonts-size-to` можно также передать количество линий, которое должен занимать заголовок. Например, так:

<pre>h3{
  @include adjust-font-size-to(1.44rem,1);
}
</pre>

Если вы попробуете у себя, то сразу увидите результат.

### Выравнивание изображений в Vertical Rhythm

Внимательный читатель должен заметить одну неточность, если он у себя повторил все шаги, описанные выше. Неточность заключается в том, что изображение не вписывается в вертикальный ритм, созданный нами на странице:<figure id="attachment_1131" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/shift_in_vertical_rhythm-600x366.jpg" alt="Смещение в вертикальном ритме" width="600" height="366" class="size-medium wp-image-1131" />][4]<figcaption class="wp-caption-text">Смещение в вертикальном ритме</figcaption></figure> 

А именно &#8211; первое изображение своим верхним краем совпадает с линией ритма. А вот нижняя граница не попадает на линию. Из-за этого весь дальнейший контент также смещается и вертикальный ритм нарушается.

Происходит это потому, что изображение мы сделали блочным элементом и присвоили ему фиксированные размеры в пикселях в HTML-коде:

<pre><img src="http://placehold.it/700x350" />
...
<img src="http://placehold.it/500x250" />
...
</pre>

Исправить ситуацию можно с помощью плагина **Keep The Rhythm** под jQuery &#8211; [Keep The Rhythm][5]. Вдаваться в подробности работы этого плагина я не буду, а сразу покажу, как он подключается и результат его работы.

Получаем с GitHub библиотеку jQuery и сам плагин к ней:

<pre>jquery-1.9.1.min.js
jquery.keeptherhythm.js
</pre>

Подключаем к HTML-странице в ее конце:

<pre></pre>

И затем создаем небольшой скрипт (адаптированный пример взят с официального сайта):

<pre></pre>

Смотрим результат:<figure id="attachment_1132" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/keep_the_rhythm-600x392.jpg" alt="Плагин Keep_The_Rhythm в действии" width="600" height="392" class="size-medium wp-image-1132" />][6]<figcaption class="wp-caption-text">Плагин Keep\_The\_Rhythm в действии</figcaption></figure> 

Все получилось! Однако, стоит заметить, что приведенный выше пример является упрощенным. Достаточно изменить масштаб страницы в окне браузера, и вертикальный ритм поломается. Поэтому плагин **Keep The Rhythm** необходимо применять в связке с медиа-запросами для правильной его работы. По крайней мере, если возникнет вопрос по работе этого плагина, то документация на официальной странице всегда под рукой.

### Заключение

Основой для написания этой статьи послужили два материала (видео и статья):

  * [Compass (Sass) — вертикальный ритм (vertical rhythm)][7]
  * [Vertical Rhythm with Compass][8]

Оцените статью:  
<span id="post-ratings-1127" class="post-ratings" data-nonce="c0fba93a07"><img id="rating_1127_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1127, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1127_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1127, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1127_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1127, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1127_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1127, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1127_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1127, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1127_text"></span></span><span id="post-ratings-1127-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/04/copybook.jpg
 [2]: http://localhost:7788/third/?p=1065 "Медиа-запросы Breakpoint в Sass"
 [3]: http://beta.compass-style.org/reference/compass/typography/vertical_rhythm/ "Vertical Rhythm"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/04/shift_in_vertical_rhythm.jpg
 [5]: http://www.gayadesign.com/diy/keep-the-rhythm-vertical-rhythm-on-objects-having-dynamic-heights/ "Keep The Rhythm"
 [6]: http://localhost:7788/third/wp-content/uploads/2014/04/keep_the_rhythm.jpg
 [7]: https://www.youtube.com/watch?v=Leert-TnSSg "Compass (Sass) — вертикальный ритм (vertical rhythm)"
 [8]: http://atendesigngroup.com/blog/vertical-rhythm-compass "Vertical Rhythm with Compass"