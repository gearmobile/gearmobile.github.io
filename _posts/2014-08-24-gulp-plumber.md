---
title: "Gulp-plumber - отслеживание ошибок в Gulp"
layout: post
categories: gulp
tags: [gulp, gulp-plumber]
share: true
---

> Кто не знаком с тем, что при написании кода очень часто возникают ошибки или банальные опечатки?

И даже если установлены такие палочки-выручалочки, как Emmet, это не всегда спасает из ситуации. А если представить, что вы пишете большой проект и в нем закралась ошибка, то нелегко будет ее найти в куче кода.

При использовании Gulp, который автоматически отслеживает события и выполняет соотвествующие задачи, ситуация несколько "облегчается" тем, что при возникновении ошибки можно увидеть тот момент, когда она произошла.

Например, Gulp настроен на автоматическое фиксирование изменений через `gulp.watch`. Если возникла ошибка, то выполнение мониторинга в Gulp прерывается:

![Прерванная работа Gulp]({{site.url}}/images/uploads/2014/08/gulp_error.png)

Но даже в этом случае довольно трудно разобраться, где именно закралась ошибка. В этой ситуации может помочь плагин [gulp-plumber][1], который формирует вывод об ошибке. Но при этом работа Gulp не прерывается.

Давайте установим и попробуем в работе плагин `gulp-plumber`.

## Установка плагина gulp-plumber

Установка плагина `gulp-plumber` стандартная, через менеджер пакетов `npm` с ключом `--save-dev`:

{% highlight powershell %}
$ sudo npm install --save-dev gulp-plumber
{% endhighlight %}

## Использование плагина gulp-plumber

Для применения плагина `gulp-plumber` в проекте необходимо создать переменную `plumber`:

{% highlight javascript %}
var plumber = require('gulp-plumber');
{% endhighlight %}

А затем дописать строку `.pipe(plumber())` в ту задачу, в которой необходимо включить возможность отслеживания ошибок. Например, пусть это будет задача минификации всех js-файлов проекта `uglify`. Тогда в ней сразу после строки `gulp.src('js/*.js')` добавляем строку `.pipe(plumber())`, чтобы отслеживались возможные ошибки во всех нижеследующих задачах, таких как `.pipe(uglify())` или `.pipe(gulp.dest('build/js'))`:

{% highlight javascript %}
// Uglify Task
gulp.task('uglify', function(){
  gulp.src('js/*.js')
    .pipe(plumber()) // plumber
    .pipe(uglify())
    .pipe(gulp.dest('build/js'))
});
{% endhighlight %}

Точно также можно поступить, если необходим контроль ошибок в другой задаче, к примеру конкатенации CSS-файлов:

{% highlight javascript %}
// Concat Task
gulp.task('concat', function(){
  gulp.src('css/*.css')
    .pipe(plumber())
    .pipe(concatCSS('concatenate.css'))
    .pipe(minifyCSS())
    .pipe(gulp.dest('build/css'))
});
{% endhighlight %}

## Запуск мониторинга ошибок gulp-plumber

Для удобства проверки работы плагина `gulp-plumber` создам задачу `gulp.watch` и помещу ее в задачу по умолчанию `default`:

{% highlight javascript %}
// Watch Task
gulp.task('watch', function() {
  gulp.watch('js/*.js', ['uglify']);
  gulp.watch('css/*.css', ['concat']);
});

// Default Task
gulp.task('default', ['watch']);
{% endhighlight %}

Запускаю в консоли процесс мониторинга в Gulp командой:

{% highlight powershell %}
$ gulp
{% endhighlight %}

... и смотрю на вывод в консоли:

![Gulp в фоновом режиме]({{site.url}}/images/uploads/2014/08/gulp_watch.png)

Теперь намеренно вношу ошибку в файл `jquery-1.11.1.js` и снова перевожу взгзляд на консоль:

![Плагин gulp-plumber отследил ошибку]({{site.url}}/images/uploads/2014/08/gulp_plumber-error.png)

Отлично! Плагин `gulp-plumber` выполнил свою задачу - сформировал ясный и четкий отчет об ошибке. И при этом не прервал работу самого Gulp.

Возвратим все назад и исправим ошибку, допущенную ранее. Снова взглянем на консоль:

![Плагин gulp-plumber - ошибка исправлена]({{site.url}}/images/uploads/2014/08/gulp_plumber-success.png)

Плагин `gulp-plumber` снова справился со своей задачей - ошибка нами исправлена и он прилежно ее зафиксировал.

---

[1]: https://www.npmjs.org/package/gulp-plumber "Gulp-plumber"
