---
title: "MongoDB - документы"
layout: post
categories: mongodb
tags: [mongodb, linux]
share: true
---

![MongoDB]({{site.url}}/images/uploads/2017/05/mongodb-logo.jpg "MongoDB")

## Что такое document

Понятие документа - основа MongoDB. Недаром говорится, что MongoDB - документо-ориентированная система управления базами данных.

Document входит в состав collection и наполняет ее содержимым. Document - это обычный JSON-объект.

Если есть навык создания и работы с JSON-объектами, то уже можно создавать документы в MongoDB.

Простой пример документа в базе данных MongoDB:

{% highlight javascript %}
{
  "_id" : ObjectId("591f49970f7b726a5beb58af"),
  "name" : "Anna"
}
{% endhighlight %}

Стоит обратить внимание на ключ "_id" - этот ключ и значение ключа MongoDB автоматически генерирует для уникальной идентификации каждого документа в базе данных.

Чуть более сложный пример документа в MongoDB:

{% highlight javascript %}
{
	"_id" : ObjectId("591f49970f7b726a5beb58af"),
	"name" : "Anna",
	"surname" : "Tudor",
	"music" : [
		"country",
		"blues",
		"chill-out"
	],
	"age" : 18,
	"virgin" : true
}
{% endhighlight %}

В данном случае документ состоит из нескольких типов данных - Number, Array, String, Boolean.

Два документа в коллекции canada базы данных users:

{% highlight javascript %}
{
	"_id" : ObjectId("591f49970f7b726a5beb58af"),
	"name" : "Anna",
	"surname" : "Tudor",
	"music" : [
		"country",
		"blues",
		"chill-out"
	],
	"age" : 18,
	"virgin" : true
}
{
	"_id" : ObjectId("591f4eaf02ed4d6e1d81bc97"),
	"name" : "Leanne Graham",
	"username" : "Bret",
	"email" : "Sincere@april.biz",
	"address" : {
		"street" : "Kulas Light",
		"suite" : "Apt. 556",
		"city" : "Gwenborough",
		"zipcode" : "92998-3874",
		"geo" : {
			"lat" : "-37.3159",
			"lng" : "81.1496"
		}
	},
	"phone" : "1-770-736-8031 x56442",
	"website" : "hildegard.org"
}
{% endhighlight %}

Таких документов в коллекции canada может быть сколько угодно.

Вот в принципе и все, что нужно знать о документах в MongoDB.

На этом все.

***
