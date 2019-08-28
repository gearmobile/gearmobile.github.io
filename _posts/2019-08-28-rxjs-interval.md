---
title: 'RxJs - interval'
layout: post
categories: rxjs
tags: [rxjs, timer]
share: true
---

Метод _interval_ является упрощенным вариантом метода _timer_.
Подключение - _import { interval } from 'rxjs';_

Синтаксис - _interval(intervalTime)_

**Пример кода**:

{% highlight typescript %}
const source = interval(1000);
source.subscribe(data => console.log(data));
{% endhighlight %}

... здесь в консоли появится серия _0,1,2,3 и тд_ - после задержки в одну секунду и затем с интервалом в одну секунду.

---

Ссылки:

- [](Learn RxJs - interval)
- [](RxJS Marbles - interval)
