---
title: "MongoDB - управление службой"
layout: post
categories: mongodb
tags: [linux, mongodb]
share: true
---

![MongoDB]({{site.url}}/images/uploads/2017/05/mongodb-logo.jpg "MongoDB")

## Управление MongoDB

MongoDB управляется так же, как и все остальные процессы в системе Linux.

### Запуск MongoDB

Сервер MongoDB запускается командой:

{% highlight bash %}
sudo service mongod start
{% endhighlight %}

Будет "висеть" в фоновом режиме и слушать команды на порту 27017.

### Остановка MongoDB

Остановить сервер MongoDB можно командой:

{% highlight bash %}
sudo service mongod stop
{% endhighlight %}

### Перезапуск MongoDB

Если нужно перезапустить сервер MongoDB, то это выполняется командой:

{% highlight bash %}
sudo service mongod restart
{% endhighlight %}

### Статус MongoDB

Посмотреть статус сервера MongoDB можно командой:

{% highlight bash %}
sudo service mongod status
{% endhighlight %}

Покажет, запущен сервер MongoDB и его текущее состояние.

***
[1]: https://www.mongodb.com "MongoDB"
[2]: https://docs.mongodb.com/master/tutorial/install-mongodb-on-ubuntu/ "Install MongoDB Community Edition on Ubuntu"

