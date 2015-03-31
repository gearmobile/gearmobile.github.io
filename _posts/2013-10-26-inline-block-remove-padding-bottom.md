---
title: "Элемент inline - пять способов убрать отступ"
layout: post
categories: css
tags: [css, inline]
share: true
---

> При оборачивании изображения в блок `div` внизу картинки возникает странный отступ.

Появляется он потому, что элемент `img` является строчным `inline`. При верстке часто возникает задача его убрать, так как он лишний и только портит дизайн. Решений данного вопроса существует несколько.

С тремя из них я был уже знаком благодаря замечательному ресурсу для верстальщиков - [xiper.net][1]. А вот на сайте [htmlbook.ru][2] Влада Мержевича в разделе "Практикум" узнал, что таких способ не три, а пять. С задачкой справился, а решения захотел поместить у себя.

## Пять способов убрать отступ под картинкой

Создаем блок `div` с классом `.image`, для которого назначаем ширину, центрирование и границу для наглядности. Внутрь блока `div.image` помещаем картинку:

{% highlight html %}
<div class="image">
  <img src="img/charlize_theron.jpg" width="307" height="230" alt="Charlize Theron">
</div>
{% endhighlight %}

{% highlight css %}
.image {
  border: 2px solid #000;
  width: 307px;
  margin: 0 auto;
}
{% endhighlight %}

Видим этот отступ под изображением:

![Изображение с отступом]({{site.url}}/images/uploads/2013/10/inline-block_origin.png)

И пробуем пятью различными способами убрать этот отступ.

## 1. Сделать элемент img блочным

![Сделать элемент inline блочным - display: block]({{site.url}}/images/uploads/2013/10/inline-block_block.png)

{% highlight css %}
.block {
  display: block;
}
{% endhighlight %}

## 2. Задать вертикальное выравнивание

Так как элемент `img` является строчным `inline`, то к нему применимо свойство `vertical-align`, как к любому строчному элементу. Мне такой способ нравиться больше всего:

![Элемент inline - присвоить vertical-align: top]({{site.url}}/images/uploads/2013/10/inline-block_vertical-align.png)

{% highlight css %}
.vertical {
  vertical-align: top;
}
{% endhighlight %}

## 3. Сделать элемент плавающим через float

Задать для элемента `img` свойство `float: left` или `float: right`. Если элемент делается плавающим через `float`, то из строчного `inline` он становится блочным `block`.

И отступ также пропадает. Только надо не забыть добавить для контейнера `div.image` свойство `overflow: hidden`, иначе пропадет граница вокруг изображения.

Что и понятно, так как при `float: left` или `float: right` элемент "вырывается" из общего потока, становится плавающим:

![Элемент inline - присвоить float: left]({{site.url}}/images/uploads/2013/10/inline-block_float.png)

{% highlight css %}
.float {
  float: left;
}
{% endhighlight %}

## 4. Сделать картинку таблицей

Для изображения задать свойство `display: table`:

![Элемент inline - присвоить display: table]({{site.url}}/images/uploads/2013/10/inline-block_table.png)

{% highlight css %}
.table {
  display: table;
}
{% endhighlight %}

## 5. Задать высоту для блока

Для блока-контейнера `div.image` жестко задать высоту, равную высоте изображения. В моем случае высота картинки равна 230 пикселей, поэтому и для блока-обертки задаю такую же - 230 пикселей:

![Элемент inline - присвоить width]({{site.url}}/images/uploads/2013/10/inline-block_width.png)

{% highlight css %}
.height {
  height: 230px;
}
{% endhighlight %}

Все пять способов проверены мною и должны работать в реальности.

На это все.

---

[1]: xiper.net "Xiper.net"
[2]: htmlbook.ru "HTML Book"
