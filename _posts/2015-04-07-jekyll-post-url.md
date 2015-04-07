---
title: "Внутренние ссылки на Jekyll"
layout: post
categories: jekyll
tags: [jekyll, post url]
share: true
---

> Вольный перевод небольшого раздела руководства по Jekyll.

Причина перевода и написания этого поста заключается в разъяснении вопроса добавления внутренних ссылок в постах сайта. То есть, ситуация - когда необходимо на странице сайта сделать ссылку на другую страницу этого же сайта.

## Тег post_url

Если необходимо добавить внутреннюю ссылку на странице сайта, то специальный тег `post_url` сгенерирует постоянную ссылку для указанной записи.

Синтаксис тега `post_url` выглядит таким образом:

{% highlight powershell %}
{% post_url 2010-07-21-name-of-post %}
{% endhighlight %}

Например, если на странице сайта добавить строку такого вида:

{% highlight powershell %}
{% post_url 2015-01-28-git-undoing-changes %}
{% endhighlight %}

... то эта строка преобразуется в ссылку на указанную запись сайта:

{% highlight powershell %}
/git/git-undoing-changes/
{% endhighlight %}

## Адрес поддиректории

Если записи на сайте организованы в поддиректории (по тематическому признаку), то путь к поддиректории необходимо добавить в адрес записи:

{% highlight powershell %}
{% post_url /webdevelopment/2015-01-16-rupture-breakpoints-stylus %}
{% endhighlight %}

При использовании тега `post_url` нет необходимости указывать расширение после имени файла с записью.

То есть, **не нужно** писать таким образом:

{% highlight powershell %}
{% post_url 2015-01-28-git-undoing-changes.md %}
{% endhighlight %}

... так как будет **достаточно указать** только имя файла записи:

{% highlight powershell %}
{% post_url 2015-01-28-git-undoing-changes %}
{% endhighlight %}

## Внутренняя ссылка

Создать внутренню ссылку в каком-либо посте сайта можно, используя такой синтаксис:

{% highlight powershell %}
[name_of_link]({% post_url 2010-07-21-name-of-post %}) 
{% endhighlight %}

Оригинал статьи расположен здесь - [Jekyll Post URL][1].

На этом все.

---

[1]: http://jekyllrb.com/docs/templates/#post-url "Post URL"
