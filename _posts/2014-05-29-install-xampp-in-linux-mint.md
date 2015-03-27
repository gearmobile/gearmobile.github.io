---
title: Установка XAMPP под Linux Mint 17
author: gearmobile
excerpt: 'В этой статье будет рассмотрен вопрос установки локального сервера XAMPP под операционной системой Linux Mint 17. Почему этот локальный сервер и, тем более, почему именно Linux? Ответы просты - для меня лично сервер XAMPP является наиболее интуитивно понятным. А Linux - потому что в ней мне более удобно кодить на HTML &amp; CSS, нежели под Windows.'
layout: post
permalink: /install-xampp-in-linux-mint/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
categories:
  - OS Linux
tags:
  - linux
  - wordpress
  - xampp
---
В этой статье будет рассмотрен вопрос установки локального сервера XAMPP под операционной системой Linux Mint 17. Почему этот локальный сервер и, тем более, почему именно Linux? Ответы просты &#8211; для меня лично сервер XAMPP является наиболее интуитивно понятным. А Linux &#8211; потому что в ней мне более удобно кодить на HTML & CSS, нежели под Windows. Хотя бы взять удобный и полноценный терминал Linux, который всегда под рукой. Также, локальный сервер под Linux, по моим субъективным оценкам, работает гораздо быстрее, нежели под Windows.

С преимуществами работы кодера под Linux разобрались &#8211; осталось установить и настроить локальный сервер под эту операционную систему. В этом вопросе нет ничего сложного и есть даже локализованная версия инструкции на официальном сайте Apache Friends -[FAQ Linux][1]. В этой статье я постараюсь дать более подробное описание этого процесса, с картинками.

Локальный сервер под Linux выполнен в виде пошагового графического инсталлятора наподобие того, как это делается под Windows. С одной стороны это несколько непривычно для Linux; но с другой стороны так можно быстро и легко установить пакет для новичков в этой операционной системе.

### Пакет инсталляции XAMPP под Linux Mint

Скачиваем пакет инсталлятора по ссылке [Download][2] официального сайта Apache Friends. При этом определяемся, под 32 или 64-битную систему необходим пакет &#8211; такой и выбираем. Помимо этого есть две версии пакета &#8211; стабильный 1.8.2/PHP 5.4.27 и более новый 1.8.3/PHP 5.5.11. Мною был выбран пакет 1.8.2/PHP 5.4.27 (именно из-за его стабильности) версии 64-бита, под операционную систему Linux Mint 17 &#8220;Qiana&#8221; Cinnamon 64-bit.

После скачивания пакета открываю директорию Downloads (туда попадают все скачиваемые под Linux файлы) в терминале. Команда `ls` показывает мне содержимое этой директории &#8211; и файл `xampp-linux-x64-1.8.2-5-installer.run` в частности. В этом же терминале делаю этот файл исполняемым:

<pre>$ sudo chmod 755 xampp-linux-x64-1.8.2-5-installer.run
  </pre>

&#8230; затем запускаю файл `xampp-linux-x64-1.8.2-5-installer.run` на выполнение командой:

<pre>$ sudo ./xampp-linux-x64-1.8.2-5-installer.run
  </pre>

### Инсталляция XAMPP под Linux Mint

Запуститься пошаговый графический инсталлятор локального сервера. Пользователи Windows могут почувствовать себя здесь немного в своей стихии. Ниже приведу скриншоты все шагов установки сервера с кратким их описанием, где это необходимо.

Сервер будет установлен в директорию `/opt/lampp`:<figure id="attachment_1274" style="width: 502px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_1.png" alt="Запуск установки XAMPP" width="502" height="418" class="size-full wp-image-1274" />][3]<figcaption class="wp-caption-text">Запуск установки XAMPP</figcaption></figure> <figure id="attachment_1275" style="width: 502px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_2.png" alt="Выбор компонентов установки XAMPP" width="502" height="418" class="size-full wp-image-1275" />][4]<figcaption class="wp-caption-text">Выбор компонентов установки XAMPP</figcaption></figure> <figure id="attachment_1276" style="width: 502px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_3.png" alt="Директория установки XAMPP" width="502" height="418" class="size-full wp-image-1276" />][5]<figcaption class="wp-caption-text">Директория установки XAMPP</figcaption></figure> 

В этом шаге необходимо убрать галочку в строке &#8220;Learn more about Bitnami for XAMPP&#8221;:<figure id="attachment_1277" style="width: 502px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_4.png" alt="Приложение Bitnami под XAMPP" width="502" height="418" class="size-full wp-image-1277" />][6]<figcaption class="wp-caption-text">Приложение Bitnami под XAMPP</figcaption></figure> <figure id="attachment_1278" style="width: 502px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_5.png" alt="Установка начата" width="502" height="418" class="size-full wp-image-1278" />][7]<figcaption class="wp-caption-text">Установка начата</figcaption></figure> <figure id="attachment_1279" style="width: 502px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_6.png" alt="Процесс инсталляции" width="502" height="418" class="size-full wp-image-1279" />][8]<figcaption class="wp-caption-text">Процесс инсталляции</figcaption></figure> 

В этом шаге оставляем галочку в строке &#8220;Launch XAMPP&#8221;, чтобы локальный сервер автоматически запустился после установки:<figure id="attachment_1280" style="width: 502px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_7.png" alt="Завершение установки XAMPP" width="502" height="418" class="size-full wp-image-1280" />][9]<figcaption class="wp-caption-text">Завершение установки XAMPP</figcaption></figure> 

### Запуск и остановка XAMPP под Linux Mint

Помимо самого локального сервера будет установлено графическое приложение, задача которого &#8211; облегчить управление локальным сервером. Это приложение также запуститься автоматически, но его можно при необходимости запустить и вручную командой:

<pre>cd /opt/lampp
  sudo ./manager-linux-x64.run
  </pre><figure id="attachment_1281" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_first_launch-600x406.png" alt="Приложение для управления XAMPP" width="600" height="406" class="size-medium wp-image-1281" />][10]<figcaption class="wp-caption-text">Приложение для управления XAMPP</figcaption></figure> 

Переходим в этом приложении на вкладку &#8220;Manage Servers&#8221; и видим список служб локального сервера. Напротив каждой службы в виде лампочки показан ее статус &#8211; запущена она (Running) или остановлена (Stopped).<figure id="attachment_1282" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_manage_servers-600x406.png" alt="Управление сервисами в XAMPP" width="600" height="406" class="size-medium wp-image-1282" />][11]<figcaption class="wp-caption-text">Управление сервисами в XAMPP</figcaption></figure> 

Первоначально запущен только локальный сервер Apache; база данных &#8220;MySQL Database&#8221; и FTP-сервер &#8220;ProFTPD&#8221; остановлены. Их можно запустить из данного приложения, просто нажав кнопку &#8220;Start&#8221;, но я поступлю более Linux-way и воспользуюсь терминалом. Для этого я введу в нем всего одну комадну:

<pre>$ sudo /opt/lampp/lampp start
  </pre>

Если все пройдет успешно, то в терминале будет следующий вывод:

<pre>Starting XAMPP for Linux 1.8.2-5...
  XAMPP: Starting Apache...ok.
  XAMPP: Starting MySQL...ok.
  XAMPP: Starting ProFTPD...ok.
  </pre>

&#8230; что можно проверить и в приложении:<figure id="attachment_1283" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_all_services_start-600x406.png" alt="Запуск всех сервисов в XAMPP" width="600" height="406" class="size-medium wp-image-1283" />][12]<figcaption class="wp-caption-text">Запуск всех сервисов в XAMPP</figcaption></figure> 

Остановить локальный сервер можно также из терминала командой:

<pre>$ sudo /opt/lampp/lampp stop
  ...
  Stopping XAMPP for Linux 1.8.2-5...
  XAMPP: Stopping Apache...ok.
  XAMPP: Stopping MySQL...ok.
  XAMPP: Stopping ProFTPD...ok.
  </pre>

### Установка WordPress под XAMPP в Linux Mint

С установкой локального сервера под Linux Mint разобрались. Стоит еще раз оговориться, что по моим субъективным оценкам он работает гораздо шустрее под Linux, нежели под Windows.

Переходим к заключительной части данной статьи и рассмотрим вопрос установки CMS WordPress под XAMPP в Linux Mint. Все виртуальные сервера располагаются в директории `/opt/lampp/htdocs/`. То есть, если необходимо создать отдельный экземпляр какой-либо CMS (Joomla, WordPress, Drupal и так далее), то нужно просто создать поддиректорию в директории `htdocs` и распаковать туда нужную CMS. В моем случае такой CMS будет WordPress-3.9.1.

Создаю поддиректорию `travel` командой:

<pre>$ sudo mkdir -p /opt/lampp/htdocs/travel
  </pre>

&#8230; и распаковываю в нее скачанный архив WordPress с помощью незаменимой консольной программы mc (не забудьте запустить ее через sudo, иначе получите ошибку прав доступа):<figure id="attachment_1284" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/xampp_mc_wordpress_unpack-600x304.png" alt="Распаковка WordPress в XAMPP" width="600" height="304" class="size-medium wp-image-1284" />][13]<figcaption class="wp-caption-text">Распаковка WordPress в XAMPP</figcaption></figure> 

После распаковки WordPress приступим к его установке. Создадим вручную конфигурационный файл `wp-config.php` чтобы избежать ошибки прав доступа при обычной пошаговой инсталляции WordPress (не забываем, что мы находимся под Linux!). Для этого скопируем файл-шаблон `wp-config-sample.php` в ту же директорию под именем `wp-config.php`:

<pre>$ sudo cp /opt/lampp/htdocs/travel/wp-config-sample.php /opt/lampp/htdocs/travel/wp-config.php
  </pre>

&#8230; и отредактируем его через редактор nano:

<pre>$ sudo nano -w /opt/lampp/htdocs/travel/wp-config.php
  </pre>

Затем в адресной строке браузера введем (XAMPP у нас все еще запущен, не забываем об этом!):

<pre>http://localhost/phpmyadmin

  </pre>

&#8230; и в приложении phpMyAdmin создаем базу данных под наш будущий локальный сайт, на котором будет &#8220;крутиться&#8221; WordPress. Перезапускаем локальный сервер, чтобы он &#8220;подхватил&#8221; изменения в базе данных MySQL и создание виртульного сервера `travel` в директории `htdocs`:

<pre>$ sudo /opt/lampp/lampp restart
  ...
  Restarting XAMPP for Linux 1.8.2-5...
  XAMPP: Stopping Apache...ok.
  XAMPP: Stopping MySQL...ok.
  XAMPP: Stopping ProFTPD...ok.
  XAMPP: Starting Apache...ok.
  XAMPP: Starting MySQL...ok.
  XAMPP: Starting ProFTPD...ok.
  </pre>

В браузере в адресной строке запускаем установку WordPress:

<pre>http://localhost/travel

  </pre>

&#8230; далее проходим оставшиеся стандартные шаги инсталляции WordPress и получаем готовый локальный сайт &#8211; переходим на него по адресу:

<pre>http://localhost/travel

  </pre>

На этом установка CMS WordPress под локальный сервер успешно завершена. А также успешно выполнена рассмотренная выше инсталляция локального сервера под операционной системой Linux Mint 17 &#8220;Qiana&#8221; Cinnamon 64-bit.

### Заключение

Итог выполненных выше шагов &#8211; возможность иметь всегда &#8220;под рукой&#8221; готовый к работе локальный сервер. Еще один плюс к удобству кодинга под Linux. А кодинг под Linux субъективно для меня удобнее кодинга под Windows.

Стоит также сказать, что при установке и настройке могут возникнуть проблемы. В частности, автором данной статьи первоначально производилась установка &#8220;чистого&#8221; LAMPP, которая потом была удалена. И, хотя деинсталляция была произведена правильно, последующая установка XAMPP привела к тому, что данный сервер не запускался на компьютере.

Оцените статью:  
<span id="post-ratings-1272" class="post-ratings" data-nonce="6e975d9fe5"><img id="rating_1272_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1272, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1272_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1272, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1272_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1272, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1272_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1272, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1272_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1272, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1272_text"></span></span><span id="post-ratings-1272-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: https://www.apachefriends.org/ru/faq_linux.html "FAQ Linux"
 [2]: https://www.apachefriends.org/ru/download.html "Download"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_1.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_2.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_3.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_4.png
 [7]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_5.png
 [8]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_6.png
 [9]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_step_7.png
 [10]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_first_launch.png
 [11]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_manage_servers.png
 [12]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_all_services_start.png
 [13]: http://localhost:7788/third/wp-content/uploads/2014/05/xampp_mc_wordpress_unpack.png