---
title: "Angular - покрытие кода тестами"
layout: post
categories: angular
tags: [angular, test, coverage]
share: true
---

В Angular есть встроенный инструмент, который позволяет проверить, насколько покрыты тестами различные части проекта.

Запуск для генерации отчета покрытия тестами - команда:

{% highlight bash %}
ng test --watch=false --code-coverage
{% endhighlight %}

После выполнения команды в корне проекта будет создана директория _coverage_ - внутри нужно найти файл _index.html_, который нужно открыть в браузере. Отобразится страница с графиками покрытия различных частей тестами.

В конфигурационном файле _karma.conf_ можно настроить минимумы, допустимые в проекте для покрытия тестами его функциональных частей.

Для этого в файле нужно найти поле _coverageIstanbulReporter_ и дописать в нем ключ _thresholds_ со значениями:

{% highlight bash %}
coverageIstanbulReporter: {
  reports: [ 'html', 'lcovonly' ],
  fixWebpackSourcePaths: true,
  thresholds: {
    statements: 70,
    lines: 70,
    branches: 70,
    functions: 70
  }
}
{% endhighlight %}

... где 70 - это 70 процентов (%) - пороговое значение _threshold_ для каждой из частей проекта.

---
