---
title: "Flattering operators"
layout: post
categories: Development
tags: [rxjs, switchmap, mergemap, concatmap, exhaustmap]
share: true
---

Для управления конкурентностью при общении с api.

### mergeMap

... будет триггерить все запросы, конкурентно создавая гонку.

### exhaustMap

... будет игнорировать все запросы, пока не завершится активный запросы.

### concatMap

... будет создавать очередь запросов, где будет только один запрос активный, а остальные запросы будут ждать своей очереди.

### switchMap

... отменит предыдущий запрос, гарантируя один активный запрос.

### Наиболее популярные кейсы на практике для их использования

В кейсе формы создания какой-то сущности с последующим редиректом, _exhaustMap_, чтобы не отправлять тысячу запросов, если юзер будет кликать по кнопке, а она не дизейблится

В кейсе, когда у нас есть поиск и нам необходимо отправлять запрос на бэк, лучше подойдет _switchMap_, так как он будет отменять предыдущий запрос, если он не успел завершится и отправлять новый, с актуальными данными

Если мы патчим какую-то сущность, тогда в большинстве случаев лучше будет concatMap, чтобы дожидаться когда бэк пропатчит данные в первый раз, а потом отправлять второй запрос, чтобы сохранять консистентность данных (конечно это больше задача бэкенда, но иногда легче это делать на фронте, что не очень Юзер Френдли конечно)

В случаях где порядок выполнения запросов не важен, можно использовать mergeMap, он никого не ждет и с каждым новым значением в основном потоке, открывает новую подписку, но в данном случае сложнее следить за текущим состоянием (например loading)

### Разбор примера

{% highlight typescript %}
export const productsLoadEffect = createEffect(
  (actions$ = inject(Actions), productsService = inject(ProductsService)) =>
    actions$.pipe(
      ofType(ProductsActions.loadProducts),
      exhaustMap(() =>
        productsService.getAll().pipe(
          map((products) =>
            ProductsAPIActions.productsLoadedSuccess({ products }),
          ),
          catchError((error: Error) =>
            of(
              ProductsAPIActions.productsLoadedFail({ message: error.message }),
            ),
          ),
        ),
      ),
    ),
  { functional: true },
);

export const productsAddEffect = createEffect(
  (actions$ = inject(Actions), productsService = inject(ProductsService)) =>
    actions$.pipe(
      ofType(ProductsActions.addProduct),
      mergeMap(({ product }) =>
        productsService.add(product).pipe(
          map((product) => ProductsAPIActions.addProductSuccess({ product })),
          catchError((error: Error) =>
            of(ProductsAPIActions.addProductFail({ message: error.message })),
          ),
        ),
      ),
    ),
  { functional: true },
);

export const productsUpdateEffect = createEffect(
  (actions$ = inject(Actions), productsService = inject(ProductsService)) =>
    actions$.pipe(
      ofType(ProductsActions.updateProduct),
      concatMap(({ product }) =>
        productsService.update(product).pipe(
          map((product) =>
            ProductsAPIActions.updateProductSuccess({ product }),
          ),
          catchError((error: Error) =>
            of(
              ProductsAPIActions.updateProductFail({ message: error.message }),
            ),
          ),
        ),
      ),
    ),
  { functional: true },
);

export const productsRemoveEffect = createEffect(
  (actions$ = inject(Actions), productsService = inject(ProductsService)) =>
    actions$.pipe(
      ofType(ProductsActions.removeProduct),
      mergeMap(({ id }) =>
        productsService.delete(id).pipe(
          map((product) => ProductsAPIActions.removeProductSuccess({ id })),
          catchError((error: Error) =>
            of(
              ProductsAPIActions.removeProductFail({ message: error.message }),
            ),
          ),
        ),
      ),
    ),
  { functional: true },
);
{% endhighlight %}

1. так как нет никаких параметров (фильтры, сортировка, пагинация), то нет смысла делать несколько запросов для загрузки одних и тех же данных
2. Добавление новых продуктов не требует жесткого порядка, нам без разницы какой запрос на добавление нового продукта выполнится раньше, первый или второй, главное чтобы они добавились, поэтому mergeMap
3. Для сохранение консистентности данных, для апдейта продукта используется concatMap, на самом деле реализация здесь не очень хорошая, так как concatMap будет использоваться для всех продуктов, а не для единственного, но если мы будем обновлять один и тот же продукт, существует вероятность, что второй запрос обработается раньше и данные из первого запроса это перетрут (так как на сервере конкурентные потоки и если ими плохо управляют, то такая ситуация вполне возможна), соответственно понимаем, что порядок в данном случае важен, поэтому используется concatMap
4. Ну как и во втором пункте, при удалении продуктов, нам не важно в каком порядке выполнятся запросы на удаление продуктов, поэтому можем пускать их в параллель, поэтому mergeMap

Если бы в первом случае была динамическая фильтрация или сортировка, то switchMap был бы лучшим решением
Если бы была пагинация в виде lazy loading, то ее обычно выносят в отдельный эффект и используют concatMap так как в данном случае порядок тоже важен (в случае с сортировкой)

### Ссылки по теме

- [RxJS: switchMap, concatMap, mergeMap, exhaustMap - как работают](https://youtu.be/O8Pr47VyfDQ?si=uTR_QKQ6DklWAKgO)
- [RxJs switchMap vs mergeMap - Intro to Flattening Operators](https://youtu.be/qYdKmYp95Jg?si=ELlgVJ2KC7XrYr0H)
- [RxJs Operators - ExhaustMap vs concatMap](https://youtu.be/nh13_aPRQ0Q?si=sSXd87CmC1nVNZqa)