---
title: 'Jeet.gs &#8211; первое знакомство'
author: gearmobile
excerpt: Первое знакомство с системой разметки jeet.gs. Установка под Stylus, рассмотрение основных функций системы. Создание файла настроек и задание переменных.
layout: post
permalink: /jeet-gs-first-introduction/
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Кодинг
tags:
  - grid system
  - jeet.gs
  - stylus
---
### Вступление

> Доброго времени суток всем! Сегодня приступим к знакомству с системой построения сеток jeet.gs. 

Читатели могут спросить &#8211; отлично, но чем плоха [Susy][1]? Ответ прост &#8211; Susy работает на Ruby, она просто несовместима со Stylus.

Так как с недавнего времени я перешел с Sass(SCSS) на [Stylus][2] и *совсем не жалею об этом*, то сразу принялся искать замену Susy. Надо сказать, я быстро ее нашел и этой заменой оказалась [jeet.gs][3]. &#8220;Grid system для людей&#8221; &#8211; как ее &#8220;обозвали&#8221; в прекрасном task runner [CodeKit][4]. Кстати, сам факт присутствия jeet.gs в CodeKit говорит за себя.

Система jeet.gs *изначально адаптивная*, она проста в использовании и изучении. Если честно, Susy я так до конца и не освоил (*только необходимые основы*), так как она достаточно сложна в изучении, несмотря на прекрасную документацию. Еще можно сказать, что jeet.gs очень молода &#8211; ей всего 9 месяцев и поэтому я с вами, уважаемый читатель, иду в ногу со временем, я на cutting edge <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" /> !

Существование и использование jeet.gs имеет мало смысла без системы контрольных точек (breakpoint). В Susy в этом качестве служит хороший инструмент [Breakpoint][5]. Под jeet.gs конечно же существует аналог под названием [Rupture][6]. Эта система также проста и наглядна, как и jeet.gs.

Стоит также оговориться, что под Stylus имеются не менее прекрасные проекты [Typographic][7] и [Axis][8], с которыми я планирую познакомиться в свое время.

### Jeet.gs &#8211; grid system под Stylus

Итак, фанфары прозвучали в честь обоих героев сегодняшнего дня. Пора приступать к более детальному знакоству с ними. И начнем с главного героя &#8211; системы сеток (grid system) jeet.gs.

#### Установка Jeet.gs под Stylus

Любое знакомство начинается с установки пакета. На официальной странице [jeet.gs][3] прекрасно оформлено описание инсталляции &#8211; она проста. Кстати, стоит оговориться, что jeet.gs можно установить и под Sass(SCSS). Но я этого делать не буду &#8211; мне это не интересно и не нужно.

Предполагается, что у читателя рабочей операционной системой является MacOSX или Linux OS (*все команды в этой статье будут показаны применительно к этим двум родственным системам*). Также предполагается, что в любой из этих систем уже установлены Node.js и Stylus (*иначе вы немного забежали вперед, уважаемый читатель*).

*Установка* jeet.gs выполняется одной строкой:

<pre>// Command Line

sudo npm install jeet --global
</pre>

Далее библиотека jeet.gs *импортируется* в файл проекта `*.styl` с помощью директивы `@import`:

<pre>// Stylus

@import 'jeet'
</pre>

После этого можно *запустить мониторинг и компиляцию* командой:

<pre>// Command Line

sudo stylus -u jeet -w style.styl
</pre>

где `-u` &#8211; это сокращение от `--using`, `-w` &#8211; от `--watch`. То есть, мониторить (watch) все изменения файла style.styl и при этом учитывать (using) возможности подключенной библиотеки jeet.gs.

Пакет jeet.gs можно заставить работать несколько иначе &#8211; *крутиться под Gulp*. Для этого достаточно правильно оформить файл `gulpfile.js`:

<pre>// Javascript

  var gulp = require('gulp'),
  ...
  nib = require('nib'),
  jeet = require('jeet'),
  rupture = require('rupture');


  // STYLUS WITH NIB AND JEET AND RUPTURE
  gulp.task('stylus', function(){
    gulp.src('app/styles/style.styl')
      .pipe(plumber())
      .pipe(stylus({use:[nib(),jeet(),rupture()]}))
      .pipe(gulp.dest('dist/'));
  });
</pre>

#### Возможности Jeet.gs

С документацией по jeet.gs можно ознакомиться на оф. сайте в разделе Jeet&#8217;s API или же на страничке GitHub &#8211; [jeet/stylus][9].

##### Функция column()

*Синтаксис*:

<pre>column(ratios = 1, offset = 0, cycle = 0, uncycle = 0, gutter = jeet.gutter)</pre>

Основой любой современной grid system являются колонки\столбцы &#8211; column. Так как jeet.gs изначально является *адаптивной системой*, то задать ширину column можно как *дробную часть* от ширины блока-контейнера &#8211; 1/3, 1/6, 1/10, 1/100 и так далее. Не обязательно можно задавать в виде дроби, можно в *десятичном* виде &#8211; .3, .25, .15.

Пример задания ширины для двух блоков `.sidebar` и `.main`. В обоих случаях используется функция `column()`, у которой есть более используемое сокращение &#8211; `col()`:

<pre>// Stylus

.sidebar
  col(1/4)
.main
  col(3/4)
</pre>

Функция `column()` может принимать целый ряд аргументов, с помощью которых возможна тонкая настройка блоков в разметке.

Смещение колонок\столбцов выполняется с помощью аргумента `offset`, который может принимать как положительное, так и отрицательное значение. Положительное значение offset задает у столбца `margin-left` &#8211; и столбец смещается влево. Отрицательное значение задает `margin-right` &#8211; и блок смещается вправо.

<pre>// Stylus

.block
  column(1/3, offset: 1/4)
</pre>

Аргумент `cycle` позволяет создавать *галлереи*. Допустим, необходимо создать галлерею из картинок, в которой должно быть 4 (четыре) картинки в ряду. Тогда для функции `column()` задаем параметр `cycle: 4` :

<pre>// Stylus

.block
  column(1/3, cycle: 4)
</pre>

Аргумент `uncycle` позволяет создавать мобильные версии галерей. Допустим, desktop-версия галлереи &#8211; `column(1/3, cycle: 4)`. Чтобы создать мобильную версию этой галлереи, в которой картинки будут располагаться по две в ряд, достаточно прописать так:

<pre>// Stylus

.block
  column(1/3, uncycle: 4, cycle: 2)
</pre>

Аргумент `gutter` позволяет управлять шириной gutter между столбцами в каждом конкретном случае. Допустим, таким образом:

<pre>// Stylus

.block
  column(1/3, uncycle: 4, cycle: 2, gutter: .5)
</pre>

##### Функция span()

*Синтаксис*:

<pre>span(ratio = 1, offset = 0)</pre>

Эта функция является своего рода облегченным вариантом функции `column()`. Функция `span()` не &#8220;понимает&#8221; такого свойства, как отступы `gutter` у блоков. По одной простой причине &#8211; функция `span()` создает разметку из блоков, плотно прилегающих друг к другу, без `margin`.

Такая разметка крайне полезна при создании горизонтальной навигации. Например, создать навигацию из восьми пунктов:

<pre>// Stylus

  .nav
    cf()
    a
      span(1/8)
</pre>

##### Функция shift()

*Синтаксис*:

<pre>shift(ratios = 0, col_or_span = column, gutter = jeet.gutter)</pre>

Эта функция служит для изменения порядка расположения элементов в нормальном потоке, с помощью свойства `position: relative`. Величина смещения задается аргументом `ratios` и применяется подобное смещение в виде свойства `left` к блоку. При этом функции `shift()` с помощью задания или не задания аргумента `gutter` можно указать, является ли данный блок столбцом (через функцию `column()`) или блоком span (через функцию `span()`).

Функция `shift()` точно также, как и аргумент `offset`, может принимать отрицательные значения для изменения направления смещения блока. Также, функция `shift()` может принимать не только целые, но и дробные значения для точного позиционирования.

##### Функция unshift()

*Синтаксис &#8211; отсутствует*

Эта функция не принимает каких-либо аргументов. Ее задача &#8211; отменить действие функции `shift()`.

##### Функция edit()

*Синтаксис &#8211; отсутствует*

Данная функция не создает разметку напрямую. Ее задача &#8211; помочь в создании разметки. С ее помощью каждый элемент на странице *окрашивается в определенный оттенок серого цвета*. Это помогает визульно контролировать правильность процесса создания разметки.

Чтобы функция заработала, достаточно включить ее в файле проекта в любом месте:

<pre>// Stylus

edit()
</pre>

Вид разметки будет примерно таким:<figure id="attachment_2192" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2015/01/jeet_edit-600x380.png" alt="jeet.gs edit" width="600" height="380" class="size-medium wp-image-2192" />][10]<figcaption class="wp-caption-text">Функция edit() в jeet.gs</figcaption></figure> 

##### Функция center()

*Синтаксис*:

<pre>center(max-width = 1410px, pad = 0)</pre>

Задача функции `center()` &#8211; быстро и грамотно выполнять центрирование блока в разметке. Как видно из синтаксиса, функция принимает два аргумента:

  * максимальную ширину `max-width`, равную по умолчанию `1410px`;
  * `padding-left` и `padding-right` для блока, задаваемые в виде шортката `pad` и равного нулю по умолчанию; то есть, нельзя управлять `padding-left` и `padding-right` по отдельности &#8211; только одно значение сразу для двух свойств.

##### Функция cf()

*Синтаксис &#8211; отсутствует*

Данная функция &#8211; это всего лишь clearfix от Nicholas Gallagher. Думаю, дальнейшее объяснение излишне. Принимать &#8211; маленькими дозами для любых блоков с `column()` или `span()` <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

##### Функция align()

Функция для выравнивания блока внутри блока-контейнера с помощью `position: absolute`. Вертикальное выравнивание в браузерах IE9+ теперь простая вещь.

##### Функция stack()

*Синтаксис*:

<pre>stack(pad = 0, align = false)</pre>

Данная функция предназначена для расположения блоков стопкой (stack), друг над другом. Такой вид расположения блоков применим для модильной версии страницы. Функция `stack()` принимает два вида аргументов:

  * `pad` &#8211; отступы `padding-left` и `padding-right` для блока;
  * `align` &#8211; выпавнивание текста внутри блока.

##### Функция unstack()

*Синтаксис &#8211; отсутствует*

Данная функция отменяет действие функции `stack()`. Однако, действие этой функции не возвращает разметку к прежнему виду, с применением функции `column()`. Чтобы вернуть разметку к такому результату, необходимо снова использовать функцию `column()`.

#### Настройки Jeet.gs

Настройки системы jeet.gs очень просты. Первоначально необходимо создать файл `_settings.styl`, который нужно подключить в файл стилей директивой `@import '_settings'`. При этом необходимо, чтобы строка `@import '_settings'` размещалась сразу после строки `@import 'jeet'`.

Содержимое файла настроек `_settings.styl` &#8211; это несколько переменных:

  * **jeet[&#8216;gutter&#8217;] = 3** &#8211; размер ширины gutter в процентах, от общей ширины страницы
  * **jeet[&#8216;parent-first&#8217;] = false** &#8211; если сказать коротко, каким образом будет производиться вычисление ширины блока; относительно конкретного блока-родителя; или же относительно корневого блока-родителя
  * **jeet[&#8216;layout-direction&#8217;] = LTR** &#8211; направление текста внутри разметки

### Заключение по Jeet.gs

Итак, познакомились с системой создания разметки jeet.gs. На удивление, она оказалась проста и достаточно полчаса, чтобы разобраться в ней. Не сравнить с Susy, конечно.

Но этого мало, естественно. Хотелось бы посмотреть на живые примеры сайтов, созданных с помощью jeet.gs. В этом вопросе может помочь сам официальный сайт [Jeet.gs][11] &#8211; милости просим <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

Создано по материалам:

  * [Jeet for Stylus][12]
  * [A grid system for humans][13]
  * [Fondations responsive avec Stylus, Jeet et Rupture][14]

#### P.S.

В данной статье возможны (и 100% &#8211; что есть) неточности и мелкие ошибки. Это и понятно &#8211; это мое первое знакомство с Jeet.gs. Поэтому, если будут замечания &#8211; милости просим.

Оцените статью:  
<span id="post-ratings-2189" class="post-ratings" data-nonce="cc82ba50b9"><img id="rating_2189_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2189, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2189_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2189, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2189_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2189, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2189_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2189, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2189_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2189, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2189_text"></span></span><span id="post-ratings-2189-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://susy.oddbird.net/ "Susy"
 [2]: http://learnboost.github.io/stylus/ "Stylus"
 [3]: http://jeet.gs/ "jeet.gs"
 [4]: http://incident57.com/codekit/ "CodeKit"
 [5]: http://breakpoint-sass.com/ "Breakpoint"
 [6]: https://github.com/jenius/rupture "Rupture"
 [7]: https://github.com/corysimmons/typographic "Typographic"
 [8]: https://github.com/jenius/axis "Axis"
 [9]: https://github.com/mojotech/jeet/tree/master/stylus "jeet/stylus"
 [10]: http://localhost:7788/third/wp-content/uploads/2015/01/jeet_edit.png
 [11]: http://jeet.gs/ "Jeet.gs"
 [12]: https://github.com/mojotech/jeet/tree/master/stylus "Jeet for Stylus"
 [13]: http://jeet.gs/ "A grid system for humans"
 [14]: https://wooster.checkmy.ws/2014/04/responsive-grid-typographie/ "Fondations responsive avec Stylus, Jeet et Rupture"