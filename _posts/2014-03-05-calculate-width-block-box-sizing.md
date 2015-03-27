---
title: "Вычисление ширины блока через box-sizing"
layout: post
categories: css
share: true
tags: [box-sizing, css]
---

> В CSS3 появилось свойство `box-sizing`, смысл которого в способе вычисления ширины HTML-блока браузером. Но, прежде чем переходить к его рассмотрению, сначала давайте вспомним, как обычно браузер производит расчет ширины блока элемента в HTML-разметке?

Вычисление всегда выполняется по формуле: `Width = Margin + Border + Padding + Content`. То есть, если ширина контента задана в 200px, `padding` равен 25px, `border` равен 10px, а `margin` равен 15px; то результирующая ширина блока будет равна 300px.

Такой способ вычисления ширины блока делают все современные браузеры:

~~~ raw
200px + 25px*2 + 10px*2 + 15px*2 = 300px
~~~

![Модель расчета ширины блока в браузере по умолчанию]({{site.url}}/images/uploads/2014/03/content-box.jpg)

Однако, были времена, когда не все браузеры вычисляли размеры блока элемента подобным образом. Существовал Internet Explorer версии 5/6, который ширину блока считал несколько иначе: **из заданной ширины блока вычитались padding и border, получалась результирующая ширина области content**. В те времена веб-разработчики "показывали пальцем" на этот браузер и говорили, что это ошибка и недочет разработчиков IE5/6.

Но теперь времена изменились благодаря появлению адаптивного (`responsive`) дизайна. Причины возникновения адаптивного дизайна - в огромном количестве устройств с разными размерами экранов, по большей части мобильных. Задача адаптивного дизайна в "подстраивании" одного и того же дизайна сайта под различные размеры мониторов. При таком "подстраивании" важной становиться задача вычисления ширины блоков элементов, чтобы верстка не "разваливалась".

Чтобы такого не произошло, как раз и становиться удобным "возврат" к той модели расчета ширины блока, какая присутствовала в IE5/6. Для этого было разработано свойство `box-sizing`, с помощью которого можно управлять подобной моделью расчета.

Свойство `box-sizing` принимает **три значения** (*три модели вычисления ширины блока*): **content-box || padding-box || border-box**.

## Свойство box-sizing: content-box

Первая модель `content-box` является *способом вычисления ширины блока по умолчанию*, принятым в современных браузерах:

~~~ css
box-sizing: content-box
~~~

Ширина блока равна сумме: `Width = Width (Content) + Padding + Border + Margin`

![Свойство box-sizing со значением content-box]({{site.url}}/images/uploads/2014/03/content-box.jpg)

## Свойство box-sizing: padding-box

Вторая модель `padding-box` заключается в том, что ширина блока включает в себя ширину контента (`content`) и ширину `padding`. Остальные - `border-box` и `margin-box` - приплюсовываются к заданной ширине, как обычно. Данная модель, хоть и заявлена в спецификации CSS3, не поддерживается на сегодняшний день почти никакими браузерами; *так что о ней можно забыть (пока забыть)*:

~~~ css
box-sizing: padding-box
~~~

Ширина блока равна сумме: `Width = Width (Content + Padding) + Border + Margin`

![Свойство box-sizing со значением padding-box]({{site.url}}/images/uploads/2014/03/padding-box.jpg)

## Свойство box-sizing: border-box

Третья модель `border-box` очень похожа на предыдущую модель `padding-box`. Но, в данном случае, ширина блока включает в себя еще и `border-box`; то есть ширина блока включает в себя область `content-box`, `padding-box` и `border-box`. Область `margin-box` прибавляется к ширине блока элемента, как обычно.

~~~ css
box-sizing: border-box
~~~

Ширина блока равна сумме: `Width = Width (Content + Padding + Border) + Margin`

![Свойство box-sizing со значением border-box]({{site.url}}/images/uploads/2014/03/border-box.jpg)

## Практический пример свойства box-sizing

Теперь не мешало бы продемонстрировать на практике, каким образом браузеры выполняют вычисления ширины блоков элементов под управлением свойства `box-sizing`. Допустим, у нас имеется блок-обертка `div class="wrap"`, внутри которого расположены два плавающих блока-потомка `div class="left"` и `div class="right"`.

HTML-разметка представлена ниже:

~~~ html
<div class="wrap">
  <div class="left"></div>
  <div class="right"></div>
</div>
~~~

... и CSS-таблица, обычная для такого случая. Единственное "новое" правило в этом коде - это свойство `box-sizing`, указанное с вендорными префиксами. Обычно его можно не указывать, так как у браузеров по умолчанию свойство `box-sizing` установлено в значении `content-box` (*как уже упоминалось ранее*). Но в нашем случае понадобится **явно указать** это свойство. Для блоков-потомков здесь намерено мы не указываем (*пока не указываем*) `padding`, `border` и `margin`:

~~~ css
*{
  margin: 0;
  padding: 0;
}

html{
  background-color: #a7c5a8;
}

body {
  width: 80%;
  margin: 0 auto;
}

.wrap{
  width: 800px;
  height: 400px;
  margin: 50px auto;
  background-color: #778899;
  border: 3px solid #ff0000;
}

.left, .right{
  float: left;
  width: 400px;
  height: 400px;
  -webkit-box-sizing: content-box;
  -moz-box-sizing: content-box;
  box-sizing: content-box;
}

.left{
  background-color: #000;
}

.right{
  background-color: #fff;
}
~~~

![Свойство box-sizing со значением content-box]({{site.url}}/images/uploads/2014/03/box-sizing_default.jpg)

Блоки-потомки четко вписываются в блок-родитель, так как у них нет `border`, `padding` и `margin`; ширина блоков-потомков точно равна половине ширине блока-родителя.

Теперь добавим для блоков-потомков `padding: 5px`:

~~~ css
.left, .right{
  float: left;
  width: 400px;
  height: 400px;
  -webkit-box-sizing: content-box;
  -moz-box-sizing: content-box;
  box-sizing: content-box;
  padding: 5px;
}
~~~

Картина будет заранее предсказуемая - один из блоков-потомков опуститься вниз из-за добавления `padding: 5px` к обоим блокам:

![Свойство box-sizing со значением content-box и padding: 5px]({{site.url}}/images/uploads/2014/03/box-sizing_padding.jpg)

Настало время применить свойство `box-sizing` со значением `border-box`. Браузер сразу же **пересчитает ширину обоих блоков** и картина, как по волшебству, изменится:

~~~ css
.left, .right{
  float: left;
  width: 400px;
  height: 400px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding: 5px;
}
~~~

![Свойство box-sizing со значением border-box и padding: 5px]({{site.url}}/images/uploads/2014/03/box-sizing_padding_border-box.jpg)

Даже если добавить к блокам-потомкам границу `border`, то картинка останется прежней:

~~~ css
.left{
  background-color: #000;
  border: 6px solid #0000ff;
}

.right{
  background-color: #fff;
  border: 6px solid #00ff00;
}
~~~

![Свойство box-sizing со значением border-box и border: 6px]({{site.url}}/images/uploads/2014/03/box-sizing_padding_border_border-box.jpg)

Но если прибавить к блокам `div class="left"` и `div class="right"` правило `margin`, то наша разметка снова "сломается":

~~~ css
.left, .right{
  float: left;
  width: 400px;
  height: 400px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding: 5px;
  margin-left: 5px;
}
~~~

Это происходит потому, что в модель вычисления `border-box` поля `margin` не входят. Поле `margin-left` размером 5px прибавляется к ширине блока-потомка. Суммарная ширина обоих блоков-потомков превышает ширину блока-родителя и один из них выходит из его, опускаясь (*снова*) вниз:

![Свойство box-sizing со значением border-box и margin-left: 5px]({{site.url}}/images/uploads/2014/03/box-sizing_padding_border_margin_border-box.jpg)

В этом примере мы не применили к свойству `box-sizing` значения `padding-box`, потому что [браузеры не понимают этого значения][1] и свойство `box-sizing` работать не будет в этом случае.

## Заключение

Вот и все, что можно сказать о свойстве `box-sizing`. Понимание этого свойства понадобиться еще, когда придет время изучать адаптивный (*responsive*) дизайн.

Основой для данной статьи послужила замечательная "Большая книга CSS3 Д. Макфарланд (*3-е издание*).

[1]: https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing "MDN | CSS - box-sizing"
