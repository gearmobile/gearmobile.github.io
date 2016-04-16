---
title: "Linux Mint - Midnight Commander Skins"
layout: post
categories: linux
tags: [linux, mc, skin]
share: true
---

Небольшая заметка, посвященная вопросу настройки тем оформления (skins) в популярном и очень полезном консольном файловом менеджере [Midnight Commander](http://www.midnight-commander.org/ "Midnight Commander").

И попутно затрагивается вопрос с настройкой отображения кириллицы в Midnight Commander под управлением OSX.

## Пару хвалебных слов

Midnight Commander - это консольный файловый менеджер. Консольный - потому что он работает в консоли, из эмулятора терминала. Внешне он очень похож на аналогичный [Far Manager](http://farmanager.com/index.php?l=ru "Far Manager") под операционной системой Windows.

Midnight Commander - очень легкий, потому что для своей работы он использует псевдографику.

Midnight Commander - обладает большими возможностями, больше половины которых обычный пользователь даже не применяет на практике.

Устанавливается Midnight Commander из пакетного менеджера, так как эта утилита имеется в репозиториях любого дистрибутива Linux. В Debian \ Ubuntu \ Mint установка производится такой командой:

{% highlight bash %}
sudo apt-get install mc
{% endhighlight %}

## Оформление Midnight Commander

После установки Midnight Commander и его первоначального запуска внешний вид программы будет примерно таким:

![Midnight Commander Default Skin]({{site.url}}/images/uploads/2016/04/linux-mc-01.png "Midnight Commander Default Skin")

Прямо скажем, зрелище не очень привлекательное, особенно - зеленый шрифт на синем фоне. Это тема оформления (skin) по умолчанию для Midnight Commander и называется она также - `default`.

Но оформление Midnight Commander можно (и нужно) поменять и сделать это просто, так как эта программа идет с предустановленным набором тем оформления.

Готовые темы оформления (skins) после установки Midnight Commander располагаются по пути:

{% highlight bash %}
~|⇒ ll /usr/share/mc/skins
{% endhighlight %}

Туда можно заглянуть и выбрать, что понравиться:

{% highlight bash %}
~|⇒ ll /usr/share/mc/skins
total 212K
-rw-r--r-- 1 root root 3,0K Dec  5  2013 darkfar.ini
-rw-r--r-- 1 root root 3,0K Dec  5  2013 dark.ini
-rw-r--r-- 1 root root 2,7K Dec  5  2013 default.ini
-rw-r--r-- 1 root root 2,7K Dec  5  2013 double-lines.ini
-rw-r--r-- 1 root root 3,1K Dec  5  2013 featured.ini
-rw-r--r-- 1 root root 2,2K Dec  5  2013 gotar.ini
-rw-r--r-- 1 root root 2,3K Dec  5  2013 mc46.ini
-rw-r--r-- 1 root root 4,0K Dec  5  2013 modarcon16-defbg.ini
-rw-r--r-- 1 root root 4,0K Sep 24  2012 modarcon16-defbg-thin.ini
-rw-r--r-- 1 root root 4,0K Dec  5  2013 modarcon16.ini
-rw-r--r-- 1 root root 4,0K Dec  5  2013 modarcon16root-defbg.ini
-rw-r--r-- 1 root root 4,0K Sep 24  2012 modarcon16root-defbg-thin.ini
-rw-r--r-- 1 root root 4,0K Dec  5  2013 modarcon16root.ini
-rw-r--r-- 1 root root 4,0K Sep 24  2012 modarcon16root-thin.ini
-rw-r--r-- 1 root root 4,0K Sep 24  2012 modarcon16-thin.ini
-rw-r--r-- 1 root root 4,1K Dec  5  2013 modarin256-defbg.ini
-rw-r--r-- 1 root root 4,1K Sep 24  2012 modarin256-defbg-thin.ini
-rw-r--r-- 1 root root 4,1K Dec  5  2013 modarin256.ini
-rw-r--r-- 1 root root 4,1K Dec  5  2013 modarin256root-defbg.ini
-rw-r--r-- 1 root root 4,1K Sep 24  2012 modarin256root-defbg-thin.ini
-rw-r--r-- 1 root root 4,1K Dec  5  2013 modarin256root.ini
-rw-r--r-- 1 root root 4,1K Sep 24  2012 modarin256root-thin.ini
-rw-r--r-- 1 root root 4,1K Sep 24  2012 modarin256-thin.ini
-rw-r--r-- 1 root root 2,9K Dec  5  2013 nicedark.ini
-rw-r--r-- 1 root root 5,4K Dec  5  2013 sand256.ini
-rw-r--r-- 1 root root 3,9K Dec  5  2013 xoria256.ini
{% endhighlight %}

Выбрать тему оформления для Midnight Commander можно командой:

{% highlight bash %}
~|⇒ mc -S darkfar
{% endhighlight %}

Здесь ключ `-S` указывает, что при запуске Midnight Commander необходимо использовать тему оформления. Имя темы оформления (skin) указывается после ключа. Результат приведенной выше команды будет следующим:

![Midnight Commander Darkfar Skin]({{site.url}}/images/uploads/2016/04/linux-mc-darkfar.png "Midnight Commander Darkfar Skin")

Уже значительно лучше, не правда ли? Таким образом можно перебрать все имеющиеся в комплекте темы и выбрать понравившуюся.

Когда тема оформления выбрана, нужно прописать ее в конфигурационном файле Midnight Commander, чтобы последний запускался каждый раз именно с этим skin'ом.

Файл настроек Midnight Commander располагается по пути `~|⇒ ll ~/.config/mc/ini` и запускается на редактирование таким образом:

{% highlight bash %}
~|⇒ nano ~/.config/mc/ini
{% endhighlight %}

В этом файле нужно найти строчку `skin` и изменить значение параметра на название файла темы (из `/usr/share/mc/skins`):

{% highlight bash %}
...
editor_filesize_threshold=64M
mcview_eof=
ignore_ftp_chattr_errors=true
skin=modarin256

[Layout]
message_visible=1
keybar_visible=1
...
{% endhighlight %}

Обратите внимание на название skin'а в данном случае - `modarin256`. Здесь 256 - это количество цветов отображения, которые используются в этой теме.

По умолчанию в Linux Mint консоль **не поддерживает** отображение такого количества цветов. Если запустить Midnight Commander с темой `modarin256` (к примеру), то появится ошибка и предложении использовать тему по-умолчанию (`default`).

Включить поддержку отображения 256 цветов в консоли можно, добавив строку `export TERM=xterm-256color` в файле `.bash_profile` (если используется [BASH](https://habrahabr.ru/post/47163/ "BASH")), в файле `.zshrc` (если используется [ZSH](http://zsh.sourceforge.net/ "ZSH")), в файле `.profile` (если используется OSX).

В моем случае используется [ZSH](http://zsh.sourceforge.net/ "ZSH") и файл `.zshrc` будет выглядеть таким образом:

{% highlight bash %}
# User configuration
...
export TERM=xterm-256color
...
{% endhighlight %}

Если все сделано без ошибок, то запуск Midnight Commander выдаст такой результат (используется тема оформления `modarin256`):

![Midnight Commander Modarin Skin]({{site.url}}/images/uploads/2016/04/linux-mc-modarin.png "Midnight Commander Modarin Skin")

Можно попробовать тему `xoria256` - хорошо проработанная тема, с которой также приятно работать. Об этой теме была статья на Хабрахабр - [Цветовая схема Xoria256 для Midnight Commander](https://habrahabr.ru/post/111605/ "Цветовая схема Xoria256 для Midnight Commander"):

![Midnight Commander Xoria Skin]({{site.url}}/images/uploads/2016/04/linux-mc-xoria.png "Midnight Commander Xoria Skin")

## Midnight Commander и кириллица в OSX

Установка и настройка Midnight Commander в операционной системе OSX мало отличается от аналогичных действий в Linux.

Устанавливать Midnight Commander в OSX проще всего с помощью [Homebrew](http://brew.sh/ "Homebrew"):

{% highlight bash %}
$ brew update
$ brew install mc
{% endhighlight %}

Не забываем включить поддержку 256 цветов в консоли OSX, если хотим использовать богатые цветом темы оформления Midnight Commander, такие как `modarin256` или `xoria256`.

Для этого редактируем файл `.bash_profile` или файл `.zshrc` (если используется ZSH):

{% highlight bash %}
...
export TERM=xterm-256color
...
{% endhighlight %}

Дополнительным шагом будет добавление в файл `.bash_profile` (или `.zshrc`) двух строчек:

{% highlight bash %}
...
export LC_CTYPE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
...
{% endhighlight %}

... для того, чтобы в Midnight Commander правильно отображались **русскоязычные** имена файлов и директорий. Иначе вместо вразумительных имен файлов будут одни вопросительные знаки.

Вариант с добавлением строки `export LANG=ru_RU.UTF-8` в файле `.bash_profile` у меня не сработал.

***

На этом все.
