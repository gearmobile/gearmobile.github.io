---
title: "Virtual Host под XAMPP в Linux Mint"
layout: post
categories:
tags: [linux, virtual host, xampp]
share: true
---

> Под локальным сервером XAMPP можно создавать неограниченное количество виртуальных хостов.

Что такое виртуальный хост (Virtual Host)? Применительно в серверу XAMPP - это поддиректории, в которых размещаются отдельные сайты. То есть, имеется директория `htdocs`, а в ней размещены поддиректории `site_1`, `site_2`, `site_3` (или же так - `redface`, `football`, `greenpark`, название может быть любым).

В каждой из этих поддиректорий распакован и установлен движок CMS WordPress (к примеру). Вот эти поддиректории `site_1`, `site_2`, `site_3` и являются виртуальными хостами под локальным сервером XAMPP.

Как уже упоминалось выше, сервер XAMPP может поддерживать неограниченное количество виртуальных хостов. Однако, по умолчанию разрешено использовать только два хоста. Но редактирование конфигурационного файла позволяет добавлять столько, сколько нужно.

Настройка виртуальных хостов на XAMPP под Linux Mint почти ничем не отличается от подобной настройки под Windows, меняются только пути конфигурационных файлов. Весь процесс настройки можно свести к двум шагам:

1. Настройка хостов в файле `/etc/hosts`
2. Настройка виртуальных хостов в файле `/opt/lampp/etc/extra/httpd-vhosts.conf`

Ниже на примере расмотрим подробное описание создания одного виртуального хоста на XAMPP под Linux Mint.

## Создание поддиректории виртуального хоста (Virtual Host)

Для начала подготовим место, где будет располагаться будущий виртуальный хост. Для этого создадим поддиректорию `redface` (имя произвольное) и обязательно разместим в ней индексный файл `index.html`:

{% highlight powershell %}
$ sudo mkdir -p /opt/lampp/htdocs/redface
$ sudo touch /opt/lampp/htdocs/redface/index.html
{% endhighlight %}

Виртуальный хост с именем `redface` почти создан. Осталось "сказать" об этом локальному серверу XAMPP и операционной системе Linux Mint.

## Редактирование файла /etc/hosts

Операционной системе Linux Mint нужно "сказать", что виртуальный хост `redface` размещен по адресу `127.0.0.1`. Для этого открываем для редактирования файл `/etc/hosts` командой:

{% highlight powershell %}
$ sudo nano -w /etc/hosts
{% endhighlight %}

... и дописываем в нем строку `127.0.0.1 redface.dev`:

{% highlight powershell %}
127.0.0.1 localhost
127.0.1.1 zmk

# Virtual hosts
127.0.0.1 redface.dev
{% endhighlight %}

Окончание `.dev` является произвольным и служит для того, чтобы вебмастер не забыл, что данный сайт является локальным. Вместо `.dev` можно использовать `.lc` и какое угодно другое имя.

Сохраняем <kbd>Ctrl+O</kbd> и выходим <kbd>Ctrl+X</kbd> из редактора `nano`.

## Включение поддержки виртуального хоста в XAMPP

По умолчанию в настройках XAMPP отключена поддержка виртуальных хостов. Для включения такой возможности нужно отредактировать конфигурационный файл `httpd.conf` сервера Apache.

Для этого открываем его командой:

{% highlight powershell %}
$ sudo nano -w /opt/lampp/etc/httpd.conf
{% endhighlight %}

В открытом файле `httpd.conf` нужно найти (в редакторе это сочетание <kbd>Ctrl+W</kbd>) строку `# Virtual hosts` и раскомментировать (снять знак решетки `#`) строку:

{% highlight powershell %}
#Include etc/extra/httpd-vhosts.conf
{% endhighlight %}

## Создание виртуального хоста в файле httpd-vhosts.conf

Открываем для редактирования файл `httpd-vhosts.conf` и знакомимся с его содержимым:

{% highlight powershell %}
$ sudo nano -w /opt/lampp/etc/extra/httpd-vhosts.conf
{% endhighlight %}

В начале идет много закомментированных строк с кратким описанием виртуального хоста и принципом его создания в данном файле. Можно смело почистить файл `httpd-vhosts.conf` от этого мусора.

Далее идут два блока с открывающим тегом `<VirtualHost *:80>` и закрывающим тегом `</VirtualHost>`. Данные блоки являются виртуальными хостами - их два по умолчанию, но можно добавить сколько необходимо.

Эти блоки не рабочие, а всего лишь примеры, как нужно создавать свой собственный виртуальный хост. Внутри тегов `<VirtualHost *:80>`/`</VirtualHost>` размещена служебная информация - описание виртуального хоста:

{% highlight powershell %}
<VirtualHost *:80>
  ServerAdmin webmaster@dummy-host.example.com
  DocumentRoot "/opt/lampp/docs/dummy-host.example.com"
  ServerName dummy-host.example.com
  ServerAlias www.dummy-host.example.com
  ErrorLog "logs/dummy-host.example.com-error_log"
  CustomLog "logs/dummy-host.example.com-access_log" common
</VirtualHost>
{% endhighlight %}

Жизненно необходимыми для существования виртуального хоста (Virtual Host) под XAMPP являются две строки:

* DocumentRoot - путь размещения виртуального хоста в файловой системе
* ServerName - доменное имя виртуального хоста

Остальные строки носят дополнительный характер:

* ServerAdmin - e-mail адрес "администратора" хоста
* ServerAlias - синоним доменного имени ServerName
* ErrorLog и CustomLog - логи виртуального хоста

Эти два блока-примера можно отредактировать для конкретного случая, а можно создать свой собственный блок (виртуальный хост) на их основе. Давайте пойдем по второму пути и создадим свой собственный блок для виртуального хоста `redface`:

{% highlight powershell %}
<VirtualHost *:80>
  ServerAdmin         redface@mail.dev
  DocumentRoot        "/opt/lampp/htdocs/redface"
  ServerName          redface.dev
  ServerAlias         www.redface.dev
  ErrorLog            "logs/redface-error_log"
  CustomLog           "logs/redface-access_log" common
</VirtualHost>
{% endhighlight %}

Обратите внимание, как поменялись значения в этм блоке на конкретные, под хост `redface`.

Запускаем (если еще не запущен) или перезапускаем (если уже был запущен) локальный сервер XAMPP:

{% highlight powershell %}
$ sudo /opt/lampp/lampp start
Starting XAMPP for Linux 1.8.2-5...
XAMPP: Starting Apache...ok.
XAMPP: Starting MySQL...ok.
XAMPP: Starting ProFTPD...ok.
{% endhighlight %}

... и "вбиваем" в адресной строке браузера доменное имя созданного нами виртуального хоста `redface.dev`:

![Virtual Host под XAMPP]({{site.url}}/images/uploads/2014/06/xampp_virtual-host_ready.png)

ОК, все работает!

## Проблемы с правами доступа на виртуальном хосте

При создании виртуального хоста (Virtual Host) под XAMPP в директории `htdocs` для создания или редактирования файлов потребуется изменение прав доступа. По умолчанию поддиректория, в которой располагается виртуальный хост, и все файлы внутри этого хоста имеют разрешение только на чтение.

Чтобы можно был вносить в них изменения с правами обычного пользователя, нужно выполнить команду:

{% highlight powershell %}
$ sudo chmod g+w /opt/lampp/htdocs/redface/index.html
{% endhighlight %}

## Изменение точки монтирования виртуального хоста

В этой статье точка монтирования виртуальных хостов (Virtual Hosts) располагалась по адресу - `/opt/lampp/htdocs/`. То есть, поддиректории виртуальных хостов находились внутри директории `htdocs`.

Однако, у локального сервера XAMPP имеется возможность переопределить местоположение виртуальных хостов внутри файловой системы Linux Mint. Например, можно расположить все хосты в домашней директории пользователя. Плюсом такого выбора является то, что нет необходимости настраивать права доступа для папок и файлов.

Вся настройка для переопределения точки монтирования виртуальных хостов (Virtual Hosts) сводится к одному действию - изменить значение строки `DocumentRoot`. Но, к моему сожалению, мне не удалось настроить XAMPP на своем ноутбуке подобным образом.

Все попытки переименовать значение строки `DocumentRoot` приводили к тому, что XAMPP не мог открыть индексную страницу.

В чем причина подобного отказа со стороны XAMPP, я так и не разобрался. Может быть, внимательный читатель подскажет, в чем причина?

## P.S. от 09.09.2014

Добавил в статью комментарий пользователя Alexandr. Сам комментарий мне понравился - подробный и ценный. Поэтому перенес его в статью, как есть. Ниже привожу полный текст, с небольшими стилистическими правками.

Так можно добавить в рабочую папку с проектами на другом диске (например, для использования на Linux и Windows отдельно):

### 1. Файл httpd.conf

Найти строки и заменить (Имя пользователя):

* User (username)
* Group (по умолчанию или username)

Не меняем:

{% highlight powershell %}
DocumentRoot "/opt/lampp/htdocs” и Directory “/opt/lampp/htdocs"
{% endhighlight %}

### 2. Создаем мягкую ссылку:

{% highlight powershell %}
$ sudo ln –s /media/(username)/mydisk/Open Server/domains /opt/lampp/htdocs
{% endhighlight %}

Права на мягкую ссылку "opt/lampp/htdocs/domains" д. б. 777 ( или около того )

### 3. Файл httpd-vhosts.conf

{% highlight powershell %}
#localhost
  
  <VirtualHost *:80>
    DocumentRoot "/opt/lampp/htdocs"
    ServerName localhost
  </VirtualHost>

  <VirtualHost *:80>
    ServerAdmin mydomain@mail
    DocumentRoot "/opt/lampp/htdocs/domains/mydomain/www"
    ServerName mydomain
    ServerAlias http://www.mydomain
  </VirtualHost>
{% endhighlight %}

### 4. Файл /etc/hosts

{% highlight powershell %}
#Virtual hosts
  127.0.0.1 localhost
  127.0.0.1 mydomain
{% endhighlight %}

### 5. Меняем владельца файла

Меняем владельца файла `/opt/lampp/htdocs/xampp/lang.tmp`:

{% highlight powershell %}
$ chown (username) /opt/lampp/htdocs/xampp/lang.tmp
{% endhighlight %}

Иначе `localhost xampp` дальше стартовой страницы может не загрузиться.

### 6. Перезапуск сервера

Перезапуск сервера:

{% highlight powershell %}
$ sudo /opt/lampp/lampp restart
{% endhighlight %}

... и проверка в браузере: `http://mydomain/`

Каждый раз при запуске компьютера, сайты будут не доступны, до тех пор пока диск не примонтирован к системе (для этого нужно просто зайти на тот диск, с помощью файл-менеджера или придумать свой способ).

Если каким-то образом, диск в Linux откажется монтироваться, нужно в Windows отключить быструю загрузку (Fast Boot) в параметрах электропитания.

Для тестирования IE в Linux ставится виртуальная машина (например, VirtualBox), куда устанавливаем Windows7 и любимый браузер IE. В самой Windows редактируем файл `hosts` также как и в Linux, с одним условием – нужно вписывать другой IP, вместо 127.0.0.1, нужно вписывать 10.0.2.2.

Вот так:

{% highlight powershell %}
c:/windows/system32/drivers/etc/hosts
  10.0.2.2 localhost
  10.0.2.2 mydomain
{% endhighlight %}

Сайт через виртуальную машину будет также доступен.

---