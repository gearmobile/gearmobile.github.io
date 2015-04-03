---
title: "Gulp - именованная задача (named task)"
layout: post
categories: gulp
tags: [gulp, named task]
share: true
---

> В предыдущей статье "Gulp - установка и запуск плагина gulp-uglify", где мы учились устанавливать и запускать плагины под Gulp, мы создавали задачу под этот плагин.

Сами не зная того, тогда мы создали именованную задачу (named task). Как вы помните из вводной статьи "Gulp - знакомство и первый запуск", в этом менеджере имеется два типа задач - задача по умолчанию (default) и именованная задача (named task).

В этом разделе мы углубимся в вопрос задач в Gulp и рассмотрим детально, каким образом создается именованная задача (named task) или несколько именованных задач (named tasks), как можно объединять именованные задачи (named tasks) в последовательности, как можно вызывать выполнение одной задачи из другой задачи.

## Создание named task в Gulp

В менеджере Gulp может существовать тысячи задач, каждая из которых нацелена на получение конкретного результата. Давайте создадим отдельную задачу для конкатенации файлов. Для этой цели существует плагин `gulp-concat`. На странице документации этого плагина описан процесс установки и настройки - [gulp-concat][1].

Установим плагин `gulp-concat` в проект:

{% highlight powershell %}
$ sudo npm install --save-dev gulp-concat
{% endhighlight %}

И создадим в файле `gulpfile.js` отдельную задачу для этого плагина:

{% highlight javascript %}
// Concat Task
  gulp.task('concat', function() {
    gulp.src('css/*.css')
    .pipe(concat('one.css'))
    .pipe(gulp.dest('build/css'))
  })
{% endhighlight %}

... а также создадим отдельную переменную для этого плагина:

{% highlight javascript %}
var concat = require('gulp-concat');
{% endhighlight %}

Кстати, если вы еще не задались вопросом, а что это за странные строки - `gulp.src`, `gulp.dest`, `gulp.task`, то могу вкратце сказать, что это встроенные функции Gulp, каждая из которых выполняет свою задачу.

Осталось запустить в консоли именованную задачу (named task) `concat`, которая произведет слияние в один файл всех файлов с расширением .css, расположенных в директории css:

{% highlight powershell %}
$ gulp concat
  [09:53:28] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [09:53:28] Starting 'concat'...
  [09:53:28] Finished 'concat' after 9.91 ms
{% endhighlight %}

Отлично - мы создали named task!

## Создание последовательности named tasks в Gulp

В Gulp можно создавать последовательность задач, в которой выполнение всех задач будет производиться в том порядке, в котором они помещены в очередь. Для этого несколько отдельных именованных задач (named tasks) помещают внутрь задачи по умолчанию (default).

Вместо callback-функции разместим массив, состоящий из списка имен тех именованных задач (named tasks), которые мы хотим поместить в очередь. Фактически, в данном случае выполнение одной задачи будет производиться через вызов другой задачи.

Допустим, у нас имеются две именованные задачи (named tasks):

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

Поместим их в задачу по умолчанию:

{% highlight javascript %}
// Default Task
  gulp.task('default', ['concat', 'uglify']);
{% endhighlight %}

Теперь в консоли достаточно запустить одну команду `gulp` на выполнение задачи по умолчанию (default). Тем самым мы запустим выполнение последовательности нескольких отдельных команд - `'concat', 'uglify'`:

{% highlight powershell %}
$ gulp
  [10:05:36] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [10:05:36] Starting 'concat'...
  [10:05:36] Finished 'concat' after 7.17 ms
  [10:05:36] Starting 'uglify'...
  [10:05:36] Finished 'uglify' after 2.64 ms
  [10:05:36] Starting 'default'...
  [10:05:36] Finished 'default' after 7.04 μs
{% endhighlight %}

В выводе консоли видим, что сначала запустилась задача `concat` и выполнилась за 7.17 миллисекунд, затем запустилась задача `uglify` и на ее выполнение ушло 2.64 милисекунды. И затем запустилась задача по умолчанию `default`, которая выполнилась за 7.04 миллисекунд.

Все прошло успешно.

---

[1]: https://www.npmjs.org/package/gulp-concat "Gulp-concat"
