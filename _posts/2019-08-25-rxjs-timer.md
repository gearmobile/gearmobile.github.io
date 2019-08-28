---
title: 'RxJs - timer'
layout: post
categories: rxjs
tags: [rxjs, timer]
share: true
---

Метод _timer_ позволяет создавать удобную возможность выполнять что-либо через заданный промежуток времени.

Синтаксис - _timer(delayTime, intervalTime)_.

Подключение - _import { timer } from 'rxjs';_

Пример кода:

{% highlight typescript %}
const source = timer(1000, 1000);
source.subscribe(data => console.log(data));
{% endhighlight %}

Здесь - с задержкой в одну секунду (и с интервалом также в одну секунду) в консоли пойдут значения - _0, 1, 2, 3, 4 и тд_. Если задержка не нужна, тогда можно поставить _0_:

{% highlight typescript %}
const source = timer(0, 1000);
source.subscribe(data => console.log(data));
{% endhighlight %}

Если нужно, чтобы _timer_ сработал как метод _setTimeout_ в классическом JavaScript, то нужно опустить второй аргумент - интервал выполнения:

{% highlight typescript %}
const source = timer(1000);
source.subscribe(data => console.log(data));
{% endhighlight %}

... в этом случае команда выполнится один раз - в задержкой в одну секунду.

Маленький практический пример использования _timer_:

{% highlight typescript %}
const source = timer(0, 1000);
source.subscribe(data => console.log(new Date()));
{% endhighlight %}

... это получился простейший таймер (_не обратного отсчета_). При использовании в Angular можно задействовать встроенный _pipe_ - _date: 'hh:mm:ss'_.

Интересная особенность - первым параметром можно задать дату запуска таймера - _signature: timer(initialDelay: number | Date, period: number, scheduler: Scheduler): Observable_.
Не пробовал, но надо взять на заметку.

На _timer_ очень похож метод _interval_, однако _timer_ можно рассматривать как расширенный и более гибкий вариант _interval_.

---

Ссылки:

- [<https://www.learnrxjs.io/operators/creation/timer.html>](Learn RxJs - timer)
- [<https://rxmarbles.com/#timer>](RxJS Marbles - timer)
