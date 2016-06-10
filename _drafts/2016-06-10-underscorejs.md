---
title: "Underscore.js - знакомство"
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

Более сложный пример применения метода _.each(). Уже здесь начинается демонстрация привлекательности underscore.js.

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

Метод _.partition() создает из одного массива новый массив, который состоит из двух подмассивов. Первый подмассив будет содержать элементы, которые удовлетворяют условию. Второй подмассив - элементы, которые не удовлетворяют условию.








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
