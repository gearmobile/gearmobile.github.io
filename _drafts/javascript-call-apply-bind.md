---
title: "Javascript - методы call, apply, bind"
layout: post
categories: javascript
tags: [javascript, call, apply, bind]
share: true
---

## Метод call

Метод call и apply достаточно древние - они оба из стандарта ES3. Суть создания и работы методов - заставить некоторую произвольную функцию работать на каком-то объекте. Точнее - использовать контекст этого объекта.

Чтобы было понятнее, начнем с примера. Есть функция, которая работает таким образом:

{% highlight javascript %}
function getName() {
  const name = this.name
  console.log(name)
}
{% endhighlight %}

Что будет, если вызвать эту функцию таким образом?

{% highlight javascript %}
getName()
{% endhighlight %}

Сложный вопрос, так как мы видим, что в теле функции используется ключевое слово this. Это - ссылка на текущий объект и на свойство name этого объекта. Что это за объект? Неизвестно. Все будет зависеть от того, где будет вызвана функция getName() на исполнение. Допустим, если вызвать функцию в консоли браузера, то парсер обратиться к глобальному объекту window и попробует найти у него свойство name. В итоге мы аверняка получил undefined, так как вряд ли у объекта window есть свойство name.

При помощи метода call можно "привязать" функцию getName() к любому объекту. Другими словами - привязать контекст функции getName() к контексту объекта. Как?

Допустим, у нас есть объект:

{% highlight javascript %}
const user1 = {
  name: 'Ivan',
  position: 'frontent developer',
  salary: 1200
}
{% endhighlight %}

Мы сделаем так:

{% highlight javascript %}
const result1 = getName.call(user1)
{% endhighlight %}

Что будет происходить здесь? В этом случае ключевое слово this (в теле функции getName) будет указывать на объект user1, у которого есть свойство name. Как результат - в константе result1 будет находиться значение Ivan.

Если создадим еще один объект:

{% highlight javascript %}
const user2 = {
  name: 'Joshua',
  position: 'ui designer',
  salary: 2200
}
{% endhighlight %}

И на нем вызовем функцию getName():

{% highlight javascript %}
const result2 = getName.call(user2)
{% endhighlight %}

Что будет? В этом случае функция getName будет ссылаться уже на объект user2! И в константе result2 уже будет значение свойства name объекта user2 - Joshua.

### call - более сложный вариант

Рассмотрим более сложный случай - когда фунция принимает аргумент(ы). Допустим, такая функция,

{% highlight javascript %}
function promote(position, salary) {
  this.salary = salary
  this.position = position
  return this.position + ' earns ' + this.salary + ' dollars'
}
{% endhighlight %}

И есть два объекта:

{% highlight javascript %}
const junior = {
  name: 'Fritz',
  position: 'junior developer',
  salary: 1000
}
const middle = {
  name: 'Max',
  position: 'middle developer',
  salary: 2000
}
const senior = {
  name: 'Manu',
  position: 'senior developer',
  salary: 3000
}
{% endhighlight %}

Вызовем функцию promote() на каждом из объектов:

{% highlight javascript %}
const result1 = promote.call(junior, 'super junior developer', 1200)
const result2 = promote.call(middle, 'super middle developer', 2200)
const result3 = promote.call(senior, 'super senior developer', 3200)
{% endhighlight %}

Что здесь произойдет? При каждом вызове функции promote() у нее будет разный контекст выполнения - объект junior, middle или senior. И обращаться функция promote() будет каждый раз к свойствам разных объектов - junior, middle или senior. Соответственно, результат тоже будет разным:

{% highlight javascript %}
super junior developer earns 1200 dollars
super middle developer earns 2200 dollars
super senior developer earns 3200 dollars
{% endhighlight %}

## Метод apply

Метод apply очень похож на метод call, за одним исключением. Аргументы метод apply принимает в виде массива, а не в виде списка, как метод call.

Проиллюстририруем пример - переделаем вызов функции promote() при помощи метода apply:

{% highlight javascript %}
const resultA = promote.apply(junior, [ 'super junior developer', 1200 ])
const resultB = promote.apply(middle, [ 'super middle developer', 2200 ])
const resultC = promote.apply(senior, [ 'super senior developer', 3200 ])
{% endhighlight %}

Видим, что аргументы передаются в виде массива, но результат будет тот же. Как часто упоминается в различных туториалах, это сделано для того, чтобы передать неограниченное и заранее неизвестное количество аргументов.

## Метод bind

Этот метод похож на предыдущие два - call и apply. Однако, у него есть два отличия - этот метод появился в стандарте ES5; и второе отличие - этот метод позволяет выполнить отложенный вызов функции.

То есть - метод call или apply вызываются на исполнение сразу, и результат их работы мы получаем сразу.



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
