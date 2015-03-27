---
title: 'Joomla &#8211; как восстановить пароль к административной панели'
author: gearmobile
layout: post
permalink: /joomla-%d0%ba%d0%b0%d0%ba-%d0%b2%d0%be%d1%81%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%b8%d1%82%d1%8c-%d0%bf%d0%b0%d1%80%d0%be%d0%bb%d1%8c-%d0%ba-%d0%b0%d0%b4%d0%bc%d0%b8%d0%bd%d0%b8%d1%81%d1%82%d1%80/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - CMS Joomla
tags:
  - joomla
---
Восстановить пароль пользователя к Joomla на самом деле совсем просто. Весь процесс занимает не более двух минут и пары-тройки действий. Недавно сам столкнулся с такой проблемой.

Вариантов восстановления существует несколько, но самым простым и надежным для меня является ручная правка записи в базе данных MySQL. Для этого лучше всего воспользоваться удобным приложением, созданным специально для работы с подобными базами данных &#8211; phpMyAdmin (pma).

Заходим в панель управления хостингом и открываем в ней phpMyAdmin. Далее находим ту базу данных, которой соответствует сайт на Joomla, к которому потерян пароль. Открываем ее и в левом окне находим таблицу, в которой размещены данные всех зарегистрированных пользователей. Обычно такая таблица имеет имя xxxx_users, где хххх &#8211; это префикс таблицы:<figure id="attachment_511" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/users_table-600x317.png" alt="Таблица пользователей в базе данных MySQL" width="600" height="317" class="size-medium wp-image-511" />][1]<figcaption class="wp-caption-text">Таблица пользователей в базе данных MySQL</figcaption></figure> 

Открываем эту таблицу. В правом окне отображаются все пользователи, внесенные в базу данных MySQL:<figure id="attachment_512" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/edit_user_joomla-600x315.png" alt="Пользователи сайта в базе данных MySQL" width="600" height="315" class="size-medium wp-image-512" />][2]<figcaption class="wp-caption-text">Пользователи сайта в базе данных MySQL</figcaption></figure> 

Выбираем в таблице того пользователя, пароль которого нужно отредактировать. Если пользователей несколько, то нужно найти нужного и отметить его галочкой. Если же один, то достаточно просто нажать на ссылку &#8220;Изменить&#8221; напротив этой записи.

Откроется большая таблица, в которой нужно найти строку &#8220;password&#8221;. В столбце &#8220;Значение&#8221; отображено значение текущего пароля, зашифрованного по алгоритму MD5. Восстановление его с практической точки зрения не имеет смысла. Может быть, это и можно сделать, но данный процесс займет слишком много времени и усилий. Проще заменить пароль на другой, заранее нам известный:<figure id="attachment_513" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/07/edit_password_user-600x285.png" alt="Редактирование пароля пользователя Joomla" width="600" height="285" class="size-medium wp-image-513" />][3]<figcaption class="wp-caption-text">Редактирование пароля пользователя Joomla</figcaption></figure> 

Для этого очищаем поле ввода в столбце &#8220;Значение&#8221;. В столбце &#8220;Функция&#8221; в поле ввода находится ниспадающий список. В нем нужно выбрать алгоритм шифрования MD5. И вводим новый пароль в поле &#8220;Значение&#8221;, например 123123. После того, как нажмем кнопку ОК, введенный заново пароль 123123 зашифруется и подставится наместо введенного нами.

Нажимаем кнопку ОК и выходим из phpMyAdmin. Проверяем результат изменений. Переходим в административную панель Joomla по адресу http://super-site.com/administrator и вводим в форме входа пару логин и измененный пароль. Все должно работать, если не было допущено каких-либо ошибок.

Оцените статью:  
<span id="post-ratings-509" class="post-ratings" data-nonce="dfd74d6a47"><img id="rating_509_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(509, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_509_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(509, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_509_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(509, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_509_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(509, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_509_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(509, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_509_text"></span></span><span id="post-ratings-509-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/07/users_table.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/07/edit_user_joomla.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/07/edit_password_user.png