---
title: "TypeScript - размеченные объединения"
layout: post
categories: TypeScript
tags: [typescript, union types]
share: true
---

> Потзовательское объединение типов - что это и как можно использовать

Помимо объединения **примитивных** типов данных (например):

{% highlight typescript %}
type myType = number | string;
{% endhighlight %}

... в TypeScript можно делать и объединение **пользовательских** типов данных:

{% highlight typescript %}
interface Rectange {
  width: number,
  height: number
}

interface Circle {
  radius: number
}

type Shape = Rectange | Circle;
{% endhighlight %}

Более того, пользовательские типы можно **связать** между собой при помощи общего для всех типов поля:

{% highlight typescript %}
interface Rectange {
  width: number,
  height: number,
  type: 'rectange'
}

interface Circle {
  radius: number,
  type: 'circle'
}

type Shape = Rectange | Circle;
{% endhighlight %}

... здесь поле `type` - является таким связующим звеном; такое поле называется _дискриминантом_.

Прелесть такого объдинения типов заключается в том, что можно проверять значение этого поля и в зависимости от результата - выполнять нужное действие. Например, можно создать такую функцию `calcArea`:

{% highlight typescript %}
function calcArea(shape: Shape): number {
  const { type } = shape;

  switch(type) {
    case 'rectange':
      return shape.width * shape.height;
    case 'circle':
      return Math.round(Math.PI * shape.radius ** 2);
  }
}
{% endhighlight %}

... и тогда пример использования этой функции и обединенного типа будет таким:

{% highlight typescript %}
interface Rectange {
  width: number,
  height: number,
  type: 'rectange'
}

interface Circle {
  radius: number,
  type: 'circle'
}

type Shape = Rectange | Circle;

function calcArea(shape: Shape): number {
  const { type } = shape;

  switch(type) {
    case 'rectange':
      return shape.width * shape.height;
    case 'circle':
      return Math.round(Math.PI * shape.radius ** 2);
  }
}

const rectangle: Rectange = { width: 10, height: 10, type: 'rectange' };
const circle: Circle = { radius: 20, type: 'circle' };

console.log(calcArea(rectangle)); // => 100
console.log(calcArea(circle)); // => 1257
{% endhighlight %}

---