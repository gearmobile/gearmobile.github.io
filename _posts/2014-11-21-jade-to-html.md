---
title: 'Jade &#8211; два способа компиляции в HTML'
author: gearmobile
excerpt: 'Два способа настройки компиляции jade-файлов в HTML. Первый способ - с помощью родной утилиты Jade. Второй способ - с помощью плагина gulp-jade под Gulp. Настройка подсветки синтаксиса Jade в редакторе Sublime Text 3.'
layout: post
permalink: /jade-to-html/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 5
ratings_score:
  - 22
ratings_average:
  - 4.4
categories:
  - Web Development
tags:
  - jade
---
В этом посте поделюсь своим опытом реализации задачи компиляции jade-файлов в HTML-формат.

Рассмотрю два способа реализации этой задачи. Первый &#8211; самый нативный, с помощью родной утилиты `jade`. Второй &#8211; с помощью плагина `gulp-jade` под Gulp.

Но способов компиляции Jade в HTML существует больше &#8211; есть плагин под Sublime Text, существует плагин под Grunt. Обладатели Mac OS X могут воспользоваться прекрасной программой CodeKit. И я уверен, что это только малая часть того, чем можно воспользоваться.

Кратко остановлюсь на вопросе, зачем мне понадобился [Jade][1]. Честно сказать, до недавнего момента я даже не подозревал о сущестовании такого шаблонизатора. Тихо-спокойно пользовался Sublime Text + Emmet и считал, что я на вершине современных требований к web-разработчику.

Однако это оказалось не совсем так. Мне посоветовали посмотреть в сторону Jade и разобраться с работой в нем. Хотя бы с синтаксисом, для начала.

И я скажу вам &#8211; мне понравилось! Даже простое использование синтаксиса. Первое впечатление и ощущение &#8211; использование этого шаблонизатора освобождает от рамок HTML при написании кода. Точнее &#8211; при создании кода сосредотачиваешься на содержимом, которое создаешь.

Но у Jade есть еще и миксины, с которыми мне предстоит познакомиться. Так что &#8211; лучшее только впереди!

Написание кода в этом шаблонизаторе чем-то похоже на написание текста в [Markdown][2]. Под Markdown имеются (и должны иметься) утилиты\программы для компиляции в HTML. Точно также для Jade должны иметься (и имеются) утилиты\программы для компиляции в HTML.

### Jade &#8211; синтаксис для Sublime Text 3

Прежде чем писать код в редакторе, в моем случае необходимо настроить поддержку синтаксиса Jade. Я использую Sublime Text 3, который изначально не имеет таковой.

Исправить это легко &#8211; достаточно через `Package Control` установить пакет `Jade`. Помимо подсветки синтаксиса, появиться поддержка автоматической табуляции, что значительно упрощает процесс написания кода.

Пример подсветки синтаксиса Jade в Sublime Text 3:<figure id="attachment_2024" style="width: 501px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/jade-501x600.png" alt="Пример подсветки синтаксиса Jade в Sublime Text 3" width="501" height="600" class="size-medium wp-image-2024" />][3]<figcaption class="wp-caption-text">Пример подсветки синтаксиса Jade в Sublime Text 3</figcaption></figure> 

### Jade &#8211; родная утилита шаблонизатора

Разработчиками была создана **родная утилита** для преобразования jade-файлов в HTML-файлы. Имя утилиты легко запомнить &#8211; это `jade`.

Утилита является **модулем под Node.js**, поэтому последний у вас должен быть заранее установлен (*если еще не установлен по какой-то необъяснимой причине*).

Инсталляция утилиты производиться **банально**:

<pre>// Command Line

  $ sudo npm install -g jade
  </pre>

Утилита имеет немногочисленные параметры, с кратким описанием которых можно ознакомиться на странице официальной документации &#8211; [Jade &#8211; Command Line][4].

Но стоит обратить внимание на некоторые **интересные параметры**:

**К примеру**:

  * `-P, --pretty` &#8211; создание &#8220;удобочитаемого&#8221; HTML-кода
  * `-w, --watch` &#8211; мониторинг изменений файлов

Использование утилиты также является простым делом. К примеру, можно указать ей производить компиляцию всех файлов в директории `templates`:

<pre>// Command Line

  $ jade templates
  </pre>

Утилита может сама создавать jade-файлы:

<pre>// Command Line

  $ jade {foo,bar}.jade
  </pre>

Или же можно реализовать **два способа вывода**:

<pre>// Command Line

  $ jade &lt; my.jade > my.html
  </pre>

<pre>// Command Line

  $ echo "h1 Jade!" | jade
  </pre>

Или же осуществить рендеринг двух директорий `foo` и `bar` в директорию `tmp`:

<pre>// Command Line

  $ jade foo bar --out /tmp
  </pre>

### Gulp-jade &#8211; компиляция под Gulp

Кто знаком с task-manager&#8217;ом Gulp, тот может воспользоваться соответствующим плагином `gulp-jade` под него. Страничка плагина размещена здесь &#8211; [gulp-jade][5].

Установка плагина **стандартная**:

<pre>// Command Line

  $ npm install --save-dev gulp-jade
  </pre>

Затем нужно создать задачу (task) для компиляции jade-файлов в HTML-файлы. Ниже приведу свой рабочий task:

<pre>// JavaScript

  var gulp = require('gulp'),
  jade = require('gulp-jade');

  // Jade
  gulp.task('jade', function(){
    gulp.src('./template/*.jade')
      .pipe(jade())
      .pipe(gulp.dest('./dist/'))
  });

  // Watch
  gulp.task('watch', function(){
   gulp.watch('./template/*.jade',['jade']);
  });
  </pre>

В Сети есть еще один интересный Gulp-task. Работоспособность его **не проверял**, взял как есть, для &#8211; &#8220;чтобы было&#8221;.

Как говориться на [странице-оригинале][6], эта задача производит компиляцию файлов из директории `app/` в директорию `_public/`:

<pre>// CoffeeScript

  jade = require 'gulp-jade'

  gulp.task 'jade', ->
    gulp.src parameters.app_path + '/*.jade'
    .pipe jade pretty: true
    .pipe gulp.dest parameters.web_path
    .on 'error', gutil.log
  </pre>

### Заключение

Я запомнил (*записал для себя*), а вы (*уважаемый читатель*) познакомились (*если не знали*) с двумя способами настройки компиляции jade-файлов в HTML-файлы.

Оцените статью:  
<span id="post-ratings-2022" class="post-ratings" data-nonce="d0ab5f29a6"><img id="rating_2022_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2022, 1, '1 Star');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2022_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2022, 2, '2 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2022_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2022, 3, '3 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2022_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2022, 4, '4 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2022_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2022, 5, '5 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>5</strong> votes, average: <strong>4,40</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2022_text"></span></span><span id="post-ratings-2022-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://jade-lang.com/ "Jade"
 [2]: http://localhost:7788/third/?p=717 "Язык Markdown - обзор редакторов для работы"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/11/jade.png
 [4]: http://jade-lang.com/command-line/ "Jade - Command Line"
 [5]: https://www.npmjs.org/package/gulp-jade "gulp-jade"
 [6]: http://david.nowinsky.net/gulp-book/example/jade.html "Compiling Jade files"