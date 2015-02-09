---
title: 'PCLinuxOS LiveCD &#8211; восстановление загрузчика Grub'
author: gearmobile
layout: post
permalink: /pclinuxos-livecd-%d0%b2%d0%be%d1%81%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%bb%d0%b5%d0%bd%d0%b8%d0%b5-%d0%b7%d0%b0%d0%b3%d1%80%d1%83%d0%b7%d1%87%d0%b8%d0%ba%d0%b0-grub/
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - OS Linux
tags:
  - pclinuxos
---
С недавних пор открыл для себя такой дистрибутив Linux как PCLinuxOS. Поставил его исключительно для того, чтобы сделать скриншоты при написании статьи. Но в процессе установки и краткого пользования мне он понравился даже больше, чем Linux Mint, которым пользовался до этого.

И все бы хорошо, но проблема подкралась незаметно. Нет, она была связана не с PCLinuxOS. Наверное, как не трудно догадаться, это была Windows XP. Я не хочу сказать, что эта операционная система так уж плоха. Хотя бы ради таких прекрасных программ, как Adobe Dreamweaver, Adobe Photoshop, AutoCAD, MS Office ее просто нужно иметь на своем компьютере.

Но вот ее нежелание видеть другие операционные системы и стремление затереть MBR вне зависимости от того, есть там какие-либо записи или нет, напрягает. Все началось с того, что я проглядел статус четвертого раздела на своем жестком диске. А надо было заметить, так как он имел флаг загрузочного раздела. И хотя Windows установилась, как я и указал, на первый раздел, но все ее главные файлы (какие они там, не знаю) расположились на четвертом разделе. Все логично. А четвертый раздел у меня служит в качестве мусорной ямы для всех операционок, установленных на компе.

Результат предсказать нетрудно. В один прекрасный момент я решил основательно почистить мусорку-раздел от лишний файлов. В корзину неглядя полетели и файлы Windows XP. Стоит оговориться, что эта операционная система стоит у меня исключительно для работы, ради программ Adobe Dreamweaver, Adobe Photoshop, ABBYY Lingvo. Потребность в ней у меня есть и серьезная. Поэтому я был весьма опечален, когда в очередной раз загрузил комп и выбрал в меню Windows XP. Но система лишь посоветовала мне нажать волшебную комбинацию клавиш Ctrl+Alt+Del.

Подумал немного и решил, что проще и быстрее мне переустановить Windows. Ничего сложного в этом нет. Но вот запись MBR была затерта. А у меня еще стоят Linux Mint и PCLinuxOS, к которым нужно открыть доступ. Хорошо, у меня сохранился PCLinuxOS LiveCD. С помощью него я быстро и в несколько шагов переустановил Grub в главную загрузочную запись жесткого диска. Ниже приведу 7 последовательный ход действий по восстановлению Grub под PCLinuxOS.

Последовательность действий:</p> 

  * Вставляю PCLinuxOS LiveCD в дисковод и перезагружаюсь. В меню BIOS выбираю загрузку с оптического диска. Операционная система PCLinuxOS загружается на компьютер
  * Открываю терминал и захожу в нем под учетную запись root с помощью команды &#8220;su -&#8220;. Пароль для root в PCLinuxOS LiveCD имеет значение root (как ни странно!)
  * Ввожу команду &#8220;grub&#8221;. При этом приглашение командной строки изменится и примет вид &#8220;grub>&#8221;<figure id="attachment_529" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/grub_pclinuxos_livecd_1.jpg" alt="Вход в оболочку Grub" width="600" height="226" class="size-full wp-image-529" />][1]<figcaption class="wp-caption-text">Вход в оболочку Grub</figcaption></figure> 

  * Задаю команду для поиска файла stage1 &#8211; find /boot/grub/stage1. На моем компьютере Grub отыскал его только на одном разделе &#8211; (hd0,2). Это абсолютно верно, так как на /dev/sda3 установлена PCLinuxOS.
  * Ввожу команду &#8220;root (hd0,2)&#8221;
  * И устанавливаю Grub в MBR &#8211; &#8220;setup (hd0)&#8221;<figure id="attachment_530" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/grub_pclinuxos_livecd_2.jpg" alt="Успешная установка Grub" width="600" height="226" class="size-full wp-image-530" />][2]<figcaption class="wp-caption-text">Успешная установка Grub</figcaption></figure> 

Задача выполнена. Выхожу из оболочки Grub &#8211; &#8220;quit&#8221;. И перезагружаюсь. Описанный здесь способ восстановления Grub с помощью PCLinuxOS LiveCD подходит не только для этой операционной системы. Для любого случая, когда в качестве загрузчика используется Grub (но не Grub2), данное описание поможет с высокой долей вероятности.

На этом все.

Оцените статью:  
<span id="post-ratings-528" class="post-ratings" data-nonce="84b2c26c2a"><img id="rating_528_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(528, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_528_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(528, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_528_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(528, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_528_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(528, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_528_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(528, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_528_text"></span></span><span id="post-ratings-528-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/grub_pclinuxos_livecd_1.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/grub_pclinuxos_livecd_2.jpg