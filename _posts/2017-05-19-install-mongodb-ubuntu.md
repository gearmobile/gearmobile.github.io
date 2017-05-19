---
title: "MongoDB - установка на Ubuntu"
layout: post
categories: mongodb
tags: [linux, mongodb]
share: true
---

![MongoDB]({{site.url}}/images/uploads/2017/05/mongodb-logo.jpg "MongoDB")

## Что такое MongoDB

[MongoDB][1] — документо-ориентированная noSQL база данных. В этом ее главное отличие от более старых и распространенных реляционных баз данных.

MongoDB является моим первым опытом знакомства с базами данных. И скажу от себя - приятным и удачным опытом знакомства.

До этого момента все мои слабые попытки познакомиться с базами данных были неудачными. Слишком сложна и запутана для меня была система взаимосвязей между таблицами в реляционных базах данных.

MongoDB мне понравилась - она очень проста в работе и имеет понятный язык команд. Кто знаком с JavaScript \ JSON, практически не заметит того, что уже работает в MongoDB.

MongoDB "делится" а две части. Первая часть - сервер mongod, который запускается в операционной системе как обычная служба ( daemon ) и работает в фоновом режиме. Задача сервера - выполнение команд для управления базами данных.

Вторая часть - mongo-shell. Это командная оболочка MongoDB, которая имеет набор консольных команд для управления базами данных MongoDB. Аналогом mongo-shell можно назвать bash \ zsh в Linux - принцип тот же самый.

## Установка MongoDB

Процесс установки MongoDB в системе Linux очень простой. Ознакомиться с ним можно и нужно на странице официальной документации - [Install MongoDB Community Edition on с][2].

Здесь приведена русскоязычная краткая версия описания установки MongoDB в Ubuntu.

Пакета MongoDB нет в официальном репозитории Ubuntu. Поэтому необходимо вручную добавить MongoDB в систему. Сначала нужно импортировать публичный GPG-ключ:

{% highlight bash %}
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
{% endhighlight %}

Затем создать файл репозитория /etc/apt/sources.list.d/mongodb-org-3.4.list командой:

{% highlight bash %}
echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
{% endhighlight %}

Обновить индекс локальных пакетов:

{% highlight bash %}
sudo apt-get update
{% endhighlight %}

Устанавливается MongoDB командой:

{% highlight bash %}
sudo apt-get install -y mongodb-org
{% endhighlight %}

Первый запуск MongoDB:

{% highlight bash %}
sudo service mongod start
{% endhighlight %}

Проверить, успешно ли запустилась MongoDB:

{% highlight bash %}
less /var/log/mongodb/mongod.log
{% endhighlight %}

... в конце файла должна быть такая строка:

{% highlight bash %}
...
[thread1] waiting for connections on port 27017
{% endhighlight %}

Еще один способ проверить успешность запуска сервиса MongoDB:

{% highlight bash %}
sudo service mongod status
{% endhighlight %}

Вывод в консоли должен быть примерно таков:

{% highlight bash %}
● mongod.service - High-performance, schema-free document-oriented database
   Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset: enabled)
   Active: active (running) since Fri 2017-05-19 12:21:18 +03; 1min 53s ago
     Docs: https://docs.mongodb.org/manual
 Main PID: 14147 (mongod)
   CGroup: /system.slice/mongod.service
           └─14147 /usr/bin/mongod --quiet --config /etc/mongod.conf
{% endhighlight %}

... здесь важна строка:

{% highlight bash %}
...
Active: active (running) since Fri 2017-05-19 12:21:18 +03; 1min 53s ago
...
{% endhighlight %}

На этом установка и первый запуск MongoDB успешно завершен.

***
[1]: https://www.mongodb.com "MongoDB"
[2]: https://docs.mongodb.com/master/tutorial/install-mongodb-on-ubuntu/ "Install MongoDB Community Edition on Ubuntu"

