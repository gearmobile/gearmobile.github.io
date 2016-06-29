---
title: "Знакомимся с Fabric.js - Часть 3"
layout: post
categories: category
tags: [tag]
share: true
---

Продолжение вычитки официальной документации по Fabric.js.

***

Мы затронули основную часть базового материала о Fabric в первой и второй частях этой серии. В этой статье будет представлен более углубленный материал.

## Группы

![Fabric.js Image]({{site.url}}/images/uploads/2016/06/fabricjs-part-3-01.png "Fabric.js Image")

Первое, о чем мы поговорим – это **группы**. Группировка объектов – один из самых мощных инструментов в Fabric. Зачем нам группировать объекты? Само собой для того, чтобы работать с множеством объектов как с единым целым:

![Fabric.js Image]({{site.url}}/images/uploads/2016/06/fabricjs-part-3-02.png "Fabric.js Image")

Помните, как мы группировали любое количество объектов при помощи мыши? Однажды сгруппировав их можно одновременно двигать, масштабировать, крутить и даже изменять свойства внешнего вида — цвет, прозрачность, рамку и т. д.

Именно для этого и существуют группы. Каждый раз, когда вы видите выделение на canvas (как на изображении выше), Fabric неявно, внутри себя, создает группы, чтобы впоследствии с ними можно было работать программно. Это основной смысл `fabric.Group`.

Создадим группу из 2 объектов - круга и текста:

{% highlight javascript %}
var circle = new fabric.Circle({
  radius: 100,
  fill: '#eef',
  scaleY: 0.5,
  originX: 'center', // центр группы
  originY: 'center' // центр группы
});

var text = new fabric.Text( 'hello world', {
  fontSize: 30,
  originX: 'center', // центр группы
  originY: 'center' // центр группы
});

var group = new fabric.Group([ circle, text ], {
  left: 150,
  top: 100,
  angle: -10
});

canvas.add(group);
{% endhighlight %}

Сначала мы создали текстовый объект "hello world". Задали свойствам `originX` и `originY` значение `center`, которое **отцентрирует** этот **объект внутри группы**.

При изначальных настройках члены группы ориентированы относительно левого верхнего угла группы. Затем круг радиусом в `100px` закрасили цветом `#eef` и вертикально сжали (коэффициент сжатия — `0.5`).

Далее создали объект `fabric.Group` c двумя параметрами. Первый параметр - это массив из 2 наших объектов. Вторым параметром задали группе позицию `150/100` и угол `-10`.

Наконец, добавили ее с помощью метода `canvas.add()` подобно любому другому объекту.

И, вуаля! Вы видите объект на canvas, который выглядит как эллипс с надписью. Заметьте, что его легко модифицировать, поменяв свойства группы. Вы можете работать с этим объектом как с единым целым.

Теперь у нас есть группа на canvas. Давайте ее немножко изменим:

{% highlight javascript %}
group.item(0).setFill( 'red' );
group.item(1).set({
  text: 'trololo',
  fill: 'white'
});

canvas.renderAll();
{% endhighlight %}

Что здесь происходит? Мы получили доступ к объектам внутри группы с помощью метода `item()` и изменили их свойства. Первый объект – это сжатый круг, второй – текст. Посмотрим, что получилось:

![Fabric.js Image]({{site.url}}/images/uploads/2016/06/fabricjs-part-3-03.png "Fabric.js Image")

Важная вещь, которую вы вероятно заметили — объекты группы выстроены **относительно центра группы**. Когда мы изменили надпись текст-объекта, он остался отцентрированным, даже после изменения его ширины.

Это поведение можно отменить, задав объекту координаты (лево\верх).

Давайте создадим и сгруппируем 3 круга так, чтобы они расположились горизонтально друг за другом:

{% highlight javascript %}
var circle1 = new fabric.Circle({
  radius: 50,
  fill: 'red',
  left: 0
});

var circle2 = new fabric.Circle({
  radius: 50,
  fill: 'green',
  left: 100
});

var circle3 = new fabric.Circle({
  radius: 50,
  fill: 'blue',
  left: 200
});

var group = new fabric.Group([ circle1, circle2, circle3 ], {
  left: 200,
  top: 100
});

canvas.add(group);
{% endhighlight %}

![Fabric.js Image]({{site.url}}/images/uploads/2016/06/fabricjs-part-3-04.png "Fabric.js Image")

Работая с группами, нужно обращать внимание на **состояние объектов**. К примеру, формируя группу изображений, вам нужно убедиться, что они **полностью загрузились**:

К счастью, у Fabric есть готовое решение:

{% highlight javascript %}
fabric.Image.fromURL( '/assets/pug.jpg', function( img ) {
  var img1 = img.scale( 0.1 ).set({ left: 100, top: 100 });

fabric.Image.fromURL( '/assets/pug.jpg', function( img ) {
	var img2 = img.scale( 0.1 ).set({ left: 175, top: 175 });

fabric.Image.fromURL( '/assets/pug.jpg', function( img ) {
  	var img3 = img.scale( 0.1 ).set({ left: 250, top: 250 });

canvas.add( new fabric.Group([ img1, img2, img3], { left: 200, top: 200 }))

    });
  });
});
{% endhighlight %}

![Fabric.js Image]({{site.url}}/images/uploads/2016/06/fabricjs-part-3-05.png "Fabric.js Image")

Есть еще несколько важных методов у групп. Метод `getObjects()`, который работает также как `fabric.Canvas#getObjects()` и возвращает массив из всех объектов группы.

Есть метод `size()`, показывающий число всех объектов группы. Также есть метод `contains()`, проверяющий наличие конкретного объекта в группе.

Упомянутый ранее метод `item()`, позволяющий брать определенный объект из группы. Метод `forEachObject()`, работающий точно также как `fabric.Canvas#forEachObject`, только с группами.

И наконец, методы `add()` и `remove()`, которые соответственно добавляют и удаляют объекты из группы.

Вы можете добавить/удалить объекты из группы двумя способами. С обновлением позиции/размеров группы и без.

Добавим прямоугольник в центр группы:

{% highlight javascript %}
group.add(new fabric.Rect({
  ...
  originX: 'center',
  originY: 'center'
}));
{% endhighlight %}

Добавим прямоугольник в `100px` от центра группы:

{% highlight javascript %}
group.add(new fabric.Rect({
  ...
  left: 100,
  top: 100,
  originX: 'center',
  originY: 'center'
}));
{% endhighlight %}

Добавим прямоугольник в центр группы и обновим размеры группы:

{% highlight javascript %}
group.addWithUpdate(new fabric.Rect({
  ...
  left: group.getLeft(),
  top: group.getTop(),
  originX: 'center',
  originY: 'center'
}));
{% endhighlight %}

Добавим прямоугольник в `100px` от центра группы и обновим размеры группы:

{% highlight javascript %}
group.addWithUpdate(new fabric.Rect({
  ...
  left: group.getLeft() + 100,
  top: group.getTop() + 100,
  originX: 'center',
  originY: 'center'
}));
{% endhighlight %}

Чтобы создать группу из объектов, которые уже есть на canvas, вам нужно их клонировать и только потом группировать:

{% highlight javascript %}
// создаем группу с копиями 2 существующих объектов
var group = new fabric.Group([
  canvas.item(0).clone(),
  canvas.item(1).clone()
]);

// удаляем все объекты и перерисовываем
canvas.clear().renderAll();

// добавляем группу на canvas
canvas.add(group);
{% endhighlight %}

## Сериализация

Когда вы начнете реализовывать функционал в котором, к примеру, вы захотите разрешить пользователю сохранять содержимое canvas, или захотите транслировать его другому клиенту, то вам понадобиться **сериализация canvas**.

Как можно послать содержимое canvas? Можно конечно экспортировать весь canvas в изображение, но загружать картинку на сервер — это громоздко и неудобно. Гораздо проще **перевести содержимое в текст**, чем как раз так сильно может порадовать нас Fabric.

### Методы toObject, toJSON

Основа сериализации в Fabriс — это методы `fabric.Canvas#toObject()` и `fabric.Canvas#toJSON()`.

Посмотрим на примере сериализация **пустого canvas**:

{% highlight javascript %}
var canvas = new fabric.Canvas( 'c' );
JSON.stringify( canvas ); // => '{ "objects": [], "background": "rgba(0, 0, 0, 0)" }'
{% endhighlight %}

Мы используем ES5 метод `JSON.stringify()`, который вызывает метод `toJSON` на объекте, если этот метод существует. Объект canvas в Fabric имеет такой метод, он эквивалентен вызову `JSON.stringify(canvas.toJSON())`.

Рассмотрим возвращающую строку, которая представляет пустой canvas. Она имеет формат JSON и состоит из свойств `objects` и `background`.

Свойство `objects` на данный момент пустое, так как на canvas ничего нет, а `background` имеет изначальное прозрачное значение (`rgba(0, 0, 0, 0)`).

Зададим canvas другой фон и посмотрим, что изменится:

{% highlight javascript %}
canvas.backgroundColor = 'red';
JSON.stringify( canvas ); // => '{ "objects": [], "background": "red" }'
{% endhighlight %}

Как и ожидалось, представление canvas теперь содержит другой фон. Теперь попробуем добавить несколько объектов:

{% highlight javascript %}
canvas.add(new fabric.Rect({
  left: 50,
  top: 50,
  height: 20,
  width: 20,
  fill: 'green'
}));
console.log(JSON.stringify( canvas ));
{% endhighlight %}

... выведет в консоль:

{% highlight javascript %}
'{"objects":[{"type":"rect","left":50,"top":50,"width":20,"height":20,"fill":"green","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":0,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"rx":0,"ry":0}],"background":"rgba(0, 0, 0, 0)"}'
{% endhighlight %}

Ух ты! На первый взгляд много чего поменялось, однако присмотревшись, мы увидим, что этот новый объект стал частью массива `objects`, сериализованный в JSON.

Обратите внимание, что его описание содержит в себе все визуальные компоненты: координаты, ширина, высота, заполнение и т. д. Если мы добавим другой объект, скажем красный круг и поместим его за прямоугольником, соответственно изменится и результат:

{% highlight javascript %}
canvas.add(new fabric.Circle({
  left: 100,
  top: 100,
  radius: 50,
  fill: 'red'
}));
console.log( JSON.stringify( canvas ) );
{% endhighlight %}


... выведет в консоль:

{% highlight javascript %}
'{"objects":[

{(Прямоугольник) "type":"rect","left":50,"top":50,"width":20,"height":20,"fill":"green","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":0,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"rx":0,"ry":0},

{(Круг) "type":"circle","left":100,"top":100,"width":100,"height":100,"fill":"red","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":0,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"radius":50}],"background":"rgba(0, 0, 0, 0)"}'
{% endhighlight %}


Я выделил `"type":"rect"` и `"type":"circle"`, чтобы указать, где **начинаются** эти объекты. Может показаться, что строка слишком длинная, но это еще цветочки, по сравнению с сериализацией изображений.

Для сравнения посмотрим на 1/10(!) строки, которую вернет нам метод `canvas.toDataURL('png')`:

{% highlight javascript %}
'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAyAAAAK8CAYAAAAXo9vkAAAgAElEQVR4Xu3dP4xtBbnG4WPAQOQ2YBCLK1qpoQE1/m+NVlCDwUACicRCEuysrOwkwcJgAglEItRQaWz9HxEaolSKtxCJ0FwMRIj32zqFcjm8e868s2fNWo/Jygl+e397rWetk5xf5pyZd13wPwIECBAgQIAAAQIECBxI4F0H+hwfQ4AAAQIECBAgQIAAgQsCxENAgAABAgQIECBAgMDBBATIwah9EAECBAgQIECAAAECAsQzQIAAAQIECBAgQIDAwQQEyMGofRABAgQIECBAgAABAgLEM0CAAAECBAgQIECAwMEEBMjBqH0QAQIECBAgQIAAAQICxDNAgAABAgQIECBAgMDBBATIwah9EAECBAgQIECAAAECAsQzQIAAAQIECBAgQIDAwQQEyMGofRABAgQIECBAgAABAgLEM0CAAAECBAgQIECAwMEEBMjBqH0QAQIECBAgQIAAAQICxDNAgAABAgQIECBAgMDBBATIwah9EAECBAgQIECAAAECAsQzQIAAAQIECBAgQIDAwQQEyMGofRABAgQIECBAgAABAgLEM0CAAAECBAgQIECAwMEEBMjBqH0QAQIECBAgQIAAAQICxDNAgAABAgQIECBAgMDBBATIwah9EAECBAgQIECAAAECAsQzQIAAAQIECBAgQIDAwQQEyMGofRABAgQIECBAgAABAgLEM0CAAAECBAgQIECAwMEEBMjBqH0QAQIECBAgQIAAAQICxDNAgAABAgQIECBAgMDBBATIwah9EAECBAgQIECAAAECAsQzQIAAAQIECBAgQIDAwQQEyMGofRABAgQIECBAgAABAgLEM0CAAAECBAgQIECAwMEEBMjBqH0QAQIECBAgQIAAAQICxDNAgAABAgQIECBAgMDBBATIwah9EAECBAgQIECAAAECAsQzQIAAAQIECBAgQIDAwQQEyMGofRABAgQIECBAgAABAgLEM0CAAAECBAgQIECAwMEEBMjBqH0QAQIECBAgQIAAAQICxDNAgAABAgQIECBAgMDBBATIwah9EAECBAgQIECAAAECyw+Qb134R/U2fevC8q+5esGWESBAgAABAgQIEFiOwPL/MC5AlvO0OBMCBAgQIECAAAECJxQQICcE9HYCBAgQIECAAAECBPYXECD7W3klAQIECBAgQIAAAQInFBAgJwT0dgIECBAgQIAAAQIE9hcQIPtbeSUBAgQIECBAgAABAicUECAnBPR2AgQIECBAgAABAgT2FxAg+1t5JQECBAgQIECAAAECJxQQICcE9HYCBAgQIECAAAECBPYXECD7W3klAQIECBAgQIAAAQInFBAgJwTc9+3z49yvmNd+dI7PzPHJOW6Y4wNzXD3HlXNc9pZdb85/vzbHK3P8aY7n5vj1HL+Y43dz417f97O9jgABAgQIECBAgMBSBATIKd2JCY5dWNwyx5fn+PwcV5U/6tXZ99M5fjjHk3Mjd6HifwQIECBAgAABAgQWLSBAirdnouP6WXfvHHfOcU1x9T6rXp4XPTLHA3NTX9jnDV5DgAABAgQIECBA4NACAuSE4hMdl8+Kr83xzTmuO+G61ttfnEXfnuN7c4PfaC21hwABAgQIECBAgMBJBQTIJQpOeFw7b71/jtsvccWh3vbYfNB9c6NfOtQH+hwCBAgQIECAAAECFxMQIMd8No7C4+F5283HfOtZv/ypOYG7hMhZ3wafT4AAAQIECBDYtoAA2fP+H/1Vqwd3f4jf8y1Lfdkunu7xV7OWenucFwECBAgQIEBg3QICZI/7O/Fxx7xs9wf3t36r3D3evciX7L7F7+6rIY8u8uycFAECBAgQIE'
{% endhighlight %}

И еще ~17000 символов ...

На первый взгляд не понятно, для чего понадобился еще один метод fabric.Canvas#toObject. Все просто: toObject возвращает такое же представление как и toJSON, только в виде объекта. Например, возьмем canvas с содержимым в виде зеленого прямоугольника. canvas.toObject() выведет в консоль:

{ "background" : "rgba(0, 0, 0, 0)",
  "objects" : [
    {
      "angle" : 0,
      "fill" : "green",
      "flipX" : false,
      "flipY" : false,
      "hasBorders" : true,
      "hasControls" : true,
      "hasRotatingPoint" : false,
      "height" : 20,
      "left" : 50,
      "opacity" : 1,
      "overlayFill" : null,
      "perPixelTargetFind" : false,
      "scaleX" : 1,
      "scaleY" : 1,
      "selectable" : true,
      "stroke" : null,
      "strokeDashArray" : null,
      "strokeWidth" : 1,
      "top" : 50,
      "transparentCorners" : true,
      "type" : "rect",
      "width" : 20
    }
  ]
}



Как вы можете убедиться, вывод toJSON это есть не что иное как переведенный в строку toObject. Метод toObject интересен и полезен тем, что он «умный» и «ленивый». То, что вы видите в массиве – это результат итерации по всем объектам canvas, и делегирования им метода toObject. Объект «класса» fabric.Path имеет собственный toObject, который возвращает массив ''points''. И fabric.Image также имеет этот метод, он возвращает свойство ''src'' у изображений. Следуя паттерну ООП, каждый объект знает, как себя сериализовать.

Это значит, что когда вы создаете свой собственный «класс», или же вы хотите изменить сериализованное представление объекта, то вам нужен метод toObject, который можно перезаписать или расширить его функционал.
Посмотрим на примере:

var rect = new fabric.Rect();
rect.toObject = function() {
  return { name: 'trololo' };
};
canvas.add(rect);
console.log(JSON.stringify(canvas));



… выведет в консоль:

'{"objects":[{"name":"trololo"}],"background":"rgba(0, 0, 0, 0)"}'



Как вы видите, массив ''objects'' теперь имеет измененное представление нашего прямоугольника. Но перезаписывать таким образом часто бывает не очень полезно, в отличии от расширения функционала toObject дополнительными свойствами.

var rect = new fabric.Rect();

rect.toObject = (function(toObject) {
  return function() {
    return fabric.util.object.extend(toObject.call(this), {
      name: this.name
    });
  };
})(rect.toObject);

canvas.add(rect);

rect.name = 'trololo';

console.log(JSON.stringify(canvas));



… выведет в консоль:

'{"objects":[{"type":"rect","left":0,"top":0,"width":0,"height":0,"fill":"rgb(0,0,0)","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":0,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"rx":0,"ry":0,"name":"trololo"}],"background":"rgba(0, 0, 0, 0)"}'



Мы расширили существующий метод toObject на объекте дополнительным свойством ''name''. Теперь оно присутствует в результате вызова метода. Нужно помнить, что при расширении функционала таким способом, «класс» объекта (в данном случае fabric.Rect) должен содержать вновь добавленное свойство в массиве ''stateProperties''. Только в этом случае все будет работать корректно.

Метод toSVG

Другое текстовое представление canvas — это SVG формат. Fabric специализируется на SVG парсинге и отображении на canvas. Тем самым предоставляется возможность конвертации из canvas в SVG и наоборот. Добавим такой же прямоугольник на canvas и посмотрим в действии метод toSVG:

canvas.add(new fabric.Rect({
  left: 50,
  top: 50,
  height: 20,
  width: 20,
  fill: 'green'
}));
console.log(canvas.toSVG());



… выведет в консоль:

'<?xml version="1.0" standalone="no" ?><!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 20010904//EN" "http://www.w3.org/TR/2001/REC-SVG-20010904/DTD/svg10.dtd"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="800" height="700" xml:space="preserve"><desc>Created with Fabric.js 0.9.21</desc><rect x="-10" y="-10" rx="0" ry="0" width="20" height="20" style="stroke: none; stroke-width: 1; stroke-dasharray: ; fill: green; opacity: 1;" transform="translate(50 50)" /></svg>'



Также как toJSON или toObject, toSVG, когда вызывается на canvas, делегирует свою логику каждому объекту, и каждый из них имеет свой собственный toSVG метод, особенный для каждого типа объектов. Если вам нужно изменить или расширить toSVG метод, вы можете сделать это также как и с методом toObject.

Преимущество SVG представления в сравнении с toObject/toJSON заключается в том, что вы можете скоординироваться с любым устройством способным к SVG-визуализации (браузер, приложение, принтер, камера и т.д.). С методами toObject/toJSON вам необходимо сначала загрузить представление в canvas. Кстати, о загрузке на canvas. Мы можем сериализовать содержимое canvas в текст, а как же нам обратно его загрузить?

Десериализация, SVG парсер

Как и в сериализации, есть 2 способа загрузить canvas из строки: из представления JSON и SVG. Для JSON существуют методы fabric.Canvas#loadFromJSON и fabric.Canvas#loadFromDatalessJSON. Для SVG — методы fabric.loadSVGFromURL и fabric.loadSVGFromString.
Обратите внимание, что первые два метода вызываются на canvas, а два других непосредственно на fabric.

Особо нечего сказать об этих методах. Они работают именно так, как от них и ожидаешь. Возьмем к примеру, предыдущий вывод JSON и поместим его на пустой canvas:

var canvas = new fabric.Canvas();

canvas.loadFromJSON('{"objects":[{"type":"rect","left":50,"top":50,"width":20,"height":20,"fill":"green","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":0,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"rx":0,"ry":0},{"type":"circle","left":100,"top":100,"width":100,"height":100,"fill":"red","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":0,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"radius":50}],"background":"rgba(0, 0, 0, 0)"}');



… Оба объекта появляются на canvas:



Ну что же, загружать canvas из строки довольно просто, а как насчет непонятного на первый взгляд метода loadFromDatalessJSON? В чем его принципиальная разница от loadFromJSON, который мы только что использовали? Чтобы понять для чего нам этот метод, нужно взглянуть на более или менее сложный path объект, например вот этот:



… и JSON.stringify(canvas) выведет следующее:

'{"objects":[{"type":"path","left":184,"top":177,"width":175,"height":151,"fill":"#231F20","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":-19,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"path":[["M",39.502,61.823],["c",-1.235,-0.902,-3.038,-3.605,-3.038,-3.605],["s",0.702,0.4,3.907,1.203],["c",3.205,0.8,7.444,-0.668,10.114,-1.97],["c",2.671,-1.302,7.11,-1.436,9.448,-1.336],["c",2.336,0.101,4.707,0.602,4.373,2.036],["c",-0.334,1.437,-5.742,3.94,-5.742,3.94],["s",0.4,0.334,1.236,0.334],["c",0.833,0,6.075,-1.403,6.542,-4.173],["s",-1.802,-8.377,-3.272,-9.013],["c",-1.468,-0.633,-4.172,0,-4.172,0],["c",4.039,1.438,4.941,6.176,4.941,6.176],["c",-2.604,-1.504,-9.279,-1.234,-12.619,0.501],["c",-3.337,1.736,-8.379,2.67,-10.083,2.503],["c",-1.701,-0.167,-3.571,-1.036,-3.571,-1.036],["c",1.837,0.034,3.239,-2.669,3.239,-2.669],["s",-2.068,2.269,-5.542,0.434],["c",-3.47,-1.837,-1.704,-8.18,-1.704,-8.18],["s",-2.937,5.909,-1,9.816],["C",34.496,60.688,39.502,61.823,39.502,61.823],["z"],["M",77.002,40.772],["c",0,0,-1.78,-5.03,-2.804,-8.546],["l",-1.557,8.411],["l",1.646,1.602],["c",0,0,0,-0.622,-0.668,-1.691],["C",72.952,39.48,76.513,40.371,77.002,40.772],["z"],["M",102.989,86.943],["M",102.396,86.424],["c",0.25,0.22,0.447,0.391,0.594,0.519],["C",102.796,86.774,102.571,86.578,102.396,86.424],["z"],["M",169.407,119.374],["c",-0.09,-5.429,-3.917,-3.914,-3.917,-2.402],["c",0,0,-11.396,1.603,-13.086,-6.677],["c",0,0,3.56,-5.43,1.69,-12.461],["c",-0.575,-2.163,-1.691,-5.337,-3.637,-8.605],["c",11.104,2.121,21.701,-5.08,19.038,-15.519],["c",-3.34,-13.087,-19.63,-9.481,-24.437,-9.349],["c",-4.809,0.135,-13.486,-2.002,-8.011,-11.618],["c",5.473,-9.613,18.024,-5.874,18.024,-5.874],["c",-2.136,0.668,-4.674,4.807,-4.674,4.807],["c",9.748,-6.811,22.301,4.541,22.301,4.541],["c",-3.097,-13.678,-23.153,-14.636,-30.041,-12.635],["c",-4.286,-0.377,-5.241,-3.391,-3.073,-6.637],["c",2.314,-3.473,10.503,-13.976,10.503,-13.976],["s",-2.048,2.046,-6.231,4.005],["c",-4.184,1.96,-6.321,-2.227,-4.362,-6.854],["c",1.96,-4.627,8.191,-16.559,8.191,-16.559],["c",-1.96,3.207,-24.571,31.247,-21.723,26.707],["c",2.85,-4.541,5.253,-11.93,5.253,-11.93],["c",-2.849,6.943,-22.434,25.283,-30.713,34.274],["s",-5.786,19.583,-4.005,21.987],["c",0.43,0.58,0.601,0.972,0.62,1.232],["c",-4.868,-3.052,-3.884,-13.936,-0.264,-19.66],["c",3.829,-6.053,18.427,-20.207,18.427,-20.207],["v",-1.336],["c",0,0,0.444,-1.513,-0.089,-0.444],["c",-0.535,1.068,-3.65,1.245,-3.384,-0.889],["c",0.268,-2.137,-0.356,-8.549,-0.356,-8.549],["s",-1.157,5.789,-2.758,5.61],["c",-1.603,-0.179,-2.493,-2.672,-2.405,-5.432],["c",0.089,-2.758,-1.157,-9.702,-1.157,-9.702],["c",-0.8,11.75,-8.277,8.011,-8.277,3.74],["c",0,-4.274,-4.541,-12.82,-4.541,-12.82],["s",2.403,14.421,-1.336,14.421],["c",-3.737,0,-6.944,-5.074,-9.879,-9.882],["C",78.161,5.874,68.279,0,68.279,0],["c",13.428,16.088,17.656,32.111,18.397,44.512],["c",-1.793,0.422,-2.908,2.224,-2.908,2.224],["c",0.356,-2.847,-0.624,-7.745,-1.245,-9.882],["c",-0.624,-2.137,-1.159,-9.168,-1.159,-9.168],["c",0,2.67,-0.979,5.253,-2.048,9.079],["c",-1.068,3.828,-0.801,6.054,-0.801,6.054],["c",-1.068,-2.227,-4.271,-2.137,-4.271,-2.137],["c",1.336,1.783,0.177,2.493,0.177,2.493],["s",0,0,-1.424,-1.601],["c",-1.424,-1.603,-3.473,-0.981,-3.384,0.265],["c",0.089,1.247,0,1.959,-2.849,1.959],["c",-2.846,0,-5.874,-3.47,-9.078,-3.116],["c",-3.206,0.356,-5.521,2.137,-5.698,6.678],["c",-0.179,4.541,1.869,5.251,1.869,5.251],["c",-0.801,-0.443,-0.891,-1.067,-0.891,-3.473]'...



… и это всего лишь 5-я (!) часть всего текста.

Что здесь происходит? Path объект состоит из сотен символов кривых Безье, которые показывают как этот объект нужно отображать. Все эти части ["c",0,2.67,-0.979,5.253,-2.048,9.079] в формате JSON – это координаты одной из кривых. И когда этих кривых сотни или тысячи не трудно догадаться, насколько огромной будет строка.

Что же делать?

Здесь приходит на помощь метод fabric.Canvas#toDatalessJSON. Давайте попробуем:

canvas.item(0).sourcePath = '/assets/dragon.svg';
console.log(JSON.stringify(canvas.toDatalessJSON()));



… выведет в консоль:

{"objects":[{"type":"path","left":143,"top":143,"width":175,"height":151,"fill":"#231F20","overlayFill":null,"stroke":null,"strokeWidth":1,"strokeDashArray":null,"scaleX":1,"scaleY":1,"angle":-19,"flipX":false,"flipY":false,"opacity":1,"selectable":true,"hasControls":true,"hasBorders":true,"hasRotatingPoint":false,"transparentCorners":true,"perPixelTargetFind":false,"path":"/assets/dragon.svg"}],"background":"rgba(0, 0, 0, 0)"}



Ну что ж, значительно меньше! Что же мы сделали? Обратите внимание, что перед вызовом метода toDatalessJSON мы в свойство «sourcePath» объекта path (dragon shape) задали значение "/assets/dragon.svg". Затем мы вызвали метод toDatalessJSON, и вся эта огромная path строка превратилась в простую строку "/assets/dragon.svg".

Работая с большим количеством сложных форм, toDatalessJSON метод позволяет нам значительно сократить текстовое представление canvas, и заменить большие path данные на простую ссылку на SVG.

Возвращаясь к методу loadFromDatalessJSON, вы наверное догадались, что он позволяет загружать canvas из представления без данных (dataless). loadFromDatalessJSON умеет загружать «path» строки (такие как "/assets/dragon.svg") и использовать их в качестве данных для path объектов.

Посмотрим на методы для загрузки SVG. Мы можем использовать строку или URL:

fabric.loadSVGFromString('...', function(objects, options) {
  var obj = fabric.util.groupSVGElements(objects, options);
  canvas.add(obj).renderAll();
});



Первый аргумент это SVG строка, второй – функция коллбэк. Функция вызывается, когда SVG загрузился. Она принимает два аргумента: objects и options. objects – массив объектов, полученных из SVG – paths, группа path-объектов (для сложных объектов), изображения, текст и т.д. Чтобы сгруппировать все эти объекты в одну коллекцию, и сделать их похожими на то, какими они были в SVG документе, мы используем fabric.util.groupSVGElements как для objects, так и для и options. В конечном итоге мы получаем fabric.Path либо fabric.PathGroup объект, который мы можем добавить на canvas.

fabric.loadSVGFromURL работает таким же образом, за исключением того, что вы используете строку содержащую URL, а не содержимое SVG. Обратите внимание, что Fabric попытается получить этот URL через XMLHttpRequest, поэтому ссылка на SVG должна соответствовать правилам SOP.

Подклассы (Subclassing)

Так как Fabric построена на принципах ООП, то создавать «подклассы» и расширять функционал объектов можно легко и непринужденно. Как вы знаете из первой части серии, в Fabric существует строгая иерархия объектов. Все 2D объекты (path, изображения, текст, и т.д.) наследуют от fabric.Object, и некоторые «классы» — вроде fabric.PathGroup — даже имеют 3-уровневое наследование.

Как насчет того, чтобы сделать «подкласс» на существующем «классе» в Fabric? Или может быть, создать новый «класс»?

Для того чтобы это сделать, нам понадобиться метод fabric.util.createClass, который является простой абстракций обычного прототипного наследования в javascript. Для начала создадим простой «класс» Point:

var Point = fabric.util.createClass({
  initialize: function(x, y) {
    this.x = x || 0;
    this.y = y || 0;
  },
  toString: function() {
    return this.x + '/' + this.y;
  }
});



createClass берет объект и использует его свойства как свойства объекта нового «класса». ''initialize'' используется в качестве конструктора. Поэтому когда мы инициализируем Point, мы создаем новый объект со свойствами ''x'', ''y'' и методом ''toString'':

var point = new Point(10, 20);

point.x; // 10
point.y; // 20

point.toString(); // "10/20"



Если мы хотим создать потомок «класса» Point, скажем, цветную точку (colored point), мы используем createClass:

var ColoredPoint = fabric.util.createClass(Point, {
  initialize: function(x, y, color) {
    this.callSuper('initialize', x, y);
    this.color = color || '#000';
  },
  toString: function() {
    return this.callSuper('toString') + ' (color: ' + this.color + ')';
  }
});



Обратите внимание, что теперь объект для наследования используется в качестве второго аргумента, а первым выступает «класс» Point, который становится родительским для данного объекта. Чтобы избежать дублирования мы используем метод callSuper, который вызывает метод на родительском «классе». Это значит, что если мы изменим Point, то изменения коснутся также и ColoredPoint. Посмотрим на примере:

var redPoint = new ColoredPoint(15, 33, '#f55');

redPoint.x; // 15
redPoint.y; // 33
redPoint.color; // "#f55"

redPoint.toString(); "15/35 (color: #f55)"



Теперь мы знаем, как создавать свои «классы» и «подклассы», но также мы можем использовать уже существующие в Fabric. Например, создадим «класс» LabeledRect, который будет просто прямоугольник с надписью. Когда экземпляр «класса» отобразится на canvas, надпись будет отображена внутри прямоугольника. Нечто подобное (круг и текст) мы уже рассматривали в главе 'Группы'. Кстати говоря, работая с Fabric можно заметить, что создавать абстракции здесь можно как при помощи групп, так и «классами».

var LabeledRect = fabric.util.createClass(fabric.Rect, {

  type: 'labeledRect',

  initialize: function(options) {
    options || (options = { });

    this.callSuper('initialize', options);
    this.set('label', options.label || '');
  },

  toObject: function() {
    return fabric.util.object.extend(this.callSuper('toObject'), {
      label: this.get('label')
    });
  },

  _render: function(ctx) {
    this.callSuper('_render', ctx);

    ctx.font = '20px Helvetica';
    ctx.fillStyle = '#333';
    ctx.fillText(this.label, -this.width/2, -this.height/2 + 20);
  }
});



Код может показаться сложным, однако тут все довольно просто.

Сначала мы определяем родительский «класс» как fabric.Rect, чтобы добавить его способности к отображению. Затем определяем свойство ''type'' и задаем ему значение ''labeledRect''. Это сделано для согласования с архитектурой Fabric, так как все объекты там имеют свойство ''type'' (прямоугольник, круг, path, текст и т.д.).

Конструктор (initialize) нам уже знаком, в нем мы вызываем callSuper, который вызывает initialize на fabric.Rect. Вдобавок мы даем объекту надпись (label), взяв значение из options.

В итоге у нас осталось 2 метода – toObject и _render. toObject, как мы помним из главы про сериализацию, ответственен за представление объекта.

Так как LabeledRect имеет те же свойства, что и обычный прямоугольник (rect), мы расширили родительский метод toObject, просто добавив ему метку (label).

Что же касается метода _render, то он отвечает за непосредственную отрисовку объекта. Он состоит из отображения прямоугольника (callSuper) и дополнительной логики отображения текста.

Теперь, если мы хотим показать такой объект:

var labeledRect = new LabeledRect({
  width: 100,
  height: 50,
  left: 100,
  top: 100,
  label: 'test',
  fill: '#faa'
});
canvas.add(labeledRect);



… мы получим следующее:



Изменение свойства (label или любого другого) приведет к ожидаемому результату:

labeledRect.set({
  label: 'trololo',
  fill: '#aaf',
  rx: 10,
  ry: 10
});






Вы можете модифицировать поведение «класса» как угодно. Например, добавить значения по умолчанию, чтобы лишний раз не задавать их в конструкторе. Или сделать настраиваемые свойства доступными на объекте. Если вы сделаете дополнительные свойства настраиваемыми, вы можете поместить их в toObject, и initialize:

...
initialize: function(options) {
  options || (options = { });

  this.callSuper('initialize', options);

  // задать всем прямоугольникам с метками фиксированную ширину/высоту в размере 100/50
  this.set({ width: 100, height: 50 });

  this.set('label', options.label || '');
}
...
_render: function(ctx) {

  // сделать шрифт и значение заполнения меток настраиваемыми
  ctx.font = this.labelFont;
  ctx.fillStyle = this.labelFill;

  ctx.fillText(this.label, -this.width/2, -this.height/2 + 20);
}
...



На этом заканчивается 3-я часть нашей серии. Теперь вы имеете представление о группах, «классах», «подклассах» и (де)сериализации. Надеюсь, что материал, изложенный в статье, поможет вам решать более сложные задачи вместе с Fabric. Еще больше информации будет представлено в четвертой части серии.













// FILE NAME
// year-month-day-name
2013-01-15-archlinux-slim.md

// CODE SNIPPET
{% highlight javascript %}
// ...
{% endhighlight %}

// INLINE LINK
[link]( "link title")

// ANNOUNCEED LINK
[text][1]

// INLINE IMAGE
![image title]({{site.url}}/images/uploads/2015/08/image.jpg "image alt")

***
[1]: http://speckyboy.com/2015/01/26/six-common-freelancing-myths/ "Six Common Freelancing Myths"
