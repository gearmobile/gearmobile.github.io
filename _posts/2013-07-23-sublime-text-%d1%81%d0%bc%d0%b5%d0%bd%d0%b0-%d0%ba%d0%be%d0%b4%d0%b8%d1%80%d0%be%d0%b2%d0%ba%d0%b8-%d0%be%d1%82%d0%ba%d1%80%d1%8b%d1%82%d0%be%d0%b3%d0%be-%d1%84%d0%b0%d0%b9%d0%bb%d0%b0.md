---
title: 'Sublime Text &#8211; смена кодировки открытого файла'
author: gearmobile
layout: post
permalink: /sublime-text-%d1%81%d0%bc%d0%b5%d0%bd%d0%b0-%d0%ba%d0%be%d0%b4%d0%b8%d1%80%d0%be%d0%b2%d0%ba%d0%b8-%d0%be%d1%82%d0%ba%d1%80%d1%8b%d1%82%d0%be%d0%b3%d0%be-%d1%84%d0%b0%d0%b9%d0%bb%d0%b0/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 26
ratings_score:
  - 130
ratings_average:
  - 5
categories:
  - Web Tools
tags:
  - sublime text
---
Иногда при открытии файла в редакторе Sublime Text вместо читаемых символов можно увидеть абракадабру. Это связано с тем, что открытый файл был создан в другом редакторе и сохранен в кодировке, отличной от той, которая по умолчанию установлена в настройках Sublime Text. Например, откроем файл shablon.html, как показано на рисунке. Это шаблон, с помощью которого создаются html-странички для одного сайта. Файл был создан (или отредактирован) в Adobe Dreamweaver и сохранен в кодировке KOI8-R. Об этом также говорит и строка в заголовке документа &#8211; charset=&#8221;KOI8-R&#8221;. Если этот файл открыть в Sublime Text, то увидим следующую картину:<figure id="attachment_707" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/SublimeEncoding_1.jpg" alt="Открытый файл с неверной кодировкой в Sublime Text 2" width="600" height="484" class="size-full wp-image-707" />][1]<figcaption class="wp-caption-text">Открытый файл с неверной кодировкой в Sublime Text 2</figcaption></figure> 

Что нужно сделать в редакторе Sublime Text, чтобы этот документ открылся правильно и был удобочитаем? Все просто!

Для этого переходим в меню &#8220;File &#8211; Reopen with Encoding&#8221;. Стрелка справа от этой записи говорит, что за ней &#8220;скрывается&#8221; подменю. Наводим мышью на эту надпись и видим открывшееся подменю с длинным списком доступных кодировок. Так как я заранее знаю, что файл shablon.html был создан в кодировке KOI8-R, то выбираю ее из списка:<figure id="attachment_708" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/SublimeEncoding_2.jpg" alt="Выбор кодировки для открытого файла в Sublime Text 2" width="600" height="484" class="size-full wp-image-708" />][2]<figcaption class="wp-caption-text">Выбор кодировки для открытого файла в Sublime Text 2</figcaption></figure> 

Редактор заново откроет этот файл, но уже в указанной мною кодировке. Результат именно тот, который мне и хотелось получить. Теперь можно работать с этим шаблоном:<figure id="attachment_709" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/SublimeEncoding_3.jpg" alt="Открытый файл в правильной кодировке в Sublime Text 2" width="600" height="484" class="size-full wp-image-709" />][3]<figcaption class="wp-caption-text">Открытый файл в правильной кодировке в Sublime Text 2</figcaption></figure> 

На этом краткую статью о смене кодировки открытого файла в Sublime Text можно считать завершенной.

Оцените статью:  
<span id="post-ratings-705" class="post-ratings" data-nonce="0512ca28f4"><img id="rating_705_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(705, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_705_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(705, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_705_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(705, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_705_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(705, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_705_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(705, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>26</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_705_text"></span></span><span id="post-ratings-705-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/07/SublimeEncoding_1.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/07/SublimeEncoding_2.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/07/SublimeEncoding_3.jpg