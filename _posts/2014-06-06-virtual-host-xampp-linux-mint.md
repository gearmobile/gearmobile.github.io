---
title: Virtual Host под XAMPP в Linux Mint
author: gearmobile
excerpt: 'Под локальным сервером XAMPP можно создавать неограниченное количество виртуальных хостов. Что такое виртуальный хост (Virtual Host)? Применительно в серверу XAMPP - это поддиректории, в которых размещаются отдельные сайты.'
layout: post
permalink: /virtual-host-xampp-linux-mint/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - OS Linux
tags:
  - linux
  - virtual host
  - xampp
---
Под локальным сервером XAMPP можно создавать неограниченное количество виртуальных хостов. Что такое виртуальный хост (Virtual Host)? Применительно в серверу XAMPP &#8211; это поддиректории, в которых размещаются отдельные сайты. То есть, имеется директория `htdocs`, а в ней размещены поддиректории `site_1`, `site_2`, `site_3` (или же так &#8211; `redface`, `football`, `greenpark`, название может быть любым). В каждой из этих поддиректорий распакован и установлен движок CMS WordPress (*к примеру*). Вот эти поддиректории `site_1`, `site_2`, `site_3` и являются виртуальными хостами под локальным сервером XAMPP.

Как уже упоминалось выше, сервер XAMPP может поддерживать неограниченное количество виртуальных хостов. Однако, по умолчанию разрешено использовать только два хоста. Но редактирование конфигурационного файла позволяет добавлять столько, сколько нужно.

Настройка виртуальных хостов на XAMPP под Linux Mint почти ничем не отличается от подобной настройки под Windows, меняются только пути конфигурационных файлов. Весь процесс настройки можно свести к двум шагам:

  1. Настройка хостов в файле `/etc/hosts`
  2. Настройка виртуальных хостов в файле `/opt/lampp/etc/extra/httpd-vhosts.conf`

Ниже на примере расмотрим подробное описание создания одного виртуального хоста на XAMPP под Linux Mint.

### Создание поддиректории виртуального хоста (Virtual Host)

Для начала подготовим место, где будет располагаться будущий виртуальный хост. Для этого создадим поддиректорию `redface` (*имя произвольное*) и обязательно разместим в ней индексный файл `index.html`:

<pre>$ sudo mkdir -p /opt/lampp/htdocs/redface
$ sudo touch /opt/lampp/htdocs/redface/index.html
</pre>

Виртуальный хост с именем `redface` почти создан. Осталось &#8220;сказать&#8221; об этом локальному серверу XAMPP и операционной системе Linux Mint.

### Редактирование файла /etc/hosts

Операционной системе Linux Mint нужно &#8220;сказать&#8221;, что виртуальный хост `redface` размещен по адресу 127.0.0.1. Для этого открываем для редактирования файл `/etc/hosts` командой:

<pre>$ sudo nano -w /etc/hosts
</pre>

&#8230; и дописываем в нем строку `127.0.0.1 redface.dev`:

<pre>127.0.0.1       localhost
127.0.1.1       zmk

# Virtual hosts
127.0.0.1       redface.dev
</pre>

Окончание `.dev` является произвольным и служит для того, чтобы вебмастер не забыл, что данный сайт является локальным. Вместо `.dev` можно использовать `.lc` и какое угодно другое имя.

Сохраняем (Ctrl+O) и выходим (Ctrl+X) из редактора `nano`.

### Включение поддержки виртуального хоста (Virtual Host) в XAMPP

По умолчанию в настройках XAMPP отключена поддержка виртуальных хостов. Для включения такой возможности нужно отредактировать конфигурационный файл `httpd.conf` сервера Apache.

Для этого открываем его командой:

<pre>$ sudo nano -w /opt/lampp/etc/httpd.conf
</pre>

В открытом файле `httpd.conf` нужно найти (в редакторе это сочетание Ctrl+W) строку `# Virtual hosts` и раскомментировать (*снять знак решетки*) строку:

<pre>#Include etc/extra/httpd-vhosts.conf
</pre>

### Создание виртуального хоста (Virtual Host) в файле httpd-vhosts.conf

Открываем для редактирования файл `httpd-vhosts.conf` и знакомимся с его содержимым:

<pre>$ sudo nano -w /opt/lampp/etc/extra/httpd-vhosts.conf
</pre>

В начале идет много закомментированных строк с кратким описанием виртуального хоста и принципом его создания в данном файле. Можно смело почистить файл `httpd-vhosts.conf` от этого мусора.

Далее идут два блока с открывающим тегом `<VirtualHost *:80>` и закрывающим тегом `</VirtualHost>`. Данные блоки являются виртуальными хостами &#8211; их два по умолчанию, но можно добавить сколько необходимо. Эти блоки не рабочие, а всего лишь примеры, как нужно создавать свой собственный виртуальный хост. Внутри тегов `<VirtualHost *:80>`/`</VirtualHost>` размещена служебная информация &#8211; описание виртуального хоста:

<pre>&lt;VirtualHost *:80>
  ServerAdmin webmaster@dummy-host.example.com
  DocumentRoot "/opt/lampp/docs/dummy-host.example.com"
  ServerName dummy-host.example.com
  ServerAlias www.dummy-host.example.com
  ErrorLog "logs/dummy-host.example.com-error_log"
  CustomLog "logs/dummy-host.example.com-access_log" common
&lt;/VirtualHost>
</pre>

Жизненно необходимыми для существования виртуального хоста (Virtual Host) под XAMPP являются две строки:

  * DocumentRoot &#8211; путь размещения виртуального хоста в файловой системе
  * ServerName &#8211; доменное имя виртуального хоста

Остальные строки носят дополнительный характер:

  * ServerAdmin &#8211; e-mail адрес &#8220;администратора&#8221; хоста
  * ServerAlias &#8211; синоним доменного имени ServerName
  * ErrorLog и CustomLog &#8211; логи виртуального хоста

Эти два блока-примера можно отредактировать для конкретного случая, а можно создать свой собственный блок (виртуальный хост) на их основе. Давайте пойдем по второму пути и создадим свой собственный блок для виртуального хоста `redface`:

<pre>&lt;VirtualHost *:80>
  ServerAdmin         redface@mail.dev
  DocumentRoot        "/opt/lampp/htdocs/redface"
  ServerName          redface.dev
  ServerAlias         www.redface.dev
  ErrorLog            "logs/redface-error_log"
  CustomLog           "logs/redface-access_log" common
&lt;/VirtualHost>
</pre>

Обратите внимание, как поменялись значения в этм блоке на конкретные, под хост `redface`.

Запускаем (*если еще не запущен*) или перезапускаем (*если уже был запущен*) локальный сервер XAMPP:

<pre>$ sudo /opt/lampp/lampp start
Starting XAMPP for Linux 1.8.2-5...
XAMPP: Starting Apache...ok.
XAMPP: Starting MySQL...ok.
XAMPP: Starting ProFTPD...ok.
</pre>

&#8230; и &#8220;вбиваем&#8221; в адресной строке браузера доменное имя созданного нами виртуального хоста `redface.dev`:<figure id="attachment_1335" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/xampp_virtual-host_ready-600x407.png" alt="Virtual Host под XAMPP" width="600" height="407" class="size-medium wp-image-1335" />][1]<figcaption class="wp-caption-text">Virtual Host под XAMPP</figcaption></figure> 

ОК, все работает!

### Проблемы с правами доступа на виртуальном хосте (Virtual Host)

При создании виртуального хоста (Virtual Host) под XAMPP в директории `htdocs` для создания или редактирования файлов потребуется изменение прав доступа. По умолчанию поддиректория, в которой располагается виртуальный хост, и все файлы внутри этого хоста имеют разрешение только на чтение.

Чтобы можно был вносить в них изменения с правами обычного пользователя, нужно выполнить команду:

<pre>$ sudo chmod g+w /opt/lampp/htdocs/redface/index.html
</pre>

### Изменение точки монтирования виртуального хоста (Virtual Host)

В этой статье точка монтирования виртуальных хостов (Virtual Hosts) располагалась по адресу &#8211; `/opt/lampp/htdocs/`. То есть, поддиректории виртуальных хостов находились внутри директории `htdocs`.

Однако, у локального сервера XAMPP имеется возможность переопределить местоположение виртуальных хостов внутри файловой системы Linux Mint. Например, можно расположить все хосты в домашней директории пользователя. Плюсом такого выбора является то, что нет необходимости настраивать права доступа для папок и файлов.

Вся настройка для переопределения точки монтирования виртуальных хостов (Virtual Hosts) сводится к одному действию &#8211; изменить значение строки `DocumentRoot`. Но, к моему сожалению, мне не удалось настроить XAMPP на своем ноутбуке подобным образом. Все попытки переименовать значение строки `DocumentRoot` приводили к тому, что XAMPP не мог открыть индексную страницу.

В чем причина подобного отказа со стороны XAMPP, я так и не разобрался. Может быть, внимательный читатель подскажет, в чем причина?

### P.S. от 09.09.2014

Добавил в статью комментарий пользователя **Alexandr**. Сам комментарий мне понравился &#8211; подробный и ценный. Поэтому перенес его в статью, как есть. Ниже привожу полный текст, с небольшими стилистическими правками.

Так можно добавить в рабочую папку с проектами на другом диске (например, для использования на Linux и Windows отдельно):

#### 1. Файл httpd.conf

Найти строки и заменить (Имя пользователя):

  * User (username)
  * Group (по умолчанию или username)

Не меняем:

<pre>DocumentRoot "/opt/lampp/htdocs” и Directory “/opt/lampp/htdocs"
</pre>

#### 2. Создаем мягкую ссылку:

<pre>sudo ln –s /media/(username)/mydisk/Open Server/domains /opt/lampp/htdocs
</pre>

Права на мягкую ссылку &#8220;opt/lampp/htdocs/domains&#8221; д. б. 777 ( или около того )

#### 3. Файл httpd-vhosts.conf

<pre>#localhost
  
  &lt;VirtualHost *:80>
    DocumentRoot "/opt/lampp/htdocs"
    ServerName localhost
  &lt;/VirtualHost>

  &lt;VirtualHost *:80>
    ServerAdmin mydomain@mail
    DocumentRoot "/opt/lampp/htdocs/domains/mydomain/www"
    ServerName mydomain
    ServerAlias http://www.mydomain
  &lt;/VirtualHost>
</pre>

#### 4. Файл /etc/hosts

<pre>#Virtual hosts
  127.0.0.1 localhost
  127.0.0.1 mydomain
</pre>

#### 5. Меняем владельца файла

Меняем владельца файла `/opt/lampp/htdocs/xampp/lang.tmp`:

<pre>chown (username) /opt/lampp/htdocs/xampp/lang.tmp
</pre>

Иначе `localhost xampp` дальше стартовой страницы может не загрузиться.

#### 6. Перезапуск сервера

Перезапуск сервера:

<pre>sudo /opt/lampp/lampp restart
</pre>

&#8230; и проверка в браузере: `http://mydomain/`

Каждый раз при запуске компьютера, сайты будут не доступны, до тех пор пока диск не примонтирован к системе (для этого нужно просто зайти на тот диск, с помощью файл-менеджера или придумать свой способ).

Если каким-то образом, диск в Linux откажется монтироваться, нужно в Windows отключить быструю загрузку (Fast Boot) в параметрах электропитания.

Для тестирования IE в Linux ставится виртуальная машина (например, VirtualBox), куда устанавливаем Windows7 и любимый браузер IE. В самой Windows редактируем файл `hosts` также как и в Linux, с одним условием – нужно вписывать другой IP, вместо 127.0.0.1, нужно вписывать 10.0.2.2.

Вот так:

<pre>c:/windows/system32/drivers/etc/hosts
  10.0.2.2 localhost
  10.0.2.2 mydomain
</pre>

Сайт через виртуальную машину будет также доступен.

Оцените статью:  
<span id="post-ratings-1333" class="post-ratings" data-nonce="edad580987"><img id="rating_1333_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1333, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1333_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1333, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1333_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1333, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1333_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1333, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1333_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1333, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_1333_text"></span></span><span id="post-ratings-1333-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/06/xampp_virtual-host_ready.png