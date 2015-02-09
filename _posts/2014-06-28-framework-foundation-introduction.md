---
title: 'Фреймворк Foundation &#8211; Знакомство'
author: gearmobile
excerpt: 'Начинаем изучение фреймворка Foundation. Этот фреймворк входит в двойку самых популярных и распространенных CSS-фреймворков на момент написания статьи - Bootstrap и Foundation. Можно по разному относиться к фреймворкам - любить их или не любить. Однако, они есть и ими пользуются при создании сайтов.'
layout: post
permalink: /framework-foundation-introduction/
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
  - foundation
---
Начинаем изучение фреймворка Foundation. Этот фреймворк входит в двойку самых популярных и распространенных CSS-фреймворков на момент написания статьи (еще один &#8211; Twitter Bootstrap). Можно по разному относиться к фреймворкам &#8211; любить их или не любить. Однако, они есть и ими пользуются при создании сайтов. Данный факт говорит о том, что фреймворки &#8211; это все-таки не такое уж и Зло. Скорее всего, нужно выработать для себя такое отношение к фреймворкам, что это быстрый способ создать что-либо непритязательное &#8211; не слишком оригинальное по дизайну, со стандартизированными элементами и не слишком оптимизированным кодом (*читай &#8211; с большой долей мусора*). А вот если к шаблону предъявляются повышенные требования, вот тогда нужно писать весь код вручную.

Но, как говорилось уже выше, фреймворки &#8211; они есть, и факт их существования говорит сам за себя. А поэтому, любой профессиональный веб-разработчик обязан знать и уметь работать с ними. В этой статье будет положено начало посильного знакомства с одним из двух популярных фреймворков &#8211; ZURB Foundation.

### Сайт проекта Foundation

Официальный сайт проекта находится по этому адресу &#8211; [Foundation][1]. Если внимательно присмотреться, то можно заметить, что на странице проекта и в других местах часто мелькает слово [ZURB][2] &#8211; это название дизайнерской фирмы, которая и создала фреймворк.

Если бегло пробежаться по документации, то можно увидеть множество &#8220;плюшек&#8221; у данного фреймворка:

  * фирменную консольную утилитку foundation для разворачивания или обновления проекта на Foundation
  * коллекцию [сниппетов под Sublime Text][3] для быстрого создания различных компонент HTML-страницы
  * тесная интерграция с препроцессором Sass

Естественно, Foundation заявляется как полностью адаптивный фреймворк, нацеленный прежде всего на создание мобильных версий сайтов (Mobile First).

### Способы установки Foundation

Как говориться на [странице документации][4], существует три способа установки фреймворка на локальном компьютере:

  * [Getting Started With Foundation CSS][5] &#8211; самый простой и быстрый способ установки и начала работы. Нужно просто скачать и распаковать архив с готовым фреймворком
  * [Getting Started With Sass][6] &#8211; разворачивание фреймворка c поддержкой Sass/Compass. Установка на локальный компьютер производится автоматически, с помощью уже упоминавшейся консольной утилиты foundation
  * [Applications][7] &#8211; это что-то связано с разработкой приложений под Foundation. В общем, для front-end это не интересно

В дальнейшей статье приступим в установке Foundation вторым способом, так как мы уже хорошо знаем и умеем пользоваться препроцессором Sass и его библиотекой Compass.

### Установка Foundation c поддержкой Sass

Для установки фреймворка на локальный компьютер с поддержкой Sass/Compass потребуется предварительное начилие на нем таких программных продуктов, как:

  * Git &#8211; нужен для работы Bower
  * Ruby &#8211; нужен для работы Sass/Compass
  * Nodejs &#8211; нужен для работы Grunt

Foundation версии 5 использует для установки своих компонентов, а также для обновления себя самого в целом менеджер пакетов Bower, поэтому его наличие также жизненно необходимо в системе. Помимо этого, фреймворк может работать совместно с менеджером задач Grunt для конкатенации файлов; но наличие Grunt не является обязательным.

Проверяю наличие трех вышеназванных пакетов в своей системе Linux Mint 17. Все три пакета были установлены мною гораздо раньше. Как выполнить установку Git, Ruby, Nodejs, Grunt и Bower под Linux Mint 17, можно почитать в этой статье &#8211; [Установка Node.js, npm и Bower под Linux Mint][8]:

<pre>$ git --version
  git version 1.9.1
  $ ruby --version
  ruby 1.9.3p484 (2013-11-22 revision 43786) [x86_64-linux]
  $ nodejs --version
  v0.10.25
  $ bower --version
  1.3.3
  </pre>

Установка Bower и Grunt, если они еще не были инсталлированы в системе, производится простой командой:

<pre>$ npm install -g bower grunt-cli
  </pre>

Все готово для установки консольной утилиты foundation. Вы спросите &#8211; что это еще за утилита такая и зачем она нужна? Все просто &#8211; это фирменная утилитка от Foundation и ее задача &#8211; автоматизированное разворачивание готового проекта на локальной машине.

Устанавливаем утилиту foundation:

<pre>$ gem install foundation
  </pre>

Сама утилитка foundation очень проста. Вызову команду `help` и все станет понятно без слов:

<pre>$ foundation help
  Commands:
    foundation help [COMMAND]  # Describe available commands or one specific command
    foundation new             # create new project
    foundation update          # update an existing project
    foundation upgrade         # Upgrade your Foundation 4 compass project
    foundation version         # Display CLI version
  </pre>

### Разворачивание Foundation c поддержкой Compass

C помощью утилиты foundation можно развернуть на локальной машине фреймворк c поддержкой:

  * Grunt и Libsass
  * Compass

Я воспользуюсь вторым вариантом и запущу установку Foundation c поддержкой Compass. Для этого нужно выполнить команду:

<pre>$ foundation new new_project_name
  </pre>

В моем случае имя нового проекта было оригинальным &#8211; foundation )) Пару секунд ожидания и я получаю папку с таким содержимым:

<pre>$ ls -l
  drwxr-xr-x bower_components
  -rw-r--r-- bower.json
  -rw-r--r-- config.rb
  -rw-rw-rw- Foundation.md
  -rw-r--r-- humans.txt
  -rw-r--r-- index.html
  drwxr-xr-x js
  -rw-r--r-- README.md
  -rw-r--r-- robots.txt
  drwxr-xr-x scss
  </pre><figure id="attachment_1388" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/new_project_in_foundation-600x360.png" alt="Новый проект на Foundation" width="600" height="360" class="size-medium wp-image-1388" />][9]<figcaption class="wp-caption-text">Новый проект на Foundation</figcaption></figure> 

Видим здесь файлы `config.rb`, `bower.json`, `index.html`; папки `bower_components`, `js`, `scss`. Другими словами &#8211; это готовый проект!

Немного подредактирую файл `config.rb` и запускаю Compass на мониторинг изменений в текущем проекте:

<pre>$ compass watch .
  </pre>

Проект готов для работы! В следующем обзоре будет рассмотрен самый простой пример работы с данным фреймворком &#8211; я с вами научусь создавать кнопки на Foundation.

Оцените статью:  
<span id="post-ratings-1386" class="post-ratings" data-nonce="cd578d1054"><img id="rating_1386_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1386, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1386_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1386, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1386_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1386, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1386_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1386, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1386_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1386, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1386_text"></span></span><span id="post-ratings-1386-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://foundation.zurb.com/ "Foundation"
 [2]: http://www.zurb.com/ "ZURB"
 [3]: https://github.com/zurb/foundation-5-sublime-snippets "сниппеты под Sublime Text"
 [4]: http://foundation.zurb.com/docs/ "Getting Started"
 [5]: http://foundation.zurb.com/docs/css.html "Getting Started With Foundation CSS"
 [6]: http://foundation.zurb.com/docs/sass.html "Getting Started With Sass"
 [7]: http://foundation.zurb.com/docs/applications.html "Applications"
 [8]: http://localhost:7788/third/install-nodejs-npm-bower-in-linux-mint/ "Установка Node.js, npm и Bower под Linux Mint"
 [9]: http://localhost:7788/third/wp-content/uploads/2014/06/new_project_in_foundation.png