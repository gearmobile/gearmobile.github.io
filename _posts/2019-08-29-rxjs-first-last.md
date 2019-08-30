---
title: 'RxJs - first и last'
layout: post
categories: rxjs
tags: [rxjs, first, last]
share: true
---

### Метод first()

Принимает на вход поток событий и возвращает первое событие этого потока, после чего завершает свое выполнение. В качестве аргумента может принимать функцию фильтрации.

Подключение _first()_ - _import { first } 'rxjs/operators'_

Пример - перехватываем только первый клик на документе, все последующие - игнорируем:

{% highlight typescript %}
import { fromEvent } from 'fxjs'
import { first } from 'rxjs/operators'

const clicks = fromEvent(document, 'click);
const click = clicks.pipe(first());

click.subscribe(response => console.log(response))
{% endhighlight %}

Более интересный пример - возвращаем первое событие потока, которое удовлетворяет условию; после чего прекращаем работу:

{% highlight typescript %}
import { from } from 'rxjs';
import { first } from 'rxjs/operators'

const source = from([1,2,3,4,5,6,7]);
const result = source.pipe(first(el => el === 3));
result.subscribe(response => console.log(response)); // 3
{% endhighlight %}

### Метод last()

Противоположность методу _first()_; принимает на вход поток событий и возвращает последнее событие этого потока; после чего прекращает свою работу.

Хорошие примеры использования _last()_ приведены здесь - [<https://www.learnrxjs.io/operators/filtering/last.html>](Learn RxJS - last).

---

Ссылки:

- [<https://rxjs.dev/api/operators/first>](RxJs - first)
- [<https://rxjs.dev/api/operators/last>](RxJs - last)
- [<https://rxmarbles.com/#first>](RxJS Marbles - first)
- [<https://rxmarbles.com/#last>](RxJS Marbles - last)
