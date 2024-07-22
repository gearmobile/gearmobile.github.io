---
title: "ChangeDetectionStrategy.OnPush по умолчанию"
layout: post
categories: Development
tags: [angular, changeDetection, OnPush]
share: true
---

Настроить в Angular ChangeDetectionStrategy.OnPush в качестве стратегии по умолчанию:

{% highlight bash %}
ng config schematics.@schematics/angular.component.changeDetection OnPush
{% endhighlight %}