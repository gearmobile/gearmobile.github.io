---
title: Clonezilla – установка на USB-флешку или USB-диск
author: gearmobile
layout: post
permalink: /clonezilla-%d1%83%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%ba%d0%b0-%d0%bd%d0%b0-usb-%d1%84%d0%bb%d0%b5%d1%88%d0%ba%d1%83-%d0%b8%d0%bb%d0%b8-usb-%d0%b4%d0%b8%d1%81%d0%ba/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - OS Linux
tags:
  - clonezilla
---
Дистрибутив Clonezilla в особом представлении не нуждается. Возможности программы достаточно широки на сегодняшний день. Проект развивается, в него добавляются все новые функции и возможности. На сегодняшний день почти все дистрибутивы Linux обладают возможностью загрузки как с диска, так и с флешки\внешнего жесткого диска. Это также может делать и Clonezilla. Дальше – шаги по установке дистра на флешку или hard disk из Windows.

### Как установить Clonezilla на USB

  * Выбираем и скачиваем (http://sourceforge.net/lirojects/clonezilla/files/) Clonezilla Live USB файл для USB (образы для флешки жесткого диска имеют расширение .zip)
  * Скачиваем утилиту HP-USB Format tool. С ее помощью можно отформатировать флешку\диск в файловую систему FAT\FAT32 и сделать загрузочной. Это может помочь, если штатные средства Windows не могут сделать ее таковой
  * Распаковываем архив Clonezilla Live Zip на съемный носитель
  * Переходим на съемный флешку\диск с уже распакованной на ней Clonezilla Live Zip, заходим в utils\win32 и запускаем makeboot.bat

> Осторожно! Запускать файл makeboot.bat нужно только на флешке или съемном жестком диске (где он и должен лежать после распаковки Clonezilla Live Zip)! Запуск его на локальном жестком диске приведет к тому, что Windows перестанет грузиться!

  * Перезагружаемся выставляем в меню BIOS’а загрузку с USB HDD или выбираем в Загрузочном меню BIOS’а тот же пункт (у меня – вход в &#8220;Загрузочное меню BIOS&#8221; – F12)
  * Происходит загрузка Clonezilla USB
  * Следуем пошаговым инструкциям wizard‘а

На этом все. Оцените статью:  
<span id="post-ratings-669" class="post-ratings" data-nonce="b3b0330060"><img id="rating_669_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(669, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_669_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(669, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_669_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(669, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_669_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(669, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_669_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(669, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_669_text"></span></span><span id="post-ratings-669-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>