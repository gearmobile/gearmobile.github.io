---
title: "Установка XAMPP под Linux Mint 17"
layout: post
categories: linux
tags: [linux, wordpress, xampp]
share: true
---

> В этой статье будет рассмотрен вопрос установки локального сервера XAMPP под операционной системой Linux Mint 17.

Почему этот локальный сервер и, тем более, почему именно Linux? Ответы просты - для меня лично сервер XAMPP является наиболее интуитивно понятным. А Linux - потому что в ней мне более удобно кодить на HTML&CSS, нежели под Windows.

Хотя бы взять удобный и полноценный терминал Linux, который всегда под рукой. Также, локальный сервер под Linux, по моим субъективным оценкам, работает гораздо быстрее, нежели под Windows.

С преимуществами работы кодера под Linux разобрались - осталось установить и настроить локальный сервер под эту операционную систему. В этом вопросе нет ничего сложного и есть даже локализованная версия инструкции на официальном сайте Apache Friends -[FAQ Linux][1]. В этой статье я постараюсь дать более подробное описание этого процесса, с картинками.

Локальный сервер под Linux выполнен в виде пошагового графического инсталлятора наподобие того, как это делается под Windows. С одной стороны это несколько непривычно для Linux; но с другой стороны так можно быстро и легко установить пакет для новичков в этой операционной системе.

## Пакет инсталляции XAMPP под Linux Mint

Скачиваем пакет инсталлятора по ссылке [Download][2] официального сайта "Apache Friends". При этом определяемся, под 32 или 64-битную систему необходим пакет - такой и выбираем. Помимо этого есть две версии пакета - стабильный 1.8.2/PHP 5.4.27 и более новый 1.8.3/PHP 5.5.11.

Мною был выбран пакет 1.8.2/PHP 5.4.27 (именно из-за его стабильности) версии 64-бита, под операционную систему Linux Mint 17 "Qiana" Cinnamon 64-bit.

После скачивания пакета открываю директорию "Downloads" (туда попадают все скачиваемые под Linux файлы) в терминале. Команда `ls` показывает мне содержимое этой директории - и файл `xampp-linux-x64-1.8.2-5-installer.run` в частности.

В этом же терминале делаю этот файл исполняемым:

{% highlight powershell %}
$ sudo chmod 755 xampp-linux-x64-1.8.2-5-installer.run
{% endhighlight %}

... затем запускаю файл `xampp-linux-x64-1.8.2-5-installer.run` на выполнение командой:

{% highlight powershell %}
$ sudo ./xampp-linux-x64-1.8.2-5-installer.run
{% endhighlight %}

## Инсталляция XAMPP под Linux Mint

Запуститься пошаговый графический инсталлятор локального сервера. Пользователи Windows могут почувствовать себя здесь немного в своей стихии. Ниже приведу скриншоты все шагов установки сервера с кратким их описанием, где это необходимо.

Сервер будет установлен в директорию `/opt/lampp`:

![Запуск установки XAMPP]({{site.url}}/images/uploads/2014/05/xampp_step_1.png)

![Выбор компонентов установки XAMPP]({{site.url}}/images/uploads/2014/05/xampp_step_2.png)

![Директория установки XAMPP]({{site.url}}/images/uploads/2014/05/xampp_step_3.png)

В этом шаге необходимо убрать галочку в строке "Learn more about Bitnami for XAMPP":

![Приложение Bitnami под XAMPP]({{site.url}}/images/uploads/2014/05/xampp_step_4.png)

![Установка начата]({{site.url}}/images/uploads/2014/05/xampp_step_5.png)

![Процесс инсталляции]({{site.url}}/images/uploads/2014/05/xampp_step_6.png)

В этом шаге оставляем галочку в строке "Launch XAMPP", чтобы локальный сервер автоматически запустился после установки:

![Завершение установки XAMPP]({{site.url}}/images/uploads/2014/05/xampp_step_7.png)

## Запуск и остановка XAMPP под Linux Mint

Помимо самого локального сервера будет установлено графическое приложение, задача которого - облегчить управление локальным сервером. Это приложение также запуститься автоматически, но его можно при необходимости запустить и вручную командой:

{% highlight powershell %}
cd /opt/lampp
sudo ./manager-linux-x64.run
{% endhighlight %}

![Приложение для управления XAMPP]({{site.url}}/images/uploads/2014/05/xampp_first_launch.png)

Переходим в этом приложении на вкладку "Manage Servers" и видим список служб локального сервера. Напротив каждой службы в виде лампочки показан ее статус - запущена она (Running) или остановлена (Stopped).

![Управление сервисами в XAMPP]({{site.url}}/images/uploads/2014/05/xampp_manage_servers.png)

Первоначально запущен только локальный сервер Apache; база данных "MySQL Database" и FTP-сервер "ProFTPD" остановлены. Их можно запустить из данного приложения, просто нажав кнопку "Start", но я поступлю более Linux-way и воспользуюсь терминалом. Для этого я введу в нем всего одну комадну:

{% highlight powershell %}
$ sudo /opt/lampp/lampp start
{% endhighlight %}

Если все пройдет успешно, то в терминале будет следующий вывод:

{% highlight powershell %}
Starting XAMPP for Linux 1.8.2-5...
  XAMPP: Starting Apache...ok.
  XAMPP: Starting MySQL...ok.
  XAMPP: Starting ProFTPD...ok.
{% endhighlight %}

... что можно проверить и в приложении:

![Запуск всех сервисов в XAMPP]({{site.url}}/images/uploads/2014/05/xampp_all_services_start.png)

Остановить локальный сервер можно также из терминала командой:

{% highlight powershell %}
$ sudo /opt/lampp/lampp stop
...
Stopping XAMPP for Linux 1.8.2-5...
XAMPP: Stopping Apache...ok.
XAMPP: Stopping MySQL...ok.
XAMPP: Stopping ProFTPD...ok.
{% endhighlight %}

## Установка WordPress под XAMPP в Linux Mint

С установкой локального сервера под Linux Mint разобрались. Стоит еще раз оговориться, что по моим субъективным оценкам он работает гораздо шустрее под Linux, нежели под Windows.

Переходим к заключительной части данной статьи и рассмотрим вопрос установки CMS WordPress под XAMPP в Linux Mint. Все виртуальные сервера располагаются в директории `/opt/lampp/htdocs/`.

То есть, если необходимо создать отдельный экземпляр какой-либо CMS (Joomla, WordPress, Drupal и так далее), то нужно просто создать поддиректорию в директории `htdocs` и распаковать туда нужную CMS. В моем случае такой CMS будет WordPress-3.9.1.

Создаю поддиректорию `travel` командой:

{% highlight powershell %}
$ sudo mkdir -p /opt/lampp/htdocs/travel
{% endhighlight %}

... и распаковываю в нее скачанный архив WordPress с помощью незаменимой консольной программы `mc` (не забудьте запустить ее через `sudo`, иначе получите ошибку прав доступа):

![Распаковка WordPress в XAMPP]({{site.url}}/images/uploads/2014/05/xampp_mc_wordpress_unpack.png)

После распаковки WordPress приступим к его установке. Создадим вручную конфигурационный файл `wp-config.php` чтобы избежать ошибки прав доступа при обычной пошаговой инсталляции WordPress (не забываем, что мы находимся под Linux!). Для этого скопируем файл-шаблон `wp-config-sample.php` в ту же директорию под именем `wp-config.php`:

{% highlight powershell %}
$ sudo cp /opt/lampp/htdocs/travel/wp-config-sample.php /opt/lampp/htdocs/travel/wp-config.php
{% endhighlight %}

... и отредактируем его через редактор nano:

{% highlight powershell %}
$ sudo nano -w /opt/lampp/htdocs/travel/wp-config.php
{% endhighlight %}

Затем в адресной строке браузера введем (XAMPP у нас все еще запущен, не забываем об этом!):

{% highlight powershell %}
http://localhost/phpmyadmin
{% endhighlight %}

... и в приложении phpMyAdmin создаем базу данных под наш будущий локальный сайт, на котором будет "крутиться" WordPress. Перезапускаем локальный сервер, чтобы он "подхватил" изменения в базе данных MySQL и создание виртульного сервера `travel` в директории `htdocs`:

{% highlight powershell %}
$ sudo /opt/lampp/lampp restart
...
Restarting XAMPP for Linux 1.8.2-5...
XAMPP: Stopping Apache...ok.
XAMPP: Stopping MySQL...ok.
XAMPP: Stopping ProFTPD...ok.
XAMPP: Starting Apache...ok.
XAMPP: Starting MySQL...ok.
XAMPP: Starting ProFTPD...ok.
{% endhighlight %}

В браузере в адресной строке запускаем установку WordPress:

{% highlight powershell %}
http://localhost/travel
{% endhighlight %}

... далее проходим оставшиеся стандартные шаги инсталляции WordPress и получаем готовый локальный сайт - переходим на него по адресу:

{% highlight powershell %}
http://localhost/travel
{% endhighlight %}

На этом установка CMS WordPress под локальный сервер успешно завершена. А также успешно выполнена рассмотренная выше инсталляция локального сервера под операционной системой Linux Mint 17 "Qiana" Cinnamon 64-bit.

## Заключение

Итог выполненных выше шагов - возможность иметь всегда "под рукой" готовый к работе локальный сервер. Еще один плюс к удобству кодинга под Linux. А кодинг под Linux субъективно для меня удобнее кодинга под Windows.

Стоит также сказать, что при установке и настройке могут возникнуть проблемы. В частности, автором данной статьи первоначально производилась установка "чистого" LAMPP, которая потом была удалена. И, хотя деинсталляция была произведена правильно, последующая установка XAMPP привела к тому, что данный сервер не запускался на компьютере.

На этом все.

---

 [1]: https://www.apachefriends.org/ru/faq_linux.html "FAQ Linux"
 [2]: https://www.apachefriends.org/ru/download.html "Download"
