---
title: "MongoDB - создание документа"
layout: post
categories: mongodb
tags: [mongodb, linux]
share: true
---

![MongoDB]({{site.url}}/images/uploads/2017/05/mongodb-logo.jpg "MongoDB")

Приступили к самому основному - операциям создания, чтения, изменения и удаления документов в MongoDB.

Аббревиатура для этих четырех операций - CRUD ( Create, Read, Update, Delete ).

В этом обзоре будет рассмотрен процесс создания документа - Create.

Два основных метода для создания нового документа в коллекции - метод insert и метод save.

## Метод insert()

Команда создания нового документа в коллекции выглядит так:

{% highlight bash %}
db.COLLECTION_NAME.insert(document)
{% endhighlight %}

COLLECTION_NAME - это имя коллекции, в которой будет создаваться новый документ. document - это JavaScript-объект.

Создам новый документ в коллекции customers базы данных users. Для этого перейду в эту базу данных:

{% highlight bash %}
> use users
switched to db users
{% endhighlight %}

Создам коллецию customers в базе данных users:

{% highlight bash %}
> db.createCollection('customers')
{ "ok" : 1 }
{% endhighlight %}

Создам в коллекции customers новый документ. Можно использовать как одинарные, так и двойные кавычки - дело вкуса:

{% highlight bash %}
> db.customers.insert( { name: 'Leanne Graham', username: 'Bret', email: 'sincere@april.biz' } )
WriteResult({ "nInserted" : 1 })
{% endhighlight %}

MongoDB выдает отчет о выполнении команды в строке:

{% highlight bash %}
...
WriteResult({ "nInserted" : 1 })
{% endhighlight %}

Видно, что операция WriteResult успешно выполнилась - nInserted в значении true.

Как хорошо видно, создаваемый документ - это объект. Если нужно создать сразу несколько документов, то методу insert передается массив этих объектов:

{% highlight bash %}
> db.customers.insert( [ { name: 'Ervin Howell', username: 'Antonette', email: 'shanna@melissa.tv' }, { name: 'Clementine Bauch', username: 'Samantha', email: 'nathan@yesenia.net' } ] )
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 2,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
{% endhighlight %}

BulkWriteResult выдает подробную информацию о выполненных операциях. Видно, что была выполнена только операция создания документа - "nInserted" : 2.

### Просмотр списка документов

Вывести список созданных документов в коллекции customers можно при помощи метода .find():

{% highlight bash %}
> db.customers.find()
{ "_id" : ObjectId("59200cdc2bd83e7289a5cae4"), "name" : "Leanne Graham", "username" : "Bret", "email" : "sincere@april.biz" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae5"), "name" : "Ervin Howell", "username" : "Antonette", "email" : "shanna@melissa.tv" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae6"), "name" : "Clementine Bauch", "username" : "Samantha", "email" : "nathan@yesenia.net" }
>
{% endhighlight %}

Видно, что у каждого созданного мною документа есть ключ _id со значением ObjectId(). Этого ключа я не указывал при создании документа.

Все правильно - этот ключ и его значение MongoDB генерирует автоматически и присваивает каждому создаваемому документу. Таким образом MongoDB делает все документы уникальными - нет ни одного документа с одинаковым _id.

Можно сделать вывод метода .find() более читабельным, если подключить к нему по цепочке еще один метод - .pretty():

{% highlight bash %}
> db.customers.find().pretty()
{
	"_id" : ObjectId("59200cdc2bd83e7289a5cae4"),
	"name" : "Leanne Graham",
	"username" : "Bret",
	"email" : "sincere@april.biz"
}
{
	"_id" : ObjectId("59200e3b2bd83e7289a5cae5"),
	"name" : "Ervin Howell",
	"username" : "Antonette",
	"email" : "shanna@melissa.tv"
}
{
	"_id" : ObjectId("59200e3b2bd83e7289a5cae6"),
	"name" : "Clementine Bauch",
	"username" : "Samantha",
	"email" : "nathan@yesenia.net"
}
>
{% endhighlight %}

## Метод save()

С помощью метода save() также можно создавать новый документ в коллекции. Создам еще один документ:

{% highlight bash %}
> db.customers.save( { name: 'Patricia Lebsack', username: 'Karianne', email: 'julianne.conner@kory.org' } )
WriteResult({ "nInserted" : 1 })
{% endhighlight %}

Сообщение от MongoDB говорит мне, что операция была выполнена успешно. Посмотрю на результат:

{% highlight bash %}
> db.customers.find()
{ "_id" : ObjectId("59200cdc2bd83e7289a5cae4"), "name" : "Leanne Graham", "username" : "Bret", "email" : "sincere@april.biz" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae5"), "name" : "Ervin Howell", "username" : "Antonette", "email" : "shanna@melissa.tv" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae6"), "name" : "Clementine Bauch", "username" : "Samantha", "email" : "nathan@yesenia.net" }
{ "_id" : ObjectId("592013152bd83e7289a5cae7"), "name" : "Patricia Lebsack", "username" : "Karianne", "email" : "julianne.conner@kory.org" }
>
{% endhighlight %}

Отличие метода save() от метода insert() заключается в том, что если при создании документа будет передан ключ _id уже существующего документа, то существующий документ будет перезаписан новым.

Вот у меня создан документ:

{% highlight bash %}
> db.customers.save( { name: 'Chelsey Dietrich', username: 'kamren', email: 'Lucio_Hettinger@annie.ca' } )
WriteResult({ "nInserted" : 1 })
{% endhighlight %}

И он успешно добавлен в коллекцию customers с уникальным ключом "_id" : ObjectId("5920166b986c86064996f59e"):

{% highlight bash %}
> db.customers.find()
{ "_id" : ObjectId("59200cdc2bd83e7289a5cae4"), "name" : "Leanne Graham", "username" : "Bret", "email" : "sincere@april.biz" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae5"), "name" : "Ervin Howell", "username" : "Antonette", "email" : "shanna@melissa.tv" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae6"), "name" : "Clementine Bauch", "username" : "Samantha", "email" : "nathan@yesenia.net" }
{ "_id" : ObjectId("5920166b986c86064996f59e"), "name" : "Chelsey Dietrich", "username" : "kamren", "email" : "Lucio_Hettinger@annie.ca" }
> 
{% endhighlight %}

Теперь я создаю новый документ, но передаю в него существующую пару ключ-значение "_id" : ObjectId("5920166b986c86064996f59e"):

{% highlight bash %}
> db.customers.save( { "_id" : ObjectId("5920166b986c86064996f59e"), name: 'Chelsey Dietrich', username: 'chelsey', email: 'c.dietrich@gmail.com' } )
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
{% endhighlight %}

Смотрю результат:

{% highlight bash %}
> db.customers.find()
{ "_id" : ObjectId("59200cdc2bd83e7289a5cae4"), "name" : "Leanne Graham", "username" : "Bret", "email" : "sincere@april.biz" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae5"), "name" : "Ervin Howell", "username" : "Antonette", "email" : "shanna@melissa.tv" }
{ "_id" : ObjectId("59200e3b2bd83e7289a5cae6"), "name" : "Clementine Bauch", "username" : "Samantha", "email" : "nathan@yesenia.net" }
{ "_id" : ObjectId("5920166b986c86064996f59e"), "name" : "Chelsey Dietrich", "username" : "chelsey", "email" : "c.dietrich@gmail.com" }
>
{% endhighlight %}

... и вижу, что последний документ был полностью перезаписан. Вуаля.

На этом все.

***
