---
title: "RxJs - способы отписаться"
layout: post
categories: Development
tags: [rxjs, unsubscibe]
share: true
---

### Императивный способ отписки

{% highlight typescript %}
export class AwesomeComponent implements OnInit, OnDestroy {
  private readonly service = inject(TodoService);
  private subscription!: Subscription;

  public todos: Todo[] = [];

  ngOnInit(): void {
    this.subscription = toObservable(this.service.todos).subscribe(
      (todos) => (this.todos = todos)
    );
  }

  ngOnDestroy(): void {
    this.subscription?.unsubscribe();
  }
}
{% endhighlight %}

### Декларативный способ отписки

{% highlight typescript %}
export class AwesomeAnotherComponent {
  private readonly service = inject(TodoService);
  private destroy$ = new Subject<void>();

  public todos: Todo[] = [];

  ngOnInit(): void {
    toObservable(this.service.todos)
      .pipe(takeUntil(this.destroy$))
      .subscribe((todos) => (this.todos = todos));
  }

  ngOnDestroy(): void {
    this.destroy$.next();
    this.destroy$.complete();
  }
}
{% endhighlight %}

### async

Тут особо говорить нечего - и так все понятно.

### Оператор takeUntilDestroyed

takeUntilDestroyed - более новый споосб отписки в RxJs. Материалы по теме:

- [Use takeUntilDestroyed to Unsubscribe from Angular's Observables](https://youtu.be/Cr4NRfZxaP0?si=gUE9LJ0SVXVlub-0)
- [Getting to Know the takeUntilDestroyed Operator in Angular](https://netbasal.com/getting-to-know-the-takeuntildestroyed-operator-in-angular-d965b7263856)
- [takeUntilDestroyed Angular New Way to Unsubscribe](https://monsterlessons-academy.com/posts/take-until-destroyed-angular-new-way-to-unsubscribe)