---
title: Командная строка (cmd) для веб-мастера
author: gearmobile
layout: post
permalink: /%d0%ba%d0%be%d0%bc%d0%b0%d0%bd%d0%b4%d0%bd%d0%b0%d1%8f-%d1%81%d1%82%d1%80%d0%be%d0%ba%d0%b0-cmd-%d0%b4%d0%bb%d1%8f-%d0%b2%d0%b5%d0%b1-%d0%bc%d0%b0%d1%81%d1%82%d0%b5%d1%80%d0%b0/
ratings_users:
  - 7
ratings_score:
  - 33
ratings_average:
  - 4.71
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - cmd
---
Для веб-разработчика, и для верстальщика в частности, первые вещи, которые он обязан знать, это языки HTML, CSS, Javascript с библиотекой jQuery. Желательно знание основ PHP, популярных CMS &#8211; WordPress, Joomla, Drupal. Обязательно знание основ работы в Photoshop, иначе просто не сможет верстальщик работать. Но причем здесь командная строка Windows, скажете вы? Это системному администратору в его ремесле она необходима, чтобы создавать bat-файлы, через терминал управлять удаленными соединениями, создавать и настраивать локальные сети. Для чего же она нужна человеку, который работает с веб-приложениями?

Оказывается, нужна. Не вся ее мощь, не все ее DOS-команды &#8211; только самые распространенные и необходимые. А нужна при работе с препроцессорами CSS, такими как SASS или LESS. Насчет LESS &#8211; это можно еще поспорить, а вот для SASS она понадобиться однозначно. Установка препроцессора SASS производиться через командную строку; процесс мониторинга также запускается через командную оболочку.

Так что давайте подтянем свои знания в этой области на тот уровень, который необходим. Ниже приведено краткое описание с примерами всех тех команд, которые могут потребоваться. Некоторые читатели могут сказать &#8211; а зачем плодить еще одну статью по командной строке Windows? В Интернете и так таких статей пруд пруди! На это могу сказать одно &#8211; этот сайт является моей записной книжкой. И здесь я выкладываю записи по принципу: &#8220;чтобы не забыть&#8221;, &#8220;описать задачу и ее выполнение самому, чтобы лучше понять&#8221;. Ну, лирика закончена, приступаем к делу.

### Горячие клавиши командной оболочки

  * Win+R &#8211; быстрый запуск командной оболочки;
  * Alt+Space &#8211; меню настройки командной строки;
  * F7 &#8211; показ списка введенных команд в оболочке;

cmd /f:on &#8211; включение перебора директорий по сочетанию Ctrl+D и перебора файлов по сочетанию Ctrl+F; (очень полезное свойство &#8211; благодаря ему не нужно вручную писать имя каталога, куда необходимо попасть, достаточно найти его методом перебора).

### Создание папок

  * mkdir sass &#8211; создание новой папки sass в корне текущего диска;
  * md sass &#8211; аналогично предыдущей (укороченный вариант);
  * md sassverstka &#8211; создание вложенных директорий;
  * md F:verstkarevoltz &#8211; создание директорий в указанном диске;

### Просмотр содержимого каталогов

  * tree &#8211; показ дерева каталогов;
  * tree /f &#8211; показ дерева каталогов с их содержимым;
  * tree F:sass &#8211; показ &#8220;куска&#8221; дерева каталогов, начиная с указанного места;
  * dir &#8211; просмотр содержимого текущего диска (каталога) в виде списка;
  * dir F: &#8211; просмотр содержимого диска F;
  * dir /p F: &#8211; постраничный вывод содержимого диска F:
  * type test.txt &#8211; просмотр содержимого файла (расширение файла указывать обязательно);

### Перемещение по каталогам и дискам

  * cd /d F: &#8211; переход в корень диска F: (*для меня, как бывшего линуксоида, странное и неудобное нагромождение с ключом*)
  * cd.. &#8211; перейти на уровень вверх;
  * cd FolderFolder2Folder3 &#8211; перейти в папку Folder3;

### Удаление файлов и каталогов

  * del test.txt &#8211; удалить файл (расширение файла указывать обязательно);
  * rmdir folder3 &#8211; удалить папку (директорию);

### Копирование и перемещение

  * copy text.txt FolderFolder2Folder3 &#8211; скопировать файл в директорию Folder3;
  * move text.txt FolderFolder2Folder3 &#8211; переместить файл в директорию Folder3;

### Разное

  * cls &#8211; очистка экрана ввода;

Для работы в командной строке также желательно ее настроить, облагородить под себя. Ибо изначально вид командной оболочки достаточно непригляден. Для открытия свойств окна терминала достаточно щелкнуть ПКМ на любом месте заголовка окна. Затем перейти в свойства &#8211; окно с четырьмя вкладками.

Первую &#8211; Options &#8211; можно пропустить, там ничего особо интересного нет.

Вторая вкладка &#8211; Font &#8211; для настройки шрифтов. Лучше всего поставить шрифт Lucida Console и кегль 12:<figure id="attachment_61" style="width: 386px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/font-cmd.jpg" alt="Шрифты терминала Windows" width="386" height="474" class="size-full wp-image-61" />][1]<figcaption class="wp-caption-text">Шрифты терминала Windows</figcaption></figure> 

Третья вкладка &#8211; Layout &#8211; для настройки размеров окна. Наиболее удобные размеры приведены на рисунке:<figure id="attachment_62" style="width: 386px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/layout-cmd.jpg" alt="Размеры окна терминала Windows" width="386" height="474" class="size-full wp-image-62" />][2]<figcaption class="wp-caption-text">Размеры окна терминала Windows</figcaption></figure> 

Четвертая вкладка &#8211; Colors &#8211; для настройки цветов фона, текста. Всплывающее окно (появляется по нажатию клавиши F7) также настраивается с помощью фонового цвета и цвета текста &#8211; но кто его использует? (*можно оставить &#8220;как есть&#8221;*):<figure id="attachment_63" style="width: 386px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/colors-cmd.jpg" alt="Цвета терминала Windows" width="386" height="474" class="size-full wp-image-63" />][3]<figcaption class="wp-caption-text">Цвета терминала Windows</figcaption></figure> 

Конечно, все настройки индивидуальны. Как говориться, на вкус и цвет&#8230; Поэтому рисунок ниже &#8211; примерный вид того, каким может быть настроенный терминал Windows:<figure id="attachment_64" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/terminal-cmd-600x327.jpg" alt="Вид терминала Windows" width="600" height="327" class="size-medium wp-image-64" />][4]<figcaption class="wp-caption-text">Вид терминала Windows</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-58" class="post-ratings" data-nonce="c73d892e95"><img id="rating_58_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(58, 1, '1 Star');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_58_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(58, 2, '2 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_58_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(58, 3, '3 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_58_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(58, 4, '4 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_58_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(58, 5, '5 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>7</strong> votes, average: <strong>4,71</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_58_text"></span></span><span id="post-ratings-58-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/10/font-cmd.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/10/layout-cmd.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/10/colors-cmd.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2013/10/terminal-cmd.jpg