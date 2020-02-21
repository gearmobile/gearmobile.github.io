---
title: "Tslint - включить поддержку tabs"
layout: post
categories: ts
tags: [tabs, ts, lint]
share: true
---

По умолчанию при scaffolding нового проекта в настройках используется пробелы (spaces) для задания отступов (indent). Но иногда требования бывают такими, что нужно использовать tabs вместо spaces.
Для этого нужно изменить настройки проекта в некоторых местах.

Файл _tslint.json_:

{% highlight typescript %}
...
"indent": [true, "tabs", 2] -> enable tabs
"indent": [true, "spaces", 2] -> enable spaces
...
{% endhighlight %}

Файл _.prettierrc_ - если используется Prettier в проекте:

{% highlight typescript %}
...
"useTabs": true -> enable tabs
...
{% endhighlight %}

Файл _.editorconfig_:

{% highlight typescript %}
[*]
indent_style = tabs -> enable tabs
...
{% endhighlight %}

---
