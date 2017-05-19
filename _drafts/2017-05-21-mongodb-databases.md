---
title: "MongoDB - управление базами данных"
layout: post
categories: mongodb
tags: [mongodb, linux]
share: true
---

## Создание базы данных

В двух предыдущих примерах научились устанавливать MongoDB. А также научились запускать и останавливать сервер MongoDB.

Настало время научиться создавать базы данных в MongoDB. Для этого нужно запустить и зайти в командную оболочку MongoDB.

Командная оболочка MongoDB носит имя mongo-shell и запускается в Linux одной командой:

{% highlight bash %}
mongo
{% endhighlight %}

В консоли отобразится сообщение и приглашение командной строки, говорящее о том, что мы находимся в командной оболочке MongoDB:

{% highlight bash %}
MongoDB shell version v3.4.4
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.4
...
> 
{% endhighlight %}

### Список баз данных

Увидеть список всех существующих баз данных можно командой:

{% highlight bash %}
show dbs
{% endhighlight %}

Вот список баз данных на момент установки MongoDB в системе Linux. Видно, что обе базы пустые:

{% highlight bash %}
> show dbs
admin  0.000GB
local  0.000GB
> 
{% endhighlight %}

### Создать базу данных

Команда создания новой базы данных в MongoDB очень проста:

{% highlight bash %}
use new_database
{% endhighlight %}

Например, создам новую базу данных по имени users:

{% highlight bash %}
> use users
switched to db users
> 
{% endhighlight %}

Команда user универсальная. Если база данных users уже существует, то будет выполнен перед в эту базу данных.

Если базы данных users не существует, то она будет создана и будет выполнен автоматический переход в эту базу данных.

Узнать имя текущей ( в которой на данный момент нахожусь ) базы данных можно командой:

{% highlight bash %}
db
{% endhighlight %}

В моем случае это будет так:

{% highlight bash %}
> db
users
>
{% endhighlight %}



{% highlight bash %}

{% endhighlight %}

## Удаление базы данных

// FILE NAME
// year-month-day-name
2013-01-15-archlinux-slim.md

// CODE SNIPPET
{% highlight javascript %}
// ...
{% endhighlight %}

// INLINE LINK
[link]( "link title")

// ANNOUNCEED LINK
[text][1]

// INLINE IMAGE
![image title]({{site.url}}/images/uploads/2015/08/image.jpg "image alt") 

***
[1]: http://speckyboy.com/2015/01/26/six-common-freelancing-myths/ "Six Common Freelancing Myths"
