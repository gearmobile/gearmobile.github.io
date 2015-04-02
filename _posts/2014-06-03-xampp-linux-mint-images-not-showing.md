---
title: "XAMPP Linux Mint - не отображаются картинки"
layout: post
categories: css
tags: [wordpress, xampp]
share: true
---

> Столкнулся с небольшой, но достаточно неприятной проблемой.

Занимался изучением настройки сверстанного HTML-шаблона под WordPress. То есть, другими словами - создания темы WordPress из готового HTML-шаблона.

Для этой задачи у меня на Linux Mint 17 Cinnanom 64-bit установлен локальный сервер XAMPP. Если кто не знает, как сервер XAMPP устанавливается под Linux, то могут почитать в этой статье - "Установка XAMPP под Linux Mint 17". Под локальным сервером у меня "крутятся" виртуальные хосты на основе движка WordPress.

## Предпросмотр темы не отображается в WordPress

После создания директории под новую тему - `Choose` закинул к нее скриншот готовой темы для preview в менедежере тем WordPress - `wp-admin/themes.php`. Но вот неожиданность - картинка-скриншот будущей темы Choose не отобразилась!

Перепробовал достаточно способов, в том числе и с официального сайта XAMPP - [XAMPP работает, но почему картинки не отображаются?][1]. То, что там описано - изменение двух строк файла `/opt/lampp/etc/httpd.conf`:

{% highlight json %}
#EnableMMAP off
#EnableSendfile off
{% endhighlight %}

... не сработало, так как в моем конфигурационном файле `httpd.conf` обе строчки были расскоментированы по умолчанию:

{% highlight json %}
EnableMMAP off
EnableSendfile off
{% endhighlight %}

Решение оказалось на удивление простым. Я и не подозревал, что настройка прав доступа в Linux может быть такой "коварной" штукой! Сначала обратил внимание на тот факт, что preview тем WordPress, которые идут "в комплекте" с ним - "Twenty Fourteen", "Twenty Thirteen", "Twenty Twelve" нормально отображаются на странице. А вот `preview` моей темы - не отображается:

![Предпросмотр темы не отображается в WordPress]({{site.url}}/images/uploads/2014/06/xampp_theme-wordpress_not_show.png)

Решил проверить догадку методом "научного тыка" - тупо сравнить два файла-preview `screenshot.png` из разных тем, своей "Choose" и стандартной "Twenty Fourteen":

{% highlight powershell %}
$ ls -l choose/wp-content/themes/twentyfourteen/screenshot.png
-rw-r--r-- 1 choose/wp-content/themes/twentyfourteen/screenshot.png

$ ls -l choose/wp-content/themes/choose/screenshot.png
-rw------- 1 choose/wp-content/themes/choose/screenshot.png
{% endhighlight %}

Вот оно! У файла `screenshot.png` из темы "Twenty Fourteen" имеются права на чтение `r` для - владельца, группы и всех остальных `-rw-r-r-`. У файла `screenshot.png` из моей темы "Choose" имеются права на просмотр `r` только для владельца данного файла `-rw- - -`.

Ну что-же, нужно добавить `+` права чтения `r` для всех `a` пользователей файла `screenshot.png` темы "Choose":

{% highlight powershell %}
$ sudo chmod a+r /opt/lampp/htdocs/choose/wp-content/themes/choose/screenshot.png
{% endhighlight %}

... и проверить результат:

{% highlight powershell %}
$ ls -l /opt/lampp/htdocs/choose/wp-content/themes/choose/screenshot.png
-rw-r--r-- 1 /opt/lampp/htdocs/choose/wp-content/themes/choose/screenshot.png
{% endhighlight %}

Перехожу в WordPress на страницу управления темами `wp-admin/themes.php` и смотрю, что получилось:

![Рабочее preview создаваемой темы WordPress]({{site.url}}/images/uploads/2014/06/xampp_theme-wordpress.png)

Картинка по центру изображения - это preview создаваемой темы "Choose" под WordPress. Как видно, все прошло удачно.

## Картинки темы WordPress не отображаются под XAMPP

Но вышеназванное решение оказалось лишь половиной дела. Вторая проблема заключалась в том, что при активации вновь созданной темы под WordPress изображения из нее не отображаются на странице.

Фоновые изображения, картинки в HTML-файле - ничего не появляется на странице. Firebug не смог мне помочь - единственное, что он "подсказал" - "Файл невозможно загрузить". Многословно, ничего не скажешь!

Помог незаменимый ресурс для front-end разработчика - [Stack Overflow][2]. Решение проблемы заключено в двух строках:

{% highlight powershell %}
$ cd /opt/lampp/htdocs
$ sudo chmod 777 -R .
{% endhighlight %}

То есть, переходим в директорию `htdocs` и меняем рекурсивно `-R` права на все действия `777` для всего содержимого текущей `.` директории. Не знаю, как там с вопросами безопасности в этом случае, но факт остается фактом - все стало работать, как и надо было:

![Изображения темы WordPress корректно отображаются на странице]({{site.url}}/images/uploads/2014/06/xampp_theme-wordpress_show_pictures.png)

В принципе, на этом все.

---

[1]: https://www.apachefriends.org/ru/faq_linux.html "XAMPP - картинки не отображаются"
[2]: http://stackoverflow.com/ "Stack Overflow"
