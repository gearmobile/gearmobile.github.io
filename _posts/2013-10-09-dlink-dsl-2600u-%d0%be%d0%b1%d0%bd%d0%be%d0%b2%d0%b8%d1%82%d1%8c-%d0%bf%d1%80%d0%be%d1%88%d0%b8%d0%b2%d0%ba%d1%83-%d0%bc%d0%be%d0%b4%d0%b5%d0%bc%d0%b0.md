---
title: 'DLink DSL-2600U &#8211; обновить прошивку модема'
author: gearmobile
layout: post
permalink: /dlink-dsl-2600u-%d0%be%d0%b1%d0%bd%d0%be%d0%b2%d0%b8%d1%82%d1%8c-%d0%bf%d1%80%d0%be%d1%88%d0%b8%d0%b2%d0%ba%d1%83-%d0%bc%d0%be%d0%b4%d0%b5%d0%bc%d0%b0/
ratings_users:
  - 21
ratings_score:
  - 100
ratings_average:
  - 4.76
cleanretina_sidebarlayout:
  - default
categories:
  - Разное
tags:
  - DLink DSL-2600U
---
Являюсь &#8220;счастливым&#8221; обладателем сего чуда техники. И все было хорошо до вчерашнего дня, когда по причинам, для меня совсем не ясным, сей модем перестал работать. Просто не мог подключиться к Интернету. То есть, как показывало окно &#8220;Diagnostics&#8221;, он честно пытался подключиться к местному ISP, но тот его упорно &#8220;отфутболивал&#8221;:<figure id="attachment_250" style="width: 485px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/dsl-2600u_bru_c_front.jpg" alt="DLink 2600 BRU" width="485" height="400" class="size-full wp-image-250" />][1]<figcaption class="wp-caption-text">DLink 2600 BRU</figcaption></figure> 

Первым делом перебил настройки в модеме – пароль, логин и т. п. Результата не дало. На следующий день отправился в местное отделение моего провайдера с вопросами. Там сказали, что настройки (парольлогин – в частности), они сами не могут видеть (???) и проверитьвыдать его мне, соответственно. Посоветовали принести модем, чтобы они сами попробовали подключить его и проверить.

Как честный idioto vero, отнес я модем к ним. «Специалист» подключил его, вбил мои же настройки и сказал – да, он у Вас не подключается. Затем мило выписал квитанцию на 100 рублей за &#8220;сервисное тестирование&#8221;. Единственным решением проблемы, которое приходило в голову, было – перепрошить модем. Итак, с чего начинаем.

1. Нужно точно определиться с аппаратной ревизией нашего модема. Увидеть ее можно, перевернув его кверху «пузом». На задней стороне имеется наклейка наподобие такой:<figure id="attachment_251" style="width: 200px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/2540_a1.jpg" alt="Этикетка с версией аппаратного обеспечения DLink 2600 BRU" width="200" height="100" class="size-full wp-image-251" />][2]<figcaption class="wp-caption-text">Этикетка с версией аппаратного обеспечения DLink 2600 BRU</figcaption></figure> 

Здесь строка H/W Ver.:A1 и есть та самая аппаратная ревизия. Зачем нужна такая точность с ней? Затем, что если выбрать прошивку не для того «железа», в итоге можно получить кусок металлолома. Вторая строка – F/W Ver. RU_1.00 (у меня было) является версией прошивки. Это заводская прошивка.

2. С именами определились. Теперь надо скачать прошивку. Все они находятся на ftp-сервере фирмы-производителя D-Link – ftp://ftp.dlink.ru/pub/ADSL/. Единственное затруднение у меня вызвало то, что для ревизии А1 там не было ничего. Только для ревизии С и для ревизии С2. После общения на форумах выяснилось, что можно смело брать прошивку от ревизии С для А1. Скачиваю ее и затем распаковываю.

3. Подключаю модем по кабелю, набираю в строке браузера 192.168.1.1. После ввода пары логинпароль попадаю в административную панель модема. Перехожу в &#8220;Management &#8211; Update Software&#8221;:<figure id="attachment_252" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/update-600x531.png" alt="Обновление прошивки DLink 2600 BRU" width="600" height="531" class="size-medium wp-image-252" />][3]<figcaption class="wp-caption-text">Обновление прошивки DLink 2600 BRU</figcaption></figure> 

Здесь выбираю, где лежит скачанная мною прошивка и нажимаю кнопку &#8220;Update Software&#8221;. Процесс пошел.

4. После завершения захожу в &#8220;Management &#8211; Settings &#8211; Restore Default&#8221; и сбрасываю настройки модема до заводских:<figure id="attachment_253" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/restore-600x531.png" alt="Сброс настроек DLink 2600 до заводских" width="600" height="531" class="size-medium wp-image-253" />][4]<figcaption class="wp-caption-text">Сброс настроек DLink 2600 до заводских</figcaption></figure> 

5. Перехожу в &#8220;Device Info&#8221; и смотрю версию прошивки: Software Version RU_1.23. Все ОК. Прошивка встала:<figure id="attachment_254" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/software-version-600x397.png" alt="Проверка текущей версии прошивки модема" width="600" height="397" class="size-medium wp-image-254" />][5]<figcaption class="wp-caption-text">Проверка текущей версии прошивки модема</figcaption></figure> 

6. Осталось только вбить настройки, данные ISP. Для WAN:<figure id="attachment_255" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/wan-600x397.png" alt="Настройка Интернет-соединения на DLink 2600 BRU" width="600" height="397" class="size-medium wp-image-255" />][6]<figcaption class="wp-caption-text">Настройка Интернет-соединения на DLink 2600 BRU</figcaption></figure> 

Проверить, что все работает. И затем настроить WiFi:<figure id="attachment_256" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/wifi-600x397.png" alt="Настройка wifi-соединения на модеме" width="600" height="397" class="size-medium wp-image-256" />][7]<figcaption class="wp-caption-text">Настройка wifi-соединения на модеме</figcaption></figure> 

7. По завершении нелишним будет сделать backup настроек модема:<figure id="attachment_257" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/backup-600x397.png" alt="Резервная копия настроек DLink 2600 BRU" width="600" height="397" class="size-medium wp-image-257" />][8]<figcaption class="wp-caption-text">Резервная копия настроек DLink 2600 BRU</figcaption></figure> 

P.S.

После перепрошивки скорость заметно (видно даже на глаз) возросла.

P.S.S.

На ftp-сервере имеется также раздел &#8220;Software&#8221; для этой модели модема. Там находится утилита конфигурирования DCC_DSL-2600U. Ее предназначение – настройка модема (wizard) для подключения к местному провайдеру (ISP) по VCI, VPI, login, password (то есть, те данные, которые провайдер предоставляет в заключенном договоре). С помощью нее можно сделать тоже самое, что и через web-интерфейс по кабелю Ethernet – настроить модем на подключение к Интернету. Другими словами, такую настройку можно производить двумя способами:

  * классический – через web-интерфейс (браузер)
  * с помощью утилиты DCC_DSL-2600U (сам не пробовал, ибо нужды в лишнем софте не вижу)

P.S.S.S.

По заявлению на сайте производителя D-Link, модем DSL-2600U/BRU/C (DSL-2600U H/W Ver. A1 – его еще более древняя версия) уже снят с производства. Заменой ему является DSL-2600U/BRU/C2:<figure id="attachment_258" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/dsl-2600u_bru_c2_front-600x446.jpg" alt="DSL-2600U BRU C2" width="600" height="446" class="size-medium wp-image-258" />][9]<figcaption class="wp-caption-text">DSL-2600U BRU C2</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-249" class="post-ratings" data-nonce="c5255f7520"><img id="rating_249_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(249, 1, '1 Star');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_249_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(249, 2, '2 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_249_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(249, 3, '3 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_249_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(249, 4, '4 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_249_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(249, 5, '5 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>21</strong> votes, average: <strong>4,76</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_249_text"></span></span><span id="post-ratings-249-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/dsl-2600u_bru_c_front.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/2540_a1.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/update.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/restore.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/11/software-version.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/11/wan.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/11/wifi.png
 [8]: http://localhost:7788/third/wp-content/uploads/2013/11/backup.png
 [9]: http://localhost:7788/third/wp-content/uploads/2013/11/dsl-2600u_bru_c2_front.jpg