---
title: 'WordPress &#8211; восстановление базы данных из резервной копии sql'
author: gearmobile
layout: post
permalink: /wordpress-%d0%b2%d0%be%d1%81%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%bb%d0%b5%d0%bd%d0%b8%d0%b5-%d0%b1%d0%b0%d0%b7%d1%8b-%d0%b4%d0%b0%d0%bd%d0%bd%d1%8b%d1%85-%d0%b8%d0%b7-%d1%80%d0%b5%d0%b7%d0%b5/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 5
ratings_score:
  - 21
ratings_average:
  - 4.2
categories:
  - CMS WordPress
tags:
  - wordpress
---
Недавно столкнулся с такой задачей. Когда-то у меня имелся свой собственный сайт под управлением CMS WordPress. Но примерно через год пользования сайт был заброшен, домен продан и площадка на хостинге аннулирована провайдером за неуплату.

Казалось бы, все, сайт пропал бесследно, как в воду канул. Но, в те далекие времена у меня хватило благоразумия делать регулярные резервные копии сайта, благо, под WordPress имеются несколько плагинов для этой цели. Удобных и относящихся к разряду &#8220;must have&#8221;.

Одним из них я и воспользовался. Названия этого плагина уже не помню. Но результатом его работы была заархивированная резервная копия базы данных сайта, которую плагин отправлял на мой почтовый ящик в качестве вложения в письмо. Файл-вложение имел примерный вид cifero\_wrdp1\_wp\_20100225\_594.sql.gz. Из расширения этого файла видно, что это архивированная (о чем говорит расширение .gz) база данных (расширение .sql). Цифры 20100225 &#8211; это дата, когда было выполнено резервное архивирование &#8211; 25 февраля 2010 года, а cifero &#8211; это домен, на котором когда-то располагался данный сайт.

Порывшись в старых письмах на почтовом ящике, я выбрал самую последнюю по дате резервную копию. Раз она самая последняя, значит эта копия должна быть самой полной перед тем моментом, когда сайт перестал существовать. Затем скачал эту копию на свой локальный компьютер и стал думать, что же мне с нею делать? Как с помощью этой копии восстановить сайт на своем компьютере?

Первыми моими шагами были следующие. Резервную копию предполагалось развернуть на локальном сервере. Наиболее известным в этом плане является пакет Denwer. Поэтому он был скачан и установлен на локальную систему. Сам процесс установки Denwer в данной статье я описывать не буду, так как в Интернет имеется достаточное количество хороших материалов на эту тему.

В мою задачу входит восстановление статей, которые были когда-то размещены на этом сайте. С точки зрения полноценного восстановления сайта способ, описанный здесь, является незаконченным, так как сам сайт (его front-end, в частности) восстановлен не был, что привело к так называемому &#8220;белому экрану смерти&#8221;. Стоит также оговориться, что, возможно, существуют команды sql и правки резервной копии базы данных, с помощью которых можно &#8220;напрямую&#8221; восстановить статьи, не заморачиваясь с phpMyAdmin и WordPress. Но для автора такие команды неизвестны, а способ, приведенный ниже, является более наглядным и простым.

Мною был скачана свежая версия CMS WordPress &#8211; 3.5. Но только скачана &#8211; не установлена. Данный шаг будет в дальнейшей последовательности действий самым последним.

Теперь все необходимое для восстановления сайта у меня есть. Приступаю к пошаговому разворачиванию локальной копии моего бывшего сайта cifero.ru.

1. Запускаю локальный сервер Denwer. Это можно сделать разными способами, но если установка происходила в точности по инструкциям самого пакета, то на Рабочем столе должны быть три ярлычка &#8211; &#8220;Start Denwer&#8221;, &#8220;Restart Denwer&#8221;, &#8220;Stop Denwer&#8221; &#8211; которые запускают, перезапускают или останавливают Denwer. Я такими ярлычками и воспользовался, щелкнув мышью на ярлыке &#8220;Start Denwer&#8221;. На несколько секунд мелькнет и пропадет окно терминала, а в панели задач появится значок Denwer&#8217;а, говорящий о том, что локальный сервер запустился и готов к работе:<figure id="attachment_387" style="width: 330px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/denwer.png" alt="Локальный сервер Denwer" width="330" height="206" class="size-full wp-image-387" />][1]<figcaption class="wp-caption-text">Локальный сервер Denwer</figcaption></figure> 

2. Вторым шагом мне необходим доступ к базам данных локального сервера. В состав пакета Denwer входит графическое приложение phpMyAdmin, с помощью которого очень удобно работать с базами данных MySQL. Иногда в Интернет встречается сокращенное название этого приложения &#8211; pma. Так как сервер уже запущен, то я захожу в панель управления базами, набрав к адресной строке браузера (любого &#8211; это дело вкуса и дела совсем не меняет) &#8211; http://localhost/tools/phpmyadmin/. Откроется окно phpMyAdmin, в левой половине которого будет список уже имеющихся баз данных, созданных во время инсталляции локального сервера:<figure id="attachment_388" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/denwer_pma_dblist-600x431.png" alt="Список баз данных в phpMyAdmin" width="600" height="431" class="size-medium wp-image-388" />][2]<figcaption class="wp-caption-text">Список баз данных в phpMyAdmin</figcaption></figure> 

3. Теперь необходимо создать новую базу данных, в которой и будет развернуты резервные копии таблиц сайта cifero.ru. Стоит заранее оговориться, что база данных будет в нашем случае создана пустой, таблиц в ней не будет. Последние будут взяты из backup&#8217;а. Итак, перехожу на вкладку &#8220;Базы данных&#8221; и создаю новую, введя в поле нужное мне имя &#8211; cifero. На самом деле имя может быть любым. Нажимаю кнопку &#8220;Создать&#8221;. База данных cifero появляется в списке:<figure id="attachment_389" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/denwer_db_cifero-600x431.png" alt="Созданная база данных cifero" width="600" height="431" class="size-medium wp-image-389" />][3]<figcaption class="wp-caption-text">Созданная база данных cifero</figcaption></figure> 

4. Перед импортом резервной копии базы данных необходимо отметить один момент. Доменное имя, на котором находился когда-то сайт, нужно поменять. Ведь в таблицах резервной копии везде прописана ссылка на http://cifero.ru, а в нашем случае копия будет восстанавливаться на домене cifero.lc. Также в таблицах необходимо исправить имя базы данных &#8211; она также изменилась и теперь называется cifero. Можно также изменить и пароль пользователя, но проще это сделать уже потом, после импорта в phpMyAdmin.

Если не выполнить вышеуказанные действия, то импортированная база данных просто не подключиться и восстановление сайта будет невозможно.

Итак, в первую очередь, распаковываю резервную копию cifero\_wrdp1\_wp\_20100225\_594.sql.gz. В результате получился файл довольно приличного размера &#8211; около 4Мб. По своей сути он представляет из себя обычный текстовый файл, который можно и нужно открыть в любом редакторе.

5. Запускаю его в AkelPad и начинаю правку. Нахожу строчку Database: \`cifero_wrdp1\` (она находится в самом начале файла, тут проблем не возникает) и меняю ее значение на Database: \`cifero\`. Все &#8211; имя базы данных исправлено. Теперь необходимо найти все ссылки вида http://www.cifero.ru/, http://cifero.ru и заменить их на http://cifero.lc. Для этого воспользуюсь автоматизированным инструментом поиска и замены в редакторе AkelPad, иначе вручную эта операция может занять неизвестно сколько времени:<figure id="attachment_390" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/db_modify-600x488.png" alt="Правка резервной копии сайта" width="600" height="488" class="size-medium wp-image-390" />][4]<figcaption class="wp-caption-text">Правка резервной копии сайта</figcaption></figure> 

Сохраняю измененный файл и закрываю его. Стоит также упомянуть еще один момент. При редактировании файла можно заметить многочисленные ссылки, указывающие на плагины, которые когда то были установлены в WordPress на сайте cifero.ru. Но в версии WordPress, которую я буду устанавливать на локальном хостинге Denwer, их не будет. Этот факт приведет к эффекту так называемого &#8220;белого экрана смерти&#8221; в WordPress. То есть, при вводе в адресной строке браузера http:/cifero.lc/ страница откроется, но изображено на ней ничего не будет &#8211; она будет пуста, как чистый лист бумаги. Но для меня данный факт не является критичным. В мою задачу, как уже говорилось ранее, входит восстановление статей, но не самого сайта.

Теперь можно импортировать таблицы в созданную пустую базу данных cifero.

6. Захожу в эту базу данных (для этого достаточно кликнуть одинарным щелчком мыши на самом названии этой базы в списке) и вижу, что она действительно пустая, о чем говорит надпись &#8220;Таблиц в базе данных не обнаружено&#8221;. Но я их и не собираюсь создавать &#8211; они у меня уже есть, только в резервной копии. Мне нужно только их импортировать из ранее скачанного backup&#8217;а в базу данных cifero. Для этого перехожу на вкладку &#8220;Импорт&#8221; и выбираю файлик cifero\_wrdp1\_wp\_20100225\_594.sql:<figure id="attachment_391" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/denwer_import_db-600x431.png" alt="Импорт базы данных cifero" width="600" height="431" class="size-medium wp-image-391" />][5]<figcaption class="wp-caption-text">Импорт базы данных cifero</figcaption></figure> 

Нажимаю кнопку ОК в самом низу окна. Начнется процесс импорта. И тут же возникает ошибка:<figure id="attachment_392" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/error_import_db_pma-600x300.png" alt="Импорт в базу данных успешно завершен" width="600" height="300" class="size-medium wp-image-392" />][6]<figcaption class="wp-caption-text">Импорт в базу данных успешно завершен</figcaption></figure> 

Это говорит о том, что в настройках Denwer имеется ограничение по размеру загружаемого файла, моем случае это cifero\_wrdp1\_wp\_20100225\_594.sql. Основной файл настроек Denwer&#8217;а &#8211; php.ini, а параметр, отвечающий за размер загружаемого файла &#8211; upload\_max\_filesize.

Расположение файла php.ini я не знаю (а если и знал, то забыл), поэтому проще всего найти его с помощью инструмента поиска TotalCommander:<figure id="attachment_393" style="width: 500px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/find_php_ini_file.png" alt="Ищем файл php.ini" width="500" height="401" class="size-full wp-image-393" />][7]<figcaption class="wp-caption-text">Ищем файл php.ini</figcaption></figure> 

Перехожу к найденному php.ini с помощью кнопки &#8220;Перейти к файлу&#8221; и открываю его в текстового редакторе (может быть любым, но лучше специализированный &#8211; Notepad++ или AkelPad). Теперь необходимо найти параметр upload\_max\_filesize. Для этого опять воспользуюсь инструментом поиска, но уже текстового редактора (у меня это AkelPad):<figure id="attachment_394" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/find_upload_max_filesize_file-600x432.png" alt="Находим параметр upload_max_filesize" width="600" height="432" class="size-medium wp-image-394" />][8]<figcaption class="wp-caption-text">Находим параметр upload\_max\_filesize</figcaption></figure> 

Вижу, что значение по умолчанию для этого параметра равно 2Мб. Мой распакованный файл резервной копии sql имеет размер 3,88Мб. Поэтому меняю параметр upload\_max\_filesize на 8Мб (с запасом). Сохраняю изменения в файле php.ini и обязательно не забываю перезапустить Denwer, чтобы изменения вступили в силу.

Снова пробую импортировать таблицы в базу данных cifero. На этот раз операция проходит успешно:<figure id="attachment_395" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/denwer_import_db_success-600x253.png" alt="Успешный импорт таблиц в базу данных" width="600" height="253" class="size-medium wp-image-395" />][9]<figcaption class="wp-caption-text">Успешный импорт таблиц в базу данных</figcaption></figure> 

Осталась последняя операция с таблицами в базе данных. Так как ни имени пользователя, ни пароля к нему я не помню (давно уже это было), то необходимо изменить хотя бы пароль для входа в административную часть сайта. Открываю в phpMyAdmin базу данных cifero (если она еще не открыта) и в левом списке нахожу таблицу wp_users. Открываю ее и вижу одну единственную строку, в которой прописана учетная запись в WordPress, под которой я размещал статьи.

Нажимаю на ссылку &#8220;Изменить&#8221; для входа в редактирование учетной записи. Появится небольшая табличка с десятью строками. Мне необходима строка user_pass. В столбце &#8220;Функция&#8221; из раскрывающегося списка выбираю алгоритм шифрования MD5. В поле столбца &#8220;Значение&#8221; прописан предыдущий пароль в зашифрованном виде. Очищаю это поле и ввожу туда новый пароль, пусть это будет 123:<figure id="attachment_396" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/denwer_change_password-600x371.png" alt="Изменяем пароль пользователя WordPress" width="600" height="371" class="size-medium wp-image-396" />][10]<figcaption class="wp-caption-text">Изменяем пароль пользователя WordPress</figcaption></figure> 

Логин пользователя &#8211; gughai &#8211; оставляю без изменений, только выписываю его отдельно, чтобы снова не забыть. Нажимаю кнопку ОК для сохранения внесенных в таблицу wp_users изменений. Опять перезапускаю Denwer.

7. Половина дела сделана. Теперь осталось только установить саму систему управления контентом WordPress. При установке созданная мною база данных подключится к этой CMS.

Открываю файловый менеджер (для меня удобнее всего работать с Total Commander), перехожу на локальный диск Z, созданный и запущенный программой Denwer. В Total Commander последовательно создаю директории для будущей локальной копии сайта cifero. Сперва создаю директорию homecifero.lc, затем еще одну вложенную директорию homecifero.lcwww.

Распаковываю скачанный WordPress версии 3.5 по пути z:homecifero.lcwww. Проще всего это сделать таким образом. Открыть архив в WordPress в другой панели Total Commander, выделить все содержимое архива (Ctrl+A) и перетащить выделенные файлы мышью в противоположную панель Total Commander. Программа спросит, распаковывать ли такие-то файлы в указанное место. Соглашаюсь и через пару секунд разархивация и копирование будут выполнены:<figure id="attachment_397" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/denwer_archive_wordpress-600x348.png" alt="Распаковка WordPress на Denwer" width="600" height="348" class="size-medium wp-image-397" />][11]<figcaption class="wp-caption-text">Распаковка WordPress на Denwer</figcaption></figure> 

8. Перезапускаю Denwer с помощью ярлыка &#8220;Restart Denwer&#8221; на Рабочем столе. Это необходимо для того, чтобы все изменения, внесенные мною &#8211; создание базы данных cifero и импорт в нее таблиц &#8211; вступили в силу.

9. Остается только установить саму систему управления контентом WordPress. Процесс инсталляции стандартный и мало отличается от предыдущих версий WordPress, разве что немного изменился сам интерфейс пошагового мастера и стал удобнее. В адресной строке браузера ввожу http://cifero.lc и жму Enter. Установка WordPress начата:<figure id="attachment_398" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/wp_installation_step1-600x345.png" alt="Установка WordPress - шаг первый" width="600" height="345" class="size-medium wp-image-398" />][12]<figcaption class="wp-caption-text">Установка WordPress &#8211; шаг первый</figcaption></figure> 

Соглашаюсь с пошаговым мастером и нажимаю кнопку &#8220;Создать файл настроек&#8221;. После успешного создания файла настроек wp-config.php откроется окно, которое является вторым шагом при установке WordPress. Оно не требует ввода каких-либо данных. Просто жму кнопку &#8220;Вперед&#8221;.

Третье окно является, если так можно сказать, самым главным, так как здесь необходимо ввести такую важную информацию, как имя базы данных, которая будет подключена к устанавливаемой системе WordPress, имя пользователя (и его пароль) указанной базы данных. В моем случае я не стал усложнять задачу и создавать отдельного пользователя для базы данных cifero. Воспользовался учетной записью root, созданной пакетом Denwer по умолчанию. Так как для этой учетной записи не установлен пароль, то в поле ввода &#8220;Пароль&#8221; просто стер предыдущее значение и оставил его пустым:<figure id="attachment_399" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/wp_installation_step3-600x473.png" alt="Подключение базы данных к WordPress" width="600" height="473" class="size-medium wp-image-399" />][13]<figcaption class="wp-caption-text">Подключение базы данных к WordPress</figcaption></figure> 

Два последних поля ввода можно оставить без изменений, так как сервер базы данных и так располагается локально (localhost), а префикс подключаемой базы данных имеет точно такое же значение (wp_).

Жму отправить. Мастер установки отрапортует, что все в порядке, указанные мною данные верны и существующая база данных cifero успешно подключена. Можно запускать установку WordPress. Нажимаю кнопку &#8220;Запустить установку&#8221;.

В браузере появиться сообщение о том, что: &#8220;Вы уже установили WordPress. Для переустановки, пожалуйста, сначала очистите старые таблицы в базе данных&#8221;. Нажимаю на кнопку &#8220;Войти&#8221;. Откроется обычное окно для входа в административную панель WordPress. Ввожу логин пользователя &#8211; gughai, и пароль (который я изменил) &#8211; 123.

Откроется еще одно окно с предупреждением о том, что необходимо обновить базы данных:<figure id="attachment_401" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/db_update-600x276.png" alt="Обновление базы данных" width="600" height="276" class="size-medium wp-image-401" />][14]<figcaption class="wp-caption-text">Обновление базы данных</figcaption></figure> 

Соглашаюсь с предложением. После сообщения о том, что: &#8220;База данных WordPress успешно обновлена!&#8221; жму кнопочку &#8220;Продолжить&#8221;.

Откроется панель администратора WordPress. Красным будет ярко высвечена надпись о том, что: &#8220;ОШИБКА: Директория тем либо пуста, либо не существует. Убедитесь, что дистрибутив установлен полностью&#8221;. Что же, данный факт, помимо отсутствия плагинов, будет причиной белого экрана сайта.

Перехожу в пункт меню &#8220;Записи&#8221; и вижу то, ради чего все и затевалось &#8211; записи, записи, записи&#8230; Вверху шапка сайта с таким романтическим названием&#8230; )))<figure id="attachment_402" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/wp_results_notes-600x371.png" alt="Восстановленные записи" width="600" height="371" class="size-medium wp-image-402" />][15]<figcaption class="wp-caption-text">Восстановленные записи</figcaption></figure> 

Любую запись можно открыть, отредактировать или сохранить в другом месте компьютера. Или перенести на действующий сайт. На этом поставленную задачу считаю выполненной.

Оцените статью:  
<span id="post-ratings-385" class="post-ratings" data-nonce="5df9e4b23b"><img id="rating_385_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(385, 1, '1 Star');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_385_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(385, 2, '2 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_385_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(385, 3, '3 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_385_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(385, 4, '4 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_385_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(385, 5, '5 Stars');" onmouseout="ratings_off(4.2, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>5</strong> votes, average: <strong>4,20</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_385_text"></span></span><span id="post-ratings-385-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/04/denwer.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/04/denwer_pma_dblist.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/04/denwer_db_cifero.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/04/db_modify.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/04/denwer_import_db.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/04/error_import_db_pma.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/04/find_php_ini_file.png
 [8]: http://localhost:7788/third/wp-content/uploads/2013/04/find_upload_max_filesize_file.png
 [9]: http://localhost:7788/third/wp-content/uploads/2013/04/denwer_import_db_success.png
 [10]: http://localhost:7788/third/wp-content/uploads/2013/04/denwer_change_password.png
 [11]: http://localhost:7788/third/wp-content/uploads/2013/04/denwer_archive_wordpress.png
 [12]: http://localhost:7788/third/wp-content/uploads/2013/04/wp_installation_step1.png
 [13]: http://localhost:7788/third/wp-content/uploads/2013/04/wp_installation_step3.png
 [14]: http://localhost:7788/third/wp-content/uploads/2013/04/db_update.png
 [15]: http://localhost:7788/third/wp-content/uploads/2013/04/wp_results_notes.png