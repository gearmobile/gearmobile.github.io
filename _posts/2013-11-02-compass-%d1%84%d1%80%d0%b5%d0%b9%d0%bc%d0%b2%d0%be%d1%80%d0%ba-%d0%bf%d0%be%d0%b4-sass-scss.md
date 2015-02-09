---
title: 'Compass &#8211; фреймворк под SASS (SCSS)'
author: gearmobile
layout: post
permalink: /compass-%d1%84%d1%80%d0%b5%d0%b9%d0%bc%d0%b2%d0%be%d1%80%d0%ba-%d0%bf%d0%be%d0%b4-sass-scss/
ratings_users:
  - 11
ratings_score:
  - 47
ratings_average:
  - 4.27
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - compass
---
Приступаем к изучению Compass. А что такое? Говоря официальным языком &#8211; это фреймворк для SASS. Если неофициальным &#8211; то библиотека (коллекция) готовых mixin&#8217;ов, которые можно подключать к рабочему проекту. В этой коллекции есть наборы миксинов практически на все случаи жизни &#8211; для создания скругленных углов, линейных и радиальных градиентов, теней для блоков и текста и многое другое.

Но вернемся к Compass &#8211; ведь это практически неотъемлемая часть SASS. И логично было бы продолжить изучение последнего, перейдя к Compass. Этот фреймворк, также как и сам SASS, является приложением, написанном на Ruby. Установка Compass производится точно также, как и SASS &#8211; с помощью менеджера пакетов gem.

Запускаем терминал Windows сочетанием клавиш Win+R и вводим в нем команду:

<pre>gem install compass</pre>

Если все прошло успешно, то вывод командной строки должен быть следующим:<figure id="attachment_132" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/compass-installed-600x327.jpg" alt="Успешная установка Compass под Windows" width="600" height="327" class="size-medium wp-image-132" />][1]<figcaption class="wp-caption-text">Успешная установка Compass под Windows</figcaption></figure> 

Введем в терминале команду справки по этому фреймворку, чтобы получить полный список доступных команд (*обратите внимание, что у ключей команды compass нет двойных дефисов, как у sass*):

<pre>compass help</pre>

Самые нужные команды из этого списка:</p> 

  * watch &#8211; мониторинг scss-файлов (аналог этой команды в sass)
  * create &#8211; создать новый compass-проект
  * init &#8211; создать новый compass-проект из существующего css-проекта

Давайте создадим новый проект. Перейдем через терминал в заранее подготовленную для этой цели директорию и запустим там команду:

<pre>compass create</pre>

Если теперь взглянуть на содержимое этой директории, то увидим интересные вещи:<figure id="attachment_133" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/compass-project-600x347.jpg" alt="Содержимое директории с Compass-проектом" width="600" height="347" class="size-medium wp-image-133" />][2]<figcaption class="wp-caption-text">Содержимое директории с Compass-проектом</figcaption></figure> 

Видим, что появились папки stylesheets, sass, файл config.rb. Все они созданы командой compass и являются заготовками для будущего проекта. В папке sass находятся scss-файлы, в папке stylesheets &#8211; css-файлы, результат преобразования из scss. Файл config.rb &#8211; это конфигурация текущего проекта. Настройки минимальные и очень просты:<figure id="attachment_134" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/compass-config-600x368.jpg" alt="Файл настроек проекта Compass" width="600" height="368" class="size-medium wp-image-134" />][3]<figcaption class="wp-caption-text">Файл настроек проекта Compass</figcaption></figure> 

Переменная css\_dir со значением stylesheets &#8211; это &#8220;выходная&#8221; папка проекта, в которой хранятся css-файлы, сконвертированные из scss-файлов. Переменная sass\_dir хранит имя директории, в которой находятся рабочие scss-файлы. Переменная images\_dir &#8211; сюда складываются все изображения проекта. Ну и переменная javascript\_dir &#8211; здесь лежат все js-скрипты.

Значения всех этих переменных можно изменить на свой вкус &#8211; кто как привык. Например, images на img, javascript на js, stylesheets на styles. Но при этом не забыть переименовать соответствующие папки в проекте.

Давайте откроем файл screen.scss и обратим внимание на одну строчку (она там действительно одна, не считая комментариев):<figure id="attachment_135" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/compass-include-600x368.jpg" alt="Compass с подключенным модулем Reset" width="600" height="368" class="size-medium wp-image-135" />][4]<figcaption class="wp-caption-text">Compass с подключенным модулем Reset</figcaption></figure> 

Эта строка подключает в проект фреймворк Compass и один из его модулей &#8211; файл сброса CSS-стилей reset. Как известно, таких файлов существует несколько видов, но в данном случае используется самый популярный &#8211; от Эрика Мейера. Модуль reset подключается автоматически, при создании нового проекта. Но, помимо этого модуля, у Compass существуют еще несколько, которые нужно подключать аналогично, но вручную.

Теперь нам стоит отвлечься от терминала и перейти в браузер. Вводим в адресной строке http://compass-style.org/, чтобы попасть на домашнюю страницу проекта. Все оставшееся время мы будем проводить там за увлекательным чтением документации. Переходим по ссылке reusable patterns (http://compass-style.org/reference/compass/), где размещены сами модули Compass. По своему функционалу они разбиты на три большие группы: CSS3, Typography, Utilities . К примеру, перейдем в раздел CSS3. Чтобы воспользоваться миксинами модуля CSS3, необходимо подключить этот модуль.

Делается это так:<figure id="attachment_136" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/compass-css3-600x450.jpg" alt="Подключение модуля CSS3 фреймворка Compass" width="600" height="450" class="size-medium wp-image-136" />][5]<figcaption class="wp-caption-text">Подключение модуля CSS3 фреймворка Compass</figcaption></figure> 

Ниже представлен список ссылок с миксинами, отсортированными по их функционалу. К примеру, Border Radius &#8211; это mixin для создания скругленных углов блоков. Аналогично, подключаем другой модуль (к примеру &#8211; Typography) и применяем на практике наработки других веб-дизайнеров.

Удобство использования фреймворка Compass и его миксинов я расписывать не буду &#8211; это и так ясно. И что касается применения каждого из миксинов в отдельности &#8211; также. На сайте они описаны подробно и с примерами. Пересказ всех их является пустой задачей. Просто учите английский, кто не знает. ))

Оцените статью:  
<span id="post-ratings-131" class="post-ratings" data-nonce="166e57013a"><img id="rating_131_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(131, 1, '1 Star');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_131_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(131, 2, '2 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_131_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(131, 3, '3 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_131_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(131, 4, '4 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_131_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(131, 5, '5 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>11</strong> votes, average: <strong>4,27</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_131_text"></span></span><span id="post-ratings-131-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/compass-installed.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/compass-project.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/compass-config.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/compass-include.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2013/11/compass-css3.jpg