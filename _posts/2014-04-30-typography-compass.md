---
title: "Типографика с помощью Compass"
layout: post
categories: compass
tags: [compass, typography]
share: true
---

> Отличный момент познакомиться с еще одной безграничной возможностью библиотеки Compass - это поработать с типографикой.

Для этого дела в Compass имеется достаточно большой набор готовых миксинов. И хотя принцип большинства из них прост, суть дела от этого не меняется.

## Убрать подчеркивание у ссылок в Compass

Начнем с простого и попробуем настроить вид и поведение ссылок с помощью Compass. Для этого необходимо подключить модуль в текущий проект в виде строки:

<pre>
@import "compass/typography/links";
</pre>

Затем создадим в HTML-файле пару параграфов с ссылками:

{% highlight html %}
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eius, eos, dolorum, eum blanditiis laudantium placeat aspernatur esse dolorem <a href="#">optio molestiae provident</a> nobis sint architecto dolores repudiandae magnam iste assumenda minima.</p>

<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sequi, nobis, maiores, quasi molestias dignissimos repellendus quis nemo quibusdam <a href="#">accusamus culpa numquam</a> voluptas sunt dolor inventore pariatur cumque a unde ut.</p>
{% endhighlight %}

... и применим к ссылкам миксин `hover-link`:

{% highlight css %}
p {
  margin-bottom: 20px;

  a {
    @include hover-link;
  }
}
{% endhighlight %}

Если теперь посмотрим на скомпилированный вывод в CSS-файле, то увидим две до удивления простые строчки:

{% highlight css %}
p a {
  text-decoration: none;
}

p a:hover {
  text-decoration: underline;
}
{% endhighlight %}

То есть, суть миксина `hover-link` в убирании подчеркивания у ссылки в ее обычном состоянии; и добавлении подчеркивания при состоянии hover. Попробуйте ввести показанный выше код в своем HTML-редакторе и посмотреть результат.

### Изменение цвета ссылок в Compass

В Compass имеется миксин `link-colors` для управления цветом ссылок. То есть, с помощью этого миксина можно изменять стандартные цвета ссылки при ее различных состояниях.

Синтаксис миксина достаточно устрашающий, с первого взгляда:

{% highlight css %}
link-colors($normal, $hover, $active, $visited, $focus)
{% endhighlight %}

Однако здесь нет ничего сложного. Пять переменных миксина принимают в качестве аргументов цвета для ссылки в пяти ее состояниях:

{% highlight html %}
<ul>
  <li>$normal - цвет обычного состояния ссылки</li>
  <li>$hover - цвет ссылки при наведенном на нее курсоре мыши</li>
  <li>$active - цвет ссылки в момент нажатия на нее</li>
  <li>$visited - цвет посещенной ссылки</li>
  <li>$focus - цвет ссылки, получившей фокус с клавиатуры</li>
</ul>
{% endhighlight %}

При этом только один из параметров миксина `link-colors` является обязательным - `$normal`. Остальные можно опустить и тогда будут использоваться цвета по умолчанию.

Давайте поэскпериментируем и немного изменим цвета для ссылок в нашем примере. Перед этим не забудем подключить соответствующий модуль строкой:

{% highlight css %}
@import "compass/typography/links/link-colors"
{% endhighlight %}

Откроем таблицу цветов, расположенную по адресу [w3schools - HTML Colors][1] и наугад возмем оттуда пять цветов в HEX-формате, которые передадим миксину в качестве аргументов:

{% highlight css %}
a{
  @include link-colors(#CC0000, #CC3300, #CC6600, #CC9900, #CCCC00);
}
{% endhighlight %}

В скомпилированном CSS-файле появиться несколько строчек такого вида:

{% highlight css %}
p a:visited {
  color: #cc9900;
}

p a:focus {
  color: #cccc00;
}

p a:hover {
  color: #cc3300;
}

p a:active {
  color: #cc6600;
}
{% endhighlight %}

Введите показанный здесь код у себя и посмотрите на результат.

## Сброс всех стилей для ссылок в Compass

Последний миксин из данного раздела позволяет производить сброс всех стилей для ссылок и превращении их в обычный текст, внутри которого находятся данные ссылки.

Например, имеется параграф с классом `.woo`, внутри которого расположена ссылка. Применим к ней миксин `unstyled-link` для сброса всех стилей, предварительно подключив модуль:

{% highlight css %}
@import "compass/typography/links/unstyled-link";
{% endhighlight %}

{% highlight css %}
p.woo a {
  @include unstyled-link;
}
{% endhighlight %}

Посмотрим на результат компиляции кода в CSS и увидим такую картину:

{% highlight css %}
p.woo a {
  color: inherit;
  text-decoration: inherit;
  cursor: inherit;
}

p.woo a:active,
.wrap p.woo a:focus {
  outline: none;
}
{% endhighlight %}

Ссылка наследует от параграфа (то есть - текста, входящего в этот параграф) свойства цвета, подчеркивание и вид курсора; а также убирается рамка `outline` при получении ссылкой фокуса или щелчка мыши по ней.

То есть, другими словами, ссылка становиться полностью похожей внешне и по поведению на весь остальной текст, который ее окружает. Попробуйте у себя вышеприведенный код, чтобы увидеть результат.

На этом все.

---

[1]: http://www.w3schools.com/html/html_colors.asp "HTML Colors"
