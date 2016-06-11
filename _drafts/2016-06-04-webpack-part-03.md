---
title: "webpack - / часть 3 /"
layout: post
categories: javascript
tags: [javascript, webpack]
share: true
---

Webpack в своем конфигурационном файле имеет настройку `watch: true` для **автосборки** модулей.

## webpack - автоматическая пересборка

Другими словами, это отслеживание изменений в фоновом режиме и автоматический перезапуск сборки, если какой-либо из файлов изменился:

{% highlight javascript %}
module.exports = {
  entry: './app.js',
  output: {
    filename: './build.js'
  },
  library: 'lib.js',
  watch: true
}
{% endhighlight %}

У настройки `watch` есть дополнительная опция `watchOptions`, одним из ключей которой является возможность **временной задержки** перед сборкой.

Это имеет смысл делать для того, чтобы дать время редактору кода (Sublime Text, WebStorm, Atom и любой другой) успеть сохранить изменения в файлах, которые были отредактированы.

Выглядит это таким образом:

{% highlight javascript %}
module.exports = {
  entry: './app.js',
  output: {
    filename: './build.js'
  },
  library: 'lib.js',
  watch: true,
  watchOptions: {
    aggregateTimeout: 100
  }
}
{% endhighlight %}

По умолчанию значение ключа `aggregateTimeout` равно 300, но можно поменять его на 100.

***
Здравые комментарии и замечания только приветствуются.