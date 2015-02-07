---
title: 'Gulp &#8211; установка и запуск плагина gulp-uglify'
author: gearmobile
excerpt: Установка и создание задачи под Gulp на примере одного из его плагинов gulp-uglify. Произведем установку плагина, настройку именованной задачи и ее запуск.
layout: post
permalink: /gulp-install-and-launch-gulp-uglify/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 7
ratings_score:
  - 35
ratings_average:
  - 5
categories:
  - 'Javascript &amp; jQuery'
tags:
  - gulp
  - gulp-uglify
---
В предыдущей статье [Gulp &#8211; знакомство и первый запуск][1] мы познакомились с установкой менеджера Gulp и запуском первой задачи под него. В этой статье мы перейдем к еще более интересному материалу, в котором узнаем, как **устанавливать и запускать плагины под Gulp** на примере одного из них &#8211; [gulp-uglify][2].

Как я уже упоминал ранее, Gulp имеет модульную структуру. Под Gulp, несмотря на молодость проекта, уже написано достаточное количество плагинов. Конечно, оно не сравниться с огромной коллекцией таковых под мега-популярный Grunt, но для большинства случаев жизни уже сейчас их хватит. Каждый из плагинов &#8211; это код, решающий только одну задачу. Например, один плагин умеет сжимать изображения, другой сжимает js-файлы, третий сжимает css-файлы; еще один умеет компилировать scss-файлы в css-файлы. И так далее &#8211; список можно продолжать и продолжать.

Становиться понятно, что для конкретной задачи нам нужно установить нужный плагин и создать задачу (task) в файле `gulpfile.js`. А затем запустить Gulp на выполнение этой задачи. Конечно, задач может быть не одна, а несколько. Все зависит о того, какие именно задачи нам необходимо выполнять.

Давайте рассмотрим процесс установки плагинов и настройки задач на примере одного из них &#8211; `gulp-uglify`. Данный плагин служит для минификации js-файлов &#8211; он удаляет пробелы, запятые, точки с запятой. В результате js-файл получается меньшим по размеру.

Все плагины под Gulp размещены по этому адресу &#8211; [Gulp Plugins][3]. В строке поиска нужно вводить имя искомого плагина, в результате получаем (*или не получаем*) страницу с описанием плагина и командой для его установки.

### Устанавливаем gulp-uglify под Gulp

На странице плагина [gulp-uglify][2] описана команда установки этого плагина, которую мы повторим для себя, в своем проекте:

<pre>$ npm install --save-dev gulp-uglify
</pre>

Опять таки, ключ `--save-dev` &#8220;говорит&#8221; менеджеру `npm` добавить плагин `gulp-uglify` в качестве зависимости в файл `package.json`:

<pre>$ cat package.json
  {
    "name": "first",
    "version": "0.0.1",
    "devDependencies": {
      "gulp": "~3.8.7",
      "gulp-uglify": "~0.3.1"
    }
  }
</pre>

### Создаем задачу gulp-uglify под Gulp

Плагин `gulp-uglify` установлен и теперь самое время прописать в файле `gulpfile.js` именованную задачу (named task) под него. Надеюсь, уважаемый читатель помнит о двух типах задач под Gulp, описанных в предыдущей статье [Gulp &#8211; знакомство и первый запуск][1].

Открываем файл `gulpfile.js` в редакторе кода (у меня это Sublime Text) и вносим туда следующие строки:

<pre>var gulp = require('gulp'),
      uglify = require('gulp-uglify');
  ...
  // Gulp Uglify
  gulp.task('gulp-uglify', function(){
    gulp.src('js/*.js')
    .pipe(uglify())
    .pipe(gulp.dest('build/js'))
  });
</pre>

В принципе, можно и не вводить вышеприведенные строки вручную, а просто скопировать их со страницы описания плагина [gulp-uglify][2]. Они размещены в блоке с заголовком **Usage**.

Но это не главное. Важнее разобраться, что из себя представляет каждая из этих строк. Так вот, строка `uglify = require('gulp-uglify')` &#8211; это создание переменной с именем `uglify`, в которую помещается плагин `gulp-uglify`. Обратите внимание на **синтаксис этой строки и ее табуляцию** &#8211; оба аспекта важны и их несоблюдение приведет к тому, что **Gulp не будет работать**. По большому счету, можно написать и так &#8211; `var uglify = require('gulp-uglify');`, но предыдущая запись является более правильной.

Далее идут строки для **новой именованной задачи** для Gulp. Имя задачи задаем произвольно и пусть оно будет таким &#8211; `gulp-uglify`. В теле callback-функции пропишем директорию, содержимое которой Gulp должен отслеживать &#8211; `gulp.src('js/*.js')`. В данном случае указываем, что Gulp должен следить за изменениями всех файлов с расширением .js, расположенных внутри директории `js`. Следующая строка `.pipe(uglify())` получает в виде потока содержимое директории `js` и обрабатывает его с помощью плагина `gulp-uglify`, помещенного внутрь переменной `uglify`. Результат обработки передается в виде потока в строку `.pipe(gulp.dest('build/js'))`, которая сохраняет его по пути `build/js`.

Вот мы и разобрали суть задачи в Gulp! Ведь ничего сложного, правда?!

### Запускаем задачу gulp-uglify в Gulp

Переходим от слов к делу и запустим на выполнение только что созданную нами задачу `gulp-uglify`. Не забываем, что именованные задачи в Gulp запускаются с указанием их имени:

<pre>$ gulp gulp-uglify
  [21:47:43] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [21:47:43] Starting 'gulp-uglify'...
  [21:47:43] Finished 'gulp-uglify' after 12 ms
</pre>

Вуаля! Видим (по аналогии с предыдушим опытом запуска дефолтной задачи), что именованная задача `gulp-uglify` успешно запустилась, выполнилась за 12 миллисекунд и также успешно завершилась. По идее, теперь по пути `build/js` у нас должен располагаться минифицированный js-файл (в моем случае это был `jquery-1.11.1.js`).

Посмотрим и видим, что так оно и есть, файлик `jquery-1.11.1.js` помещен туда, куда мы и прописывали:

<pre>$ ls build/js/
  jquery-1.11.1.js
</pre>

А точно ли он минифицированный? Это легко проверить &#8211; открываем его в Sublime Text и наблюдаем такую картину:<figure id="attachment_1604" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp_gulp_uglify-600x291.png" alt="Минифицированный с помощью gulp-uglify файл в Gulp" width="600" height="291" class="size-medium wp-image-1604" />][4]<figcaption class="wp-caption-text">Минифицированный с помощью gulp-uglify файл в Gulp</figcaption></figure> 

### Полезные плагины под Gulp

Мы успешно установили и запустили плагин под Gulp &#8211; можно **в очередной раз поздравить себя**! В данном случае это был плагин `gulp-uglify` для минификации js-файлов.

Однако, как можно догадаться, существует большое количество других полезных плагинов. Все они устанавливаются и настраиваются точно также, как и рассмотренный нами `gulp-uglify`.

Ниже я приведу примерный **список наиболее полезных плагинов под Gulp**, существующих на сегодняшний день:

  * **gulp-minify-html** // минификация HTML-файлов
  * **gulp-minify-css** // минификация CSS-файлов
  * **gulp-csso** // еще один плагин минификации CSS-файлов
  * **gulp-uglify** // минификация JS-файлов
  * **gulp-sass** // компиляция SCSS-файлов в CSS-файлы
  * **gulp-ruby-sass** // компиляции SCSS-файлов в CSS-файлы, более стабильный
  * **gulp-concat** // конкатенация (соединение нескольких файлов в один файл)
  * **gulp-jshint** // ???
  * **gulp-livereload** // запуск плагина LiveReload
  * **gulp-watch** // мониторинг файлов в фоновом режиме в Gulp
  * **gulp-notify** // вывод окна с уведомлением о событиях в Gulp
  * **gulp-imagemin** // сжатие изображений в Gulp
  * **gulp-rename** // переименование файлов в Gulp
  * **gulp-plumber** // настройка обработки ошибок в Gulp

Оцените статью:  
<span id="post-ratings-1603" class="post-ratings" data-nonce="079cfa562b"><img id="rating_1603_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1603, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1603_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1603, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1603_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1603, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1603_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1603, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1603_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1603, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>7</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1603_text"></span></span><span id="post-ratings-1603-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1588 "Gulp - знакомство и первый запуск"
 [2]: https://www.npmjs.org/package/gulp-uglify/ "gulp-uglify"
 [3]: http://gulpjs.com/plugins/ "Gulp Plugins"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp_gulp_uglify.png