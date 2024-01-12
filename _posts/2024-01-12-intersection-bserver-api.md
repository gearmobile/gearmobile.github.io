---
title: "Что такое Intersection Observer API"
layout: post
categories: Development
tags: [typescript, provider]
share: true
---

## Intersection Observer API

**Itersection Observer API** - это API браузера, позволяющий наблюдать за пересечениями элементов. Например, карточка оплаты на странице оплаты по мере прокрутки страницы пересекает верхнюю и/или нижнюю часть основного контента страницы. Данное API браузера позволяет отследить эти пересечения. В проекте для упрощения работы с ним используется пакет https://www.npmjs.com/package/@ng-web-apis/intersection-observer

### Что требуется знать для работы с этой библиотекой

Использование **IntersectionObserverAPI** можно конфигурировать. Настраиваемые параметры:

- **root** - тот элемент, который будет отслеживаться браузером. Если не указан, по дефолту считается viewport'ом браузерного окна.
- **rootMargin** - смещение прямоугольника root-элемента. С помощью этого параметра можно сжать root-элемент. Дефолтное значение _0px 0px 0px 0px_.
- **thresholds** - массив значений, при которых должны срабатывать callback-пересечения. Указывается в процентах (_0.15 - 15%_, _.5 - 50%_: означает, что при пересечении целевого элемента вверх или вниз от root-элемента при 15% или 50% будет срабатывать событие callback'а). **Важно**: событие происходит при **примерном** пересечении целевого элемента границ root-элемента.

### При использовании провайдеров используются следующие токены

1. **INTERSECTION_THRESHOLD**

Использование:

{% highlight typescript %}
{
    provide: INTERSECTION_THRESHOLD,
    useValue: 0.5 // => В качестве значения можно указать и массив чисел [0, 0.5, 1]
}
{% endhighlight %}

2. **INTERSECTION_ROOT_MARGIN**

Использование:

{% highlight typescript %}
{
    provide: INTERSECTION_ROOT_MARGIN,
    useValue: '0px 0px 0px 0px' // значение указывается в любом стиле CSS (all), (horizontal, vertical), (top, left, bottom, right)
}
{% endhighlight %}

3. **IntersectionObserverService**

Данный сервис унаследован _Observable<IntersectionObserverEntry[]>_ и является основной единицей использования при отслеживании пересечения элементов:

{% highlight typescript %}
@Component({
selector: 'my-component',
providers: [
    SgmDestroyService,
    IntersectionObserverService,
    {
        provide: INTERSECTION_THRESHOLD,
        useValue: 0.5,
    },
    {
        provide: INTERSECTION_ROOT_MARGIN,
        useValue: '10px',
    },
],
})

export class MyComponent {
    constructor(
        private _destroy$: SgmDestroyService,
        @Inject(IntersectionObserverService)
        entries$: IntersectionObserverService
    ) {
        entries$.pipe(
            takeUntil(this._destroy$)
        ).subscribe(entries => {
            console.log(entries);
        });
    }
}
{% endhighlight %}

**Важно**: если элемент при создании содержит высоту, равную _0px_ - следует оформлять подписку на _entries$_ в _ngAfterViewInit_.

Объект _IntersectionObserverEntry_ поставляется из _entries$_ и имеет следующие свойства:

- _boundingClientRect_ - Возвращает прямоугольник границ таргет-элемента в виде. Границы вычисляются, как описано в документации для Element.getBoundingClientRect().

- _intersectionRatio_ - Возвращает отношение _intersectionRect_ к _boundingClientRect_.

- _intersectionRect_ - Возвращает границы, представляющие видимую область таргет-элемента.

- _isIntersecting_ - Булево значение, которое является истинным, если таргет элемент пересекается с root-элементом. Если это значение истинно, то запись IntersectionObserverEntry описывает переход в состояние пересечения; если оно ложно, то переход происходит от пересечения к непересечению.

- _rootBounds_ - Возвращает границы для root - элемента.

- _target_ - Таргет - элемент.

- _time_ - Указывает время, в которое было зарегистрировано пересечение, относительно начала отсчета времени жизни IntersectionObserver.
