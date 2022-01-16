---
title: "Prisma - колонки выборочно"
layout: post
categories: Prisma
tags: [prisma, orm]
share: true
---

## Как в Prisma - получать колоноки выборочно

Самый простой пример получения **всех** данных (колонок) из таблицы в базе данных - при помощи [Prisma][1] такой:

{% highlight typescript %}
const user = await prismaClient.users.findUnique({
    where:{
        id: userId
    }
})
{% endhighlight %}

... что является аналогом такой sql-команды, например:

{% highlight bash %}
SELECT * FROM users AS u WHERE u.user_id = 2;
{% endhighlight %}

Но что, если нужно получить в Prisma - только определенный набор колонок? При помощи sql-команды это делается просто:

{% highlight bash %}
SELECT u.user_name, u.user_gender, u.user_birthday FROM users AS u WHERE u.user_id = 2;
{% endhighlight %}

Как же выполнить точно такой же запрос - в Prisma? Это можно сделать при помощи дополнительной опции [select][2]. В принципе - в оф. доке все описано - "... select defines which fields are included in the object that Prisma Client returns ..." - "... select определяет, какие поля будут включены в объект, который возвращает Prisma Client ...".

И вот пример, как это можно сделать:

{% highlight typescript %}
const user = await prismaClient.users.findUnique({
    select:{
        user_name: true,
        user_gender: true,
        user_birthday: true,
    },
    where:{
        id: userId
    }
})
{% endhighlight %}

***
[1]: https://www.prisma.io/ "Next-generation Node.js and TypeScript ORM"
[2]: https://www.prisma.io/docs/reference/api-reference/prisma-client-reference#model-query-options "Model query options"
