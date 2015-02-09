---
title: 'Gulp &#8211; именованная задача (named task)'
author: gearmobile
excerpt: Создание именованной задачи (named task) в Gulp на примере установки и настройки плагина gulp-concat для конкатенации файлов. Вызов задачи из другой задачи.
layout: post
permalink: /gulp-named-task/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 14
ratings_average:
  - 4.67
categories:
  - 'Javascript &amp; jQuery'
tags:
  - gulp
  - named task
---
В предыдущей статье [Gulp &#8211; установка и запуск плагина gulp-uglify][1], где мы учились устанавливать и запускать плагины под Gulp, мы создавали задачу под этот плагин. Сами не зная того, тогда мы создали **именованную задачу** (named task). Как вы помните из вводной статьи [Gulp &#8211; знакомство и первый запуск][2], в этом менеджере имеется два типа задач &#8211; **задача по умолчанию** (default) и **именованная задача** (named task).

В этом разделе мы углубимся в вопрос задач в Gulp и рассмотрим детально, каким образом создается именованная задача (named task) или несколько именованных задач (named tasks), как можно объединять именованные задачи (named tasks) в последовательности, как можно вызывать выполнение одной задачи из другой задачи.

### Создание named task в Gulp

В менеджере Gulp может существовать тысячи задач, каждая из которых нацелена на получение конкретного результата. Давайте создадим отдельную задачу для конкатенации файлов. Для этой цели существует плагин `gulp-concat`. На странице документации этого плагина описан процесс установки и настройки &#8211; [gulp-concat][3].

Установим плагин `gulp-concat` в проект:

<pre>$ sudo npm install --save-dev gulp-concat
</pre>

И создадим в файле `gulpfile.js` отдельную задачу для этого плагина:

<pre>// Concat Task
  gulp.task('concat', function() {
    gulp.src('css/*.css')
    .pipe(concat('one.css'))
    .pipe(gulp.dest('build/css'))
  })
</pre>

&#8230; а также создадим отдельную переменную для этого плагина:

<pre>var concat = require('gulp-concat');
</pre>

Кстати, если вы еще не задались вопросом, а что это за странные строки &#8211; `gulp.src`, `gulp.dest`, `gulp.task`, то могу вкратце сказать, что это встроенные функции Gulp, каждая из которых выполняет свою задачу.

Осталось запустить в консоли именованную задачу (named task) `concat`, которая произведет слияние в один файл всех файлов с расширением .css, расположенных в директории css:

<pre>$ gulp concat
  [09:53:28] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [09:53:28] Starting 'concat'...
  [09:53:28] Finished 'concat' after 9.91 ms
</pre>

Отлично &#8211; мы создали named task!

### Создание последовательности named tasks в Gulp

В Gulp можно создавать **последовательность задач**, в которой выполнение всех задач будет производиться в том порядке, в котором они помещены в очередь. Для этого несколько отдельных именованных задач (named tasks) помещают внутрь задачи по умолчанию (default). Вместо callback-функции разместим массив, состоящий из списка имен тех именованных задач (named tasks), которые мы хотим поместить в очередь. Фактически, в данном случае выполнение одной задачи будет производиться через вызов другой задачи.

Допустим, у нас имеются две именованные задачи (named tasks):

<pre>// Uglify Task
  gulp.task('uglify', function(){
    gulp.src('js/*.js')
    .pipe(uglify())
    .pipe(gulp.dest('build/js'))
  });

  // Concat Task
  gulp.task('concat', function() {
    gulp.src('css/*.css')
    .pipe(concat('one.css'))
    .pipe(gulp.dest('build/css'))
  });
</pre>

Поместим их в задачу по умолчанию:

<pre>// Default Task
  gulp.task('default', ['concat', 'uglify']);
</pre>

Теперь в консоли достаточно запустить одну команду `gulp` на выполнение задачи по умолчанию (default). Тем самым мы запустим выполнение последовательности нескольких отдельных команд &#8211; `'concat', 'uglify'`:

<pre>$ gulp
  [10:05:36] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [10:05:36] Starting 'concat'...
  [10:05:36] Finished 'concat' after 7.17 ms
  [10:05:36] Starting 'uglify'...
  [10:05:36] Finished 'uglify' after 2.64 ms
  [10:05:36] Starting 'default'...
  [10:05:36] Finished 'default' after 7.04 μs
</pre>

В выводе консоли видим, что сначала запустилась задача `concat` и выполнилась за 7.17 миллисекунд, затем запустилась задача `uglify` и на ее выполнение ушло 2.64 милисекунды. И затем запустилась задача по умолчанию `default`, которая выполнилась за 7.04 миллисекунд. Все прошло успешно.

Оцените статью:  
<span id="post-ratings-1622" class="post-ratings" data-nonce="eda72eba77"><img id="rating_1622_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1622, 1, '1 Star');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1622_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1622, 2, '2 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1622_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1622, 3, '3 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1622_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1622, 4, '4 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1622_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1622, 5, '5 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>4,67</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1622_text"></span></span><span id="post-ratings-1622-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1603 "Gulp - установка и запуск плагина gulp-uglify"
 [2]: http://localhost:7788/third/?p=1588 "Gulp - знакомство и первый запуск"
 [3]: https://www.npmjs.org/package/gulp-concat "gulp-concat"