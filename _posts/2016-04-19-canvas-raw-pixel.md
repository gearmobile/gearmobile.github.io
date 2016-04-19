---
title: "Canvas - Raw Pixel"
layout: post
categories: linux
tags: [javascript, html5, canvas, raw pixel]
share: true
---

Попытка разобраться с интересной возможностью canvas, которая называется "манипуляция с пикселями" (raw pixel). Основная суть этой возможности заключается в том, что можно получить информацию о цвете и фльфа-канале любого пикселя, расположенного в произвольном месте canvas.

Образно выражаясь, можно сделать снимок (*снять цветовой отпечаток*) с любого участка canvas. Причем, этот отпечаток может быть любого размера (20х20 пикселей, 100х100 пикселей, 1х1 пиксель) - какой потребуется.

Техника Raw Pixel возможна благодаря объекту [ImageData](https://developer.mozilla.org/en-US/docs/Web/API/ImageData "ImageData"), у которого есть три свойства:

* ImageData.width - ширина объекта в пикселях
* ImageData.height - высота объекта в пикселях
* ImageData.data - массив данных

Первые два свойства примитивно просты - это геометрические размеры объекта ImageData. Самым интересным свойством объекта ImageData является последнее - `ImageData.data`. Данное свойство в свою очередь является объектом, а если быть точнее - одномерным массивом. В этом массиве на каждый пиксель из "отпечатка" отводится 4 байта:

* imageData.data[0] — значение красного цвета (число от 0 до 255);
* imageData.data[1] — значение зеленого цвета (число от 0 до 255);
* imageData.data[2] — значение синего цвета (число от 0 до 255);
* imageData.data[3] — значение прозрачности (число от 0 до 255);

В результате получается значение цвета в формате RGBA.

У Canvas есть несколько методов для работы с объектом ImageData:

* getImageData()
* putImageData()
* toDataURL()
* createIamgeData()

Наиболее интересные и полезные два первых метода - `getImageData` и `putImageData`.

## Метод getImageData

Метод `getImageData` позволяет создать экземпляр объекта ImageData на основе существующего canvas. Другими словами, этот метод "делает снимок" существующего canvas и преобразует этот "снимок" в объект ImageData.

Создадим простой пример для наглядного отображения работы метода `getImageData`:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

  var ctx = document.querySelector('#canvas').getContext('2d');

  if ( ctx ) {

    var rawPixel;

    ctx.canvas.width = 400;
    ctx.canvas.height = 400;

    ctx.fillStyle = '#00f';
    ctx.fillRect(0, 0, 100, 100);

    ctx.fillStyle = 'rgba(0, 255, 0, .5)';
    ctx.fillRect(30,30,100,100);

    rawPixel = ctx.getImageData(40, 40, 1, 1);
    console.log(rawPixel.data[0], rawPixel.data[1], rawPixel.data[2], rawPixel.data[3]);

    rawPixel = ctx.getImageData(20, 20, 1, 1);
    console.log(rawPixel.data[0], rawPixel.data[1], rawPixel.data[2], rawPixel.data[3]);

  }
});
{% endhighlight %}

Что происходит в выше приведенном коде? Все просто - создаются два блока с синим и зеленым цветом, причем блок с зеленым цветом намеренно накладывается на блок с синим цветом. А затем с помощью метода `getImageData` делаем снимок (снимаем отпечаток - если хотите) размером 1х1 пиксель с уже готового рисунка в canvas.

В первом случае левый верхний угол "отпечатка" будет находиться в точке (40, 40) координатной сетки canvas; во-втором случае левый верхний угол "отпечатка" будет находиться в точке (20, 20). В обоих случая ширина и высота "отпечатка" (снимка) равна 1x1 пиксель - то есть, будет делаться "снимок" размером (площадью) в 1 пиксель.

Результат метода `getImageData` помещается в переменную `rawPixel`. Так как эта переменная не что иное, как ссылка на конкретный экземпляр объекта ImageData, то мы можем воспользоваться свойством `data` этого объекта,  а точнее - массивом данных. Обращаясь по индексу к каждому из элементов массива, в итоге мы получаем значение цвета данного пикселя в формате RGBA.

Площадь "снимка" можно произвольно увеличить и тогда массив данных также увеличиться. К примеру, такой код:

{% highlight javascript %}
rawPixel = ctx.getImageData(20, 20, 2, 2);
{% endhighlight %}

... создаст массив вида:

![Canvas getImageData]({{site.url}}/images/uploads/2016/04/canvas-getimagedata.png "Canvas getImageData")

Как видим, к любому элементу этого массива можно обратиться по его индексу, чтобы получить значение цвета конкретного пикселя.

Сделаем приведенный выше пример более интересным (*и наглядным для понимания*) - добавим в него динамики. Преобразуем его так, чтобы в любой момент времени в отдельном информационном блоке выводился цвет (в формате RGBA) того участка canvas, над которым в данный момент находится курсор мыши. Будем считать, что курсор мыши имеет размер 1х1 пиксель.

{% highlight javascript %}
  var picker = document.querySelector('#picker').getContext('2d');
  var colorBox = document.querySelector('#colorBox');

  var image = new Image();
  image.src = 'images/rhino.jpg';

  function getColor(event) {
    var cx = event.clientX - picker.canvas.offsetLeft;
    var cy = event.clientY - picker.canvas.offsetTop;
    var currentColor = picker.getImageData(cx, cy, 1, 1);
    colorBox.style.background = 'rgba(' + currentColor.data[0] + ',' + currentColor.data[1] + ',' + currentColor.data[2] + ',' + currentColor.data[3] + ')';
    colorBox.textContent = 'rgba(' + currentColor.data[0] + ',' + currentColor.data[1] + ',' + currentColor.data[2] + ',' + currentColor.data[3] + ')';
  }

  if ( picker ) {

    picker.canvas.width = 400;
    picker.canvas.height = 300;

    image.addEventListener('load', function () {
      picker.drawImage(image, 0, 0, picker.canvas.width, picker.canvas.height);
      image.crossOrigin = "Anonymous";
    });

    picker.canvas.addEventListener('mousemove', getColor);

  }
{% endhighlight %}

В этом коде функция `getColor` при движении курсора мыши (событие `mousemove`) над областью canvas (`picker.canvas`) считывает координаты этого курсора в переменные `cx` и `cy`. Значения этих переменных передаются в качестве параметров методу `getImageData`, результат работы которого помещается в переменную `currentColor`.

Из переменной `currentColor` с помощью свойства `data` достаются значения (как элементы массива, по индексу) для каждого из RGBA-каналов. Все четыре значения конкатенируются и передаются в виде строкового значения - как фоновый RGBA-цвет для блока `colorBox`.

Для пущей наглядности с помощью свойства `textContent` в блок `colorBox` передается текущее значение цвета.

Представленный выше функционал - не что иное, как обычный Color Picker в любом графическом редакторе. Просто в данном примере достаточно изменить событие `mousemove` на событие `click`, чтобы все заработало как надо.

## Метод putImageData

Возможности метода `putImageData` значительно шире, так как этот метод позволяет редактировать canvas. Другими словами, с помощью метода `getImageData` получается конкретный экземпляр объекта ImageData из текущего canvas. Затем при помощи произвольной функции производится преобразование данных этого объекта. Отредактировванные данные возвращаются обратно в canvas с помощью метода `putImageData`.

Давайте на конкретном примере рассмотрим описанный выше пример:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

  var ctx = document.querySelector('#canvas').getContext('2d');

  if ( ctx ) {

    ctx.canvas.width = 400;
    ctx.canvas.height = 300;

    var image = new Image();
    image.src = 'images/rhino.jpg';

    image.addEventListener('load', function () {
      imageDraw(this);
    });

    function imageDraw(img) {

      ctx.drawImage(img,0,0,ctx.canvas.width,ctx.canvas.height);
      var imageData = ctx.getImageData(0,0,ctx.canvas.width,ctx.canvas.height);

      function imageInvert() {
        for ( var i = 0; i < imageData.data.length; i += 4 ) {
          imageData.data[i] = 255 - imageData.data[i];
          imageData.data[i + 1] = 255 - imageData.data[i + 1];
          imageData.data[i + 2] = 255 - imageData.data[i + 2];
        }
        ctx.putImageData(imageData,0,0);
      }

      function grayScaleImage() {
        for ( var i = 0; i < imageData.data.length; i += 4 ) {
          var averageColor = ( imageData.data[i] + imageData.data[i+1] + imageData.data[i+2] ) / 3;
          imageData.data[i] = imageData.data[i+1] = imageData.data[i+2] = averageColor;
        }
        ctx.putImageData(imageData,0,0);
      }

      document.querySelector('#graScaleColor').addEventListener('click', grayScaleImage);
      document.querySelector('#invertColor').addEventListener('click', imageInvert);

    }

  }

}, false);
{% endhighlight %}

В приведенном выше коде динамически (с помощью конструктора) создается экземпляр изображения и задается значение для его атрибута `src`. Затем на это изображение "вешается" функция, задача которой - отрисовать это изображение в canvas.

Изображение отрисовывается в canvas:

{% highlight javascript %}
ctx.drawImage(img,0,0,ctx.canvas.width,ctx.canvas.height);
{% endhighlight %}

... и тут же с него снимается отпечаток  - создается объект ImageData:

{% highlight javascript %}
var imageData = ctx.getImageData(0,0,ctx.canvas.width,ctx.canvas.height);
{% endhighlight %}

Полученный объект `imageData` обрабатывается двумя произвольными функциями - `imageInvert()` и `grayScaleImage()` при событии `click` на кнопках:

{% highlight javascript %}
document.querySelector('#graScaleColor').addEventListener('click', grayScaleImage);
document.querySelector('#invertColor').addEventListener('click', imageInvert);
{% endhighlight %}

Функция `imageInvert()` инвертирует цвета - "пробегается" по массиву `imageData.data` и производит простое вычитание текущего значения цвета из 255:

{% highlight javascript %}
imageData.data[i] = 255 - imageData.data[i];
imageData.data[i + 1] = 255 - imageData.data[i + 1];
imageData.data[i + 2] = 255 - imageData.data[i + 2];
{% endhighlight %}

Функция `grayScaleImage()` также "пробегается" по массиву `imageData.data`, но при этом производит усреднение значения цвета для каждого из пикселов:

{% highlight javascript %}
var averageColor = ( imageData.data[i] + imageData.data[i+1] + imageData.data[i+2] ) / 3;
imageData.data[i] = imageData.data[i+1] = imageData.data[i+2] = averageColor;
{% endhighlight %}

Приведем еще один пример инвертации цвета. В произвольной функции будет производится перемена цвета местами - значение красного канала будет помешаться в зеленый канал; значение зеленого цвета будет помещаться в красный канал:

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

  var ctxCanvas = document.querySelector('#replaceImage').getContext('2d');
  var originImage = document.querySelector('#originImage');

  if ( ctxCanvas ) {

    ctxCanvas.canvas.width = originImage.naturalWidth;
    ctxCanvas.canvas.height = originImage.naturalHeight;
    ctxCanvas.drawImage(originImage, 0, 0);
    ctxCanvas.canvas.style.display = 'none';

    function shiftColors () {
      var imageData = ctxCanvas.getImageData(0, 0, ctxCanvas.canvas.width, ctxCanvas.canvas.height);
      for ( var i = 0; i < imageData.data.length; i += 4 ) {
        var dump = imageData.data[i];
        imageData.data[i+1] = imageData.data[i];
        imageData.data[i] = dump;
      }
      ctxCanvas.putImageData(imageData, 0, 0);
      ctxCanvas.canvas.style.display = 'inline';
    }

    document.querySelector('#btnReplace').addEventListener('click', shiftColors, false);

  }

}, false);
{% endhighlight %}

В этом коде canvas задаются размеры оригинального изображения:

{% highlight javascript %}
ctxCanvas.canvas.width = originImage.naturalWidth;
ctxCanvas.canvas.height = originImage.naturalHeight;
{% endhighlight %}

Затем в цикле производится взаимозамещение красного и зеленого каналов:

{% highlight javascript %}
var dump = imageData.data[i];
imageData.data[i+1] = imageData.data[i];
imageData.data[i] = dump;
{% endhighlight %}

## Метод toDataURL()

Еще одним интересным методом при работе с замещением пикселей является метод `toDataURL()`. Суть его проста - также как и метод `getImageData()`, этот метод получается "снимок" текущего canvas и сохраняет результат в виде изображения в двух форматах на выбор - jgp или png.

Синтаксис этого метода таков:

{% highlight javascript %}
var imageJPG = canvas.toDataURL('image/png');
var imagePNG = canvas.toDataURL('image/jpg',1);
{% endhighlight %}

Стоит обратить внимание на явное указание (с помощью MIME) формата, в котором производится сохранение изображения. Помиом этого, при сохранении в формате jpg возможно указание второго параметра, который служит для задания качества сохраняемого изображения (от 0 до 1).

Кроме этого, стоит обратить внимание, что изображение кодируется в base64 формате и именно в этом виде может быть использовано; но никак не в форматах jpg или png.

Для внесения большей ясности давайте рассмотрим еще один интересный пример, в котором будет показана работа метода `toDataURL()`.

{% highlight javascript %}
window.addEventListener('DOMContentLoaded', function () {

  var mouseDown = false;
  var drawCtx = document.querySelector('#draw').getContext('2d');

  var link = document.createElement('a');
  link.innerHTML = 'download image';
  link.href = '#';
  link.download = 'result.png';
  document.body.insertBefore(link, drawCtx.canvas);

  if ( drawCtx ) {

    drawCtx.canvas.width = 400;
    drawCtx.canvas.height = 400;
    drawCtx.fillStyle = '#f00';

    function drawCanvas (event) {
      if ( mouseDown ) {
        var xCoor = event.clientX - drawCtx.canvas.offsetLeft;
        var yCoor = event.clientY - drawCtx.canvas.offsetTop;
        drawCtx.beginPath();
        drawCtx.arc(xCoor, yCoor, 2, 0, 360*Math.PI/180);
        drawCtx.fill();
      }
    }

    drawCtx.canvas.addEventListener('mousemove', drawCanvas, false);

    drawCtx.canvas.addEventListener('mousedown', function () {
      mouseDown = true;
    }, false);

    drawCtx.canvas.addEventListener('mouseup', function () {
      link.href = drawCtx.canvas.toDataURL('image/png');
      mouseDown = false;
    }, false);

  }

}, false);
{% endhighlight %}

Что мы имеем в приведенном выше коде? Ну, во-первых, это конечно же canvas. На этом canvas'е при помощи мыши мы можем рисовать - за это отвечает функция `drawCanvas()`.

У этой функции работа проста, но есть одна фишка - это флаг `mouseDown`. Когда курсор мыши попадает в область canvas и начинает двигаться в пределах области этого canvas (событие `mousemove`), то запускается функция `drawCanvas (event)`. Но результата работы этой функции **нет**, так условие не срабатывает из-за значения флага `mouseDown == false`. С помощью событий `mousedown` и `mouseup` в коде производится переключение состояний флага `mouseDown` из `false` в `true` и обратно.

Также при событии `mouseup` производится "снимок" текущего canvas и помещение его в атрибут `href` ссылки `a`:

{% highlight javascript %}
link.href = drawCtx.canvas.toDataURL('image/png');
{% endhighlight %}

Обратите внимание на редкий HTML5-атрибут `download`, в котором задается имя скачиваемого изображения. Если для ссылки указан атрибут `download`, то при клике по этой ссылке перехода никуда не происходит, а выполняется скачивание изображения с именем по-умолчанию (заданном в атрибуте `download`).

## Заключение

Вот в принципе и все о манипуляцих с пикселями (raw pixel) в canvas. На самом деле это конечно же не все, что можно рассказать и сделать с помощью этой техники. Здесь я просто сам познакомился с нею и вкратце описал моменты, которые мне показались наиболее интересными.

Этой статьи бы не было, если бы не существовали источники, которые и помогли ей родиться:

* [Справочник HTML5 Canvas](http://xiper.net/manuals/canvas/ "Справочник HTML5 Canvas")
* [Pixel manipulation with canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Pixel_manipulation_with_canvas "Pixel manipulation with canvas")
* [Canvas, images and pixels](https://codepo8.github.io/canvas-images-and-pixels/ "Canvas, images and pixels") - статья с большим набором отличных примеров, некоторые из которых я использовал в своем скромном обзоре

## P.S.

"Живых" примеров кода из этого обзора я не привожу, ибо лень ) Адекватная критика и замечания приветствуются )

***

На этом все.
