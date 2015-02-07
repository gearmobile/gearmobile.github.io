---
title: 'GitHub и Git &#8211; создание и работа с репозиторием'
author: gearmobile
excerpt: Создание учетной записи на GitHub. Создание ssh-ключей под Linux Mint. Настройка авторизации Git с GtiHub с помощью ssh-ключей, созданных под Linux Mint 17.
layout: post
permalink: /github-and-git/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 20
ratings_average:
  - 5
categories:
  - Кодинг
tags:
  - github
  - ssh-keys
---
Данная статья является попыткой осмыслить (*в первую очередь для себя, конечно*) такой вопрос, как создание git-репозитория на GitHub, клонирование этого репозитория на локальный компьютер, внесение изменений в клонированный репозиторий, отправка изменений обратно на GitHub.

Вот такие получаются шаги, которые нужно осветить. Profit у всех этих сложностей, описанных мною выше, один &#8211; но большой! Заключается он в том, что проект, над которым вы работаете (*даже в гордом одиночестве*) находится на удаленном сервере, к которому можно подключиться из любого места и с любой машины. Так как он находиться на remote server, то с ним ничего не случиться, даже если ваша машина упадет\утонет\разобьется.

В статье большая часть времени будет посвящена автоматизации процесса авторизации на сервисе GitHub с помощью такой вещи, как ssh-ключи. Такие ключи предназначены как раз для возможности авторизации пользователя на каком-либо сервисе, без необходимости каждый раз вводить логин\пароль. Естественно, на стороне сервиса должна быть настроена такая возможность &#8211; на GitHub она настроена и даже является почти обязательным условием настройки аккаунта.

Все действия, описанные в этой статье, будут производиться под операционной системой Linux Mint 17 Cinnamon, в консоли. Поэтому пользователи Mac OS X найдут для себя почти все идентичным. Система Windows остается в стороне.

### Создание SSH-ключей под Linux

Первоначально необходимо создать (*если их еще нет*) ssh-ключи, которые будем использоваться для авторизации на GitHub. В системе Linux такие ключи расположены в домашней директории пользователя и выглядят примерно так:

<pre>$ ls ~/.ssh
  id_rsa id_rsa.pub known_hosts
</pre>

Один из этих ключей `id_rsa` &#8211; это приватный ключ, который должен храниться только у пользователя. Другой ключ `id_rsa.pub` &#8211; это публичный ключ, который предоставляется всем и который я отправлю на GitHub. Представленные выше имена ключей являются создаваемыми по умолчанию, но можно указать и свои собственные.

Если показанная выше команда &#8220;скажет&#8221; вам, что директории `.ssh` не существует, то это означает, что у вас с системе установлен пакет SSH, отвечающий за создание и обработку ssh-ключей.

#### Установка пакета SSH

Под Linux Mint его нужно установить командой:

<pre>$ sudo apt-get install ssh
</pre>

#### Создание пары ssh-ключей

Теперь можно приступать к созданию пары ssh-ключей. Выполняется это командой:

<pre>$ ssh-keygen -t rsa -C "g***e@gmail.com"
</pre>

Чтобы было немного понятно, что это я сделал в данной команде, немного расшифрую ее. Утилита `ssh-keygen` входит в комплект пакета `ssh` и предназначена для одной цели &#8211; создания ssh-ключей. Часть команды &#8211; `-t rsa` &#8211; указывает, что необходимо создать ssh-ключи типа `rsa`. Обязательный параметр `"g***e@gmail.com"` &#8211; электронный адрес, к которому &#8220;привязывается&#8221; создаваемый ssh-ключ; данный email будет также использоваться мною для регистрации на GitHub.

Как только будет введена представленная выше команда, утилита `ssh-keygen` запросит имя файла и местоположение для создаваемых ssh-ключей. Можно ничего не вводить, а просто нажать Enter. В этом случае программулька создаст и положит их по пути по умолчанию (который показан ею в скобочках):

<pre>$ ssh-keygen -t rsa -C "g***e@gmail.com"
  Generating public/private rsa key pair.
  Enter file in which to save the key (/home/aaron/.ssh/id_rsa):
</pre>

Утилита задаст еще один вопрос, который крайне не рекомендуется игнорировать:

<pre>$ ssh-keygen -t rsa -C "g***e@gmail.com"
  Generating public/private rsa key pair.
  Enter file in which to save the key (/home/aaron/.ssh/id_rsa):
  Enter passphrase (empty for no passphrase):
</pre>

Здесь `passphrase` &#8211; это пароль к создаваемым ssh-ключам. Каждый раз, когда придется использовать эти ключи, нужно вводить данный пароль. Это обезопасит их в случае кражи. В качестве пароля можно использовать любую текстовую строку.

После успешного ввода `passphrase` ssh-ключи будут созданы:

<pre>$ ssh-keygen -t rsa -C "g***e@gmail.com"
  Generating public/private rsa key pair.
  Enter file in which to save the key (/home/aaron/.ssh/id_rsa):
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in /home/aaron/.ssh/id_rsa.
  Your public key has been saved in /home/aaron/.ssh/id_rsa.pub.
</pre>

В состав пакета `ssh` входит утилита `ssh-agent`, задача которой в управлении созданными ssh-ключами. Передадим ей в пользование только созданные мною ssh-ключи:

<pre>$ eval "$(ssh-agent -s)"
  Agent pid 17461
  $ ssh-add ~/.ssh/id_rsa
  Enter passphrase for /home/aaron/.ssh/id_rsa:
  Identity added: /home/aaron/.ssh/id_rsa (/home/aaron/.ssh/id_rsa)
</pre>

Можно посмотреть, что утилита `shh-add` &#8220;подхватила&#8221; и распознала предоставленные ею ssh-ключи:

<pre>$ ssh-add -l
  2048 e4:4d:fe:73:cb:b9:bb:ee:26:32:6b:f5:f1:6a:db:38 /home/aaron/.ssh/id_rsa (RSA)
</pre>

Под операционную систему Linux имеется консольная утилита `xclip`, которая умеет получать содержимое любого файла и отправлять это содержимое в буфер обмена, и все это в консоли. По умолчанию такой утилиты нет в системе (*в том числе и у меня*), поэтому первоначально установлю ее:

<pre>$ sudo apt-get install xclip
</pre>

&#8230; а затем передам ей на вход содержимое публичного ключа `id_rsa.pub`, который буду применять на сервисе GitHub:

<pre>$ xclip -sel clip &lt; ~/.ssh/id_rsa.pub
</pre>

Если вам, уважаемый читатель, такой путь покажется слишком сложным, то можно открыть файл `id_rsa.pub` в любом редакторе кода и скопировать его содержимое в буфер обмена.

### Добавление ssh-ключа на GitHub

Переходим на сервис GitHub и создаем на нем новую учетную запись. Описывать процесс создания такой записи на GitHub не буду, так как там все просто. Более интересный момент - это добавление ssh-ключа в профиль пользователя GitHub.

Для этого нажимаю на значок шестеренки в правом верхнем углу окна браузера - настройки профиля пользователя. В открывшемся окне (в его левой части) находим строку `SSH key` и нажимаем ее:<figure id="attachment_1735" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github_ssh_keys-600x464.png" alt="SSH ключи на GitHub" width="600" height="464" class="size-medium wp-image-1735" />][1]<figcaption class="wp-caption-text">SSH ключи на GitHub</figcaption></figure> 

Откроется окно для добавления новых ssh-ключей в учетную запись пользователя на GitHub. Здесь все элементарно просто - нажимаем кнопку `Add SSH key`. В поле `Title` вводим название (произвольное) для импортируемого ssh-ключа. В поле `Key` просто нажимаем Ctrl+V - содержимое буфера обмена (которое я получил ранее с помощью утилиты `xclip`) вставиться в это поле:<figure id="attachment_1734" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github_add_ssh_keys-600x464.png" alt="Добавление ssh-ключа на GitHub" width="600" height="464" class="size-medium wp-image-1734" />][2]<figcaption class="wp-caption-text">Добавление ssh-ключа на GitHub</figcaption></figure> 

Жму на зеленую кнопку `Add key` внизу окна. Ключ добавлен на GitHub и появиться в списке SSH-ключей:<figure id="attachment_1733" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github_added_ssh_keys-600x464.png" alt="Добавленный на GitHub ssh-ключ" width="600" height="464" class="size-medium wp-image-1733" />][3]<figcaption class="wp-caption-text">Добавленный на GitHub ssh-ключ</figcaption></figure> 

### Проверка SSH-соединения с GitHub

В предыдущих шагах мною были созданы пара ssh-ключей, а также учетная запись на GitHub. В эту учетную запись был импортирован публичный ssh-ключ. Теперь неплохо было бы проверить, что все шаги пройдены мною успешно и ssh-связь с сервисом GitHub устанавливается. Проще сказать - что сервис GitHub авторизует меня у себя с помощью ssh-ключей.

Для этой цели ввожу команду:

<pre>$ ssh -T git@github.com
  The authenticity of host 'github.com (192.30.252.131)' can't be established.
  RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
  Are you sure you want to continue connecting (yes/no)? yes
</pre>

На ошибку в строке `The authenticity of host 'github.com (192.30.252.131)' can't be established.` не стоит обращать внимание. В запросе командной строки печатаем `yes` и получаем:

<pre>Warning: Permanently added 'github.com,192.30.252.131' (RSA) to the list of known hosts.
  Hi gearmobile! You've successfully authenticated, but GitHub does not provide shell access.
</pre>

Отлично! GitHub "узнал" меня и поприветствовал в строке `Hi gearmobile! You've successfully authenticated, but GitHub does not provide shell access.`. Это говорит о том, что ssh-соединение моей машины с GitHub установлено успешно и GitHub авторизует меня.

Однако, при настройке ssh-соединения возможны и ошибки. В этом случае может помочь статья - [Error: Permission denied (publickey)][4].

### Создание нового репозитория на GitHub

Создаем новый репозиторий на GitHub. Ввожу новое уникальное имя для репозитория, краткое его описание и включаю галочку "Initialize this repository with a README":<figure id="attachment_1732" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github_create_new_repo-600x464.png" alt="Создание нового репозитория на GitHub" width="600" height="464" class="size-medium wp-image-1732" />][5]<figcaption class="wp-caption-text">Создание нового репозитория на GitHub</figcaption></figure> 

Отлично! На GitHub я только что создал новый репозиторий `arbeit`. Теперь можно скопировать (склонировать) его на свою локальную машину командами:

<pre>$ mkdir arbeit
  $ git clone git@github.com:gearmobile/arbeit.git
  Cloning into 'arbeit'...
  Warning: Permanently added the RSA host key for IP address '192.30.252.130' to the list of known hosts.
  remote: Counting objects: 3, done.
  remote: Compressing objects: 100% (2/2), done.
  remote: Total 3 (delta 0), reused 0 (delta 0)
  Receiving objects: 100% (3/3), done.
  Checking connectivity... done
</pre>

Переходим в локальную копию репозитория `arbeit`. Вношу изменения, а затем последовательно:

<pre>$ git add .
  $ git commit -m 'Added changes'
  $ git push
</pre>

Команда `git commit -m 'Added changes'` фиксирует изменения в локальном репозитории. Команда `git push` отправляет внесенные и зафиксированные изменения в локальном репозитории на удаленный репозиторий.

Вот, таким образом я наладил Git-работу своей машины с GitHub.

Оцените статью:  
<span id="post-ratings-1730" class="post-ratings" data-nonce="59616f7a65"><img id="rating_1730_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1730, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1730_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1730, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1730_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1730, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1730_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1730, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1730_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1730, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1730_text"></span></span><span id="post-ratings-1730-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/08/github_ssh_keys.png
 [2]: http://localhost:7788/third/wp-content/uploads/2014/08/github_add_ssh_keys.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/08/github_added_ssh_keys.png
 [4]: https://help.github.com/articles/error-permission-denied-publickey "Error: Permission denied (publickey)"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/08/github_create_new_repo.png