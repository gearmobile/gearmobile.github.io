---
title: "TypeScript - Union Type"
layout: post
categories: typescript
tags: [typescript, union type]
share: true
---

В TypeScript есть возможность объявлять переменную, которая может хранить в себе значения двух или нескольких типов данных.

Такая возможность называется - Объединение Типов (Union Type).

Давайте рассмотрим пример:

{% highlight typescript %}
let someVariable: string | string[];
someVariable = 'apple'; // => apple
someVariable = ['apple', 'tomato', 'mango']; // => ['apple', 'tomato', 'mango']
someVariable = 12; // => Type '12' is not assignable to type 'string | string[]'
{% endhighlight %}

Что мы сделали в коде выше? Мы объявили переменную _someVariable_ и указали, что эта переменная может хранить в себе значения только двух типов - строка (string) или же массив строк (string[]).

Присвоив переменной строку или же массив строк, мы не получим ошибки компиляции, так как это удовлетворяет условию - _string_ или _string[]_.

Но если присвоим переменной число _12_, то получим ошибку

{% highlight typescript %}
Type '12' is not assignable to type 'string | string[]'
{% endhighlight %}

... так как тип _number_ не объявлен в числе допустимых типов значений для переменной _someVariable_.

***
