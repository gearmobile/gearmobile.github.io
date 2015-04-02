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

Перепробовал достаточно способов, в том числе и с официального сайта XAMPP - [XAMPP работает, но почему картинки не отображаются?][2]. То, что там описано - изменение двух строк файла `/opt/lampp/etc/httpd.conf`:

<pre>#EnableMMAP off
  #EnableSendfile off
  </pre>

&#8230; не сработало, так как в моем конфигурационном файле `httpd.conf` обе строчки были расскоментированы по умолчанию:

<pre>EnableMMAP off
  EnableSendfile off
  </pre>

Решение оказалось на удивление простым. Я и не подозревал, что настройка прав доступа в Linux может быть такой "коварной" штукой! Сначала обратил внимание на тот факт, что preview тем WordPress, которые идут "в комплекте" с ним - Twenty Fourteen, Twenty Thirteen, Twenty Twelve нормально отображаются на странице. А вот preview моей темы - не отображается:<figure id="attachment_1327" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/xampp_theme-wordpress_not_show-600x192.png" alt="Предпросмотр темы не отображается в WordPress под XAMPP" width="600" height="192" class="size-medium wp-image-1327" />][3]<figcaption class="wp-caption-text">Предпросмотр темы не отображается в WordPress</figcaption></figure>

Решил проверить догадку методом "научного тыка" - тупо сравнить два файла-preview `screenshot.png` из разных тем, своей Choose и стандартной Twenty Fourteen:

<pre>$ ls -l choose/wp-content/themes/twentyfourteen/screenshot.png
  -rw-r--r-- 1 choose/wp-content/themes/twentyfourteen/screenshot.png
  $ ls -l choose/wp-content/themes/choose/screenshot.png
  -rw------- 1 choose/wp-content/themes/choose/screenshot.png
  </pre>

Вот оно! У файла `screenshot.png` из темы Twenty Fourteen имеются права на чтение (r) для - владельца, группы и всех остальных (-rw-r-r-). У файла `screenshot.png` из моей темы Choose имеются права на просмотр (r) только для владельца данного файла (-rw&#8212;&#8212;-).

Ну что-же, нужно добавить (+) права чтения (r) для всех (a) пользователей файла `screenshot.png` темы Choose:

<pre>$ sudo chmod a+r /opt/lampp/htdocs/choose/wp-content/themes/choose/screenshot.png
  </pre>

&#8230; и проверить результат:

<pre>$ ls -l /opt/lampp/htdocs/choose/wp-content/themes/choose/screenshot.png
  -rw-r--r-- 1 /opt/lampp/htdocs/choose/wp-content/themes/choose/screenshot.png
  </pre>

Перехожу в WordPress на страницу управления темами `wp-admin/themes.php` и смотрю, что получилось:<figure id="attachment_1326" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/xampp_theme-wordpress-600x190.png" alt="Рабочее preview создаваемой темы WordPress под XAMPP" width="600" height="190" class="size-medium wp-image-1326" />][4]<figcaption class="wp-caption-text">Рабочее preview создаваемой темы WordPress</figcaption></figure>

Картинка по центру изображения - это preview создаваемой темы Choose под WordPress. Как видно, все прошло удачно.

### Картинки темы WordPress не отображаются под XAMPP

Но вышеназванное решение оказалось лишь половиной дела. Вторая проблема заключалась в том, что при активации вновь созданной темы под WordPress изображения из нее не отображаются на странице.

Фоновые изображения, картинки в HTML-файле - ничего не появляется на странице. Firebug не смог мне помочь - единственное, что он "подсказал" - "Файл невозможно загрузить". Многословно, ничего не скажешь!

Помог незаменимый ресурс для front-end разработчика - [Stack Overflow][5]. Решение проблемы заключено в двух строках:

<pre>$ cd /opt/lampp/htdocs
  $ sudo chmod 777 -R .
  </pre>

То есть, переходим в директорию `htdocs` и меняем рекурсивно (-R) права на все действия (777) для всего содержимого текущей (.) директории. Не знаю, как там с вопросами безопасности в этом случае, но факт остается фактом - все стало работать, как и надо было:<figure id="attachment_1328" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/xampp_theme-wordpress_show_pictures-600x175.png" alt="Изображения темы WordPress корректно отображаются на странице XAMPP" width="600" height="175" class="size-medium wp-image-1328" />][6]<figcaption class="wp-caption-text">Изображения темы WordPress корректно отображаются на странице</figcaption></figure>

В принципе, на этом все.

Оцените статью:
<span id="post-ratings-1322" class="post-ratings" data-nonce="3410c444ee"><img id="rating_1322_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1322, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1322_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1322, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1322_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1322, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1322_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1322, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1322_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1322, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1322_text"></span></span><span id="post-ratings-1322-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1272 "Установка XAMPP под Linux Mint 17"
 [2]: https://www.apachefriends.org/ru/faq_linux.html "XAMPP работает, но почему картинки не отображаются?"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/06/xampp_theme-wordpress_not_show.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/06/xampp_theme-wordpress.png
 [5]: http://stackoverflow.com/ "Stack Overflow"
 [6]: http://localhost:7788/third/wp-content/uploads/2014/06/xampp_theme-wordpress_show_pictures.png
