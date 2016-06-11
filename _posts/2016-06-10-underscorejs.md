---
title: "Underscore.js -  приятное знакомство"
layout: post
categories: javascript
tags: [javascript, underscore.js]
share: true
---

Статья посвящена моему знакомству с [underscore.js][1]. Я рад, что познакомился с этой библиотекой. Кто плохо владеет english, то здесь находится переведенная на русский язык документация - [underscore.js russian][8];

Что такое [underscore.js][1]? Это отличная библиотека с набором javascript-методов для удобной работы с массивами, коллекциями, функциями, объектами, а также просто утилиты.

Чтобы оценить полезность и удобство работы с этой библиотекой, нужно на практике рассмотреть примеры работы методов underscore.js. Поэтому ниже будут представлены именно примеры.

Фиг его знает, но статья получилась больше смахивающей на пересказ официальной документации. Это потому, что я каждый метод (почти каждый) пробовал в действии, чтобы понять его работу.

## Введение

Библиотека underscore.js живет по этому адресу - [underscore.js][1]. Подключается как любая другая javascript-библиотека или javascript-плагин - через тег script. Есть вариант установки под Nodejs:

{% highlight bash %}
npm install underscore
{% endhighlight %}

В документе вызывается через символ подчеркивания - `_` (отсюда и название библиотеки). Кстати, расширенный вариант underscore - [lodash][6] также обыгрывает этот вариант самоназвания ( lodash == low dash ).

## underscore.js - работа с коллекциями

Список методов для работы с коллекциями достаточно обширен - [Collection Functions][2]. Рассмотрим некоторые из них.

### Метод _.each()

Служит для перебора всех элементов коллекции и применения функции к каждому из элементов. Код ниже пробежится по всем элементам коллекции a1 и выведет каждый из этих элементов в консоль браузера:

{% highlight javascript %}
var a1 = [ 1, 2, 3 ];
_.each( a1, function (el) { console.log(el) });
{% endhighlight %}

Более сложный пример применения метода `each()`. Уже здесь начинается демонстрация привлекательности underscore.js.

Код ниже является ни чем иным, как двойным циклом - один цикл вложен в другой цикл. Но с использованием underscore.js код становится буквально изящным - всего одна строка!

{% highlight javascript %}
var a2 = [
    { name: 'John', spec: 'Ruby', sal: 2000 },
    { name: 'Mary', spec: 'Python', sal: 3000 },
    { name: 'Peter', spec: 'JavaScript', sal: 4000 },
    { name: 'Jefferson', spec: 'HTML', sal: 1000 },
    { name: 'Abdul', spec: 'C++', sal: 10000 }
];
_.each( a2, function (el) { _.each( el, function (element) { console.log(element) } ) });
{% endhighlight %}

Вкратце - имеется массив a2, элементы которого - объекты со свойствами. Внешний цикл пробегается по элементам массива.

Для каждого элемента массива запускается внутренний цикл, который пробегается по свойствам элемента массива (ведь элемент массива - это объект в данном случае).

### Метод _.map()

Метод `map()` получает на вход массив и возвращает новый массив, созданный путем преобразования элементов оригинального массива \ коллекции.

Например, код ниже берет массив a3, вызывает каждый из элементов этого массива, умножает этот элемент на 3 и помещает в новый массив a4, как элемент этого массива:

{% highlight javascript %}
var a3 = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
var a4 = _.map( a3, function (el) { return el*3 } );
{% endhighlight %}

Точно также этот метод работает с коллекцией. Например, увеличим значение только одного определенного ключа коллекции a2. Вернется новый массив a5 с измененным значением ключа `sal`:

{% highlight javascript %}
var a2 = [
    { name: 'John', spec: 'Ruby', sal: 2000 },
    { name: 'Mary', spec: 'Python', sal: 3000 },
    { name: 'Peter', spec: 'JavaScript', sal: 4000 },
    { name: 'Jefferson', spec: 'HTML', sal: 1000 },
    { name: 'Abdul', spec: 'C++', sal: 10000 }
];
var a5 = _.map( a2, function (el) { el.sal += 500 } );
{% endhighlight %}

Функция для обработки элементов коллекции может быть любой. К примеру, можно создать новый массив, состоящий только из значений ключей `spec`, `name` или `sal`:

{% highlight javascript %}
var a2 = [
    { name: 'John', spec: 'Ruby', sal: 2000 },
    { name: 'Mary', spec: 'Python', sal: 3000 },
    { name: 'Peter', spec: 'JavaScript', sal: 4000 },
    { name: 'Jefferson', spec: 'HTML', sal: 1000 },
    { name: 'Abdul', spec: 'C++', sal: 10000 }
];
var specs = _.map( a2, function (el) { return el.spec } );
var names = _.map( a2, function (el) { return el.name } );
var salaries = _.map( a2, function (el) { return el.sal } );
{% endhighlight %}

### Метод _.partition()

Метод `partition()` создает из одного массива новый массив, который состоит из двух подмассивов.

Первый подмассив будет содержать элементы, которые **удовлетворяют** условию. Второй подмассив - элементы, которые **не удовлетворяют** условию.

{% highlight javascript %}
var a3 = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
var splitArr = _.partition( a3, function (el) { if ( el % 2 === 0 ) { return el } } );
{% endhighlight %}

Метод `_.partition()` также хорошо умеет работать и с коллекциями. К примеру, код ниже отсортирует массив из объектов на основе условия - значения ключа sal:

{% highlight javascript %}
var a2 = [
    { name: 'John', spec: 'Ruby', sal: 2000 },
    { name: 'Mary', spec: 'Python', sal: 3000 },
    { name: 'Peter', spec: 'JavaScript', sal: 4000 },
    { name: 'Jefferson', spec: 'HTML', sal: 1000 },
    { name: 'Abdul', spec: 'C++', sal: 10000 }
];
var splitSalary = _.partition( a2, function (el) { if ( el.sal < 4000 ) { return el } } );
{% endhighlight %}

### Метод _.shuffle()

При каждом запуске изменяет метод `shuffle()` в случайном порядке индекс элементов существующего массива. В результате получается новый массив на основе существующего массива:

{% highlight javascript %}
var a2 = [
    { name: 'John', spec: 'Ruby', sal: 2000 },
    { name: 'Mary', spec: 'Python', sal: 3000 },
    { name: 'Peter', spec: 'JavaScript', sal: 4000 },
    { name: 'Jefferson', spec: 'HTML', sal: 1000 },
    { name: 'Abdul', spec: 'C++', sal: 10000 }
];
var a3 = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
var shuffledArrObj = _.shuffle(a2);
var shuffledArr = _.shuffle(a3);
{% endhighlight %}

### Метод _.find()

С помощью этого метода можно искать элементы в коллекциях\массивах. Метод возвращает первый элемент, который удовлетворяет условию, заданному в функции:

{% highlight javascript %}
var findExample = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
var findResult = _.find( findExample, function (el) {
    return el % 2 == 0;
});
{% endhighlight %}

### Метод _.reduce()

Этот метод выполняет "склеивание" элементов массива \ коллекции - все значения элементов будут объединены в одно значение. Функция-обработчик имеет вид function ( memo, value ), где memo - это начальное значение редукции:

{% highlight javascript %}
var reduceExample = [ 1, 2, 3, 4, 5, 6, 7, 8 ];
var reduceResult = _.reduce( reduceExample, function (memo, el) {
    return memo + el;
});
{% endhighlight %}

Метод `reduceRight()` будет делать тоже самое, что и метод `reduce()`, но только справа-налево.

### Метод _.filter()

Метод для поиска элементов массива по какому-то условию. Возвращает новый массив:

{% highlight javascript %}
var filterExample = [ 1,2,3,4,5,6,7,8,9 ];
var filterResult = _.filter( filterExample, function (el) {
    return el % 3 === 0
});
{% endhighlight %}

Замечание по поводу метода `filter()` и его различия с методом `map()`.

"... underscore\lodash - методы map() и filter() - у них есть различие между собой? в оф. документации говорится, что метод map() возвращает массив преобразованных элементов; метод filter() возвращает массив элементов, удовлетворяющих условию. но ведь я могу (?) подставить в оба метода любую (?) фунцию?  
и метод filter() будет возвращать массив преобразованных элементов? или я что-то не понимаю? ..."

"... Теоретически - да, они идентичны. Но у них разное назначение - если хочется фильтровать, то используй filter, хочешь преобразовывать - map. Могу предположить (я не знаю точно), что из соображений быстродействия filter передает в функцию объект по ссылке, а не его копию, поэтому изменения объекта будут работать, но это значит, что ты отдаешься во власть реализации метода. И никто не гарантирует, что в один день underscore/lodash не начнет передавать копию объекта. В этом случае твой код может поломаться. Поэтому я бы использовал функции по назначению. ..."

### Метод _.pluck()

Метод служит для возвращения массива, содержащего значения ключа, указанного в условии.

Синтаксис метода до чрезвычайности прост - указываем имя обрабатываемой коллекции и названия ключа, значение которого хотим получить:

{% highlight javascript %}
var school = [ { name: 'Mary', age: 12 }, { name: 'John', age: 10 }, { name: 'Peter', age: 13 }, { name: 'David', age: 11 }, { name: 'George', age: 15 } ];
var schoolNames = _.pluck( school, 'name');
{% endhighlight %}

Название метода смешное - привет, [Кин-дза-дза!][9]. В официальной документации говорится, что это самый часто используемый метод библиотеки underscore.

## underscore.js - работа с массивами

Рассмотренные выше несколько методов underscore.js могут одинаково хорошо работать как с массивами, так и с коллекциями.

Однако, помимо этих методов, у underscore.js есть методы исключительно для работы с массивами. По этой ссылке можно ознакомиться со списком таких методов - [Underscore.js - Arrays][3].

### Метод _.first()

Этот метод возвращает первый элемент массива - все просто и понятно:

{% highlight javascript %}
var a1 = [ 1, 2, 3 ];
var firstEl = _.first(a1);
{% endhighlight %}

Есть метод `last()`, который аналогичен методу `firts()`, но возвращает последний элемент коллекции\массива.

### Метод _.flatten()

Этот метод преобразует массив с вложенными подмассивами (многоуровневый массив) в один, **одноуровневый** массив:

{% highlight javascript %}
var fltArr = _.flatten( [ 11, 12, 13, [ 21, 22, 23, [ 31, 32, 33, [ 41, 42, 43, [ 51, 52, 53, [ 61 ] ] ] ] ] ] );
{% endhighlight %}

### Метод _.zip()

Этот метод интересен и является примером того, насколько библиотека underscore.js удобная и изящная. Допустим, имеются три массива:

{% highlight javascript %}
var r1 = [ '1-1', '1-2', '1-3' ];
var r2 = [ '2-1', '2-2', '2-3' ];
var r3 = [ '3-1', '3-2', '3-3' ];
{% endhighlight %}

Если передать эти три массива на вход методу `zip()`, то он преобразует их в один массив, состоящий из трех подмассивов. При этом элементы этих подмассивов будут выглядеть таким образом:

{% highlight javascript %}
var r4 = _.zip( r1 , r2 , r3 );
r4 = [ [ '1-1', '2-1', '3-1' ], [ '1-2', '2-2', '3-2' ], [ '1-3', '2-3', '3-3' ] ];
{% endhighlight %}

Теперь представьте, что вам пришлось бы затратить достаточно времени для написания кода на нативном JavaScript, чтобы обработать такой пример.

### Метод _.object()

Этот метод преобразует несколько массивов в один объект:

{% highlight javascript %}
var names = [ 'Peter', 'Mary', 'John' ];
var ages = [ 30, 20, 40 ];
var peoples = _.object( names, ages );
peoples = {Peter: 30, Mary: 20, John: 40};
{% endhighlight %}

## underscore.js - работа с функциями

Методы работы с функциями с underscore.js "расположены" здесь - [Underscore.js - Functions][4]. Их не так много. Они немного сложнее для понимания. Хотя ничего сложного нет.

### Метод _.bind()

Этот метод "привязывает" исполнение функции только к определенному объекту. Чтобы было понятнее, начнем из далека, из классики.

Создадим три объекта, у каждого из которых будет ключ `name`:

{% highlight javascript %}
var someObj1 = {};
var someObj2 = {};
var someObj3 = {};
someObj1.name = 'Peter';
someObj2.name = 'Mary';
someObj3.name = 'John';
{% endhighlight %}

Создадим функцию `greeting` такого вида:

{% highlight javascript %}
var greeting = function (el) {
    console.log( el + ', ' + this.name );
};
{% endhighlight %}

А теперь вызовем функцию `greeting` на каждом из двух первых объектов:

{% highlight javascript %}
greeting.apply( someObj1, ['Hello'] );
greeting.apply( someObj2, ['Holla'] );
{% endhighlight %}

Результатом будет такой текст:

{% highlight javascript %}
Hello, Peter
Holla, Mary
{% endhighlight %}

... потому что `this.name` каждый раз будет ссылаться на разный объект - в зависимости от того, на котором из объектов было вызвано исполнение функции.

А теперь воспользуемся методом `bind()` библиотеки underscore.js таким образом:

{% highlight javascript %}
var greetingBind = _.bind( greeting, someObj3 );
{% endhighlight %}

Что мы сделали в этом коде? Мы создали новый экземпляр `greetingBind` функции `greeting` и привязали исполнение этого нового экземпляра на объект someObj3.

И только на него. Теперь нам не надо даже указывать, что функцию нужно исполнять на объекте someObj3 - мы просто вызываем функцию `greetingBind` на исполнение и передаем ей аргумент:

{% highlight javascript %}
greetingBind('Welcome');
greetingBind('Chao');
{% endhighlight %}

Вывод кода будет таким:

{% highlight javascript %}
Welcome, John
Chao, John
{% endhighlight %}

Такой способ привязки функции к объекту носит название [карринг][5] и мы только что познакомились с ним на практике.

Есть еще методы `debounce()`, `once()`, `after()` - с ними еще не познакомился. Но они весьма любопытны и полезны.

## underscore.js - работа с объектами

### Метод _.keys()

Преобразует ключи объекта в массив:

{% highlight javascript %}
var fruits = { apple: 10, melon: 20, potato: 30, tomato: 50 };
var fruitSorts = _.keys( fruits );
{% endhighlight %}

### Метод _.values()

Преобразует значения ключей объекта в массив:

{% highlight javascript %}
var fruitsvalues = _.values( fruits );
{% endhighlight %}

### Метод _.pairs()

Преобразует пары ключ-значение объекта в массив, состоящий из подмассивов:

{% highlight javascript %}
var fruitsPairs = _.pairs( fruits );
{% endhighlight %}

### Метод _.invert()

Инвертирует пару ключ:значение в объекте:

{% highlight javascript %}
var fruitsInvert = _.invert( fruits );
{% endhighlight %}

### Метод _.pick()

Вернет новый объект, в котором будут только указанные ключи:

{% highlight javascript %}
var fruitsPicked = _.pick( fruits, [ 'melon', 'tomato' ] );
{% endhighlight %}

### Метод _.clone()

Возвращает полную копию оригинального объекта:

{% highlight javascript %}
var man = { weight: 80, age: 30, height: 180, gender: 'male' };
var manDouble = _.clone( man );
man.age = 32;
manDouble.gender = 'female';
console.log( man );
console.log( manDouble );
{% endhighlight %}

### Метод _.extend()

Копируем свойства одного объекта в другой:

{% highlight javascript %}
var brick = { weight: 200, width: 250, height: 150, thickness: 100 };
var color = { color: 'red' };
var brickFull = _.extend( brick, color );
{% endhighlight %}

## underscore.js - утилиты

### Метод _.random()

Возвращает случайное число из диапазона min - max ( включительно нижнюю и верхнюю границы )

{% highlight javascript %}
var rnd = _.random( 0, 255 );
{% endhighlight %}

### Метод _.now()

Возвращает текущее время:

{% highlight javascript %}
var currTime = _.now();
console.log( currTime );
{% endhighlight %}

### Метод _.times()

Запускаем функцию на исполнение три раза:

{% highlight javascript %}
_.times(3, function () {
    console.log( 'Holla!' );
});
{% endhighlight %}

## underscore.js - template

Интересная возможность создания шаблонов. Кто знаком с HTML-шаблонизаторами (такими, как [Pug][10] (бывший [Jade][11])), станет все сразу понятно с первого взгляда.

Кому не станет ясно с первого взгляда, есть хорошая статья у Ильи Катора - [Шаблонизатор LoDash][12].

Но по коду, как мне кажется, станет ясно без объяснений:

{% highlight html %}
<button id="add" type="button">add underscore template</button>
<div class="canvas"></div>
{% endhighlight %}

{% highlight javascript %}
var users = [ 'Peter', 'Mary', 'John', 'Josef' ];
var messages = [ 'Hello', 'Holla', 'Welcome', 'Greeting' ];
var block;
var compiled = _.template( "<dl class='info'><dt><%= name %></dt><dd><%= message %></dd></dl>" );

function insertBlock () {
    block = compiled({ name: users[ _.random( 0, users.length-1 ) ], message: messages[ _.random( 0, messages.length-1 ) ] });
    document.querySelector('.canvas').innerHTML += block;
}

document.querySelector('#add').addEventListener('click', insertBlock, false);
{% endhighlight %}

## Заключение

Личное впечатление от underscore.js - я очень доволен, что познакомился с этой библиотекой! Она крайне полезная, удобная и приятная в работе. Теперь буду стараться использовать ее там, где это понадобится.

Как мне позже подсказали на frontendbelarus.slack.com, библиотека underscore.js является родоначальником другой библиотеки - [lodash][6]:

"... Lodash — расширенная версия underscore ..."

"... Когда-то был только underscore, но потом John-David Dalton форкнул его и стал расширять своими методами и оптимизировать производительность. Сейчас стандарт де-факто — это Lodash ..."

"... некоторое время назад был план их объединения в одну библиотеку, не знаю, насколько им это удалось ..."

Еще стоит заметить один немаловажный факт - некоторые методы underscore\lodash [планируются\внесены][13] в стандарт ES6 (например, методы `map()` и `filter()`).

***
[1]: http://underscorejs.org/ "Underscore.js"
[2]: http://underscorejs.org/#collections "Underscore.js - Collections"
[3]: http://underscorejs.org/#arrays "Underscore.js - Arrays"
[4]: http://underscorejs.org/#functions "Underscore.js - Functions"
[5]: https://ru.wikipedia.org/wiki/%D0%9A%D0%B0%D1%80%D1%80%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5 "Каррирование"
[6]: https://lodash.com/ "Lodash"
[7]: https://www.youtube.com/watch?v=cD9utLH3QOk "Lo-Dash and JavaScript Performance Optimizations"
[8]: http://underscorejs.ru/# "Underscore.js - Русская документация"
[9]: https://ru.wikipedia.org/wiki/%D0%9A%D0%B8%D0%BD-%D0%B4%D0%B7%D0%B0-%D0%B4%D0%B7%D0%B0! "Кин-дза-дза!"
[10]: https://www.npmjs.com/package/pug "Pug"
[11]: http://jade-lang.com/ "Jade"
[12]: https://learn.javascript.ru/template-lodash "Шаблонизатор LoDash"
[13]: https://www.sitepoint.com/lodash-features-replace-es6/ "10 Lodash Features You Can Replace with ES6"
