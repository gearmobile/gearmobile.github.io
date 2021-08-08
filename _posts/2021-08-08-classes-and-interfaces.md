---
title: "TypeScript - classes vs interfaces"
layout: post
categories: TypeScript
tags: [typescript, class, interface]
share: true
---

> Классы против интерфейсов в TypeScript - когда использовать, преимущества и недостатки

## Классы

В TypeScript можно использовать классы для создании пользовательских типов данных. Например, так:

{% highlight typescript %}
class Person {
  constructor(
    public name: string,
    public age: number
  ) {}
}

const person: Person = {
  name: 'John',
  age: 12
}
{% endhighlight %}

Однако, это не совсем правильный пример.

**Преимуществом** при использовании класса является тот факт, что можно создавать экземпляры этого класса:

{% highlight typescript %}
class Person {
  constructor(
    public name: string,
    public age: number
  ) {}
}

const person: Person = new Person('John', 12);
{% endhighlight %}

Еще одно **преимущество** использования класса в TypeScript - возможность использования оператора `instanceof`:

{% highlight typescript %}
class Person {
  constructor(
    public name: string,
    public age: number
  ) {}
}

const person: Person = new Person('John', 12);

if (person instanceof Person) {
  console.log('yes');
}
{% endhighlight %}

... в этом случае условие выполнится и проверка сработает, так как `person` является экземпляром класса `Person`.

**Недостаток** использования класса в TypeScript - при транспиляции в JavaScript в результирующем коде останется этот класс - или ввиде функции (ES5):

{% highlight javascript %}
var Person = /** @class */ (function () {
  function Person(name, age) {
    this.name = name;
    this.age = age;
  }
  return Person;
}());
var person = new Person('John', 12);
{% endhighlight %}

... или ввиде класса (ES6):

{% highlight javascript %}
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
const person = new Person('John', 12);
{% endhighlight %}

## Интерфейсы

Главное преимущество использования интерфейса в TypeScript - то, что в скомпилированном JS-коде не остается следов использования интерфейса; результирующий код - не утяжеляется:

{% highlight javascript %}
"use strict";
const person = { name: 'John', age: 12 };
if (person instanceof Person) {
  console.log('yes');
}
{% endhighlight %}

... однако, использовать оператор `instanceof` в данном случае уже не получится - будет ошибка `'Person' only refers to a type, but is being used as a value here`.