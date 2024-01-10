---
title: "Git - смена репозитория для загрузки"
layout: post
categories: git
tags: [github, set-url]
share: true
---

> Продолжаю изучение темы Git и GitHub. На повестке дня стоит вопрос - каким образом можно изменить ссылку существующего репозитория?

Нет - не так! Попробую зайти с другой стороны и сказать иначе. Имеется готовый репозиторий Template, размещенный на сервере GitHub. Этот репозиторий является шаблоном (template starter) при создании разнообразных проектов. Нечто похожим на известный [HTML5 Boilerplate][1].

Репозиторий Template клонируется на локальную машину с именем разрабатываемого проекта, такой командой:

{% highlight bash %}
$ git clone https://github.com/gearmobile/template.git project
{% endhighlight %}

Затем в созданном репозитории Project разрабатывается требуемый проект.

Но есть одно НО - необходимо преобразовать видоизмененный репозиторий Project в отдельный, самостоятельный репозиторий. Конечно, по большому счету, это уже и есть отдельный, самостоятельный репозиторий.

Но вот ссылка у репозитория Project указывает на оригинал - репозиторий Template. И если произвести _push_ на GitHub, то произойдет обновление репозитория Template.

А этого крайне нежелательно допустить, так как этот репозиторий является стартовым, чистым листом для всех новых проектов!

У меня же стоит такая задача - скопировать стартовый репозиторий  Template на локальную машину, преобразовать его в конкретный проект, вновь залить на GitHub уже как самостоятельный репозиторий с именем проекта в качестве имени репозитория. Как поступить?

Можно решить вопрос несколькими способами. Ниже приведу пару из них - самых простых и доступных для моего понимания вечного newbie в Git\GitHub. Может быть, по мере освоения темы дополню статью более универсальным и грамотным способом.

## Правка config

У клонированного на локальную машину репозитория ссылка на его удаленный оригинал размещена в конфигурационном файле _config_ по пути _.git/config_, в секции _[remote "origin"]_, в переменной с именем _url_:

{% highlight bash %}
$ cat .git/config

[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
  ignorecase = true
  precomposeunicode = true

[remote "origin"]
  url = https://github.com/gearmobile/template.git
  fetch = +refs/heads/*:refs/remotes/origin/*

[branch "master"]
  remote = origin
  merge = refs/heads/master
{% endhighlight %}

Поэтому в локальном репозитории Project можно просто изменить эту ссылку с помощью любого текстового редактора.

Отредактирую файл _config_ и изменю в нем ссылку с:

{% highlight bash %}
https://github.com/gearmobile/template.git
{% endhighlight %}

... на:

{% highlight bash %}
https://github.com/gearmobile/project.git
{% endhighlight %}

... где последняя - это ссылка на новый пустой репозиторий Project, который я создал на GitHub.

Теперь конфигурационный файл _config_ для локального репозитория Project будет выглядеть таким образом (обратить внимание на переменную _url_):

{% highlight bash %}
$ cat .git/config

[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
  ignorecase = true
  precomposeunicode = true

[remote "origin"]
  url = https://github.com/gearmobile/project.git
  fetch = +refs/heads/*:refs/remotes/origin/*

[branch "master"]
  remote = origin
  merge = refs/heads/master
{% endhighlight %}

Все - теперь локальный репозиторий Project является абсолютно самостоятельным и уникальным репозиторием, связанным ссылкой со своей удаленной копией на сервере GitHub.

Осталось только сделать _push_, чтобы залить на GitHub. Правда, здесь придется воспользоваться ключом _-f_ (как это описано в предыдущей статье [Откат коммитов на GitHub]({% post_url 2015-04-07-github-fallback-commit %})):

{% highlight bash %}
$ git push -f
{% endhighlight %}

## Команда set-url

Второй способ практически идентичен предыдущему за тем лишь исключением, что он более правильный, так как для изменения url-адреса репозитория используется предназначенная для этого консольная команда Git - _set-url_.

Точно также создаю на локальной машине копию Another Project удаленного репозитория Template:

{% highlight bash %}
$ git clone https://github.com/gearmobile/template.git another-project
{% endhighlight %}

Ссылка в новом репозитории Another-Project все также указывает на свой оригинал - репозиторий Template:

{% highlight bash %}
$ cat .git/config

[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
  ignorecase = true
  precomposeunicode = true

[remote "origin"]
  url = https://github.com/gearmobile/template.git
  fetch = +refs/heads/*:refs/remotes/origin/*

[branch "master"]
  remote = origin
  merge = refs/heads/master
{% endhighlight %}

Создаю на GitHub новый репозиторий Another-Project, который будет удаленной копией локального (уже существующего) репозитория Another-Project. И изменяю ссылку на вновь созданный удаленный репозиторий Another-Project:

{% highlight bash %}
$ git remote set-url origin https://github.com/gearmobile/another-project.git
{% endhighlight %}

Проверяю, изменилась ли ссылка в конфигурационном файле _config_ (переменная _url_):

{% highlight bash %}
$ cat .git/config

[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
  ignorecase = true
  precomposeunicode = true

[remote "origin"]
  url = https://github.com/gearmobile/another-project.git
  fetch = +refs/heads/*:refs/remotes/origin/*

[branch "master"]
  remote = origin
  merge = refs/heads/master
{% endhighlight %}

Да, ссылка была успешно изменена на новый удаленный репозиторий Another-Project. Можно вносить изменения и выполнять _push_ на GitHub.

## Небольшое заключение

Преимущество двух описанных выше способ в том, что не теряется история коммитов.

На этом пока все.

---

[1]: https://html5boilerplate.com/ "HTML5 Boilerplate"
