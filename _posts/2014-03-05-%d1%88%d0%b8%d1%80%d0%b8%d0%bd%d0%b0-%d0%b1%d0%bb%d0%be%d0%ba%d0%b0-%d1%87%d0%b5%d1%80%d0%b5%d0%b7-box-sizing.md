---
title: Вычисление ширины блока через box-sizing
author: gearmobile
layout: post
permalink: /%d1%88%d0%b8%d1%80%d0%b8%d0%bd%d0%b0-%d0%b1%d0%bb%d0%be%d0%ba%d0%b0-%d1%87%d0%b5%d1%80%d0%b5%d0%b7-box-sizing/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - box-sizing
---
В CSS3 появилось свойство **box-sizing**, смысл которого в способе вычисления ширины HTML-блока браузером. Но, прежде чем переходить к его рассмотрению, сначала давайте вспомним, как обычно браузер производит расчет ширины блока элемента в HTML-разметке?

Вычисление всегда выполняется по формуле: **Width = Margin + Border + Padding + Content**. То есть, если ширина контента задана в 200px, *padding* равен 25px, *border* равен 10px, а *margin* равен 15px; то результирующая ширина блока будет равна 300px.

Такой способ вычисления ширины блока делают все современные браузеры:

<pre>200px + 25px*2 + 10px*2 + 15px*2 = 300px</pre><figure id="attachment_973" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/content-box-600x569.jpg" alt="Модель расчета ширины блока в браузере по умолчанию" width="600" height="569" class="size-medium wp-image-973" />][1]<figcaption class="wp-caption-text">Модель расчета ширины блока в браузере по умолчанию</figcaption></figure> 

Однако, были времена, когда не все браузеры вычисляли размеры блока элемента подобным образом. Существовал Internet Explorer версии 5/6, который ширину блока считал несколько иначе: **из заданной ширины блока вычитались padding и border, получалась результирующая ширина области content**. В те времена веб-разработчики &#8220;показывали пальцем&#8221; на этот браузер и говорили, что это ошибка и недочет разработчиков IE5/6.

Но теперь времена изменились благодаря появлению адаптивного (*responsive*) дизайна. Причины возникновения адаптивного дизайна &#8211; в огромном количестве устройств с разными размерами экранов, по большей части мобильных. Задача адаптивного дизайна в &#8220;подстраивании&#8221; одного и того же дизайна сайта под различные размеры мониторов. При таком &#8220;подстраивании&#8221; важной становиться задача вычисления ширины блоков элементов, чтобы верстка не &#8220;разваливалась&#8221;.

Чтобы такого не произошло, как раз и становиться удобным &#8220;возврат&#8221; к той модели расчета ширины блока, какая присутствовала в IE5/6. Для этого было разработано свойство **box-sizing**, с помощью которого можно управлять подобной моделью расчета.

Свойство **box-sizing** принимает **три значения** (*три модели вычисления ширины блока*): **content-box || padding-box || border-box**.

### Свойство box-sizing: content-box

Первая модель **content-box** является *способом вычисления ширины блока по умолчанию*, принятым в современных браузерах:

<pre>box-sizing: content-box</pre>

Ширина блока равна сумме: **Width = Width (Content) + Padding + Border + Margin**<figure id="attachment_973" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/content-box-600x569.jpg" alt="Свойство box-sizing со значением content-box" width="600" height="569" class="size-medium wp-image-973" />][1]<figcaption class="wp-caption-text">Свойство box-sizing со значением content-box</figcaption></figure> 

### Свойство box-sizing: padding-box

Вторая модель **padding-box** заключается в том, что ширина блока включает в себя ширину контента (content) и ширину padding. Остальные &#8211; border-box и margin-box &#8211; приплюсовываются к заданной ширине, как обычно. Данная модель, хоть и заявлена в спецификации CSS3, не поддерживается на сегодняшний день почти никакими браузерами; *так что о ней можно забыть (пока забыть)*:

<pre>box-sizing: padding-box</pre>

Ширина блока равна сумме: **Width = Width (Content + Padding) + Border + Margin**<figure id="attachment_974" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/padding-box-600x568.jpg" alt="Свойство box-sizing со значением padding-box" width="600" height="568" class="size-medium wp-image-974" />][2]<figcaption class="wp-caption-text">Свойство box-sizing со значением padding-box</figcaption></figure> 

### Свойство box-sizing: border-box

Третья модель **border-box** очень похожа на предыдущую модель padding-box. Но, в данном случае, ширина блока включает в себя еще и border-box; то есть ширина блока включает в себя область content-box, padding-box и border-box. Область margin-box прибавляется к ширине блока элемента, как обычно.

<pre>box-sizing: border-box</pre>

Ширина блока равна сумме: **Width = Width (Content + Padding + Border) + Margin**<figure id="attachment_975" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/border-box-600x568.jpg" alt="Свойство box-sizing со значением border-box" width="600" height="568" class="size-medium wp-image-975" />][3]<figcaption class="wp-caption-text">Свойство box-sizing со значением border-box</figcaption></figure> 

### Практический пример свойства box-sizing

Теперь не мешало бы продемонстрировать на практике, каким образом браузеры выполняют вычисления ширины блоков элементов под управлением свойства **box-sizing**. Допустим, у нас имеется блок-обертка `div class="wrap"`, внутри которого расположены два плавающих блока-потомка `div class="left"` и `div class="right"`.

HTML-разметка представлена ниже:

<pre><div class="wrap">
  <div class="left">
    
  </div>
    
  
  <div class="right">
    
  </div>
  
</div>
</pre>

&#8230; и CSS-таблица, обычная для такого случая. Единственное &#8220;новое&#8221; правило в этом коде &#8211; это свойство **box-sizing**, указанное с вендорными префиксами. Обычно его можно не указывать, так как у браузеров по умолчанию свойство **box-sizing** установлено в значении **content-box** (*как уже упоминалось ранее*). Но в нашем случае понадобится **явно указать** это свойство. Для блоков-потомков здесь намерено мы не указываем (*пока не указываем*) **padding**, **border** и **margin**:

<pre>*{
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
</pre><figure id="attachment_976" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_default-600x590.jpg" alt="Свойство box-sizing со значением content-box" width="600" height="590" class="size-medium wp-image-976" />][4]<figcaption class="wp-caption-text">Свойство box-sizing со значением content-box</figcaption></figure> 

Блоки-потомки четко вписываются в блок-родитель, так как у них нет **border**, **padding** и **margin**; ширина блоков-потомков точно равна половине ширине блока-родителя.

Теперь добавим для блоков-потомков **padding: 5px**:

<pre>.left, .right{
  float: left;
  width: 400px;
  height: 400px;
  -webkit-box-sizing: content-box;
  -moz-box-sizing: content-box;
  box-sizing: content-box;
  padding: 5px;
}
</pre>

Картина будет заранее предсказуемая &#8211; один из блоков-потомков опуститься вниз из-за добавления **padding: 5px** к обоим блокам:<figure id="attachment_977" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding-600x590.jpg" alt="Свойство box-sizing со значением content-box и padding: 5px" width="600" height="590" class="size-medium wp-image-977" />][5]<figcaption class="wp-caption-text">Свойство box-sizing со значением content-box и padding: 5px</figcaption></figure> 

Настало время применить свойство **box-sizing** со значением **border-box**. Браузер сразу же **пересчитает ширину обоих блоков** и картина, как по волшебству, изменится:

<pre>.left, .right{
  float: left;
  width: 400px;
  height: 400px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding: 5px;
}
</pre><figure id="attachment_978" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding_border-box-600x590.jpg" alt="Свойство box-sizing со значением border-box и padding: 5px" width="600" height="590" class="size-medium wp-image-978" />][6]<figcaption class="wp-caption-text">Свойство box-sizing со значением border-box и padding: 5px</figcaption></figure> 

Даже если добавить к блокам-потомкам границу **border**, то картинка останется прежней:

<pre>.left{
  background-color: #000;
  border: 6px solid #0000ff;
}

.right{
  background-color: #fff;
  border: 6px solid #00ff00;
}
</pre><figure id="attachment_979" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding_border_border-box-600x590.jpg" alt="Свойство box-sizing со значением border-box и border: 6px" width="600" height="590" class="size-medium wp-image-979" />][7]<figcaption class="wp-caption-text">Свойство box-sizing со значением border-box и border: 6px</figcaption></figure> 

Но если прибавить к блокам `div class="left"` и `div class="right"` правило **margin**, то наша разметка снова &#8220;сломается&#8221;:

<pre>.left, .right{
  float: left;
  width: 400px;
  height: 400px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding: 5px;
  margin-left: 5px; 
}
</pre>

Это происходит потому, что в модель вычисления **border-box** поля **margin** не входят. Поле **margin-left** размером 5px прибавляется к ширине блока-потомка. Суммарная ширина обоих блоков-потомков превышает ширину блока-родителя и один из них выходит из его, опускаясь (*снова*) вниз:<figure id="attachment_980" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding_border_margin_border-box-600x590.jpg" alt="Свойство box-sizing со значением border-box и margin-left: 5px" width="600" height="590" class="size-medium wp-image-980" />][8]<figcaption class="wp-caption-text">Свойство box-sizing со значением border-box и margin-left: 5px</figcaption></figure> 

В этом примере мы не применили к свойству **box-sizing** значения **padding-box**, потому что [браузеры не понимают этого значения][9] и свойство **box-sizing** работать не будет в этом случае. 

### Заключение

Вот и все, что можно сказать о свойстве **box-sizing**. Понимание этого свойства понадобиться еще, когда придет время изучать адаптивный (*responsive*) дизайн.

Основой для данной статьи послужила замечательная &#8220;Большая книга CSS3&#8243; Д. Макфарланд (*3-е издание*).

Оцените статью:  
<span id="post-ratings-971" class="post-ratings" data-nonce="c14e879767"><img id="rating_971_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(971, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_971_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(971, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_971_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(971, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_971_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(971, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_971_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(971, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_971_text"></span></span><span id="post-ratings-971-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/03/content-box.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2014/03/padding-box.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2014/03/border-box.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_default.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding_border-box.jpg
 [7]: http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding_border_border-box.jpg
 [8]: http://localhost:7788/third/wp-content/uploads/2014/03/box-sizing_padding_border_margin_border-box.jpg
 [9]: https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing "MDN | CSS - box-sizing"