---
title: "MongoDB - управление коллекциями"
layout: post
categories: mongodb
tags: [mongodb, linux]
share: true
---

![MongoDB]({{site.url}}/images/uploads/2017/05/mongodb-logo.jpg "MongoDB")

## Что такое collection

В базах данных MongoDB данные объединяются в коллекции - collection. В одной базе данных может быть от одной до многих collections.

Смысл collection - объединять однотипные данные. То есть данные, котороые можно объединить по какому-либо признаку.

Например, в базе данных animals может быть две collections - cats и dogs. В коллекции cats хранятся все данные, о которых можно сказать - "это данные по кошкам". В коллекции dogs хранятся "все данные по собакам".

## Создание collection

В базе данных создать collection можно командой:

{% highlight bash %}
db.createCollection('NAME_COLLECTION')
{% endhighlight %}

Например, я создам две коллекции cats и dogs в базе данных animals. Для этого создам базу данных animals:

{% highlight bash %}
> use animals
switched to db animals
>
{% endhighlight %}

Создам коллекцию cats:

{% highlight bash %}
> db.createCollection('cats')
{ "ok" : 1 }
{% endhighlight %}

Создам коллекцию dogs:

{% highlight bash %}
> db.createCollection('dogs')
{ "ok" : 1 }
{% endhighlight %}

Посмотреть список существующих колекций базы данных можно командой:

{% highlight bash %}
show collections
{% endhighlight %}

Проверю, создались ли успешно коллеции cats и dogs в базе данных animals:

{% highlight bash %}
> show collections
cats
dogs
{% endhighlight %}

## Переименование collection

Операция переименования collection в MongoDB выполняется командой:

{% highlight bash %}
db.collection.renameCollection('NEW_NAME')
{% endhighlight %}

Например, я создал коллекцию bird в базе данных animals:

{% highlight bash %}
> db.createCollection('bird')
{ "ok" : 1 }
> show collections
bird
cats
dogs
>
{% endhighlight %}

... и хочу переименовать эту коллецию в birds:

{% highlight bash %}
> db.bird.renameCollection('birds')
{ "ok" : 1 }
> show collections
birds
cats
dogs
>
{% endhighlight %}

В результате коллекция bird успешно переименована в birds.

## Удаление collection

В MongoDB удаление коллекции выполняется командой:

{% highlight bash %}
db.COLLECTION_NAME.drop()
{% endhighlight %}

Например, я хочу удалить коллекцию birds из базы данных animals:

{% highlight bash %}
> db.birds.drop()
true
> show collections
cats
dogs
>
{% endhighlight %}

Коллекция birds успешно удалена из базы данных.

## Создание collection - автоматический способ

В MongoDB имеется способ автоматического создания collection - путем добавления документа в новую коллецию при помощи метода insert.

Например, коллекции insects в базе данных animals не существует. В будущую коллекцию insects я добавлю документ cockroach и тем самым автоматически создам коллецию insects:

{% highlight bash %}
> db.insects.insert({ name: 'cockroach' })
WriteResult({ "nInserted" : 1 })
> show collections
cats
dogs
insects
>
{% endhighlight %}

На этом все.
