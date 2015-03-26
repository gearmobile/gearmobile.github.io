---
layout: post
title: "CSS-разметка - применение outline вместо border"
author: gearmobile
tags: [layout, outline]
---

Для начала я бы хотел поговорить об использовании свойство `outline`, которое на первый взгляд кажется подобным свойству `border`. Однако у свойства `outline` есть существенное отличие, которое приобретает очень важное значение при создании разметки. Свойство `outline` может быть полезным в процессе создания разметки в качестве удобного средства диагностики.

Во время создания разметки можно визуально обозначить местоположение всех ее частей.

Например, таким образом:

`div {outline: 1px solid #ff0000}`

<figure id="attachment_879" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/layout_example-600x414.jpg" alt="Пример CSS-разметки" width="600" height="414" class="size-medium wp-image-879" />][1]
	<figcaption class="wp-caption-text">Пример CSS-разметки</figcaption>
</figure>

Вы можете решить, что точно так можно сделать и с помощью свойства `border`, но в действительности это не так. Причина заключается в том, что границы (`border`) нарушают разметку. А свойство `outline` не нарушает ее.

Вот что я имею ввиду: предположим, у вас есть три колонки div'ов, которые должны располагаться внутри контейнера-родителя div с шириной 960px. (Если вам не нравятся пиксели, то можете применить для этой же цели `em`, проценты или любую другую единицу измерения). Для всех трех div'ов-потомков устанавливаем правила `float: left; width: 33.33%` и попытаемся визуально обозначить местоположение в разметке каждого из блоков.

Если ко всем трем блокам вы добавите свойство `border: 1px solid #ff0000;`, то последний из этих трех опустится вниз и расположиться под двумя первыми:

<figure id="attachment_880" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/layout_with_borders-600x414.jpg" alt="CSS-разметка с помощью border" width="600" height="414" class="size-medium wp-image-880" />][2]
	<figcaption class="wp-caption-text">CSS-разметка с помощью border</figcaption>
</figure>

Это произошло потому, что каждый из трех блоков div имеет ширину 320px; помимо этого справа и слева к каждому блоку добавлена граница толщиной в 1px, что делает ширину блока равной, как минимум, 322px. Умножьте это значение ширины на 3 (количество блоков-колонок) и в результате получиться общая ширина 966px, что явно больше ширины блока-родителя 960px. Результат для браузера - сместить последний блок вниз!

Именно по этой причине свойство `border` нарушает разметку. Свойство `outline`, с другой стороны, не нарушает ее. С помощью него вокруг элементов рисуется линия; к примеру, в нашем случае все три блока div со свойством `outline: 1px solid #ff0000;` разместятся друг рядом с другом внутри блока-родителя.

Не имеет значения, какой толщины вы сделаете `outline`, блоки div никогда не сдвинуться и не нарушат разметку (это касается не только блока div, а любого элемента страницы). Линии сделают перекрытие друг друга, как показано на рисунке ниже:

<figure id="attachment_881" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/layout_with_outlines-600x414.jpg" alt="CSS-разметка с помощью outlines" width="600" height="414" class="size-medium wp-image-881" />][3]
	<figcaption class="wp-caption-text">CSS-разметка с помощью outlines</figcaption>
</figure>

Сразу становится ясно преимущество использования `outline` при создании разметки. Если в процессе ее создания вам кажется, что что-то идет не так, вы легко можете "нарисовать" границы интересующего вас элемента, не опасаясь при этом нарушить разметку.

Другое отличие `outline` от `border` заключается в том, что `outline` "рисуется" обязательно вокруг всего элемента, по всем четырем его сторонам. Другими словами, вы не можете просто создать левый `outline` или же правый `outline`, как вы это обычно делаете при работе с границами `border`. Может существовать только граница `outline` вокруг всех четырех сторон элемента, и не может быть по другому.

По этой же причине невозможно изменять цвет, ширину или стиль какой-либо одной из сторон элемента. Если необходимо создать границу `outline: 2px dashed yellow`, то она будет создана таковой вокруг всех сторон элемента.

Заметьте, что элемент может одновременно иметь оба свойства `border` и `outline`. В этом случае граница `outline` будет отрисована браузером снаружи от границы `border`, так что внутренний край `outline` будет соприкасаться с внешним краем границы `border`:

<figure id="attachment_884" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/outlines_with_borders-600x414.jpg" alt="Свойство outline и border для одного элемента" width="600" height="414" class="size-medium wp-image-884" />][4]
	<figcaption class="wp-caption-text">Свойство outline и border для одного элемента</figcaption>
</figure>

Если элемент также имеет `margin`, то эти поля рисуются вокруг границ `outline`; но при этом `outline` не изменяют поля `margin` и не замещают их.

**Автор статьи**: *Eric Meyer - Smashing CSS Professional Techniques for Modern Layout*

 [1]: http://localhost:7788/third/wp-content/uploads/2014/02/layout_example.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2014/02/layout_with_borders.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2014/02/layout_with_outlines.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2014/02/outlines_with_borders.jpg