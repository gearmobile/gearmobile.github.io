---
title: 'ExFAT &#8211; файловая система для Mac OS X и Linux'
author: gearmobile
excerpt: 'ExFAT - универсальная файловая система для флеш-накопителей под Mac OS X. Идеальное решение для одновременной совместимости флеш-накопителя под Mac OS X, Linux и Windows. Эта система имеет нативную поддержку с Windows и Mac OS X. Поддержка в Linux решается одной строкой в консоли. Система поддерживает диски размером больше 4Gb и создана специально для флеш-накопителей. Умеет бережно "обращаться" с флешками.'
layout: post
permalink: /exfat-mac-os-linux/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
categories:
  - Mac OS X
tags:
  - exfat
  - mac os x
---
Тема достаточно освещенная, но для меня, как новичка в мире Mac OS X &#8211; очередное маленькое открытие.

Вопрос связан с одной небольшой проблемой &#8211; **выбором файловой системы для флешек**.

Для пары **Windows + Linux** обычным решением является файловая система **NTFS**. Обе операционные системы с ней прекрасно работают &#8211; **чтение+запись**.

Для пары **Mac OS X + Linux** такой выбор не подойдет, так как NTFS в Mac OS X имеет поддержку **только чтения**. Для записи нужно ставить сторонний софт, типа Paragon. Это не является решением &#8211; нужна **нативная поддержка** в обеих системах.

Решением является файловая система **ExFAT**. В Mac OS X у нее есть поддержка &#8220;из коробки&#8221;. В Linux поддержки &#8220;из коробки&#8221; нет &#8211; но проблема решается установкой дополнительных пакетов (*как почти всегда*).

Более того, в Сети [пишут о системе ExFAT][1] как изначально созданной для флеш-накопителей. Что она умеет **бережно относится к флешкам** и **поддерживает размер более 4Gb**.

Все отлично &#8211; ставлю ее на обе свои флешки: Apacer 8Gb и Transcend 16Gb. Начну с более сложного &#8211; с системы Linux.

### ExFAT &#8211; установка в Linux

Для включения поддержки файловой системы в Linux нужно установить пару пакетов &#8211; `exfat-fuse` и `exfat-utils`:

<pre>sudo apt-get install exfat-fuse exfat-utils
</pre>

Скажу, что приведенная выше команда на моей системе Linux Mint 17 Cinnamon **оказалась действенной** &#8211; все пакеты установились без проблем и поддержка ExFAT в системе появилась сразу же.

В Интернете почти на всех ресурсах приведена другая команда для установки пакетов `exfat-fuse` и `exfat-utils` (*причем &#8211; один в один, перепечатывают друг у друга вслепую* <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" /> ):

<pre>sudo add-apt-repository ppa:relan/exfat
sudo apt-get update
sudo apt-get install fuse fuse-exfat exfat-utils
</pre>

Однако, эта команда на моей системе не запустилась &#8211; выдала **ошибку ключа при подключении репозитория** `ppa:relan/exfat`. Именно этот факт и послужил для меня поводом написать этот краткий обзор.

Все &#8211; дело сделано. Теперь отформатирую флешку под файловую систему ExFAT в Linux.

Для этого сначала нахожу, где она расположена в файловой системе (в моем случае это устройство `/dev/sdb1`):

<pre>sudo fdisk -l
</pre>

&#8230; и затем произвожу форматирование флешки командой:

<pre>sudo mkfs.exfat -n large_flash /dev/sdb1
</pre>

где ключ `-n` &#8211; это задание для флешки **имени как устройства**.

Форматирование происходит буквально за пару секунд, ждать не придется. Первая флешка готова и операция форматирования выполнена под Linux.

### ExFAT &#8211; форматирование под Mac OS X

Как уже говорилось мною выше, система Mac OS X имеет **нативную поддержку** файловой системы ExFAT. То есть, ничего дополнительно ставить не придется &#8211; все готово &#8220;из коробки&#8221;.

Операции по форматированию накопителей и другим действиям с жесткими дисками производится в стандартной утилите &#8220;Disk Utility&#8221;.

Вставляю вторую флешку и запускаю &#8220;Disk Utility&#8221;:<figure id="attachment_1952" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/small_flash_exfat-600x379.png" alt="Создание ExFAT в дисковой утилите Disk Utility" width="600" height="379" class="size-medium wp-image-1952" />][2]<figcaption class="wp-caption-text">Создание ExFAT в дисковой утилите Disk Utility</figcaption></figure> 

Разобраться с работой этой утилиты нетрудно, но вкратце опишу.

Слева находиться окно со всеми подключенными дисками, которые утилита сумела обнаружить.

Справа на вкладке &#8220;Erase&#8221; производиться настройка и выполнение форматирования (в терминологии Mac OS X форматирование называется Erase). В списке &#8220;Format&#8221; выбирается нужная файловая система (*кстати, выбор небогатый*). В списке &#8220;Name&#8221; выбирается диск, который будет форматироваться. Там же находиться одноименная кнопка &#8220;Erase&#8221; для запуска форматирования.

Ниже располагается информативное (*я был приятно впечатлен объемом и качеством подачи информации в нем*) окно, в котором можно увидеть всю информацию по подключенному диску. Внимательный читатель заметит, что флешка у меня уже отформатирована в ExFAT &#8211; обзор делал &#8220;по горячим следам&#8221; :-).

В принципе &#8211; и все. Осталось нажать кнопку &#8220;Erase&#8221; и моя флешка отформатируется под систему ExFAT.

Если ее открыть в Finder, то теперь мне будут доступны как **чтение** с нее, так и **запись** на нее.

### Заключение

Вот так &#8220;неожиданно&#8221; я решил проблему совместимости флешки под Mac OS X и Linux. Более того, данная система ExFAT **является разработкой Microsoft**, поэтому с ее поддержкой в Windows **вообще нет проблем**.

А если учитывать обещанный создателями ExFAT **бережный способ обращения** с флеш-накопителями, то этому решению вообще цены нет.

На этом все &#8211; оцените статью:  
<span id="post-ratings-1951" class="post-ratings" data-nonce="5ba4c6762a"><img id="rating_1951_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1951, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1951_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1951, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1951_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1951, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1951_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1951, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1951_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1951, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1951_text"></span></span><span id="post-ratings-1951-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://en.wikipedia.org/wiki/ExFAT
 [2]: http://localhost:7788/third/wp-content/uploads/2014/11/small_flash_exfat.png