---
title: 'Rankmirrors &#8211; выбор быстрых репозиториев в ArchLinux'
author: gearmobile
layout: post
permalink: /rankmirrors-%d0%b2%d1%8b%d0%b1%d0%be%d1%80-%d0%b1%d1%8b%d1%81%d1%82%d1%80%d1%8b%d1%85-%d1%80%d0%b5%d0%bf%d0%be%d0%b7%d0%b8%d1%82%d0%be%d1%80%d0%b8%d0%b5%d0%b2-%d0%b2-archlinux/
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
  - rankmirrors
---
В Arch имеется скрипт для настройки конфигурационного файла /etc/pacman.d/mirrorlist – rankmirrors. Что он делает? rankmirrors берет список IP-адресов зеркал репозиториев Archlinux из заранее созданного файла и проверяет их на скорость доступа. А затем формирует список самых быстрых зеркал на основе этой проверки. Что это дает? В результате работы rankmirrors в /etc/pacman.d/mirrorlist мы имеем сервера с самым быстрым (исходяя из местоположения нашей машины) доступом. При обновлении системы или установки какой-либо программы скорость инсталляции существенно возрастает (из чего складывается инсталляция? Из скачивания пакета с сервера и уже затем его установки).rankmirrors является python-скриптом. man-страницы не имеет, но есть опция &#8211;help с небольшим выбором команд.

Похожими утилитами являются netselect и особенно – mirrorselect (для Gentoo). Итак, приступим к настройке нашего списка зеркал с помощью rankmirrors.

1. Так как rankmirrors является python-скриптом, для его работы необходим установленный Python в системе. Устанавливаем, если его нет в системе:

<pre>$ sudo pacman -Sy python</pre>

2. Переходим в директорию со списком зеркал pacman‘а:

<pre>$ cd /etc/pacman.d/
</pre>

3. Делаем копию существующего списка зеркал mirrorlist:

<pre>$ sudo cp mirrorlist mirrorlist.backup
</pre>

4. Открываем копию списка зеркал в своем любимом редакторе и раскомментируем все строки с адресами серверов, географически наиболее близко расположенных к нам (по идее, это и будут сервера с самым быстрым доступом):

<pre>$ sudo nano -w mirrorlist.backup
</pre>

5. Сохраняем изменения в файле и выходим из него. Запускаем скрипт rankmirrors для выбора зеркал из указанного нами списка (для запуска rankmirrors потребуется войти в учетную запись root‘а. Под sudo у меня скрипт отказался работать, ругаясь на отсутствие прав доступа к файлу mirrorlist).

Переходим в учетную запись root‘а:

<pre>$ su -
</pre>

Запускаем rankmirrors под root‘ом:

<pre># rankmirrors -n 6 mirrorlist.backup &gt; mirrorlist
</pre>

где:

  * -n 6 – вывести (в нашем случае – записать) 6 сервером с самым маленьким временем отклика
  * mirrorlist.backup – список серверов для теста на время отклика
  * mirrorlist – файл, куда записываются адреса серверов скриптом rankmirros

В результате rankmirrors удалит все раскомментированные строки в mirrorlist и снесет адреса шести самых «быстрых» зеркал. Получится что-то вроде этого:

<pre># Result
  Server = ftp://ftp.nluug.nl/pub/metalab/distributions/archlinux/$repo/os/i686
  Server = ftp://ftp.free.fr/mirrors/ftp.archlinux.org/$repo/os/i686
  Server = ftp://ftp.mfa.kfki.hu/pub/mirrors/ftp.archlinux.org/$repo/os/i686
  Server = http://gd.tuwien.ac.at/opsys/linux/archlinux/$repo/os/i686
  Server = http://ftp.gigabit.nu/$repo/os/i686
  Server = http://mirror.svk.su/archlinux/$repo/os/i686
</pre>

Здесь я раскомментировал все зеркала, географически расположенные в Европе и получил 6 из них.

6. Теперь осталось последнее – заставить pacman перечитать список зеркал и обновить список пакетов.

Делаем:

<pre># pacman -Syy
</pre>

Результат:

<pre>:: Синхронизируются базы данных пакетов…
  core 35,8K
  65,8K/s 00:00:01 [######################] 100%
  extra 443,7K 15,4K/s 00:00:29 [#########################] 100%
  community 367,8K
  18,1K/s 00:00:20 [###########################] 100%
  archlinuxfr 24,7K 5,7K/s 00:00:04 [############################] 100%
</pre>

Данная статья является вольным переводом (опробованным для своих нужд) из Википедии Archlinux.

Оцените статью:  
<span id="post-ratings-555" class="post-ratings" data-nonce="328cb5579f"><img id="rating_555_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(555, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_555_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(555, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_555_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(555, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_555_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(555, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_555_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(555, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_555_text"></span></span><span id="post-ratings-555-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>