---
title: "Tslint - включить поддержку tabs"
layout: post
categories: ts
tags: [tabs, ts, lint]
share: true
---

По умолчанию при _scaffolding_ нового Angular-проекта в настройках используется пробелы _spaces_ для задания отступов _indent_. Но иногда требования компании\команды бывают такими, что нужно использовать _tabs_ вместо _spaces_.

Для этого нужно изменить настройки проекта в некоторых местах.

Файл _tslint.json_:

{% highlight typescript %}
...
"indent": [true, "tabs", 2]
"indent": [true, "spaces", 2]
...
{% endhighlight %}

Файл _.prettierrc_ - если используется Prettier в проекте:

{% highlight typescript %}
...
"useTabs": true
...
{% endhighlight %}

Файл _.editorconfig_:

{% highlight typescript %}
[*]
indent_style = tabs
...
{% endhighlight %}

---
