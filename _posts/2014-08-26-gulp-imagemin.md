---
title: 'Gulp-imagemin &#8211; сжатие картинок в Gulp'
author: gearmobile
layout: post
---
Крайне необходимая задача, возникающая в работе каждого верстальщика &#8211; это сжатие картинок, нарезанных из psd-макета или используемых в HTML-шаблоне. Для этой цели существует много разных инструментов, начиная с RIOT и заканчивая утилитами Linux. Но гораздо более удобной возможностью является автоматизация процесса сжатия картинок с помощью плагина под Gulp. Таким плагином является [gulp-imagemin][1]. Он умеет сжимать картинки форматов PNG, JPEG, GIF и SVG. Все остальные (*не поддерживаемые*) форматы графических файлов просто игнорируются плагином `gulp-imagemin`.

### Установка gulp-imagemin

Установка плагина `gulp-imagemin` стандартная и производиться командой `npm install` с ключом `--save-dev` для внесения пакета в список зависимостей проекта:

<pre>$ sudo npm install --save-dev gulp-imagemin</pre>

### Создание задачи под gulp-imagemin

После установки плагина `gulp-imagemin` необходимо создать задачу сжатия картинок под этот плагин. Ничего необычного в этом нет и задача создается стандартно. Сначала создаем переменную `imagemin`, в которую помещаем сам плагин `gulp-imagemin`:

<pre>var imagemin = require('gulp-imagemin');
</pre>

А затем создаем задачу с произвольным именем `compress`:

<pre>// Compress Task
    gulp.task('compress', function() {
      gulp.src('images/*')
      .pipe(imagemin())
      .pipe(gulp.dest('build/images'))
    });
</pre>

Задачу `compress` можно запускать однократно **вручную** или **автоматически**, доверив это дело Gulp и поместив ее внутрь встроенной функции `gulp.watch`. Создаю в проекте `gulp_test` директорию `images` и размещаю в ней несколько изображений формата `.jpg`, но достаточно большого размера:

<pre>$ ls images/
black (22).jpg  black (23).jpg  black (28).jpg  black (31).jpg  black (36).jpg  black (41).jpg
</pre>

Цель &#8211; проверить, действительно ли происходит сжатие графических файлов. Давайте опробуем работу плагина `gulp-imagemin` однократно, запустив в консоли команду `gulp compress`:

<pre>$ gulp compress
Using gulpfile ~/Projects/gulp_test/gulpfile.js
Starting 'compress'...
Finished 'compress' after 8.56 ms
gulp-imagemin: Minified 6 images (saved 83.02 kB - 7.2%)
</pre>

Отлично! Задача `compress` запустилась и выполнилась за 8.56 миллисекунд. При этом было обработано 6 изображений, над которыми была произведена операция сжатия. Экономия размера в результате компресии составила 7.2%.

Давайте посмотрим на изображения в оригинале, расположенные в директории `images`:<figure id="attachment_1662" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-1662" src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp_origin_images-600x341.png" alt="Оригинальные изображения в проекте" width="600" height="341" />][2]<figcaption class="wp-caption-text">Оригинальные изображения в проекте</figcaption></figure> 

&#8230; запомним примерные размеры каждого из файлов. А затем взглянем на содержимое директории `build/images/`, в которой располагаются сжатые плагином `gulp-imagemin` изображения:<figure id="attachment_1663" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-1663" src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp-imagemin_pictures-600x341.png" alt="Обработанные плагином gulp-imagemin изображения" width="600" height="341" />][3]<figcaption class="wp-caption-text">Обработанные плагином gulp-imagemin изображения</figcaption></figure> 

Видно при сравнении, что размер графических файлов, пускай и ненамного, но уменьшился.

### Gulp-imagemin &#8211; автоматический мониторинг

Давайте доведем нашу задачу до логического завершения и настроим Gulp таким образом, чтобы он автоматически отслеживал добавление в директории `images` новых изображений. И как только они появляются там, то немедлено производил бы их сжатие при помощи плагина `gulp-imagemin`.

Для этого создам задачу мониторинга `watch`:

<pre>// Watch Task
  gulp.task('watch', function() {
    gulp.watch('images/*', ['compress']);
  });
</pre>

&#8230; которую добавлю в очередь на выполнение для дефолтной задачи `default`:

<pre>// Default Task
  gulp.task('default', ['watch']);
</pre>

Полностью листниг файла `gulpfile.js` для данного случая выглядит следующим образом:

<pre>var gulp = require('gulp'),
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
</pre>

Запускаю в консоли команду `gulp`, а затем по одному добавлю в директорию `images` два файла-скриншота, созданных мною для этой статьи. Видим, что каждый раз, как в директорию `images` был добавлен файл, Gulp запускал задачу `compress` на выполнение:

<pre>$ gulp
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
</pre>

На выполнение первой задачи ушло 7 миллисекунд:

<pre>gulp-imagemin: Minified 7 images (saved 93.43 kB - 7.7%)</pre>

&#8230; на вторую задачу &#8211; 2.13 миллисекунд:

<pre>gulp-imagemin: Minified 8 images (saved 103.77 kB - 8%)</pre>

При этом я &#8220;выиграл&#8221; 7.7% и 8% размера, что скажется на скорости загрузки страницы в браузере. Также обратите внимание, что Gulp продолжает работать, **находясь в фоновом режиме**.

### Усложним задачу для gulp-imagemin

Можно немного усложнить и усовершенствовать процесс оптимизации изображений. Для этого немного перепишу задачу `compress` таким образом:

<pre>// Compress Task
  gulp.task('compress', function() {
    gulp.src('images/*')
    .pipe(imagemin({
      progressive: true
    }))
    .pipe(gulp.dest('images/'));
  });
</pre>

Первое изменение &#8211; это добавлена **опция** `progressive: true` к плагину `gulp-imagemin`. Эта опция управляет методом сжатия графических файлов и приведена мною для наглядности примера.

Второе изменение &#8211; изменена **директория назначения**. Теперь директория-источник изображений `gulp.src('images/*')` и директория-&#8220;выхлоп&#8221; `gulp.dest('images/')`, куда помещаются обработанные изображения &#8211; одна и та же. Таким образом, достаточно положить в директорию `images` какое-либо изображение и оно тут же преобразуется в точно такое же изображение, но меньшего размера! Удобно, не правда ли?

 [1]: https://www.npmjs.org/package/gulp-imagemin "gulp-imagemin"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp_origin_images.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp-imagemin_pictures.png