---
title: 'Stylus &#8211; знакомство с препроцессором'
author: gearmobile
layout: post
---
> Настало время познакомиться с препроцессором Stylus. Ниже привожу перевод статьи от David Walsh, посвященную малоизвестному, но крайне полезному препроцессору Stylus. Оригинал статьи размещен здесь &#8211; [Getting Started with Stylus][2]

<img class="aligncenter size-full wp-image-2127" src="http://localhost:7788/third/wp-content/uploads/2014/12/stylus-logo.png" alt="stylus" width="220" height="209" />

В среде web-разработчиков можно часто и постоянно слышать только о двух препроцессорах: [Sass][3] и [LESS][4]. Однако, существует еще один препроцессор, о котором слышно совсем не так часто &#8211; это [Stylus][5]. При редизайне Mozilla Developer Network мною был выбран Stylus по нескольким причинам:

  * так как Stylus основан на [Node.js][6], то отпадает необходимость в использовании сторонней технологии (Sass требует для своей работы Ruby)
  * Stylus предоставляет набор [JavaScript API][7], что делает возможным дальнейшую настройку этого инструмента
  * синтаксис Stylus не нуждается в скобках (brackets), запятых (comma), двоеточиях (colons), точках с запятыми (semicolon) &#8211; он целиком и полностью основан на использовании табуляции и пробелов; но если необходимо использовать любой из видов пунктуаций, то его можно легко применить в Stylus &#8211; компиляция произойдет корректно
  * под препроцессор Stylus имеется готовая библиотека миксинов (mixin) под названием [Nib][8]

### Установка Stylus

Препроцессор Stylus является Open Source проектом, расположенным на GitHub, поэтому его можно легко установить как из исходных файлов, так и с помощью менеджера пакетов `npm`:

{% highlight powershell %}
  $ sudo npm install stylus -g
{% endhighlight %}

CSS-файлы, созданные при помощи синтаксиса Stylus, должны иметь расширение `.styl` и могут располагаться в любом месте проекта. Препроцессор Stylus не имеет какого-либо конфигурационного файла, для начала компиляции достаточно запустить утилиту командной строки `stylus` с минимальным набором ключей:

{% highlight powershell %}
$ stylus app/main.styl --out /dist --compress
{% endhighlight %}

Представленная выше команда выполняет компиляцию исходного stylus-файла `main.styl` в директорию `/dist` с тем же самым именем `main.styl`. Другими словами, файл `main.styl` компилируется в файл `main.css` и помещается в директорию `/dist`.

Утилита `stylus` может запускаться не только для однократной компиляции, но и отслеживать изменения файлов, выполняя компиляцию на лету; для этого имеется ключ `--watch`:

{% highlight powershell %}
$ stylus --watch app/main.styl
{% endhighlight %}

Как можно догадаться, у программы `stylus` имеется гораздо больше опций, с полным списком которых можно ознакомиться здесь &#8211; [Executable][9]. В частности, с помощью нужных ключей можно выполнять обратную конвертацию из CSS в Stylus, сравнивать ввод\вывод и многое дугое.

> Но приступим к рассмотрению самого главного, ради чего и затевался данный перевод &#8211; синтаксису и возможностям препроцессора Stylus

### Основы синтаксиса Stylus

Синтаксис Stylus очень похож на синтаксис остальных препроцессоров (Sass или LESS). Но давайте более детально рассмотрим, что он из себя представляет на деле:

{% highlight css %}
/*  Простая переменная  */
  base-font-size = 12px

/* Инициализация переменной с помощью вызова миксина */
body-background = invert(#ccc)

/* Селектор и набор правил для него */
body
  color #333
  background #fff

/* Вложенность правил */
nav
  margin 10px
    ul
      list-style-type none
        > li
          display inline-block
          &#038;.current
            background-color lightblue

/* Использование вычисляемых значений */
div.column
  margin-right (grid-spacing / 2)
  margin-top (grid-spacing * 2)

/* Использование ранее установленного значения */
div.center-column
  width 200px
  margin-left -(@width / 2)

/* Задание значений, полученных как результат вычислений миксинов */
.promo
  apply-promo-style()
  apply-width-center(400px)

/* Итерация в цикле */
table
  for row in 1 2 3 4 5
    tr:nth-child({row})
      height 10px * row

/* Другой вариант итерации в цикле */
for row in (1..5)
  tr:nth-child({row})
    height 10px * row

/* Импортирование в Stylus-файл другой таблицы стилей в формате Stylus */
@import "links.styl"

/* extend существующего класса */
.warning
  @extend .block
{% endhighlight %}

В принципе, ничего нового в вышесказанном нет &#8211; все эти моменты также существуют в других препроцессорах. Если вдруг в синтаксисе не достает скобок, двоеточий или запятых, то их можно смело добавлять в код &#8211; препроцессор Stylus вас прекрасно поймет и в этом случае.

### Создание и использование миксинов

Миксины чрезвычайно полезны по нескольким причинам. Благодаря им при написании стилей на CSS можно использовать логику, а также структурировать код.

Создание миксинов в Stylus является простой задачей, а синтаксис миксинов именно такой, какой и ожидалось увидеть:

{% highlight css %}
/* Простой миксин для добавления вендорных префиксов.

  Использование:
  vendorize(box-sizing, border-box)

*/

vendorize(property, value)
  -webkit-{property} value
  -moz-{property} value
  -ms-{property} value
  {property} value
{% endhighlight %}

При создании миксинов под Stylus можно задать значения по умолчанию для аргументов:

{% highlight css %}
/* Миксин создания треугольника на CSS */

generate-arrow(arrow-width = 10px)
  &#038;:before, &#038;:after
    content ''
    height 0
    width 0
    position absolute
    border arrow-width solid transparent
{% endhighlight %}

Миксин может возвращать вычисляемое значение с помощью ключевого слова `return` или же возвращать стили, определенные внутри самого миксина. Такие стили можно применить к элементу, который вызывает этот миксин:

{% highlight css %}
/* Миксин для задания стилей к текущему элементу и дочерним элементам текущего элемента */

special-homestyles(background = '#ccc')
  background-color background
    a
      color lightblue
    &#038;.visited
      color navy
{% endhighlight %}

И конечно же, внутри миксинов можно использовать условия (впрочем, как и в любом другом месте кода на Stylus):

{% highlight css %}
/* Миксин создания grid на основе минимального\максимального значений и инкремента */

generate-grid(increment,start,end,return-dimension=false)
  total = start
for n, x in 0..((end - start) / increment)
  if return-dimension
    if x+1 is return-dimension
      return total
        else
	  .column-{x+1}
	     width total
	total = total + increment
{% endhighlight %}

Представленный выше миксин генерирует grid на основе минимального значения (минимальной ширины столбца), максимального значения (максимальной ширины столбца) и количества столбцов (которое изменяется с помощью инкремента). Последний аргумент return-dimension служит для указания того, будет ли миксин просто возвращать полученное значение, не создавая CSS-классов.

### Полезные миксины Stylus

При работе над проектом MDN мне потребовалось большое количество полезных миксинов под Stylus, например таких, как поддержка RTL, поддержка локализации, а также поддержка большого числа браузеров. Ниже я представлю некоторые из этих миксинов &#8211; возможно, они пригодятся на практике некоторым из читателей.

#### Обнуление last child

Данный миксин был создан для обнуления пустого пространства у последнего элемента блока-родителя. Как правило, такими пространствами в CSS являются `padding-bottom` и `margin-bottom`.

{% highlight css %}
/* Удаление пустого пространства у элемента, если он является последним у своего родителя */

prevent-last-child-spacing(element="*", property="padding-bottom")
  if element is "*"
    element = unquote(element)
      &#038; > {element}:last-child
        {property} 0
{% endhighlight %}

С помощью этого миксина устанавливается `margin` или `padding` для блока-родителя. А затем просто убирается пустое пространство у последнего элемента этого блока.

#### Стилизация placeholder

Стилизация placeholder является достаточно хитрой задачей из-за необходимости использования вендорных префиксов, поэтому использование миксина значительно упрощает эту задачу:

{% highlight css %}
  set-placeholder-style(prop, value)
   &#038;::-webkit-input-placeholder
     {prop} value
   &#038;::-moz-input-placeholder
     {prop} value
{% endhighlight %}

### Заключение

На этом перевод закончен.

От себя могу добавить.

  1. Под Sublime Text 3 имеется плагин [Stylus][10] для подсветки синтаксиса и автоматической табуляции. Если планируется дальнейшая работа в Stylus, то данный плагин обязателен к установке &#8211; без него просто тяжело и долго кодить.<figure id="attachment_2137" style="width: 600px;" class="wp-caption aligncenter">
[<img class="wp-image-2137 size-medium" src="http://localhost:7788/third/wp-content/uploads/2014/12/sublime_stylus-600x314.png" alt="stylus-sublime-text-3" width="600" height="314" />][11]<figcaption class="wp-caption-text">Плагин Stylus в Sublime Text 3</figcaption></figure>

  2. Плагин Emmet имеет поддержку синтаксиса Stylus (*меня Emmet не перестает радовать*). Все [горячие клавиши Emmet][12] остались неизменными и под Stylus, как если бы я кодил в старом добром CSS
  3. На моем любимом YouTube-канале Level Up Tuts недавно вышла небольшая серия видео-обзоров по Stylus &#8211; [Stylus Tutorials][13]

 [1]: #note-2122-1 "David Walsh &#8211; web-разработчик и евангелист Mozilla"
 [2]: http://blog.teamtreehouse.com/getting-started-stylus "Getting Started with Stylus"
 [3]: http://sass-lang.com/ "Sass"
 [4]: http://lesscss.org/ "LESS"
 [5]: http://learnboost.github.io/stylus/ "Stylus"
 [6]: http://nodejs.org/ "Node.js"
 [7]: https://github.com/LearnBoost/stylus/blob/master/docs/js.md "JavaScript API"
 [8]: https://github.com/visionmedia/nib "Nib"
 [9]: https://github.com/LearnBoost/stylus/blob/master/docs/executable.md "Executable"
 [10]: https://sublime.wbond.net/packages/Stylus "Stylus"
 [11]: http://localhost:7788/third/wp-content/uploads/2014/12/sublime_stylus.png
 [12]: http://docs.emmet.io/cheat-sheet/ "Emmet CheatSheet"
 [13]: http://youtu.be/eJahtnmywMI "Stylus Tutorials"
