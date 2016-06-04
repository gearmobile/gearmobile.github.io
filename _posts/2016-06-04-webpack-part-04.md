---
title: "webpack - / часть 4 /"
layout: post
categories: javascript
tags: [javascript, webpack]
share: true
---

Webpack поддерживает различные **режимы отладки**. Зачем нужен режим отладки и как его использовать - это возможность копаться не в результирующей "простыне" кода, а в исходном файле каждого из модулей в отдельности.

## webpack - sourcemaps

В браузере создается виртуальная файловая структура, состоящая из главного модуля и всех подключаемых в нему модулей. И при отладке какой-либо строки кода браузер "перебрасывает" в тот модуль, в котором эта строка находилась изначально.

Другими словами, не нужно рыться в большом `build.js`, а можно покопаться в маленьком `some-module.js`. Достоинство режима отладки - в его удобстве.

В конфигурационном файле режим отладки включается при помощи строки `devtool`:

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
  },
  // подключаем выбранный нами режим отладки
  devtool: 'cheap-inline-module-source-map'
}
{% endhighlight %}

Значениями строки могут быть любой из списка - [Webpack Devtool](http://webpack.github.io/docs/configuration.html#devtool "Webpack Devtool").

Более того, значения можно комбинировать. Например, превратить `source-map` в `cheap-inline-module-source-map`.

***
Здравые комментарии и замечания только приветствуются.