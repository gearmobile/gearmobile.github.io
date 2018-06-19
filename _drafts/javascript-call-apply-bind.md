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
  return this.position + ' earns ' + this.salary + 'dollars'
}
{% endhighlight %}

И есть два объекта:

{% highlight javascript %}
const
{% endhighlight %}


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
