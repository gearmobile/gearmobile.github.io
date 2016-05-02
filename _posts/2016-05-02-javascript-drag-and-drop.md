---
title: "JavaScript Drag-and-Drop"
layout: post
categories: javascript
tags: [javascript, html5, drag'n'drop]
share: true
---

Знакомство с техникой Drag-and-Drop и механизмом ее реализации с помощью JavaScript. Данный обзор не претендует на полноту покрытия материала. Задача статьи - познакомиться с созданием Drag-and-Drop на JavaScript. Понять сам принцип механизма и научиться применять основные инструменты для его реализации.

## Определение Drag-and-Drop

Сам механизм Drag-and-Drop интуитивно понятен - "схватил-перетащил-бросил". Преимущество внедрения Drag-and-Drop в интерфейсы заключается в упрощении реализации задач; в уменьшении количества пунктов меню типа "Copy-Paste".

## События Drag-and-Drop

Механизм Drag-and-Drop имеет в своем составе целую группу событий, с помощью которых можно контролировать процесс перетаскивания:

* `dragstart` -  пользователь начинает перетаскивание элемента
* `dragenter` - перетаскиваемый элемент входит в область целевого объекта
* `dragover` - перетаскиваемый элемент перемещается в области целевого объекта
* `dragleave` - перетаскиваемый элемент покидает область целевого объекта
* `drag` - момент начала процесса перетаскивания объекта
* `drop` - момент, когда отпускается зажатая клавиша мыши (перетаскиваемый объект "роняется")
* `dragend` - момент завершения процесса перетаскивания объекта

## Объект dataTransfer

Механизм Drag-and-Drop также имеет в своем составе объект dataTransfer, который служит для вспомогательных целей. В этом объекте хранится необходимая информация о событии перетаскивания. Помимо этого, в объект dataTransfer можно добавлять данные; а также считывать из него данные.

Свойства (наиболее важные) объекта dataTransfer:

* `dataTransfer.effectAllowed` - задаем тип перетаскивания, которое пользователь может выполнять с элементом
* `dataTransfer.dropEffect` - задаем внешний вид курсора мыши в соответствии с заданным типом перетаскивания

Методы (наиболее важные) объекта dataTransfer:

* `setData()` - добавляет данные в нужном формате
* `clearData()` - удаляет данные
* `setDragImage()` - устанавливает изображение для перетаскивания с координатами курсора (0, 0 — левый верхний угол)
* `getData()` - возвращает данные

Ниже будет рассматриваться практический пример реализации Drag-and-Drop на JavaScript.

## HTML разметка

Базовая HTML-разметка будет простой:

{% highlight html %}
<h2 id="dropStatus">application status</h2>
<h1 id="dropTitle">drop zone</h1>
<div id="dropZone"></div>
<div id="objectsZone">
    <div id="object1" class="objects">object 1</div>
    <div id="object2" class="objects">object 2</div>
    <div id="object3" class="objects">object 3</div>
</div>
<hr/>
<button type="button" id="readDropZone">get object data</button>
{% endhighlight %}

Что для чего служит в этой разметке?

Заголовок `id="dropStatus"` будет отображать текущее состояние процесса Drag-and-Drop. В него мы будет отправлять информацию о текущем состоянии Drag-and-Drop при помощи событий, о который говорилось выше.

Заголовок `id="dropTitle"` служит просто для декоративных целей.

Блок `id="dropZone"` является целевой областью - в нее мы будет перетаскивать объекты.

Объекты `id="object1"`, `id="object2"`, `id="object3"` - это перетаскиваемые объекты; их мы будем перемещать в область блока `id="dropZone"`.

Кнопка `id="readDropZone"` будет выводить информацию об перемещенных объектах.

В итоге разметка совместно со стилями будут выглядеть таким образом - [JavaScript - Drag'n'Drop - Part 1](http://codepen.io/gearmobile/full/NNEYvB/ "JavaScript - Drag'n'Drop - Part 1").

## JavaScript - разбираемся с событиями

Прежде чем детально рассматривать работу каждой из будущих функций по обработке событий, мне кажется, будет лучше просто понять, какие события и куда мы будем "вешать".

Итак, начнем с перетаскиваемых элементов `id="object1"`, `id="object2"`, `id="object3"`. На каждый из них мы повесим два события:

* `dragstart` - событие начала процесса перетаскивания элемента
* `dragend` - событие окончания процесса перетаскивания элемента

Для каждого из элементов, при возникновении на нем события, мы будем запускать соответствующую функцию `dragStart` или `dragEnd`:

{% highlight javascript %}
var objects = document.querySelectorAll('#objectsZone > .objects');
...
if ( objects ) {
    [].forEach.call(objects, function (el) {
        el.setAttribute('draggable', 'true');
        el.addEventListener('dragstart', dragStart, false);
        el.addEventListener('dragend', dragEnd, false);
    });
}
{% endhighlight %}

Обратим внимание на строку `el.setAttribute('draggable', 'true');` - здесь мы динамически добавляем для всех элементов с классом `.objects` атрибут `draggable="true"`, тем самым делая (благодаря HTML5) эти элементы доступными для перетаскивания.

На элемент `id="dropZone"` мы "повесим" гораздо больше событий:

* `dragenter` - перетаскиваемый объект (например, `id="object1"`) входит в область целевого объекта (`id="dropZone"`)
* `dragleave` - перетаскиваемый объект (например, `id="object1"`) выходит из области целевого объекта (`id="dropZone"`)
* `dragover` - перетаскиваемый объект (например, `id="object1"`) перемещается внутри области целевого объекта (`id="dropZone"`)
* `drop` - перетаскиваемый объект (например, `id="object1"`) помещается внутри целевого объекта (`id="dropZone"`)

И конечно же, для каждого события будет своя функция. JavaScript-код в итоге будет выглядеть таким образом:

{% highlight javascript %}
var dropZone = document.querySelector('#dropZone');
...
if ( dropZone ) {
    dropZone.addEventListener('dragenter', dragEnter, false);
    dropZone.addEventListener('dragleave', dragLeave, false);
    dropZone.addEventListener('dragover', dragOver, false);
    dropZone.addEventListener('drop', dragDrop, false);
}
{% endhighlight %}

Ну и на кнопку `id="readDropZone"` мы "повесим" обычный код с функцией `readZone`:

{% highlight javascript %}
var dropButton = document.querySelector('#readDropZone');
...
if ( dropButton ) {
    dropButton.addEventListener('click', readZone, false);
}
{% endhighlight %}

Если суммировать все вышесказанное, то общий вид handler'ов в нашем случае будет выглядеть таким образом:

{% highlight javascript %}
// LISTENERS

if ( objects ) {
    [].forEach.call(objects, function (el) {
        el.setAttribute('draggable', 'true');
        el.addEventListener('dragstart', dragStart, false);
        el.addEventListener('dragend', dragEnd, false);
    });
}

if ( dropZone ) {
    dropZone.addEventListener('dragenter', dragEnter, false);
    dropZone.addEventListener('dragleave', dragLeave, false);
    dropZone.addEventListener('dragover', dragOver, false);
    dropZone.addEventListener('drop', dragDrop, false);
}

if ( dropButton ) {
    dropButton.addEventListener('click', readZone, false);
}
{% endhighlight %}

Далее будет детально останавливаться на каждой из функций - что она делает и для чего.

## Функция dragStart (event)

Начнем с начала и запустим функцию для обработки старта события перетаскивания - события `dragstart`. Хочу сразу оговориться, что в процессе написания кода для обработки события перетаскивания важно четко представлять себе, какое событие и на каком элементе происходит.

В данном случае мы будем обрабатывать событие `dragstart`, которое возникает на перетаскиваемом элементе (`id="object1"`, `id="object2"` или `id="object3"` - не важно).

Событие `dragstart` в момент своего возникновения автоматически генерирует объект dataTransfer, который (как мне кажется) можно в общих чертах сравнить с событийным объектом Event; последний также хранит в себе множество данных о произошедшем событии. Некоторыми методами и свойствами объекта Event мы воспользуемся в нашем примере:

{% highlight javascript %}
var dropStatus = document.querySelector('#dropStatus');
...
function dragStart (event) {
    dropStatus.innerHTML = 'Dragging the ' + event.target.getAttribute('id');
    event.dataTransfer.dropEffect = 'move';
    event.dataTransfer.setData('text', event.target.getAttribute('id'));
}
{% endhighlight %}

Функция `dragStart` при возникновении события "берет" элемент `dropStatus` и методом `innerHTML` "пихает" внутрь него строку, часть которой представляет из себя значение атрибута `id` элемента, на котором произошло событие (`event.target`).

Для объекта dataTransfer задается значение его свойства `dropEffect` - `move`.

В третьей строке для объекта dataTransfer с помощью метода `setData()` задается имя переменной `text` и значение для этой переменной - ID текущего элемента.

## Функции dragEnter (event), dragLeave (event), dragOver (event)

Три функции, каждая из которых отслеживает событие, возникающее на элементе `dropZone`:

{% highlight javascript %}
function dragEnter (event) {
    dropStatus.innerHTML = 'You are dragging over ' + event.target.getAttribute('id');
    this.classList.add('over');
}

function dragLeave (event) {
    dropStatus.innerHTML = 'You left the ' + event.target.getAttribute('id');
    this.classList.remove('over');
    this.removeAttribute('class');
}

function dragOver (event) {
    event.preventDefault();
}
{% endhighlight %}

Первые две функции - `dragEnter (event)` и `dragLeave (event)` очень похожи между собой. Каждая из них манипулирует содержимым заголовка `dropStatus`, сигнализируя о происходящем событии.

Третья функция `dragOver (event)` может показаться странной. Все ее назначение - это отмена действия по-умолчанию. Что это за действие по-умолчанию? Дело в том, что у браузеров имеется свой собственный (помимо HTML5) механизм реализации события перетаскивания Drag-and-Drop. И если его не отключить, то он не даст срабатывать нашему механизму.

## Функция dragDrop (event)

Самая большая и самая важная функция в нашем коде. Она также срабатывает на событие, возникающее на элементе `dropZone`:

{% highlight javascript %}
var droppedIN = false;
...
function dragDrop (event) {
    event.preventDefault();
    var elementID = event.dataTransfer.getData('text');
    var element = document.getElementById(elementID);
    event.target.appendChild(element);
    element.removeAttribute('draggable');
    element.classList.add('dragged');
    element.style.cursor = 'default';
    droppedIN = true;
    dropStatus.innerHTML = 'Element ' + elementID + ' dropped into the ' + event.target.getAttribute('id');
}
{% endhighlight %}

В строке `event.preventDefault();` мы снова отменяем действие по-умолчанию. На этот раз это касается самого перетаскиваемого элемента - ведь он может быть ссылкой и браузер выполнит переход по ней (действие по-умолчанию), что нам совсем не нужно.

В строке `var elementID = event.dataTransfer.getData('text');` мы из объекта dataTransfer получаем ID перетаскиваемого элемента. Вы же помните, что в функции `dragStart (event)` с помощью строки `event.dataTransfer.setData('text', event.target.getAttribute('id'));` мы его как раз получали?

Далее находим перетаскиваемый элемент по его ID - `var element = document.getElementById(elementID);`.

И помещаем его внутрь текущего активного элемента - `event.target.appendChild(element);`.

Далее убираем у перетаскиваемого элемента атрибут `draggable` - он больше не перетаскиваемый. Визуально сигнализируем об этом, изменив вид курсора мыши - `element.style.cursor = 'default';`. И сообщаем об изменившемся статусе в заголовке - `dropStatus.innerHTML = 'Element ' + elementID + ' dropped into the ' + event.target.getAttribute('id');`.

Отдельного упоминания стоит строка `droppedIN = true;`. Это флаг, с помощью которого мы определяем, произошло ли событие `drop` или нет. Может случиться так, что объект мы перетащили в область элемента `dropZone`, но передумали его помещать туда. И "отпустили" перетаскиваемый элемент за областью элемента `dropZone`. В результате событие `dragend` произошло, но событие `drop` не выполнилось.

Такую ситуацию обрабатывает функция `dragEnd()`:

{% highlight javascript %}
function dragEnd() {
    if ( droppedIN === false ) {
        dropStatus.innerHTML = 'You let the ' + event.target.getAttribute('id') + ' to go!';
    }
    droppedIN = false;
}
{% endhighlight %}

## Функция readZone ()

Последняя функция из нашего примера - это функция-счетчик. Ее задача - просто посчитать, сколько элементов на данный момент мы "бросили" в область `dropZone`:

{% highlight javascript %}
function readZone () {
    var dropZoneChild = dropZone.children;
    for ( var i = 0; i < dropZoneChild.length; i++ ) {
        alert('Object ' + dropZoneChild[i].getAttribute('id') + ' is in ' + dropZone.getAttribute('id'));
    }
}
{% endhighlight %}

Нажимаем кнопку `dropButton` и alert'ом последовательно выводим все элементы, помещенные внутрь объекта `dropZone`.

Вот, в принципе, и все, что можно вкратце сказать. Осталось только взглянуть на готовый пример работы кода - [JavaScript - Drag'n'Drop - Part 2](http://codepen.io/gearmobile/full/bpQMEJ/ "JavaScript - Drag'n'Drop - Part 2").

На этом все. Здоровая критика и полезные замечания только приветствуются.

***
Этот скромный обзор не смог бы появиться, если бы не было двух полезных для меня ресурсов:

* [Drag and Drop Application Development DnD Tutorial](https://www.developphp.com/video/JavaScript/Drag-and-Drop-Application-Development-DnD-Tutorial "Drag and Drop Application Development DnD Tutorial")
* [Встроенные функции перетаскивания в HTML5](http://www.html5rocks.com/ru/tutorials/dnd/basics/ "Встроенные функции перетаскивания в HTML5")

Есть более детальный обзор и более интересный пример задачи на JavaScript Drag-and-Drop:

* [Мышь: Drag'n'Drop](https://learn.javascript.ru/drag-and-drop "Мышь: Drag'n'Drop")
* [Мышь: Drag'n'Drop более глубоко](https://learn.javascript.ru/drag-and-drop-objects "Мышь: Drag'n'Drop более глубоко")
