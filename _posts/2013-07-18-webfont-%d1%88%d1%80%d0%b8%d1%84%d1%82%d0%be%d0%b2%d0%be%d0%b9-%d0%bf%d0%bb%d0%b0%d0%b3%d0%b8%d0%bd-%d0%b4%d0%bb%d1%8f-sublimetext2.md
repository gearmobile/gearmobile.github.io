---
title: 'WebFont &#8211; шрифтовой плагин для SublimeText2'
author: gearmobile
layout: post
permalink: /webfont-%d1%88%d1%80%d0%b8%d1%84%d1%82%d0%be%d0%b2%d0%be%d0%b9-%d0%bf%d0%bb%d0%b0%d0%b3%d0%b8%d0%bd-%d0%b4%d0%bb%d1%8f-sublimetext2/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Web Tools
tags:
  - webfont
---
Хороший ресурс со шрифтами создан усилиями нескольких участников форума forum.htmlbook.ru. Адрес ресурса &#8211; http://webfont.ru. На этом сайте собрана коллекция самых разнообразных и, самое главное, часто используемых шрифтов для web. Шрифты постоянно обновляются и добавляются.

Пользоваться сайтом можно двумя способами.

Первый &#8211; поиск и скачивание нужного набора шрифтов на самом ресурсе. На нем реализован механизм поиска. Скачивание необходимо делать в обязательном порядке, если шрифты будут использоваться на вашем собственном сайте. На локальную машину скачивается набор шрифтов, составляющих указанное семейство, и css-файл c правилами подключения его в коде. Точно также, как у известного FontSquirrel.

Второй &#8211; участник форума forum.htmlbook.ru Softlink сделал замечательную вещь &#8211; плагин под Sublime Text 2. Плагин называется WebFont и его установка производится как обычно, через менеджер плагинов в этом редакторе:<figure id="attachment_569" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/install_plugin-600x303.png" alt="Установка плагина WebFont" width="600" height="303" class="size-medium wp-image-569" />][1]<figcaption class="wp-caption-text">Установка плагина WebFont</figcaption></figure> 

После подключения вставка в код нужного набора шрифтов производится двумя движениями. Для начала открываем сам плагин с помощью сочетания клавиш Ctrl+Alt+F:<figure id="attachment_570" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/install_font-600x303.png" alt="Выбор шрифта для установки" width="600" height="303" class="size-medium wp-image-570" />][2]<figcaption class="wp-caption-text">Выбор шрифта для установки</figcaption></figure> 

В появившемся списке выбираем нужный шрифт (можно клавишами-стрелками) и нажимаем Enter. Плагин автоматически вставит в тело документа ссылку на выбранное семейство шрифтов и в комментариях укажет, какие именно семейства были подключены. Теперь достаточно выбрать нужный font-family, а ненужные удалить или закомментировать:<figure id="attachment_571" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/import_font-600x303.png" alt="Подключенный шрифт" width="600" height="303" class="size-medium wp-image-571" />][3]<figcaption class="wp-caption-text">Подключенный шрифт</figcaption></figure> 

Стоит обратить внимание, что в этом случае в коде будет только ссылка на шрифт, который располагается на сайте WebFont. Получается аналог известного ресурса GoogleFonts.

Но, помимо этого, плагин WebFont обладает еще несколькими интересными способностями. Если посмотреть на первые три пункта списка при запуске плагина, можно увидеть следующие строки:

  * * перейти на webfont.ru
  * * обновить список шрифтов
  * * скачать шрифт

Первое действие &#8211; перейти на webfont.ru &#8211; это прямая ссылка на сайт webfont.ru. Если выбрать ее, то автоматически запуститься браузер по-умолчанию, который откроет данный сайт. А именно &#8211; сразу в каталоге шрифтов. По-моему, это полезно, когда хочется/нужно поискать шрифт на самом сайте.

Второе действие &#8211; обновить список шрифтов &#8211; говорит само за себя. Плагин обновляет список шрифтов, соотносясь с сайтом webfont.ru.

Третье действие &#8211; скачать шрифт &#8211; мне особенно понравилось. Это реализация скачивания выбранного шрифта с помощью самого плагина. Не нужно заходить на сайт, искать шрифт, потом нажимать всякие кнопочки Download, затем рыться в собственной файловой системе в поисках полученного шрифта и переноса его в нужное место (немного утрирую, но суть дела в общем такова).

Сделаю экспресс-пробежку по данной возможности.

Открываем плагин (сочетание клавиш Ctrl+Alt+F &#8211; учимся работать правильно, по максимуму забываем о мыше). Выбираем пункт &#8220;* скачать шрифт&#8221;. Откроется еще один список, который по сути будет повторением первого, но без первых трех &#8220;служебных&#8221; пунктов:<figure id="attachment_572" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/download_font_01-600x303.png" alt="Выбор шрифта для скачивания" width="600" height="303" class="size-medium wp-image-572" />][4]<figcaption class="wp-caption-text">Выбор шрифта для скачивания</figcaption></figure> 

Выбираем нужный шрифт и жмем Enter. Плагин спросит, куда нужно сохранить скачиваемый шрифт. Дело в том, что он умеет работать с файловой системой на локальном компьютере и определять в ней местоположение редактируемого файла (открытого на данный момент в редакторе Sublime Text 2). И предлагает, на выбор, варианты сохранения. Надо сказать, его &#8220;предложение&#8221; меня впечатлило. Не буду голословным и приведу лучше скриншот:<figure id="attachment_573" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/download_font_02-600x303.png" alt="Выбор места для сохранения шрифта" width="600" height="303" class="size-medium wp-image-573" />][5]<figcaption class="wp-caption-text">Выбор места для сохранения шрифта</figcaption></figure> 

Этот списочек &#8211; мининавигация по папкам относительно текущего местоположения редактируемого файла (он виден на заднем плане на изображении). Мне нужно сохранить выбранный шрифт в папке fonts. Она отображена внизу списка &#8211; это те папки, которые находятся на одном уровне с файлом MyFreeLancer.html. Выбираю ее &#8211; и опять появиться дополнительный список с вопросами. Я просто хочу &#8220;* да, распаковать сюда&#8221;:<figure id="attachment_574" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/download_font_03-600x303.png" alt="Распаковываем шрифт" width="600" height="303" class="size-medium wp-image-574" />][6]<figcaption class="wp-caption-text">Распаковываем шрифт</figcaption></figure> 

Sublime &#8220;скажет&#8221; о том, что нужно немного подождать (1-2 секунды). И все &#8211; больше ничего не появиться. Скачался шрифт или нет, неизвестно. Что-же, посмотрю сам. Открываю Total Commander и смотрю:<figure id="attachment_575" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/download_font_04-600x485.png" alt="Распакованные шрифты в системе" width="600" height="485" class="size-medium wp-image-575" />][7]<figcaption class="wp-caption-text">Распакованные шрифты в системе</figcaption></figure> 

Вот они &#8211; выделены красненьким! Более того, тут присутствует и файл css (в данном случае это acid.css) с уже готовыми правилами для вставки в код. Удобно, что сказать!

P. S.

Для меня ресурс WebFont показался полезным в первую очередь тем, что на нем собраны наиболее часто используемые шрифты. Хотя на момент написания статьи там находилось 133 семейства шрифтов. Еще одной *очень привлекательной чертой* этого ресурса является наличие плагина WebFont под редактор Sublime Text 2, с помощью которого можно подключить нужный шрифт удобно и быстро.

Оцените статью:  
<span id="post-ratings-567" class="post-ratings" data-nonce="1750d2bf68"><img id="rating_567_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(567, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_567_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(567, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_567_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(567, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_567_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(567, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_567_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(567, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_567_text"></span></span><span id="post-ratings-567-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/07/install_plugin.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/07/install_font.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/07/import_font.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/07/download_font_01.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/07/download_font_02.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/07/download_font_03.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/07/download_font_04.png