---
title: "Gulp-imagemin - оптимизация изображений в Gulp"
layout: post
categories: gulp
tags: [gulp, gulp-imagemin]
share: true
---

> Крайне необходимая задача, возникающая в работе каждого верстальщика - это оптимизация графики, нарезанной из psd-макета или используемой в HTML-шаблоне.

Для этой цели существует много разных инструментов, начиная с RIOT и заканчивая утилитами Linux. Но гораздо более удобной возможностью является автоматизация процесса сжатия картинок с помощью плагина под Gulp.

Таким плагином является [gulp-imagemin][1]. Он умеет сжимать картинки форматов PNG, JPEG, GIF и SVG. Все остальные (не поддерживаемые) форматы графических файлов просто игнорируются плагином `gulp-imagemin`.

## Установка gulp-imagemin

Установка плагина `gulp-imagemin` стандартная и производиться командой `npm install` с ключом `--save-dev` для внесения пакета в список зависимостей проекта:

{% highlight powershell %}
$ sudo npm install --save-dev gulp-imagemin
{% endhighlight %}

## Создание задачи под gulp-imagemin

После установки плагина `gulp-imagemin` необходимо создать задачу сжатия картинок под этот плагин. Ничего необычного в этом нет и задача создается стандартно. Сначала создаем переменную `imagemin`, в которую помещаем сам плагин `gulp-imagemin`:

{% highlight javascript %}
var imagemin = require('gulp-imagemin');
{% endhighlight %}

А затем создаем задачу с произвольным именем `compress`:

{% highlight javascript %}
// Compress Task

gulp.task('compress', function() {
  gulp.src('images/*')
  .pipe(imagemin())
  .pipe(gulp.dest('build/images'))
});
{% endhighlight %}

Задачу `compress` можно запускать однократно вручную или автоматически, доверив это дело Gulp и поместив ее внутрь встроенной функции `gulp.watch`.

Создаю в проекте `gulp_test` директорию `images` и размещаю в ней несколько изображений формата `.jpg`, но достаточно большого размера:

{% highlight powershell %}
$ ls images/
black (22).jpg  black (23).jpg  black (28).jpg  black (31).jpg  black (36).jpg  black (41).jpg
{% endhighlight %}

Цель - проверить, действительно ли происходит сжатие графических файлов. Давайте опробуем работу плагина `gulp-imagemin` однократно, запустив в консоли команду `gulp compress`:

{% highlight powershell %}
$ gulp compress
Using gulpfile ~/Projects/gulp_test/gulpfile.js
Starting 'compress'...
Finished 'compress' after 8.56 ms
gulp-imagemin: Minified 6 images (saved 83.02 kB - 7.2%)
{% endhighlight %}

Отлично! Задача `compress` запустилась и выполнилась за 8.56 миллисекунд. При этом было обработано 6 изображений, над которыми была произведена операция сжатия. Экономия размера в результате компресии составила `7.2%`.

Давайте посмотрим на изображения в оригинале, расположенные в директории `images`:

![Оригинальные изображения в проекте]({{site.url}}/images/uploads/2014/08/gulp_origin_images.png)

... запомним примерные размеры каждого из файлов. А затем взглянем на содержимое директории `build/images/`, в которой располагаются сжатые плагином `gulp-imagemin` изображения:

![Обработанные плагином gulp-imagemin изображения]({{site.url}}/images/uploads/2014/08/gulp-imagemin_pictures.png)

Видно при сравнении, что размер графических файлов, пускай и ненамного, но уменьшился.

## Gulp-imagemin - автоматический мониторинг

Давайте доведем нашу задачу до логического завершения и настроим Gulp таким образом, чтобы он автоматически отслеживал добавление в директории `images` новых изображений.

И как только они появляются там, то немедлено производил бы их сжатие при помощи плагина `gulp-imagemin`.

Для этого создам задачу мониторинга `watch`:

{% highlight javascript %}
// Watch Task

gulp.task('watch', function() {
  gulp.watch('images/*', ['compress']);
});
{% endhighlight %}

... которую добавлю в очередь на выполнение для дефолтной задачи `default`:

{% highlight javascript %}
// Default Task

gulp.task('default', ['watch']);
{% endhighlight %}

Полностью листниг файла `gulpfile.js` для данного случая выглядит следующим образом:

{% highlight javascript %}
var gulp = require('gulp'),
    imagemin = require('gulp-imagemin');

// Default Task
gulp.task('default', ['watch']);

// Watch Task
gulp.task('watch', function() {
  gulp.watch('images/*', ['compress']);
});

// Compress Task
gulp.task('compress', function() {
  gulp.src('images/*')
  .pipe(imagemin())
  .pipe(gulp.dest('build/images'));
});
{% endhighlight %}

Запускаю в консоли команду `gulp`, а затем по одному добавлю в директорию `images` два файла-скриншота, созданных мною для этой статьи.

Видим, что каждый раз, как в директорию `images` был добавлен файл, Gulp запускал задачу `compress` на выполнение:

{% highlight javascript %}
$ gulp
  Using gulpfile ~/Projects/gulp_test/gulpfile.js
  Starting 'watch'...
  Finished 'watch' after 8.42 ms
  Starting 'default'...
  Finished 'default' after 12 μs
  Starting 'compress'...
  Finished 'compress' after 13 ms
  gulp-imagemin: Minified 7 images (saved 93.43 kB - 7.7%)
  Starting 'compress'...
  Finished 'compress' after 2.13 ms
  gulp-imagemin: Minified 8 images (saved 103.77 kB - 8%)
{% endhighlight %}

На выполнение первой задачи ушло 7 миллисекунд:

{% highlight javascript %}
gulp-imagemin: Minified 7 images (saved 93.43 kB - 7.7%)
{% endhighlight %}

... на вторую задачу - 2.13 миллисекунд:

{% highlight javascript %}
gulp-imagemin: Minified 8 images (saved 103.77 kB - 8%)
{% endhighlight %}

При этом я "выиграл" `7.7%` и `8%` размера, что скажется на скорости загрузки страницы в браузере. Также обратите внимание, что Gulp продолжает работать, находясь в фоновом режиме.

## Усложним задачу для gulp-imagemin

Можно немного усложнить и усовершенствовать процесс оптимизации изображений. Для этого немного перепишу задачу `compress` таким образом:

{% highlight javascript %}
// Compress Task
  gulp.task('compress', function() {
    gulp.src('images/*')
    .pipe(imagemin({
      progressive: true
    }))
    .pipe(gulp.dest('images/'));
  });
{% endhighlight %}

Первое изменение - это добавлена опция `progressive: true` к плагину `gulp-imagemin`. Эта опция управляет *методом сжатия графических файлов* и приведена мною для наглядности примера.

Второе изменение - изменена директория назначения. Теперь директория-источник изображений `gulp.src('images/*')` и директория-"выхлоп" `gulp.dest('images/')`, куда помещаются обработанные изображения - одна и та же.

Таким образом, достаточно положить в директорию `images` какое-либо изображение и оно тут же преобразуется в точно такое же изображение, но меньшего размера! Удобно, не правда ли?

На этом все.

---

[1]: https://www.npmjs.org/package/gulp-imagemin "Gulp-imagemin"
