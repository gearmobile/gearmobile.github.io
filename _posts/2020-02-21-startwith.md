---
title: "RxJs - startWith"
layout: post
categories: rxjs
tags: [startwith, rxjs]
share: true
---

Оператор `startWith` - добавляет начальное значение в поток. То есть - **в начало** потока добавляется значение, которое передается в `startWith()` как аргумент; потом уже - пойдут значения самого потока:

{% highlight typescript %}
import { interval, Observable } from 'rxjs'; 
import { startWith, take } from 'rxjs/operators';

const stream$: Observable<string | number> = interval(1000).pipe(startWith('welcome'), take(5));
stream$.subscribe((v: string | number) => console.log(v));
{% endhighlight %}

Вывод будет таким:

{% highlight typescript %}
welcome
0
1
2
3
{% endhighlight %}

**Обратить внимание**! Выведен поток из **пяти** элементов! Начальное значение `welcome` также учитывается оператором `take()`!

**Обратить внимание**! В данном случае от потока отписываться не нужно, так как оператор `take()` сам отпишет (`complete()`) данный поток по завершении своей работы - особенность работы этого оператора `take()`!

---
