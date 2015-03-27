---
title: Знакомимся с редактором SassMeister
author: gearmobile
layout: post
permalink: /playground-sassmeister/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - sassmeister
---
Решил написать небольшой обзор по online-инструменту для front-end&#8217;щика под названием SassMeister. На русском языке не встречал хотя бы краткого описания, поэтому решил, что не помешает познакомиться в ним поближе.

Итак, что это за инструмент? Если сказать кратко &#8211; это online-редактор для кода, наподобие известного CodePen, который уже описывался на страницах данного блога &#8211; [Площадка для тестирования CodePen][1]. Другими словами, SassMeister является площадкой для тестирования (playground) для людей, связанный с веб-разработкой.

### Различие между CodePen и SassMeister

Также, как и CodePen, данный редактор предназначен исключительно для front-end разработчиков, так как понимает только два языка &#8211; HTML и CSS. А также всевозможные препроцессоры к этой паре языков. Как и CodePen, SassMeister позволяет сохранять созданный в нем код и делать еще пару вещей.

Но в чем же тогда отличие SassMeister от CodePen, что заставило упомянуть этот *playground*? Отличие есть и оно существенное. Площадка CodePen &#8211; это универсальный инструмент для веб-разработчика. В нем есть все необходимое для работы &#8211; зарегистрировался, открыл и работай! SassMeister &#8211; это площадка, созданная исключительно для работы с препроцессором Sass и его библиотеками. Получается, что у последнего специализация более узкая; за счет этого SassMeister выполняет свою задачу лучше, чем CodePen.

Итак, в двух словах. Вам нужен хороший универсальный инструмент front-end разработки? Это CodePen. Вам нужен хороший инструмент для работы только с препроцессором Sass? Это SassMeister.

Давайте попробуем создать пример кода в этом инструменте и на его примере поймем, как с ним работать. Итак, открываем главную страницу SassMeister &#8211; [SassMeister][2] и видим основное окно с вкладками вверху. (*Сразу стоит сказать, что редактор SassMeister имеет тесную интеграцию с сервисом GitHub, поэтому зайти в редактор можно, используя учетную запись последнего.*) Самая главная и нужная среди них &#8211; вкладка с настройками редактора, которая называется Control Panel.

### Панель управления SassMeister

Открываем ее и разберемся с ней:<figure id="attachment_1172" style="width: 312px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/sassmeister_control_panel-312x600.jpg" alt="Панель управления редактора SassMeister" width="312" height="600" class="size-medium wp-image-1172" />][3]<figcaption class="wp-caption-text">Панель управления редактора SassMeister</figcaption></figure> 

Во-первых, надпись **Sass** не дает нам забыть о том, что мы собираемся работать с препроцессором Sass (*это типа шутки*).

Вторая строка **Compiler** с тремя переключателями позволяет выбрать, какую версию препроцессора Sass мы хотим использовать: свежую 3.3.6, более раннюю 3.2.19 или же LibSass (*портированный на С препроцессор Sass*).

В третьей строке выбираем, с каким **синтаксисом** препроцессора Sass мы будем работать &#8211; с новым SCSS или же со старым Sass (*на котором почти никто не пишет на сегодняшний день*).

Отлично, идем дальше!

Опускаем взгляд еще ниже на окно с заголовком **Extensions** и останавливаемся, затаив дыхание. Да-да, вы не ошиблись! Это именно то, о чем вы подумали! Это список плагинов на выбор, которые можно подключить в наш проект один щелчком мыши. А теперь напомните мне, с каким списком расширений под Sass может работать CodePen? Не помните? Я подскажу &#8211; с двумя! Это Compass и Bourbon.

Конечно, в CodePen можно подключить на выбор не один препроцессор, а несколько &#8211; Sass, LESS, Stylus. Но вот с выбором плагинов под эти препроцессоры будет слабовато. В этом и заключается преимущество SassMeister &#8211; он делает одну вещь, но делает ее хорошо, основательно, до конца!

ОК, для нашего примера работы в SassMeister выберем из этого списка три расширения: Breakpoint, Compass, Susy. Это делается одинарным щелчком мыши на названии расширения, как будто это простая ссылка на веб-странице. Выбранное расширение автоматически добавляется в проект строкой:

<pre>@import "breakpoint";
@import "compass";
@import "susy";
</pre>

Четвертая строка **CSS** предлагает опции, с которыми внимательный читатель уже должен быть знаком. Это стандартные опции компилирования препроцессора Sass из SCSS-кода в CSS-код. Точно такие же настройки имеются в конфигурационном файле `config.rb` любого Sass/Compass-проекта.

Пятая строка **HTML** предлагает выбрать способ, которым мы будем писать код HTML. Это будет или чистый HTML, или же с помощью HTML-препроцессоров: Haml, Markdown, Textile, Jade. (*О препроцессоре Markdown имеется статья на данном блоге &#8211; [Язык Markdown &#8211; обзор редакторов для работы][4]*).

В строке **Editor** можно выбрать визуальную тему оформления для редактора SassMeister. Допустим, выберу для себя тему *Monokai*, так как люблю работать с редактором Sublime Text (*здесь нет темы Twilight, а то бы однозначно выбрал ее*).

Чекбоксы `Enable Emmet support` и `Use Vim keybindings` предназначены для любителей работать с плагином Emmet под Sublime Text и совсем крутых парней (*привет Sorax*), которые предпочитают стиль редактора Vim.

Вот и все настройки одновременно с обзором возможностей редактора SassMeister. Пора переходить к написанию кода. Для этого закрываем Control Panel и щелкаем мышью на вкладках CSS и HTML вверху. Добавятся еще два окошка CSS и HTML, соответственно. Накидаем в окне HTML совсем простенький код, немного оформим его в окне SCSS, проверим скомпилированный результат в окне CSS и полюбуемся на творение рук своих в четвертом, самом нижнем окне визуального предпросмотра:<figure id="attachment_1173" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/sassmeister_result-600x321.jpg" alt="Результат работы в редакторе SassMeister" width="600" height="321" class="size-medium wp-image-1173" />][5]<figcaption class="wp-caption-text">Результат работы в редакторе SassMeister</figcaption></figure> 

### Сохранение кода в SassMeister через GitHub Gist

Отлично! Мы успешно справились с задачей и создали великолепный образец кода в SassMeister. Теперь осталось самое малое &#8211; сохранить на века этот образец, чтобы потомки смогли восхищаться им. Нетрудно догадаться, что для этой цели служит вкладка в виде облачка. Наводим на нее мышь и видим надписи &#8211; **Save Gist** и **Reset**. Напрягаем все извилины своего мозга и щелкаем мышью по ссылке **Save Gist**. Редактор SassMeister радостно (*зелененькой надписью*) сообщает, что наш &#8220;**Gist is saved**&#8220;.

А что такое **Gist** и где оказался наш кусочек кода (*куда он сохранился*)? Еще раз наводим мышь на облачко и видим, что вкладочка то поменялась! Вместо двух там теперь появилось еще несколько ссылок: **Update Gist**, **View on GitHub**, **Fork Gist**, наша старая знакомая **Reset**. Вау, знакомые слова &#8211; **GitHub**, **Fork**! А давайте пройдем по ссылочке **View on GitHub**?<figure id="attachment_1174" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/sassmeister_github_gist-600x444.jpg" alt="Сохраненный код с SassMeister на сервисе GitHub Gist" width="600" height="444" class="size-medium wp-image-1174" />][6]<figcaption class="wp-caption-text">Сохраненный код с SassMeister на сервисе GitHub Gist</figcaption></figure> 

Ну конечно же! Мы оказались на GitHub, а точнее &#8211; на его сервисе **Gist**. Кто не знаком с этим сервисом, может уже догадаться о его предназначении. Он служит для хранения таких вот (*и не обязательно именно таких*) кусочков кода (*snippets*). Более того, у сервиса **Gist** имеется интеграция через плагин с редактором Sublime Text, которая позволяет буквально по волшебству вставлять код из **Gist** прямо в ST!

После сохранения кода на GitHub Gist в панели SassMeister появляется еще одна вкладочка &#8211; стрелка. Назначение ее предельно понятно &#8211; с помощью нее можно встраивать (*embed*) созданный здесь код в другой проект, в виде объекта.

### SassMeister &#8211; заключение

Вот, в принципе, и все, что можно рассказать об online-редакторе SassMeister. Единственный момент, с которым я не разобрался, это вкладка **Bookmark** &#8211; для чего она нужна и как с ней работать, в чем прикол ее существования в этом редакторе. Может быть, внимательный читатель подскажет, для чего она нужна?

Думаю, для кодеров, которые любят и активно используют препроцессор Sass совместно с великолепной библиотекой Compass и плагинами в ней, площадка для тестирования SassMeister понравиться однозначно!

Оцените статью:  
<span id="post-ratings-1170" class="post-ratings" data-nonce="1d5acf2067"><img id="rating_1170_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1170, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1170_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1170, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1170_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1170, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1170_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1170, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1170_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1170, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1170_text"></span></span><span id="post-ratings-1170-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=952 "Площадка для тестирования CodePen"
 [2]: http://sassmeister.com/ "SassMeister"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/05/sassmeister_control_panel.jpg
 [4]: http://localhost:7788/third/?p=717 "Язык Markdown - обзор редакторов для работы"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/05/sassmeister_result.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/05/sassmeister_github_gist.jpg