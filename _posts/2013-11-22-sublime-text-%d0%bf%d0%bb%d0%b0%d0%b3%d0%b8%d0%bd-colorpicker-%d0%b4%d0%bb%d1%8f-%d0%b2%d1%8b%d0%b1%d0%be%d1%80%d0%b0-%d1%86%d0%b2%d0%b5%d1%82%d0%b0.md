---
title: 'Sublime Text &#8211; плагин ColorPicker для выбора цвета'
author: gearmobile
layout: post
permalink: /sublime-text-%d0%bf%d0%bb%d0%b0%d0%b3%d0%b8%d0%bd-colorpicker-%d0%b4%d0%bb%d1%8f-%d0%b2%d1%8b%d0%b1%d0%be%d1%80%d0%b0-%d1%86%d0%b2%d0%b5%d1%82%d0%b0/
ratings_users:
  - 4
ratings_score:
  - 20
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - Web Tools
tags:
  - colorpicker
---
При верстке HTML-шаблонов часто ловил себя на мысли, что редактору Sublime Text не хватает одной удобной вещи &#8211; инструмента для выбора цвета в процессе кодинга. Допустим, есть блок div и мне необходимо сделать для него произвольную фоновую заливку через CSS-свойство background-color. Откуда мне взять значение нужного цвета в HEX-формате (про RGBA уже молчу)? Если скажете, что держать в голове значения этих цветов, то насмешите (можно помнить 5-10 значений, не больше). Хранить в виде таблицы цвета и их значения в HEX\RGBA? Этот список вечно куда-то девается и в нужный момент его постоянно нет под рукой.

В ходе своей деятельности я постоянно пробую новые HTML-редакторы, платные и бесплатные. Платные редакторы, конечно, более &#8220;отшлифованные&#8221; и удобные в работе. Так вот, в таких редакторах, как JetBrains WebStorm, Adobe Dreamweaver, EmEditor есть функция автоматического перехвата события, когда в процессе кодинга я пытаюсь добавить цвет для элемента:<figure id="attachment_673" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/webstorm-colorpicker-600x331.jpg" alt="Функция выбора цвета в редакторе JetBrains WebStorm" width="600" height="331" class="size-medium wp-image-673" />][1]<figcaption class="wp-caption-text">Функция выбора цвета в редакторе JetBrains WebStorm</figcaption></figure> 

Классная и удобная штучка, не правда ли? Почему бы и для редактора Sublime Text не прикрутить подобную (ведь изначально в нем нет такой надстройки)? Совсем недавно я зарегистрировался на сервисе Toster.ru, который является детищем Харба и сделан аналогом известного StackOverflow. Незаменимая вещь для кодера &#8211; там можно найти ответы на все вопросы, причем вопросы практического характера, что особенно ценно. То есть, другими словами, Toster.ru &#8211; это русский StackOverflow. И вот, один из вопросов на этом сервисе был посвящен возможности выбора цвета в редакторе Sublime Text. Ответили там кратко, но точно &#8211; это плагин ColorPicker.

Ставится ColorPicker быстро и стандартно для Sublime Text &#8211; через менеджер пакетов. Кстати, есть достаточно интересный адрес &#8211; https://sublime.wbond.net/, который является online-репозиторием для редактора Sublime Text. Чем удобен этот адрес &#8211; можно найти и почитать о любом из плагинов под этот редактор. Если интересно почитать более подробно об плагине ColorPicker, можно зайти на страницу этого проекта на GitHub &#8211; https://github.com/weslly/ColorPicker. После установки плагин ColorPicker &#8220;не слышно и не видно&#8221; в редакторе Sublime Text. Чтобы вызвать его для выбора цвета, нужно нажать сочетание клавиш:

  * для Windows: Ctrl+Shift+C
  * для OS X: Cmd+Shift+C
  * для Linux: Ctrl+Shift+C

Появится стандартное окно выбора цвета под операционную систему Windows (на Mac OS X я еще не заработал )) ):<figure id="attachment_674" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime_text-colorpicker-600x305.jpg" alt="Окно плагина ColorPicker в редакторе Sublime Text" width="600" height="305" class="size-medium wp-image-674" />][2]<figcaption class="wp-caption-text">Окно плагина ColorPicker в редакторе Sublime Text</figcaption></figure> 

Выбираем и вставляем нужный цвет. На странице проекта на GitHub (https://github.com/weslly/ColorPicker) можно увидеть скриншоты окна плагина под другие операционные системы &#8211; OS X, Linux OS, так как этот плагин можно установить и под эти платформы.

Все прекрасно. Только один момент &#8211; вызывать этот плагин придется все же &#8220;вручную&#8221;, через сочетание клавиш. Наверное, как-то и можно &#8220;повесить&#8221; плагин ColorPicker на определенное событие в редакторе Sublime Text, как это сделано в том же JetBrains WebStorm. Но как это сделать &#8211; я пока не знаю. Наверное, наподобие создания сниппетов в Sublime Text? ))

Оцените статью:  
<span id="post-ratings-672" class="post-ratings" data-nonce="896563f9ee"><img id="rating_672_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(672, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_672_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(672, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_672_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(672, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_672_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(672, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_672_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(672, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_672_text"></span></span><span id="post-ratings-672-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/webstorm-colorpicker.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/sublime_text-colorpicker.jpg