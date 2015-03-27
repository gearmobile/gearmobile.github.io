---
layout: post
title: "Photoshop - преобразовываем обводку в CSS"
author: gearmobile
tags: [photoshop, stroke, css]
---

При верстке из psd-макета можно столкнуться с такой ситуацией. Имеется какое-либо изображение, для которого в Photoshop создана обводка. Внешне это напоминает простую рамку для изображения. Но только внешне обводка похожа на рамку. На самом деле она накладывается на изображение поверх него.

У нас стоит задача преобразовать изображение с обводкой из psd-макета в html-код, используя при этом стилевые правила, где это допустимо. Само изображение преобразовать с помощью стилей невозможно - это картинка. А вот создать рамку (*в данном случае это обводка*) в помощью правил будет легко выполнить.

Осталось решить вопрос, как вырезать картинку из psd-макета, не трогая при этом обводку. Давайте посмотрим на фрагмент макета с интересующей нас картинкой и на панель слоев, отвечающих за ее прорисовку:

<figure id="attachment_348" style="width: 575px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment.png" alt="Изображение с обводкой в Photoshop" width="575" height="235" class="size-full wp-image-348" />][1]
	<figcaption class="wp-caption-text">Изображение с обводкой в Photoshop</figcaption>
</figure>

<figure id="attachment_349" style="width: 374px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer.png" alt="Слои, отвечающие за изображение и обводку в Photoshop" width="374" height="176" class="size-full wp-image-349" />][2]
	<figcaption class="wp-caption-text">Слои, отвечающие за изображение и обводку в Photoshop</figcaption>
</figure> 

На панели слоев видим два слоя - "Layer 16" и "Shape 14 copy". Именно они выполняют прорисовку картинки футболиста. На слое Shape 14 copy также видим эффекты, применяемые к этому слою. Если внимательно присмотреться к эффектам, то увидим надписи "Эффекты" - "Выполнить обводку". Это как раз обводка, от которой нам необходимо избавиться, чтобы вырезать только саму фотографию.

Отлючаем эффект обводки. Для этого щелкаем мыщью на "глазике" "Эффекты" на слое "Shape 14 copy'. "Глазик" "потухает", то есть эффект отключен. Смотрим на фотографию и видим, что обводка пропала:

<figure id="attachment_350" style="width: 381px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-disabled.png" alt="Слой с отключенным эффектом обводки в Photoshop" width="381" height="215" class="size-full wp-image-350" />][3]
	<figcaption class="wp-caption-text">Слой с отключенным эффектом обводки в Photoshop</figcaption>
</figure>

<figure id="attachment_351" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-disabled-600x235.png" alt="outline-fragment-disabled" width="600" height="235" class="size-medium wp-image-351" />][4]
	<figcaption class="wp-caption-text">outline-fragment-disabled</figcaption>
</figure> 

Теперь осталось вырезать изображение. Воспользуемся инструментом Photoshop под названием "Crop".

Выбираем его и вырезаем изображение. Затем сохраняем его для "Web и устройств" в формате `.jpg` (*наилучший вариант для фотографий*).

Однако, нам еще необходимо узнать точные размеры и цвет обводки. Для этого опять воспользуемся слоями в Photoshop. Точнее - выберем слой "Shape 14 copy' и откроем его свойства. В списке эффектов выбираем "Обводка" и смотрим на правую часть, где представлены параметры, с помощью которых она выполнена:

<figure id="attachment_352" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties-600x347.png" alt="Свойства обводки в Photoshop" width="600" height="347" class="size-medium wp-image-352" />][5]
	<figcaption class="wp-caption-text">Свойства обводки в Photoshop</figcaption>
</figure> 

Нам потребуются только два из них. Это толщина линии обводки "Размер" и цвет линии обводки "Цвет". Также проверяем, что прозрачность (альфа-канал) для цвета обводки не используется, так как стоит "Непрозр." равная 100%. Обводка выполнена сплошным цветом, так как на это указывает значение "Режим наложения: Нормальный". Цвет обводки должен быть белым, но уточняем этот факт.

Щелкаем на окошке "Цвет":

<figure id="attachment_353" style="width: 589px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties-color.png" alt="Цвет обводки в Photoshop" width="589" height="392" class="size-full wp-image-353" />][6]
	<figcaption class="wp-caption-text">Цвет обводки в Photoshop</figcaption>
</figure>

Так все и есть - цвет равен `#fff`. Все готово для написания стилей CSS:

{% highlight css %}
	img.football {
		border:2px solid #fff;
	}
{% endhighlight %}

<figure id="attachment_354" style="width: 453px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-result.png" alt="outline-fragment-result" width="453" height="421" class="size-full wp-image-354" />][7]
	<figcaption class="wp-caption-text">outline-fragment-result</figcaption>
</figure>

В результате получил иззображение с обводкой. Однако, в случае исполнения через стилевые правила CSS это будет не обводка, а чистая рамка. Размер изображения равен 62х59px. Добавляем к нему рамку размером `2px`. Получаем реальный размер картинки на сайте `64 x 61px`.

Средствами CSS на данный момент невозможно выполнить обводку, как на макете в Photoshop. Поэтому, если размер изображения критичен для шаблона, лучшим вариантом будет вырезание картинки вместе с обводкой.

### P.S.

Может быть так, что на самом слое в панели слоев эффект обводки не будет отображен:

<figure id="attachment_355" style="width: 342px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-without-effects.png" alt="Отсутствие эффектов на слое в Photoshop" width="342" height="174" class="size-full wp-image-355" />][8]
	<figcaption class="wp-caption-text">Отсутствие эффектов на слое в Photoshop</figcaption>
</figure>

В этом случае, для получения параметров обводки необходимо зайти в свойства слоя и дальше действовать также, как было описано в предыдущих шагах.

> Данное высказывание является несколько неточным. Эффекты слоя никуда не пропадают - они просто скрыты. Более подробное описание, как развернуть или скрыть отображение эффектов слоя в Photoshop можно почитать в статье "[Photoshop - скрытие и отображение эффектов слоя в палитре слоев][9]"

На этом все.

 [1]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-disabled.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-disabled.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-properties-color.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-result.png
 [8]: http://localhost:7788/third/wp-content/uploads/2013/09/outline-fragment-layer-without-effects.png
 [9]: http://localhost:7788/third/?p=357 "Photoshop - скрытие и отображение эффектов слоя в палитре слоев"