---
title: "Angular - вставить внешний скрипт в компонент"
layout: post
categories: Angular
tags: [angular, javascript, script]
share: true
---

> Есть задача - вставить в template Angular-приложения внешний js-скрипт

## Пример номер один

Самый простой, правильный и надежный способ - **добавить скрипт в сборку** приложения.

Пошагово:

1. создать папку _scripts_ внутри директории _assets_ - _src/assets/scripts_
2. поместить js-скрипт внутрь созданной папки - _src/assets/scripts/awesome.js_
3. открыть файл _angular.json_ в корне проекта
4. добавить путь к скрипту в ключе _scripts_:

{% highlight json %}
{
  "projects": {
    "awesome-project": {
      "architect": 
            "scripts": ["src/assets/scripts/awesome.js,]
          },
          ....
}
{% endhighlight %}

## Пример номер два

Есть еще способ добавления - при помощи _Renderer2_:

{% highlight typescript %}
constructor(
  @Inject(DOCUMENT) private document: Document,
  private renderer2: Renderer2
) {}

ngOnInit(): void {
  const textScript = this.renderer2.createElement('script');
  textScript.src = 'https://code.jquery.com/jquery-3.3.1.slim.min.js';
  this.renderer2.appendChild(this.document.body, textScript);

  const srcScript = this.renderer2.createElement('script');
  srcScript.type = 'text/javascript';
  srcScript.text = `
    (function() {
      console.log('Hello from Siberia!')
    }());
  `;
  this.renderer2.appendChild(this.document.body, srcScript);
}
{% endhighlight %}

Пробовал этот способ - работает; но в консоли браузера появляется ошибка о необъявленной переменной X; отказался от этого способа.

## Итог

Мне с первого раза помог **способ номер один**.