---
title: 'RxJs - take и takeLast'
layout: post
categories: rxjs
tags: [rxjs, take, takeLast]
share: true
---

Методы _take()_ и _takeLast()_ в общем очень схожи с методами _first()_ и _last()_. С тем лишь отличием, что первые два могут возвращать не просто - самое первое или самое последнее событие потока; они могут возвращать указанное количество событий.

### Метод take()

Подключение - _import { take } from 'rxjs/operators';_

Метод _take()_ принимает в качестве аргумента число - количество событий потока, которые нужно вернуть с момента старта потока.

Например:

{% highlight typescript %}
import { take } from 'rxjs/operators';
import { timer } from 'rxjs';

const source = timer(0, 1000);
const result = source.pipe(take(10));

result.subscribe(response => console.log(response));
{% endhighlight %}

... очевидно, что этот код вернет **первые десять** событий из потока _source_ -> _0,1,2,3,4,5,6,7,8,9_.

### Метод takeLast()

Подключение - _import { takeLast } from 'rxjs/operators';_

В противоположность методу _take()_, метод _takeLast()_ возвратит заданное количество **последних** событий потока.

Важный момент - метод _takeLast()_ вернет события только после того, как поток завершится.

Пример:

{% highlight typescript %}
import { takeLast } from 'rxjs/operators';
import { from } from 'rxjs';

const source = from([0,1,2,3,4,5,6,7,8,9]);
const result = source.pipe(takeLast(4));

result.subscribe(response => console.log(response));
{% endhighlight %}

... этот код вернет **последние четыре** события потока _source_ -> _6,7,8,9_.

---

Ссылки:

- [<https://reactive.how/take>](Reactive.how - take)
- [<https://rxmarbles.com/#take>](RxJS Marbles - take)
- [<https://rxmarbles.com/#takeLast>](RxJS Marbles - takeLast)
