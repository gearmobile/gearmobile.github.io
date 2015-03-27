---
title: Взлом Linux через GRUB
author: gearmobile
layout: post
permalink: /%d0%b2%d0%b7%d0%bb%d0%be%d0%bc-linux-%d1%87%d0%b5%d1%80%d0%b5%d0%b7-grub/
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - OS Linux
tags:
  - linux
---
Очень простой способ получить полный доступ (права root‘а) к системе Linux, используя загрузчик GRUB (даже LiveCD не нужен). Что для этого нужно? Только руки&#8230; Просто грузим систему и ждем появления меню GRUB‘а со списком установленных в системе операционных систем. Список может быть примерно такой:

<pre>Gentoo Linux 2.6.31-r6
  ArchLinux 2.6.31
  Ubuntu Karmic Koala 9.10
  Sabayon Linux r5.1 KDE</pre>

1. Выбираем систему (стрелочками вверх-вниз), к которой хотим получить доступ. И нажимаем буковку ‘e‘ на клавиатуре (‘e‘ – от ‘edit‘). Например, нам нужно «попасть» в Archlinux. Выбираем пункт Archlinux 2.6.31, нажимаем ‘e‘ и нам открывается для редактирования запись, соответствующая записи в конфигурационном файле GRUB menu.lst (для Debian-подобных систем, или grub.cfg – для Gentoo):

<pre>title Archlinux 2.6.31
  root (hd0,5)
  kernel /boot/vmlinuz26 root=/dev/sda6 ro vga=0?318
  initrd /boot/kernel26.img</pre>

2. Удаляем с строке kernel (в данном случае – третья по счету) все, кроме пути к ядру (/boot/vmlinuz26) и пути к разделу root (root=/dev/sda6). То есть, у нас получится запись такого вида:

<pre>kernel /boot/vmlinuz26 root=/dev/sda6</pre>

3. Дописываем в конец этой строки это: rw init=/bin/bash. В итоге запись будет выглядеть так:

<pre>kernel /boot/vmlinuz26 root=/dev/sda6 rw init=/bin/bash</pre>

4. Сохраняем результаты нашего «непосильного» труда – нажимаем ‘Enter‘ и затем грузим Archlinux с исправленными нами параметрами, нажав ‘b‘ (‘b’ – от ‘boot‘). В итоге у нас загружается консоль с правами root‘а. Что и требовалось. Дальше – только дело фантазии и умения&#8230;

Оцените статью:  
<span id="post-ratings-536" class="post-ratings" data-nonce="984e93fa21"><img id="rating_536_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(536, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_536_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(536, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_536_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(536, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_536_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(536, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_536_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(536, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_536_text"></span></span><span id="post-ratings-536-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>