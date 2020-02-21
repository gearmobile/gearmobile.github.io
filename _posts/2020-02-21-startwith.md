---
title: "RxJs - startWith"
layout: post
categories: rxjs
tags: [startwith, rxjs]
share: true
---

Оператор _startWith_ - добавляет начальное значение в поток. То есть - в начало потока добавляется значение, которое передается в _startWith()_ как аргумент;
потом уже пойдут значения самого потока.

{% highlight typescript %}
import { interval } from 'rxjs'; 
import { startWith, take } from 'rxjs/operators';

const stream$ = interval(1000).pipe(startWith('welcome'), take(12));
stream$.subscribe(v => console.log(v));
{% endhighlight %}

Вывод будет таким:

{% highlight typescript %}
welcome
0
1
2
3
{% endhighlight %}

**Обратить внимание**! Выведен поток из **пяти** элементов! Начальное значение _welcome_ также учитывается оператором _take()_!

**Обратить внимание**! В данном случае от потока отписываться не нужно, так как оператор _take()_ сам отпишет (_complete()_) данный поток по завершении своей работы - особенность работы этого оператора _take()_!

---
