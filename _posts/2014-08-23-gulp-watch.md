---
title: "Gulp - мониторинг изменений gulp.watch"
layout: post
categories: gulp
tags: [gulp, gulp.watch]
share: true
---

> В Gulp имеется встроенная функция `gulp.watch` для отслеживания изменений в любом из файлов проекта.

Это очень удобно в работе, так как отпадает необходимость вручную запускать определенную задачу каждый раз, когда нужно зафиксировать эти изменения. В предыдущих статьях мы так и делали - запускали вручную на выполнение задачи по умолчанию или же определенную именованную задачу.

![Gulp watch]({{site.url}}/images/uploads/2014/08/gulp.png){:.center-image}

Сейчас давайте рассмотрим возможность запуска автоматического мониторинга в Gulp с помощью встроенной функции `gulp.watch`. Допустим, у нас имеются две именованные задачи, одна из которых выполняет минификацию js-файлов `gulp-uglify`, а вторая - конкатенацию css-файлов `gulp-concat`:

{% highlight javascript %}
// Uglify Task

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
{% endhighlight %}

Нам нужно сделать так, чтобы Gulp запускал их каждый раз самостоятельно, когда мы внесем изменения в любой из js-файлов или css-файлов, а затем сохраним эти изменения.

Для этого создадим еще одну именованную задачу `watch`, цель которой - отслеживание изменений в указанных файлах. Создаем все как обычно (или - почти как обычно):

{% highlight javascript %}
// Watch Task

gulp.task('watch', function(){
  gulp.watch('js/*.js', ['uglify']);
});
{% endhighlight %}

Создаем задачу по имени `watch`, а внутри тела функции поместим встроенную функцию `gulp.watch`. В качестве аргументов этой функции мы передаем ей два параметра.

**Первый параметр** - что и где Gulp должен отслеживать; `js/*.js` говорит о том, что необходимо отслеживать изменения всех файлов с расширением `.js`, помещенных в директории `js`.

**Второй параметр** - что должен делать Gulp, если обнаружит изменения в указанном месте. В данном случае мы говорим ему, что необходимо запустить задачу по имени `uglify`.

Как видим, имя задачи передается функции `gulp.watch` в виде массива; отсюда можно сделать вывод, что задач может быть не одна, а несколько - в виде последовательности.

Перейдем от слов к делу и запустим в консоли выполнение мониторинга с помощью функции `gulp.watch`. Команда для мониторинга в Gulp выглядит таким образом:

{% highlight powershell %}
$ gulp watch
  [10:55:26] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [10:55:26] Starting 'watch'...
  [10:55:26] Finished 'watch' after 7.06 ms
{% endhighlight %}

Видим, что задача по имени `watch` запустилась и вроде как закончилась (`Finished 'watch' after 7.06 ms`). Но на самом деле Gulp находиться в фоновом режиме и отслеживает изменения js-файлов.

Чтобы проверить это, отредактируем и сохраним js-файл (в моем случае это `jquery.js`):

{% highlight javascript %}
$ gulp watch
    [10:55:26] Using gulpfile ~/Projects/gulp_test/gulpfile.js
    [10:55:26] Starting 'watch'...
    [10:55:26] Finished 'watch' after 7.06 ms
    [10:59:17] Starting 'uglify'...
    [10:59:17] Finished 'uglify' after 8.96 ms
{% endhighlight %}

Вау! Видим, что в консоли появились две строчки - это отработала задача `uglify`. То есть, Gulp "увидел", что я внес изменение в файле `jquery.js` и мгновенно запустил задачу `uglify`, чтобы зафиксировать это изменение. Мониторинг с помощью функции `gulp.watch` работает!

Давайте немного усложним задачу и добавим мониторинг `gulp.watch` в директории `css`. При любом изменении файлов в этой папке должна запускаться задача `concat`:

{% highlight javascript %}
// Watch Task
  gulp.task('watch', function() {
    gulp.watch('js/*.js', ['uglify']);
    gulp.watch('css/*.css', ['concat']);
  });
{% endhighlight %}

Снова запустим Gulp для мониторинга изменений в проекте.

> Кстати, а вы знаете, как останавливать Gulp, запущенный в фоновом режиме? Если нет, то это просто - в консоли Linux это выполняется сочетанием клавиш <kbd>Ctrl+C</kbd>.

{% highlight powershell %}
$ gulp watch
    [11:08:55] Using gulpfile ~/Projects/gulp_test/gulpfile.js
    [11:08:55] Starting 'watch'...
    [11:08:55] Finished 'watch' after 8.24 ms
{% endhighlight %}

Внесем и сохраним изменения в файле `normalize.css`, размещенном в директории `css`. Вернемся в консоль:

{% highlight powershell %}
$ gulp watch
    [11:08:55] Using gulpfile ~/Projects/gulp_test/gulpfile.js
    [11:08:55] Starting 'watch'...
    [11:08:55] Finished 'watch' after 8.24 ms
    [11:11:04] Starting 'concat'...
    [11:11:04] Finished 'concat' after 9.12 ms
{% endhighlight %}

О! Видим, что `gulp.watch` "подхватил" изменение в файле `normalize.css` и запустил соответствующую этому изменению задачу `concat`. Отлично - все работает!

Мониторинг `gulp.watch` можно добавить в задачу по умолчанию (`default`). Давайте создадим такую конструкцию:

{% highlight javascript %}
// Default Task

  gulp.task('default', ['concat', 'uglify', 'watch']);
{% endhighlight %}

Теперь, если запустить задачу `default` в консоли, то увидим следующее:

{% highlight powershell %}
$ gulp
    [11:20:44] Using gulpfile ~/Projects/gulp_test/gulpfile.js
    [11:20:44] Starting 'concat'...
    [11:20:44] Finished 'concat' after 7.18 ms
    [11:20:44] Starting 'uglify'...
    [11:20:44] Finished 'uglify' after 2.65 ms
    [11:20:44] Starting 'watch'...
    [11:20:44] Finished 'watch' after 7.96 ms
    [11:20:44] Starting 'default'...
    [11:20:44] Finished 'default' after 7.23 μs
{% endhighlight %}

Задачи запустились и выполнились именно в той последовательности, в какой они прописаны в массиве. Сперва выполнились две задачи на конкатенацию `concat` и минификацию `uglify`, а затем запустилась задача на мониторинг `watch`.

Gulp "повис" в фоновом режиме и отслеживает изменения с помощью функции `gulp.watch` в указанных директориях. Проверим это и внесем легкое изменение в любом из файлов (пусть это будут снова `normalize.css` и `jquery.js`):

{% highlight powershell %}
$ gulp
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
{% endhighlight %}

Функция `gulp.watch` прилежно отследила оба эти изменения и запустила соотвествующие им задачи:

{% highlight powershell %}
...
  [11:26:31] Starting 'concat'...
  [11:26:31] Finished 'concat' after 2.37 ms
  [11:26:46] Starting 'uglify'...
  [11:26:46] Finished 'uglify' after 1.49 ms
{% endhighlight %}

Отлично! Мы изучили вопрос создания задачи мониторинга в Gulp с помощью функции `gulp.watch`!

---
