---
title: 'Плагин Kareebu Secure &#8211; защищаем Joomla от злонамеренного доступа'
author: gearmobile
layout: post
permalink: /%d0%bf%d0%bb%d0%b0%d0%b3%d0%b8%d0%bd-kareebu-secure-%d0%b7%d0%b0%d1%89%d0%b8%d1%89%d0%b0%d0%b5%d0%bc-joomla-%d0%be%d1%82-%d0%b7%d0%bb%d0%be%d0%bd%d0%b0%d0%bc%d0%b5%d1%80%d0%b5%d0%bd%d0%bd%d0%be/
ratings_users:
  - 2
ratings_score:
  - 6
ratings_average:
  - 3
cleanretina_sidebarlayout:
  - default
categories:
  - CMS Joomla
tags:
  - kareebu secure
---
Узнать, на каком CMS работает тот или иной сайт можно различными способами. Это делается в автоматическом режиме с помощью плагинов или сервисов. Или в ручном режиме, просмотром исходного кода страницы. Помимо этого, существуют еще определенное количество уловок, специфичных для каждой CMS в отдельности.

Чем грозит для владельца сайта утечка такой информации? Потенциальный злоумышленник, зная движок, на котором работает данный сайт, также в курсе обо всех уязвимых местах CMS, на которой он работает. Это позволит ему предпринять попытки взломать сайт со всеми вытекающими последствиями для его владельца.

Каким же образом можно обезопасить себя? Понятно, что панацеи от всех бед не существует и существовать не может. Но настроить номинальную защиту сайта всегда не помешает.

Одной из возможностей укрепить оборону сайта является плагин kareebu Secure. Этот плагин написан два года назад и до сих пор пользуется популярностью на ресурсе Joomla! Extensions. Плагин поддерживается версиями Joomla 1.5 и 2.5, так что выбор для сайтовладельцев не ограничен.

Принцип работы kareebu Secure достаточно прост. Плагин устанавливает пароль на директорию /administrator в корневой директории сайта. Благодаря этому закрывается доступ извне и теперь без пароля невозможно просмотреть содержимое этой папки и узнать, что сайт-то работает на Joomla!

Установка плагина kareebu Secure выполняется стандартным способом, через менеджер расширений Joomla. После успешной установки необходимо перейти в раздел Менеджер плагинов и включить kareebu Secure. Выполняется это в поле &#8220;Состояние&#8221;. На изображении приведено изначальное состояние плагина, когда он еще не включен:<figure id="attachment_363" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/kareebu-Secure-plugin-600x242.png" alt="Плагин kareebu-Secure" width="600" height="242" class="size-medium wp-image-363" />][1]<figcaption class="wp-caption-text">Плагин kareebu-Secure</figcaption></figure> 

Затем переходим к настройкам kareebu Secure. Они очень просты, запутаться тут невозможно:<figure id="attachment_364" style="width: 494px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/kareebu-Secure-settings.png" alt="Настройки плагина kareebu Secure" width="494" height="172" class="size-full wp-image-364" />][2]<figcaption class="wp-caption-text">Настройки плагина kareebu Secure</figcaption></figure> 

Первое поле &#8220;Enable&#8221; включает или выключает настройки плагина. Понятно, что если настройки введены, но отключены, то плагин работать не будет.

Второе поле &#8220;Password&#8221; позволяет задать произвольный пароль, устанавливаемый на папку /administrator . Пароль может состоять из комбинации заглавных и строчных букв, а также цифр.

Третье поле &#8220;Mode&#8221; позволяет выбрать два режима авторизации на сайте с помощью плагина kareebu Secure. Первый (устаревший) режим &#8220;HTTP Authentication&#8221; работает следующим образом. В адресной строке браузера для входа в административную панель Joomla вводится:

<pre>http://localhost:7788/third/administartor?password

</pre>

где password &#8211; это тот самый пароль, который был задан во втором поле. Браузер переадресовывается в back-end сайта и открывается стандартное окно Joomla для входа в административную часть. Необходимо ввести только пароль в соответствующем поле. Поле с именем пользователя можно оставить пустым. Второй режим &#8220;Compatibility&#8221; похож на первый, но для входа в админку сайта потребуется указать как логин, так и пароль. Кстати, пароль для входа на сайт и пароль, устанавливаемый в плагине, могут и должны различаться.

Кстати, если вы обратили внимание, стандартная строка:

<pre>http://localhost:7788/third/administrator

</pre>

для входа в административную часть Joomla после установки плагина kareebu Secure изменилась и теперь представляет из себя:

<pre>http://localhost:7788/third/administartor?password

</pre>

Об этом не стоит забывать. Теперь не зная секретного пароля, невозможно получить доступ к back-end Joomla и войти в нее. На этом обзор плагина kareebu Secure можно закончить.

Оцените статью:  
<span id="post-ratings-362" class="post-ratings" data-nonce="a71eb7b3ac"><img id="rating_362_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(362, 1, '1 Star');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_362_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(362, 2, '2 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_362_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(362, 3, '3 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_362_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(362, 4, '4 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_362_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(362, 5, '5 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>3,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_362_text"></span></span><span id="post-ratings-362-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/kareebu-Secure-plugin.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/kareebu-Secure-settings.png