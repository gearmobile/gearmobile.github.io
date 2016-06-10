---
title: "Underscore.js -  приятное знакомство"
layout: post
categories: javascript
tags: [javascript, underscore.js]
share: true
---

Статья посвящена моему знакомству с [underscore.js][1]. Я рад, что познакомился с этой библиотекой.

Что такое [underscore.js][1]? Это библиотека с набором javascript-методов для удобной работы с массивами, коллекциями, функциями, объектами, а также просто утилиты.

Чтобы оценить полезность и удобство работы с этой библиотекой, нужно на практике рассмотреть примеры работы методов underscore.js. Поэтому ниже будут представлены именно примеры.

## Введение

Библиотека underscore.js живет по этому адресу - [underscore.js][1]. Подключается как любая другая javascript-библиотека или javascript-плагин - через тег script.

В документе вызывается через символ подчеркивания - `_` (отсюда и название библиотеки).

## underscore.js - работа с коллекциями

Список методов для работы с коллекциями достаточно обширен - [Collection Functions][2]. Рассмотрим некоторые из них.


### Метод _.each()

Служит для перебора всех элементов коллекции и применения функции к каждому из элементов. Код ниже пробежится по всем элементам коллекции a1 и выведет каждый из этих элементов в консоль браузера:

{% highlight javascript %}
var a1 = [ 1, 2, 3 ];
_.each( a1, function (el) { console.log(el) });
{% endhighlight %}

Более сложный пример применения метода `_.each()`. Уже здесь начинается демонстрация привлекательности underscore.js.

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

Метод _.map() получает на вход массив и выдает новый массив, созданный на основе какого-то условия.

Например, код ниже берет массив a3, вызывает каждый из элементов этого массива, умножает этот элемент на 3 и помещает в новый массив a4, как элемент этого массива:

{% highlight javascript %}
var a3 = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
var a4 = _.map( a3, function (el) { return el*3 } );
{% endhighlight %}

Точно также этот метод работает с коллекцией. Например, увеличим значение только одного определенного ключа коллекции a2. Вернется новый массив a5 с измененным значением ключа sal:

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

Функция для обработки элементов коллекции может быть любой. К примеру, можно создать новый массив, состоящий только из значений ключей spec, name или sal:

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

Метод `_.partition()` создает из одного массива новый массив, который состоит из двух подмассивов.

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

При каждом запуске изменяет метод `_.shuffle()` в случайном порядке индекс элементов существующего массива. В результате получается новый массив на основе существующего массива:

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

## underscore.js - работа с массивами

Рассмотренные выше несколько методов underscore.js могут одинаково хорошо работать как с массивами, так и с коллекциями.

Однако, помимо этих методов, у underscore.js есть методы исключительно для работы с массивами. По этой ссылке можно ознакомиться со списком таких методов - [Underscore.js - Arrays][3].

### Метод _.first()

Этот метод возвращает первый элемент массива - все просто и понятно:

{% highlight javascript %}
var a1 = [ 1, 2, 3 ];
var firstEl = _.first(a1);
{% endhighlight %}

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

Если передать эти три массива на вход методу _.zip(), то он преобразует их в один массив, состоящий из трех подмассивов. При этом элементы этих подмассивов будут выглядеть таким образом:

{% highlight javascript %}
var r4 = _.zip( r1 , r2 , r3 );
r4 = [ [ '1-1', '2-1', '3-1' ], [ '1-2', '2-2', '3-2' ], [ '1-3', '2-3', '3-3' ] ];
{% endhighlight %}

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

Создадим функцию greeting такого вида:

{% highlight javascript %}
var greeting = function (el) {
    console.log( el + ', ' + this.name );
};
{% endhighlight %}

А теперь вызовем функцию greeting на каждом из двух первых объектов:

{% highlight javascript %}
greeting.apply( someObj1, ['Hello'] );
greeting.apply( someObj2, ['Holla'] );
{% endhighlight %}

Результатом будет такой текст:

{% highlight javascript %}
Hello, Peter
Holla, Mary
{% endhighlight %}

... потому что `this.name` каждый раз будт ссылаться на разный объект - в зависимости от того, на котором из объектов было вызвано исполнение функции.

А теперь воспользуемся методом .bind() библиотеки underscore.js таким образом:

{% highlight javascript %}
var greetingBind = _.bind( greeting, someObj3 );
{% endhighlight %}

Что мы сделали в этом коде? Мы создали новый экземпляр greetingBind функции greeting и привязали исполнение этого нового экземпляра на объект someObj3. И только на него. Теперь нам не надо даже указывать, что функцию нужно исполнять на объекте someObj3 - мы просто вызываем функцию greetingBind на исполнение и передаем ей аргумент:

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
![image title]({{site.url}}/images/uploads/2015/08/images/image.jpg "image alt")

***
[1]: http://underscorejs.org/ "Underscore.js"
[2]: http://underscorejs.org/#collections "Underscore.js - Collections"
[3]: http://underscorejs.org/#arrays "Underscore.js - Arrays"
[4]: http://underscorejs.org/#functions "Underscore.js - Functions"
[5]: https://ru.wikipedia.org/wiki/%D0%9A%D0%B0%D1%80%D1%80%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5 "Каррирование"
