---
title: 'Gulp-plumber &#8211; отслеживание ошибок в Gulp'
author: gearmobile
excerpt: Задача плагина gulp-plumber заключается в отслеживании возможных ошибок, возникающих при работе Gulp. Если появляется ошибка, то gulp-plumber формирует ее удобочитаемое отображение в выводе консоли. Кроме того, благодаря плагину gulp-plumber работа Gulp не прерывается при возникновении ошибки.
layout: post
permalink: /gulp-plumber/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
categories:
  - 'Javascript &amp; jQuery'
tags:
  - gulp
  - gulp-plumber
---
Кто не знаком с тем, что при написании кода очень часто возникают ошибки или банальные опечатки? И даже если установлены такие палочки-выручалочки, как Emmet, это не всегда спасает из ситуации. А если представить, что вы пишете большой проект и в нем закралась ошибка, то нелегко будет ее найти в куче кода.

При использовании Gulp, который автоматически отслеживает события и выполняет соотвествующие задачи, ситуация несколько &#8220;облегчается&#8221; тем, что при возникновении ошибки можно увидеть тот момент, когда она произошла. Например, Gulp настроен на автоматическое фиксирование изменений через `gulp.watch`. Если возникла ошибка, то выполнение мониторинга в Gulp прерывается:<figure id="attachment_1645" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-1645" src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp_error-600x304.png" alt="Прерванная работа Gulp" width="600" height="304" />][1]<figcaption class="wp-caption-text">Прерванная работа Gulp</figcaption></figure> 

Но даже в этом случае **довольно трудно разобраться, где именно закралась ошибка**. В этой ситуации может помочь плагин [gulp-plumber][2], который формирует вывод об ошибке. Но при этом **работа Gulp не прерывается**.

Давайте установим и попробуем в работе плагин `gulp-plumber`.

### Установка плагина gulp-plumber

Установка плагина `gulp-plumber` стандартная, через менеджер пакетов `npm` с ключом `--save-dev`:

<pre>$ sudo npm install --save-dev gulp-plumber
</pre>

### Использование плагина gulp-plumber

Для применения плагина `gulp-plumber` в проекте необходимо создать переменную `plumber`:

<pre>var plumber = require('gulp-plumber');
</pre>

А затем дописать строку `.pipe(plumber())` в ту задачу, в которой необходимо включить возможность отслеживания ошибок. Например, пусть это будет задача минификации всех js-файлов проекта `uglify`. Тогда в ней сразу после строки `gulp.src('js/*.js')` добавляем строку `.pipe(plumber())`, чтобы отслеживались возможные ошибки во всех нижеследующих задачах, таких как `.pipe(uglify())` или `.pipe(gulp.dest('build/js'))`:

<pre>// Uglify Task
  gulp.task('uglify', function(){
    gulp.src('js/*.js')
      .pipe(plumber()) // plumber
      .pipe(uglify())
      .pipe(gulp.dest('build/js'))
  });
</pre>

Точно также можно поступить, если необходим контроль ошибок в другой задаче, к примеру конкатенации CSS-файлов:

<pre>// Concat Task
  gulp.task('concat', function(){
    gulp.src('css/*.css')
      .pipe(plumber())
      .pipe(concatCSS('concatenate.css'))
      .pipe(minifyCSS())
      .pipe(gulp.dest('build/css'))
  });
</pre>

### Запуск мониторинга ошибок gulp-plumber

Для удобства проверки работы плагина `gulp-plumber` создам задачу `gulp.watch` и помещу ее в задачу по умолчанию `default`:

<pre>// Watch Task
  gulp.task('watch', function() {
    gulp.watch('js/*.js', ['uglify']);
    gulp.watch('css/*.css', ['concat']);
  });

  // Default Task
  gulp.task('default', ['watch']);
</pre>

Запускаю в консоли процесс мониторинга в Gulp командой:

<pre>$ gulp
</pre>

&#8230; и смотрю на вывод в консоли:<figure id="attachment_1647" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-1647" src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp_watch-600x304.png" alt="Gulp в фоновом режиме" width="600" height="304" />][3]<figcaption class="wp-caption-text">Gulp в фоновом режиме</figcaption></figure> 

Теперь намеренно вношу ошибку в файл `jquery-1.11.1.js` и снова перевожу взгзляд на консоль:<figure id="attachment_1648" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-1648" src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp_plumber-error-600x304.png" alt="Плагин gulp-plumber отследил ошибку" width="600" height="304" />][4]<figcaption class="wp-caption-text">Плагин gulp-plumber отследил ошибку</figcaption></figure> 

Отлично! Плагин `gulp-plumber` выполнил свою задачу &#8211; сформировал ясный и четкий отчет об ошибке. И при этом не прервал работу самого Gulp.

Возвратим все назад и исправим ошибку, допущенную ранее. Снова взглянем на консоль:<figure id="attachment_1650" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-1650" src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp_plumber-success-600x304.png" alt="Плагин gulp-plumber - ошибка исправлена" width="600" height="304" />][5]<figcaption class="wp-caption-text">Плагин gulp-plumber &#8211; ошибка исправлена</figcaption></figure> 

Плагин `gulp-plumber` снова справился со своей задачей &#8211; ошибка нами исправлена и он прилежно ее зафиксировал.

Оцените статью:  
<span id="post-ratings-1643" class="post-ratings" data-nonce="8e542c4533"><img id="rating_1643_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1643, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1643_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1643, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1643_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1643, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1643_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1643, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1643_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1643, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1643_text"></span></span><span id="post-ratings-1643-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp_error.png
 [2]: https://www.npmjs.org/package/gulp-plumber "gulp-plumber"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp_watch.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp_plumber-error.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp_plumber-success.png