---
title: "RxJs - pluck"
layout: post
categories: RxJs
tags: [rxjs, pluck]
share: true
---

Задача заметки - понять, что такое метод _pluck_.

Допустим, у нас есть _input_, на который мы подписаны и у которого забираем вводимое значение:

{% highlight typescript %}
import { fromEvent } from 'rxjs';

const input = document.querySelector('#text');
const course$ = fromEvent(input, 'input');

course$.subscribe(event => console.log(event.target.value));
{% endhighlight %}

Этот метод не совсем верный, так как в _subscribe_ мы должны выводить уже готовое значение. Поэтому можно использовать метод _map_ для промежуточной обработки получаемых из потока событий:

{% highlight typescript %}
import { fromEvent } from 'rxjs';
import { map } from 'rxjs/operators';

const input = document.querySelector('#text');
const course$ = fromEvent(input, 'input');

course$
  .pipe(map((event: InputEvent) => event.target.value))
  .subscribe((value: string) => console.log(value));
{% endhighlight %}

Но в RxJs есть специальный метод _pluck_, который упрошает выборку значения из нужного поля объекта:

{% highlight typescript %}
import { fromEvent } from 'rxjs';
import { pluck } from 'rxjs/operators';

const input = document.querySelector('#text');
const course$ = fromEvent(input, 'input');

course$
  .pipe(pluck('target', 'value'))
  .subscribe((value: string) => console.log(value));
{% endhighlight %}

То есть, мы знаем, что работает с объектом _event_, у которого есть поле _target_, у которого также есть поле _value_, значение которого нам нужно получить. Поэтому воссоздаем структуру объекта _event_ так - _pluck('target', 'value')_.

---
