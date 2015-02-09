---
title: 'Joomla QuickStart &#8211; как установить и настроить'
author: gearmobile
layout: post
permalink: /joomla-quickstart-%d0%ba%d0%b0%d0%ba-%d1%83%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%b8%d1%82%d1%8c-%d0%b8-%d0%bd%d0%b0%d1%81%d1%82%d1%80%d0%be%d0%b8%d1%82%d1%8c/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - CMS Joomla
tags:
  - joomla
---
На сегодняшний день многие популярные web-студии, создающие шаблоны под CMS Joomla, помимо самих шаблонов создают пакеты QuickStart. Что это такое и для чего предназначено? На самом деле все просто. Шаблоны, выполненные такими профессиональными студиями, как GavickPro (http://www.gavick.com/) и другие, являются чуть ли не произведениями исскуства. Помимо чистого дизайна, такие шаблоны обладают поистине устарашающим набором дополнительных &#8220;примочек&#8221;, расширяющих его возможности. Эти дополнительные &#8220;навороты&#8221; могут быть общеизвестными (K2) или же являться фирменной разработкой самой студии.

В результате, чтобы установить шаблон и заставить его работать, придется еще скачать массу различных расширений, половина из которых вообще может оказаться недоступной. Но и после установки этих расширений их надо еще настроить. А для этого необходимы знания, опыт и время. Но у большинства обычных пользователей, как правило, отсутствует и первое, и второе, и третье.

Поэтому, чтобы не усложнять жизнь другим (пользователям), а также и себе (техподержка в этом случае только выигрывает), большинство студий решило пойти по наиболее легкому пути.

Пакет QuickStart представляет из себя уже развернутую и готовую к использованию Joomla. В ней программистами на студии-разработчике заранее устанавливается шаблон со всеми необходимыми дополнениями. И производится настройка самого шаблона, чтобы он работал именно так, как было задумано. Чтобы не страдал от кривых рук неумелых пользователей. Потом все это хозяйство запаковывается в обычный zip-архив &#8211; и все, пакет QuickStart готов!

Теперь простому пользователю, после того, как он приобретет такой шаблон, будет достаточно развернуть его под удаленным или локальным хостингом. В результате он получит готовую к работе Joomla с предустановленным и настроенным шаблоном.

Давайте на практике разберемся, как установить и настроить шаблон Joomla QuickStart на примере работы студии ZOOTemplate (http://www.zootemplate.com/) и ее шаблона ZT Futa.

После скачивания шаблона получаем архив весом больше 20 Mb. Великовато будет для шаблона, не правда ли? Распаковываем этот архив и видим, что на самом деле он состоит из двух файлов, которые тоже, в свою очередь, являются архивами:

  * zt\_futa25\_installpackage.zip
  * zt\_futa25\_quickstart.zip<figure id="attachment_265" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_archive-600x139.png" alt="Распакованный архив шаблона ZT Futa" width="600" height="139" class="size-medium wp-image-265" />][1]<figcaption class="wp-caption-text">Распакованный архив шаблона ZT Futa</figcaption></figure> 

Первый файл &#8211; zt\_futa25\_installpackage.zip &#8211; собственно сам шаблон. А вот второй файл &#8211; zt\_futa25\_quickstart.zip &#8211; это и есть QuickStart, на что недвусмысленно указывает само его название, которое у разных производителей может отличаться. Но практически у всех в названии шаблона будет присутствовать слово quickstart.

Теперь нужно подготовить хостинг. У меня это локальный хостинг XAMPP. Запускаю его, перехожу в панель управления базами данных phpMyAdmin и создаю новую базу данных под будущий сайт ZT Futa:<figure id="attachment_266" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/db_zt_futa-600x246.png" alt="База данных ZT Futa" width="600" height="246" class="size-medium wp-image-266" />][2]<figcaption class="wp-caption-text">База данных ZT Futa</figcaption></figure> 

Перезапускаю MySQL, перехожу в TotalCommander по пути c:\Xampp\htdocs и создаю папку zt_futa.lc. В ней будет размещаться будущий сайт.

Распаковываю архив zt\_futa25\_quickstart.zip в папку c:\Xamppht\docs\zt_futa.lc. Посмотрим, что получилось в результате:<figure id="attachment_267" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_unpacked-600x464.png" alt="Распакованный архив ZT Futa QuickStart" width="600" height="464" class="size-medium wp-image-267" />][3]<figcaption class="wp-caption-text">Распакованный архив ZT Futa QuickStart</figcaption></figure> 

Даже по структуре каталогов и файлов видно, что это именно распакованная Joomla. Теперь осталось только установить ее.

Установка стандартная и ни чем не отличается от обычной &#8220;чистой&#8221; Joomla. Приведу пошаговое описание установки в картинках:<figure id="attachment_268" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_1-600x318.png" alt="Установка ZT Futa Шаг 1" width="600" height="318" class="size-medium wp-image-268" />][4]<figcaption class="wp-caption-text">Установка ZT Futa Шаг 1</figcaption></figure> <figure id="attachment_269" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_2-600x318.png" alt="Установка ZT Futa Шаг 2" width="600" height="318" class="size-medium wp-image-269" />][5]<figcaption class="wp-caption-text">Установка ZT Futa Шаг 2</figcaption></figure> <figure id="attachment_270" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_3-600x318.png" alt="Установка ZT Futa Шаг 3" width="600" height="318" class="size-medium wp-image-270" />][6]<figcaption class="wp-caption-text">Установка ZT Futa Шаг 3</figcaption></figure> <figure id="attachment_271" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_4-600x318.png" alt="Установка ZT Futa Шаг 4" width="600" height="318" class="size-medium wp-image-271" />][7]<figcaption class="wp-caption-text">Установка ZT Futa Шаг 4</figcaption></figure> <figure id="attachment_272" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_5-600x318.png" alt="Установка ZT Futa Шаг 5" width="600" height="318" class="size-medium wp-image-272" />][8]<figcaption class="wp-caption-text">Установка ZT Futa Шаг 5</figcaption></figure> <figure id="attachment_273" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_6-600x318.png" alt="Установка ZT Futa Шаг 6" width="600" height="318" class="size-medium wp-image-273" />][9]<figcaption class="wp-caption-text">Установка ZT Futa Шаг 6</figcaption></figure> <figure id="attachment_274" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_7-600x318.png" alt="Установка ZT Futa Шаг 7" width="600" height="318" class="size-medium wp-image-274" />][10]<figcaption class="wp-caption-text">Установка ZT Futa Шаг 7</figcaption></figure> 

И смотрим результат:<figure id="attachment_275" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_ready_green-600x303.png" alt="ZT Futa Green" width="600" height="303" class="size-medium wp-image-275" />][11]<figcaption class="wp-caption-text">ZT Futa Green</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-263" class="post-ratings" data-nonce="abbb31bd9f"><img id="rating_263_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(263, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_263_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(263, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_263_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(263, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_263_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(263, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_263_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(263, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_263_text"></span></span><span id="post-ratings-263-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_archive.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/10/db_zt_futa.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_unpacked.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_1.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_2.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_3.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_4.png
 [8]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_5.png
 [9]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_6.png
 [10]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_install_step_7.png
 [11]: http://localhost:7788/third/wp-content/uploads/2013/10/zt_futa_ready_green.png