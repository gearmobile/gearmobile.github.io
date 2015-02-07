---
title: 'Gulp &#8211; мониторинг изменений gulp.watch'
author: gearmobile
excerpt: Создание задачи мониторинга в Gulp с помощью встроенной функции gulp.watch. Благодаря gulp.watch отслеживаются изменения и запускаются задачи для обработки.
layout: post
permalink: /gulp-watch/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 16
ratings_average:
  - 4
categories:
  - 'Javascript &amp; jQuery'
tags:
  - gulp
  - gulp watch
---
В Gulp имеется встроенная функция `gulp.watch` для отслеживания изменений в любом из файлов проекта. Это очень удобно в работе, так как отпадает необходимость вручную запускать определенную задачу каждый раз, когда нужно зафиксировать эти изменения. В [предыдущих статьях][1] мы так и делали &#8211; запускали вручную на выполнение задачи по умолчанию или же определенную именованную задачу.

[<img class="aligncenter  wp-image-1597" src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp.png" alt="gulp.watch" width="165" height="369" />][2]

Сейчас давайте рассмотрим возможность запуска **автоматического мониторинга** в Gulp с помощью встроенной функции `gulp.watch`. Допустим, у нас имеются две именованные задачи, одна из которых выполняет минификацию js-файлов (`gulp-uglify`), а вторая &#8211; конкатенацию css-файлов (`gulp-concat`):

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

Нам нужно сделать так, чтобы Gulp запускал их каждый раз самостоятельно, когда мы внесем изменения в любой из js-файлов или css-файлов, а затем сохраним эти изменения.

Для этого создадим еще одну именованную задачу `watch`, цель которой &#8211; отслеживание изменений в указанных файлах. Создаем все как обычно (*или &#8211; почти как обычно*):

<pre>// Watch Task
  gulp.task('watch', function(){
    gulp.watch('js/*.js', ['uglify']);
  });
</pre>

Создаем задачу по имени `watch`, а внутри тела функции поместим встроенную функцию `gulp.watch`. В качестве аргументов этой функции мы передаем ей два параметра.

**Первый параметр** &#8211; **что и где Gulp должен отслеживать**; `js/*.js` говорит о том, что необходимо отслеживать изменения всех файлов с расширением `.js`, помещенных в директории `js`.

**Второй параметр** &#8211; **что должен делать Gulp**, если обнаружит изменения в указанном месте. В данном случае мы говорим ему, что необходимо запустить задачу по имени `uglify`.

Как видим, имя задачи передается функции `gulp.watch` в виде массива; отсюда можно сделать вывод, что задач может быть не одна, а несколько &#8211; в виде последовательности.

Перейдем от слов к делу и запустим в консоли выполнение мониторинга с помощью функции `gulp.watch`. Команда для мониторинга в Gulp выглядит таким образом:

<pre>$ gulp watch
  [10:55:26] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [10:55:26] Starting 'watch'...
  [10:55:26] Finished 'watch' after 7.06 ms
</pre>

Видим, что задача по имени `watch` запустилась и вроде как закончилась (`Finished 'watch' after 7.06 ms`). Но на самом деле Gulp находиться в фоновом режиме и отслеживает изменения js-файлов. Чтобы проверить это, отредактируем и сохраним js-файл (в моем случае это `jquery.js`):

<pre>$ gulp watch
  [10:55:26] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [10:55:26] Starting 'watch'...
  [10:55:26] Finished 'watch' after 7.06 ms
  [10:59:17] Starting 'uglify'...
  [10:59:17] Finished 'uglify' after 8.96 ms
</pre>

Вау! Видим, что в консоли появились две строчки &#8211; это отработала задача `uglify`. То есть, Gulp &#8220;увидел&#8221;, что я внес изменение в файле `jquery.js` и мгновенно запустил задачу `uglify`, чтобы зафиксировать это изменение. Мониторинг с помощью функции `gulp.watch` работает!

Давайте немного усложним задачу и добавим мониторинг `gulp.watch` в директории `css`. При любом изменении файлов в этой папке должна запускаться задача `concat`:

<pre>// Watch Task
  gulp.task('watch', function() {
    gulp.watch('js/*.js', ['uglify']);
    gulp.watch('css/*.css', ['concat']);
  });
</pre>

Снова запустим Gulp для мониторинга изменений в проекте.

> Кстати, а вы знаете, **как останавливать Gulp**, запущенный в фоновом режиме? Если нет, то это просто &#8211; в консоли Linux это выполняется сочетанием клавиш **Ctrl+C**.

<pre>$ gulp watch
  [11:08:55] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [11:08:55] Starting 'watch'...
  [11:08:55] Finished 'watch' after 8.24 ms
</pre>

Внесем и сохраним изменения в файле `normalize.css`, размещенном в директории `css`. Вернемся в консоль:

<pre>$ gulp watch
  [11:08:55] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [11:08:55] Starting 'watch'...
  [11:08:55] Finished 'watch' after 8.24 ms
  [11:11:04] Starting 'concat'...
  [11:11:04] Finished 'concat' after 9.12 ms
</pre>

О! Видим, что `gulp.watch` &#8220;подхватил&#8221; изменение в файле `normalize.css` и запустил соответствующую этому изменению задачу `concat`. Отлично &#8211; все работает!

Мониторинг `gulp.watch` можно добавить в задачу по умолчанию (`default`). Давайте создадим такую конструкцию:

<pre>// Default Task
  gulp.task('default', ['concat', 'uglify', 'watch']);
</pre>

Теперь, если запустить задачу `default` в консоли, то увидим следующее:

<pre>$ gulp
  [11:20:44] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [11:20:44] Starting 'concat'...
  [11:20:44] Finished 'concat' after 7.18 ms
  [11:20:44] Starting 'uglify'...
  [11:20:44] Finished 'uglify' after 2.65 ms
  [11:20:44] Starting 'watch'...
  [11:20:44] Finished 'watch' after 7.96 ms
  [11:20:44] Starting 'default'...
  [11:20:44] Finished 'default' after 7.23 μs
</pre>

Задачи запустились и выполнились именно в той последовательности, в какой они прописаны в массиве. Сперва выполнились две задачи на конкатенацию `concat` и минификацию `uglify`, а затем запустилась задача на мониторинг `watch`.

Gulp &#8220;повис&#8221; в фоновом режиме и отслеживает изменения с помощью функции `gulp.watch` в указанных директориях. Проверим это и внесем легкое изменение в любом из файлов (пусть это будут снова `normalize.css` и `jquery.js`):

<pre>$ gulp
  [11:20:44] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [11:20:44] Starting 'concat'...
  [11:20:44] Finished 'concat' after 7.18 ms
  [11:20:44] Starting 'uglify'...
  [11:20:44] Finished 'uglify' after 2.65 ms
  [11:20:44] Starting 'watch'...
  [11:20:44] Finished 'watch' after 7.96 ms
  [11:20:44] Starting 'default'...
  [11:20:44] Finished 'default' after 7.23 μs
  [11:26:31] Starting 'concat'...
  [11:26:31] Finished 'concat' after 2.37 ms
  [11:26:46] Starting 'uglify'...
  [11:26:46] Finished 'uglify' after 1.49 ms
</pre>

Функция `gulp.watch` прилежно отследила оба эти изменения и запустила соотвествующие им задачи:

<pre>...
  [11:26:31] Starting 'concat'...
  [11:26:31] Finished 'concat' after 2.37 ms
  [11:26:46] Starting 'uglify'...
  [11:26:46] Finished 'uglify' after 1.49 ms
</pre>

Отлично! Мы изучили вопрос создания задачи мониторинга в Gulp с помощью функции `gulp.watch`!

Оцените статью:  
<span id="post-ratings-1626" class="post-ratings" data-nonce="39f22829a3"><img id="rating_1626_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1626, 1, '1 Star');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1626_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1626, 2, '2 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1626_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1626, 3, '3 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1626_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1626, 4, '4 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1626_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1626, 5, '5 Stars');" onmouseout="ratings_off(4, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>4,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1626_text"></span></span><span id="post-ratings-1626-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1622
 [2]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp.png