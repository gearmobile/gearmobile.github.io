---
title: 'Pdfimages &#8211; извлечь картинки из pdf-файлов в Linux'
author: gearmobile
layout: post
permalink: /pdfimages-%d0%b8%d0%b7%d0%b2%d0%bb%d0%b5%d1%87%d1%8c-%d0%ba%d0%b0%d1%80%d1%82%d0%b8%d0%bd%d0%ba%d0%b8-%d0%b8%d0%b7-pdf-%d1%84%d0%b0%d0%b9%d0%bb%d0%be%d0%b2-%d0%b2-linux/
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - OS Linux
tags:
  - pdfimages
---
С недавнего времени, всерьез занявшись написанием статей, столкнулся в небольшой трудностью. Заключается она в следующем: имеется материал в формате pdf, перевод которого необходимо выполнить. Естественно, в любой более-менее серьезной и качественной статье есть скриншоты, хотя бы один или два.

Что делать, если хочется создать точный &#8211; и самое главное &#8211; хороший перевод? Нужно, чтобы в этом переводе тоже присутствовали соответствующие теме скрины. И как поступить? Создавать свои собственные? Это довольно трудоемкий и длительный процесс. Конечно, речь не идет о какой-либо программе &#8211; в репозиториях Linux достаточно одной команды, чтобы ее поставить. А вот если дело касается дистрибутива? И если он &#8220;весит&#8221; около 2Gb? &#8220;Тянуть&#8221; и ставить его только ради скриншотов?

Вывод однозначен &#8211; надо &#8220;забрать&#8221; картинки из самого pdf-файла. Под OS Windows ответ напрашивается сам собой &#8211; Adobe Acrobat. Но если под Linux? Тоже выход есть! И даже еще аккуратнее &#8211; не надо мучиться с установкой гиганта Acrobat только для извлечения картинок с помощью последнего (например, у меня версия Adobe Acrobat 9.4 Pro &#8220;весит&#8221; 631Mb! Уму непостижимо &#8211; ведь это всего лишь одна программа!).

Итак, решаем проблему под Linux.

### Первый шаг

Устанавливаем пакет xpdf. Программа стара, как мир и имеется в репозитории любого уважающего себя дистрибутива Linux. А об Ubuntu/Debian и говорить не приходиться. Там как в Греции &#8211; все есть!

<pre>$ sudo aptitude install xpdf</pre>

### Шаг второй

Сама по себе &#8220;смотрелка&#8221; pdf-файлов xpdf нам в принципе не нужна. Интерфейс у нее убогий и не тянет на сравнение с тем же Okular. Но это и не важно. Мы ее не затем ставили. А ставили ради маленькой программы pdfimages, которая входит в состав этого пакета. Лишний раз проверим, так ли это. Посмотрим, есть ли она в системе после установки xpdf:

<pre>$ whereis pdfimages
    pdfimages: /usr/bin/pdfimages /usr/share/man/man1/pdfimages.1.gz</pre>

Есть. Все ОК.

### Шаг третий

Теперь, собственно, и приступаем к самому процессу извлечения. Переходим в директорию, в которой лежит наш &#8220;пациент&#8221; &#8211; jul2011.pdf:

<pre>$ cd /media/disk-2/works/journals/indian_hacker
    $ ls
    apr2011.pdf jul2011.pdf jun2011.pdf mar2011.pdf may2011.pdf</pre>

И &#8220;напускаем&#8221; на него нашу &#8220;крошку&#8221; pdfimages:

<pre>$ pdfimages -f 3 -l 9 -j jul2011.pdf nessus</pre>

Опции команды описывать не буду &#8211; они, прямо скажем, примитивны и легко узнаются по стандартной команде &#8211;help. Здесь я применил только некоторые из них (и если честно сказать &#8211; почти все):

  * -f &#8211; номер первой страницы pdf-файла, из которого будут извлекаться картинки;
  * -l &#8211; аналогично &#8211; номер последней страницы pdf-файла (то есть, опциями f и l мы задаем диапазон в pdf-файле, откуда будем извлекать картинки; это в том случае, когда не хотим получить ВСЕ картинки из ВСЕГО pdf-файла);
  * -j &#8211; конвертировать извлеченные картинки в формат jpg

Единственное, о чем стоит упомянуть &#8211; это следующее. У меня вызвано легкий ступор, ибо является неочевидным фактом: имя nessus в конце команды. Это имя может быть любым другим, на ваш выбор, но оно должно быть! Это своеобразная маска, по которой программа pdfimages создает имена графических файлов. За примером далеко ходить не надо. Смотрим на результат работы малютки &#8211; и все сразу станет понятно:

<pre>$ ls nessus-003.jpg nessus-007.ppm nessus-011.ppm nessus-015.ppm nessus-019.ppm
    nessus-023.jpg nessus-027.jpg nessus-000.ppm nessus-004.ppm nessus-008.ppm
    nessus-012.ppm nessus-016.ppm nessus-020.ppm nessus-024.ppm nessus-001.ppm
    nessus-005.ppm nessus-009.jpg nessus-013.jpg nessus-017.jpg nessus-021.jpg
    nessus-025.ppm nessus-002.jpg nessus-006.ppm nessus-010.jpg nessus-014.jpg
    nessus-018.jpg nessus-022.jpg nessus-026.jpg</pre>

Программка pdfimages даже оказалась слишком старательной &#8211; она вытянула все, что смогла. И что смогла &#8211; переконвертировала в формат jpg, как мы ей и сказали опцией -j. А что не смогла &#8211; оставила в формате ppm. Об этом же говориться и в man&#8217;е программы:<cite> &#8220;Normally, all images are written as PBM (for monochrome images) or PPM (for non-monochrome images) files. With this option, images in DCT format are saved as JPEG files. All non-DCT images are saved in PBM/PPM format as usual.&#8221; </cite>

Ну, нам ее излишняя старательность ни к чему (все, что она сохранила в формате ppm, является несущественным в данном случае), поэтому выполняем легким движением руки (точнее &#8211; пальцев):

<pre>$ rm *.ppm</pre>

И опять смотрим:

<pre>$ ls nessus-003.jpg nessus-010.jpg nessus-014.jpg nessus-018.jpg
    nessus-022.jpg nessus-026.jpg nessus-002.jpg nessus-009.jpg
    nessus-013.jpg nessus-017.jpg nessus-021.jpg nessus-023.jpg
    nessus-027.jpg</pre>

Совсем другое дело! Как раз то, что нам нужно! Можно сказать, дело в шляпе. Посмотрим результат. Ведь интересно же &#8211; действительно ли все получилось? Пусть это будет nessus-027.jpg:<figure id="attachment_631" style="width: 495px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/nessus-027.jpg" alt="Пример работы утилиты pdfimages в Linux" width="495" height="404" class="size-full wp-image-631" />][1]<figcaption class="wp-caption-text">Пример работы утилиты pdfimages в Linux</figcaption></figure> 

### Резюме

Как вам такое решение &#8220;проблемы&#8221;? Для меня, так очень даже ничего! Изящно, красиво и быстро. И самое главное &#8211; результат! И тогда зачем возиться с программами под Windows, такими как например, специализированная утилита PDF Image Extraction Wizard. Да, имеет она красивый интерфейс. Но ведь фактически нужно платить только за него. Я уже не говорю о стоимости &#8220;монстра&#8221; Adobe Acrobat!

Оцените статью:  
<span id="post-ratings-630" class="post-ratings" data-nonce="36ab0d59cf"><img id="rating_630_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(630, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_630_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(630, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_630_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(630, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_630_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(630, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_630_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(630, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_630_text"></span></span><span id="post-ratings-630-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/nessus-027.jpg