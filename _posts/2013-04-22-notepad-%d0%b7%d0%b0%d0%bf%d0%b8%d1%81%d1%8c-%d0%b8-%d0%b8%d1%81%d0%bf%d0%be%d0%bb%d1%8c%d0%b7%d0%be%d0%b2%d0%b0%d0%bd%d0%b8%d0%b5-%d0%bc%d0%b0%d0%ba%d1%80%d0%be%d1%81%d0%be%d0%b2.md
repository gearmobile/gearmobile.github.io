---
title: 'Notepad++ &#8211; запись и использование макросов'
author: gearmobile
layout: post
permalink: /notepad-%d0%b7%d0%b0%d0%bf%d0%b8%d1%81%d1%8c-%d0%b8-%d0%b8%d1%81%d0%bf%d0%be%d0%bb%d1%8c%d0%b7%d0%be%d0%b2%d0%b0%d0%bd%d0%b8%d0%b5-%d0%bc%d0%b0%d0%ba%d1%80%d0%be%d1%81%d0%be%d0%b2/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 8
ratings_score:
  - 40
ratings_average:
  - 5
categories:
  - Web Tools
tags:
  - notepad++
---
Одной из полезных возможностей программы Notepad++ является создание и использование макросов. Пользователям, которые знакомы с популярным офисным пакетом MS Office (и Microsoft Excel в частности) должно быть знакомо понятие макросов. Если не знакомо, то вкратце поясню.

Макрос &#8211; это последовательность действий пользователя в программе, записанная и сохраненная этой программой. То есть, если в своей повседневной работе вы выполняете постоянно какие либо действия, то их можно записать с тем, чтобы не повторять снова. В последствии такую последовательность действий можно запустить на выполнение одним щелчком мыши или сочетанием горячих клавиш.

Сам процесс записи очень похож на то, как если бы действия в программе записывались на видеокамеру. Только в качестве пленки в этом случае выступает программный код. Точнее, язык программирования, в который переводится все манипуляции, которые пользователь выполняет в программе. Язык программирования может быть разным и целиком зависеть от конкретной программы. Например, в Microsoft Excel таким языком является VBA (Visual Basic for Applications). Для обычного пользователя знать как язык программирования, на котором кодируется действия, совсем необязательно. Ему достаточно уметь записывать макросы и запускать их на выполнение.

Вернемся к программному блокноту Notepad++. Чем могут быть полезны макросы в этом случае. Да тем же самым. Допустим, при написании кода существуют какие-либо его участки (куски), которые повторяются постоянно. Кстати, такие повторяющиеся куски кода называются сниппетами.

Так вот, такие сниппеты приходится вводить вручную снова и снова. Чтобы ускорить работу и облегчить ее, можно записать такие программные куски в качестве последовательности действий. А затем вставлять в текст одним нажатием горячих клавиш.

Давайте на примере разберем, каким образом можно записать и использовать макросы в Notepad++. Первое, что необходимо узнать, это какие кнопки отвечают за работу макросов. Посмотрите на панель инструментов Notepad++. Ближе к концу этой панели располагаются в ряд пять кнопок, каждая из которых отвечает за определенное действие:<figure id="attachment_685" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/buttons_set_for_macros_notepad-600x303.png" alt="Набор кнопок для работы с макросами в Notepad++" width="600" height="303" class="size-medium wp-image-685" />][1]<figcaption class="wp-caption-text">Набор кнопок для работы с макросами в Notepad++</figcaption></figure> 

Назначение каждой из них по порядку:

  1. Старт записи макроса
  2. Остановка записи макроса
  3. Воспроизведение записанного макроса
  4. Многократное воспроизведение записанного макроса
  5. Сохранение записанного макроса

Набор совсем несложный и разобраться в нем легко. Теперь давайте приступим к записи какого-либо макроса, чтобы увидеть воочию, как это делается. Предположим, что в качестве часто повторяемого кода (сниппета) у нас будет выступать строка `document.write();`, которую довольно часто применяют в коде javascript-программисты.

Нажимаем кнопку &#8220;Старт записи макроса&#8221;. При этом кнопка из красной превратиться в серую, что означает &#8211; запись пошла. Без ошибок, аккуратно вводим в основном окне Notepad++ вышеуказанную строку:<figure id="attachment_686" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/start_record_macros_notepad-600x268.png" alt="Запись макроса в Notepad++" width="600" height="268" class="size-medium wp-image-686" />][2]<figcaption class="wp-caption-text">Запись макроса в Notepad++</figcaption></figure> 

Когда строка введена, нажимаем кнопку &#8220;Остановка записи макроса&#8221;. Программа Notepad++ записала наши действия. В данном случае &#8211; это строка кода, которую мы ввели. Чтобы проверить, что запись была произведена верно, нажмем кнопку &#8220;Воспроизведение записанного макроса&#8221;. Notepad++ в точности воспроизведет указанную строку, если все было выполнено нами верно. Если нужно воспроизвести записанный макрос несколько раз, можно нажать кнопку &#8220;Многократное воспроизведение записанного макроса&#8221;.

Теперь необходимо сохранить записанный нами макрос, так как он хранится в оперативной памяти программы Notepad++ только до момента ее закрытия. Как только мы ее закроем, макрос пропадет. Для сохранения нажимаем кнопку &#8220;Сохранение записанного макроса&#8221;. Появится окно, в котором предлагается задать сочетание &#8220;горячих клавиш&#8221; для сохраняемого макроса и его имя для сохранения. выбираем любое понравившееся сочетание, а также задаем имя для макроса:<figure id="attachment_687" style="width: 291px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/saving_macros_in_notepad.png" alt="Сохранение макроса в Notepad++" width="291" height="205" class="size-full wp-image-687" />][3]<figcaption class="wp-caption-text">Сохранение макроса в Notepad++</figcaption></figure> 

Проверить, произошло ли сохранение макроса, можно двумя способами. Первый &#8211; это перейти в меню &#8220;Макросы&#8221;. В выпадающей списке, наряду с общесистемными командами Notepad++ должен находиться и наш макрос `document.write();`. Второй способ &#8211; это открыть список всех сохраненных в программе макросов. Делается это через меню &#8220;Макросы &#8211; Изменить гор.клавишу/Удалить макрос&#8221;. Откроется окно редактирования, в котором должен быть представлен наш макрос:<figure id="attachment_688" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/saved_macros_notepad-600x329.png" alt="Список сохраненных макросов Notepad++" width="600" height="329" class="size-medium wp-image-688" />][4]<figcaption class="wp-caption-text">Список сохраненных макросов Notepad++</figcaption></figure> 

В этом окне можно удалить сохраненный макрос кнопкой &#8220;Delete&#8221;. Или же изменить сочетание горячих клавиш для этого макроса кнопкой &#8220;Modify&#8221;.

Как вы уже догадались, с помощью макроса можно сохранять абсолютно любой код. Это может не обязательно javascript-сниппет, но и часть html или css кода, если вы занимаетесь версткой в программе Notepad++.

На этом обзор макросов в Notepad++ закончен.

Оцените статью:  
<span id="post-ratings-683" class="post-ratings" data-nonce="afaa02c642"><img id="rating_683_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(683, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_683_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(683, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_683_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(683, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_683_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(683, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_683_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(683, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>8</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_683_text"></span></span><span id="post-ratings-683-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/04/buttons_set_for_macros_notepad.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/04/start_record_macros_notepad.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/04/saving_macros_in_notepad.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/04/saved_macros_notepad.png