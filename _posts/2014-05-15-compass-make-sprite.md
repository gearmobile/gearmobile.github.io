---
title: "Создание спрайтов в Compass"
layout: post
categories: css
tags: [compass, sprite]
share: true
---

> Как часто верстальщику в своей работе требуется создавать спрайты?

Мне кажется, что почти в каждом проекте стоит такая задача. Ведь сегодня на каждом из сайтов имеется либо панель навигации с иконками, либо ссылки на социальные сети также с иконками.

Что такое CSS-спрайты, не буду вдаваться в подробности. В чем их преимущество и в чем профит их использования. А также, каким образом они создаются и используются. Мне кажется, читатель, которого заинтересовала тема создания спрайтов на Compass, и без того знает, что это такое.

В данной статье будет рассматриваться вопрос, каким образом можно автоматизировать и ускорить процесс создания спрайтов. Не знаю, как кто другой, но я использовал ручной метод создания спрайтов, с помощью Photoshop.

Также стоит сказать, что данная статья не претендует на полноту и точность. Материал дался автору с удивительным трудом, буквально по крупицам (хотя в Сети есть много хороших материалов по этой теме на английском языке).

## Создание нового проекта в Compass

Создаем чистый Compass-проект с нуля, как обычно:

{% highlight powershell %}
compass create sprites
{% endhighlight %}

... и настраиваем конфигурационный файл `config.rb` этого проекта, приведя к следующему виду:

{% highlight ruby %}
http_path = "/"
  css_dir = "css"
  sass_dir = "sass"
  images_dir = "img"
  javascripts_dir = "js"

  output_style = :expanded
  relative_assets = true
  line_comments = false
{% endhighlight %}

Особенно стоит обратить внимание на предпоследнюю строку:

{% highlight powershell %}
relative_assets = true
{% endhighlight %}

... с помощью которой устанавливаются относительные пути к файлам изображений в проекте. Если не активировать данную строку, то спрайт не сможет подключиться к элементам в документе.

## Подключение плагина спрайтов

Делается это как обычно в библиотеке Compass, одной строкой импортирования:

{% highlight css %}
@import "compass/utilities/sprites";
{% endhighlight %}

Далее, как правило, следует долгий и нудный процесс вырезания изображений из psd-макета. В данном примере этот процесс будет заменен на более быстрый и красивый. Мы воспользуемся готовым бесплатным набором иконок, который скачаем из бескрайних просторов Интернета.

Затем создадим в каталоге `img` подкаталог `webicons` (`img/webicons`) и распакуем в него скачанный архив.

Также стоит отметить, что плагин для работы со спрайтами в библиотеке Compass может работать только с изображениями формата `.png`. Поэтому перед созданием спрайтов необходимо создать отдельный каталог, в котором будут размещены все изображения, из которых будут создаваться спрайт.

## Скачивание библиотеки с иконками

Набор темных иконок в формате `.png` подойдет любой, главное, чтобы он был бесплатным. Например, такой - [WPZOOM Developer Icon Set][1].

Далее создаем отдельную директорию, в которой будет размещен полученный набор иконок:

{% highlight powershell %}
img/webicons
{% endhighlight %}

## Подключение набора иконок в проект

Подключение набора изображений (иконок в нашем случае) в проект производится директивой:

{% highlight css %}
@import "webicons/*.png";
{% endhighlight %}

Точнее, этой директивой создается карта изображений `map`.

## Создание спрайта

Спрайт создается в библиотеке Compass c помощью миксина `@include all-[folder-name]-sprites;`, где [folder-name] - имя каталога с изображениями. В нашем случае данный миксин будет выглядеть таким образом:

{% highlight css %}
@include all-webicons-sprites;
{% endhighlight %}

Если теперь взглянуть на директорию с проектом в файловом менеджере, то увидим, что в каталоге добавился новый файл-картинка в формате `.png`:

![Созданный в Compass спрайт]({{site.url}}/images/uploads/2014/05/img_001.png)

В файле `style.css` сгенерируется код, в котором появятся имена классов для каждого из изображений. Также для каждого из изображений будет добавлено позиционирование (точнее - оно будет вычислено). Также стоит обратить внимание на CSS-свойство `background`.

Значение его имеет правильный относительный путь - `../img/...`, это сработала переменная `relative_assets = true` в конфигурационном файле `config.rb`.

{% highlight css %}
...
.webicons-sprite, .webicons-agenda, .webicons-arrow-down, .webicons-arrow-left-down, .webicons-arrow-left-up, .webicons-arrow-left, .webicons-arrow-right-down, .webicons-arrow-right-up, .webicons-arrow-right, .webicons-arrow-up {
  background: url('../img/webicons-sf124b45856.png') no-repeat;
}

.webicons-agenda {
  background-position: 0 -172px;
}

.webicons-arrow-down {
  background-position: 0 -266px;
}

.webicons-arrow-left-down {
  background-position: 0 -43px;
}

.webicons-arrow-left-up {
  background-position: 0 0;
}
...
{% endhighlight %}

## Создание списка

В HTML-документе создаем обычный маркированный список:

{% highlight html %}
<div class="wrap">
  <ul>
    <li>
      <a href="#">Link 1</a>
    </li>
    <li>
      <a href="#">Link 2</a>
    </li>
    <li>
      <a href="#">Link 3</a>
    </li>
    <li>
      <a href="#">Link 4</a>
    </li>
    <li>
      <a href="#">Link 5</a>
    </li>
  </ul>
</div>
{% endhighlight %}

... и выполняем его легкое форматирование на SCSS:

{% highlight css %}
.wrap{
  max-width: 960px;
  margin: 0 auto;
  ul{
    @include horizontal-list($padding);
    li{
      a{
        padding-left: $base-line-height;
        display: block;
      }
    }
  }
}
{% endhighlight %}

Преобразуем маркированный список с помощью магии Compass в горизонтальный список, воспользовавшись миксином `horizontal-list($padding, $direction)`. Аргумент `$direction` опустим за ненадобностью, а в качестве аргумента `$padding` передадим отступ, равный переменной:

{% highlight css %}
  ...
$base-line-height: 33px;
$padding: $base-line-height;
  ...
{% endhighlight %}

## Добавление иконок в список

Можно воспользоваться готовыми именами классов, созданными библиотекой Compass. То есть, открыть (в нашем случае) файл `style.css`, взять оттуда нужные имена классов (`.webicons-agenda`, `.webicons-arrow-down`, `.webicons-arrow-left-down`, `.webicons-arrow-left-up`, ...) и добавить их в HTML-разметку.

Но такой способ будет не совсем правильным, так как HTML-разметка будет "загрязнена" избыточными именами классов. Когда как можно легко избежать этого недостатка, применив директиву `@extend`:

{% highlight css %}
&:nth-of-type(1) a{
  @extend .webicons-arrow-left-up;
}
&:nth-of-type(2) a{
  @extend .webicons-arrow-right-down;
}
&:nth-of-type(3) a{
  @extend .webicons-arrow-left-down;
}
&:nth-of-type(4) a{
  @extend .webicons-arrow-down;
}
&:nth-of-type(5) a{
  @extend .webicons-agenda;
}
{% endhighlight %}

Оцените чистоту этого способа - HTML-разметка не тронута, а в HTML-документе все работает так, как и было задумано.

## Управлением расположения иконок на спрайте

Иногда при создании спрайта может появиться задача расположить изображения внутри создаваемого спрайта определенным образом - по-горизонтали, по-вертикали или каким-то еще образом. Библиотека Compass может помощь в этом случае и легко решить поставленную задачу.

Переменная `[folder-name]-layout: vertical | horizontal | diagonal | smart` управляет расположением иконок в создаваемом библиотекой Compass спрайте.

Имя переменной состоит из двух значений, первое из которых - это имя каталога, в котором расположены изображения. Таким образом, в случае данного примера переменная будет иметь вид:

{% highlight css %}
  $webicons-layout: vertical;
{% endhighlight %}

По умолчанию в переменной `[folder-name]-layout` используется значение `vertical`:

![Вертикальное расположение иконок]({{site.url}}/images/uploads/2014/05/compass_sprites_vertical_layout.png)

... которое можно поменять на **три других**:

  * `горизонтальное` - `horizontal`:

![Горизонтальное расположение иконок]({{site.url}}/images/uploads/2014/05/compass_sprites_horizontal_layout.png)

  * `диагональное` - `diagonal`:

![Диагональное расположение иконок]({{site.url}}/images/uploads/2014/05/compass_sprites_diagonal_layout.png)

  * стоит особо отметить "умное" расположение - `smart`, которое умеет экономить место на спрайте (сравните в почти точно таким же расположением изображений при вертикальном `layout` и почувствуйте разницу!):

![Умное расположение иконок]({{site.url}}/images/uploads/2014/05/compass_sprites_smart_layout.png)

Добавлять переменную `[folder-name]-layout` нужно перед объявлением каталога с иконками:

{% highlight css %}
  ...
$webicons-layout: 'smart';
  ...
@import "webicons/*.png";
{% endhighlight %}

## Управление расстоянием между изображениями на спрайте

На создаваемом спрайте все изображения расположены таким образом, чтобы быть максимально тесно прижатыми друг к другу. Таким образом убирается лишнее пустое пространство и уменьшается общий размер спрайта в целом.

Но может потребоваться задача увеличить расстояние между изображениями на спрайте. С помощью библиотеки Compass это можно выполнить при помощи переменной `[folder-name]-spacing`.

В имени этой переменной `folder-name` - это имя каталога с расположенными в нем изображениями. В нашем случае имя каталога `webicons`, поэтому имя переменной будет - `$webicons-spacing`.

Для примера зададим расстояние в 10px между изображениями на спрайте:

{% highlight css %}
$webicons-spacing: 10px;
  ...
@import "webicons/*.png";
{% endhighlight %}

В результате между изображениями появиться промежуток, равный 10px:

![Увеличенное расстояние между изображениями на спрайте]({{site.url}}/images/uploads/2014/05/compass_sprites_spacing.png)

## Управление именами создаваемых классов в спрайте

Можно изменить тот способ, каким библиотека Compass создает имена классов в спрайте.

Первоначальный (по умолчанию) вид имен классов имеет представление:

{% highlight css %}
...
.webicons-arrow-down {
  background-position: 0 -326px;
}

.webicons-arrow-left-down {
  background-position: 0 -53px;
}

.webicons-arrow-left-up {
  background-position: 0 0;
}
...
{% endhighlight %}

Можно отделить имя директории с расположенными в нем изображениями от имени каждого из изображений, по отдельности. Чтобы было более понятно, сразу выполним такое преобразование:

{% highlight css %}
.webicons{
  .arrow-left-up {@include webicons-sprite(arrow-left-up);}
  .arrow-right-down {@include webicons-sprite(arrow-right-down);}
}
{% endhighlight %}

... и посмотрим на конечный результат:

{% highlight css %}
.webicons .arrow-left-up {
  background-position: 0 0;
}

.webicons .arrow-right-down {
  background-position: 0 -106px;
}
{% endhighlight %}

Видно, что вместо одного длинного имени появилось два класса. Преимуществом такого способа мне кажется отсутствие необходимости "городить" длинные имена, как в примере с подключением:

{% highlight css %}
...

&:nth-of-type(1) a{
  @extend .webicons-arrow-left-up;
}

&:nth-of-type(2) a{
  @extend .webicons-arrow-right-down;
}

&:nth-of-type(3) a{
  @extend .webicons-arrow-left-down;
}

...
{% endhighlight %}

## Получение размеров создаваемого спрайта

Иногда может потребоваться так, чтобы при генерации спрайта библиотекой Compass автоматически были "отображены" в файле `.css` размеры каждого изображения. Входящего в состав этого спрайта.

По умолчанию размеры изображений не отображаются в готовом CSS-коде:

{% highlight css %}
...

.webicons-arrow-down {
background-position: 0 -326px;
}
...

.webicons-arrow-left-down {
background-position: 0 -53px;
}
...
{% endhighlight %}

Но при включении переменной `[folder-name]-sprite-dimensions: true;` (по умолчанию ее значение равно `false`) размеры каждого из изображений будут отображены в CSS-коде:

{% highlight css %}
...
.webicons-arrow-down {
background-position: 0 -326px;
height: 46px;
width: 42px;
}

.webicons-arrow-left-down {
background-position: 0 -53px;
height: 43px;
width: 43px;
}
...
{% endhighlight %}

Как и в предыдущих случаях с переменными в спрайте библиотеки Compass, вместо `folder-name` необходимо подставить имя каталога, в котором размещены файлы изображений. В нашем случае имя переменной будет выглядеть следующим образом:

{% highlight css %}
$webicons-sprite-dimentions: true;
  ...
@include 'webicons/*.png';
{% endhighlight %}

Пока на этом все ...

---

 [1]: http://www.wpzoom.com/wpzoom/new-freebie-wpzoom-developer-icon-set-154-free-icons/
