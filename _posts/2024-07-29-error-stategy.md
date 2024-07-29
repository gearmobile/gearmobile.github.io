---
title: "RxJs - стратегии обработки ошибок"
layout: post
categories: Development
tags: [rxjs, error, strategy]
share: true
---

### Стратегия замены (подмены)

Самый простой вариант - это стратегия замены:

{% highlight typescript %}
const stream$ = from([1, 2, 3, 'text', 4, 5]);
stream$
  .pipe(
    map((value) => {
      if (isNaN(value)) {
        throw new Error('Value is not a number!');
      }
      return parseInt(value);
    }),
    catchError((error) => of())
  )
  .subscribe({
    next: (value) => console.log('stream emit value', value),
    error: (error) => console.log('complete stream with error', error),
    complete: () => console.log('complete stream'),
  });
{% endhighlight %}

Что мы здесь имеем? Есть поток stream$, который обрабатывается в pipe при помощи операторов map и catchError. Эвенты последовательно приходят из потока в оператор map, внутри которого выполняется проверка при помощи isNaN. Для первых трех эвентов - 1, 2, 3 - условие if не выполняется, поэтому выполняется следующая операция parseInt(value) и преобразованный эвент - попадает в оператор catchError. Так как эвент не является ошибкой, то оператор catchError - пропускает эвент дальше; эвент попадает в подписку subscribe - конкретно в next.

Но вот для эвента со значением 'text' - все складывается по другому. Когда он попадает в оператор map, то выполняется условие if и оператор map возвращает вновь созданный эвент со сгенерированной ошибкой. Этот эвент попадает в оператор catchError и так как в данном эвенте содержится ошибка, то сработает callback-функция внутри оператора catchError, которая вернет как результат - новый поток of(). И этот поток - подменит собой поток stream$, в результате subscribe переподпишется на новый поток of(). Этот новый поток не эммитит эвентов, поэтому он сразу завершает свою работу, и в subscribe сработает callback-функция для случая complete.

Стоит обратить внимание, что в данном примере случай error внутри subscribe не сработает, так как обработка ошибки выполняется внутри потока pipe.

### Стратегия перенаправления

Чуть более усложеннный вариант предыдущей стратегии:

{% highlight typescript %}
const stream$ = from([1, 2, 3, 'text', 4, 5]);
stream$
  .pipe(
    map((value) => {
      if (isNaN(value)) {
        throw new Error('Value is not a number!');
      }
      return parseInt(value);
    }),
    catchError((error) => {
      return throwError(() => error);
    })
  )
  .subscribe({
    next: (value) => console.log('stream emit value', value),
    error: (error) => console.log('complete stream with error', error),
    complete: () => console.log('complete stream'),
  });
{% endhighlight %}

В данном случае мы имеем почти тот же случай, что и со стратегией подмены. Но - теперь callback-функция внутри оператора catchError - возвращает новый поток, который создан при помощи оператора throwError. То есть - в данном случае не происходит подмены данных в потоке, так как таже ошибка, что пришла из map и catchError, прокидывается дальше - только уже в другом потоке - в subscribe. Этот поток эммити ничего, кроме той самой ошибки, которую он получил от оператора throwError и аварийно завершает свою работу. Поэтому внутри переподписанного на него subscribe - сработает случай error.

Обратим внимание, что в данном случае внутри subscribe сработает случай error и вызовется на исполнение callback-функция, прописанная в нем.

### Стратегия повторных попыток

{% highlight typescript %}
const stream$ = from([1, 2, 3, 'text', 4, 5]);
stream$
  .pipe(
    map((value) => {
      if (isNaN(value)) {
        throw new Error('Value is not a number!');
      }
      return parseInt(value);
    }),
    retry(3),
    catchError((error) => {
      return throwError(() => error);
    })
  )
  .subscribe({
    next: (value) => console.log('stream emit value', value),
    error: (error) => console.log('complete stream with error', error),
    complete: () => console.log('complete stream'),
  });
{% endhighlight %}

Данная стратегия почти ничем не отличается от предыдущей стратегии перенаправления, за исключением использования оператора retry(). Как само собой понятно - при возникновении ошибки, которую обнаружит оператор catchError - мы заново перезапустим поток stream$. И таких попыток - в данном случае у нас будет три, то есть - поток перезапустится трижды. Если все три попытки оказались неудачными - выбросится новый поток при помощи оператора throwError и мы упадем в subscribe на случай error.

Есть более продвинутая версия оператора retry() - retryWhen(); можно гибко управлять моментом, когда должна запуститься новая попытка.