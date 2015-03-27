---
title: 'Gulp &#8211; плагин gulp-livereload'
author: gearmobile
layout: post
---
Сегодня рассмотрим еще один очень нужный и полезный плагин для web-разработчика. Это плагин `gulp-livereload` под Gulp, который должен иметь каждый веб-разработчик в своей копилке. 

Суть плагина `gulp-livereload` в **автоматизации обновления страниц в окне браузера**. Это тоже самое, что и связка &#8211; плагин LiveReload под Sublime Text + плагин LiveReload под браузер. Но в данном случае получается связка &#8211; плагин `gulp-livereload` + плагин LiveReload под браузер.

Сказать честно, предыдущий опыт настройки LiveReload, описанный в этой статье &#8211; [Установка LiveReload в Sublime Text 2][1] меня полностью не удовлетворял и я им не пользовался. Причина заключалась в том, что иногда эта связка работала, а иногда &#8211; почему-то нет. Нестальность работы плагина под Sublime Text (у меня) отбивала всякое желание иметь с ним дело.

А вот связка плагин `gulp-livereload` + плагин LiveReload под браузер **работает стабильно**. Кроме того, если Node.js + Gulp уже настроен для текущего проекта, то не возникает никакой проблемы в установке дополнительного плагина `gulp-livereload`.

### Установка плагина gulp-livereload

Плагин `gulp-livereload` проживает по указанному адресу &#8211; [gulp-livereload][2]. Установка в проект производиться командой:

<pre>$ npm install --save-dev gulp-livereload
</pre>

В виде зависимостей проекта запись в файле `package.json` должна выглядеть (*как минимум*) так:

<pre>{
 "name": "test",
 "version": "0.0.1",
 "devDependencies": {
  "gulp": "~3.8.7",
  "gulp-livereload": "~2.1.1"
 }
}
</pre>

Добавляем переменную `livereload` в файл `gulpfile.js` для инициализации плагина `gulp-livereload` и дальнейшей работы с ним:

<pre>var gulp = require('gulp'),
    livereload = require('gulp-livereload');
</pre>

### Установка плагина LiveReload под браузер

Следующим шагом будет установка расширения LiveReload под браузер. В моем случае это будет Mozilla Firefox, однако расширение LiveReload существует и под два других популярных браузера &#8211; Google Chrome и Safari.

Для установки расширения под Firefox не стоит искать его на странице расширений Mozilla &#8211; [LiveReload 0.6.4][3]. Там находится **устаревшая версия плагина**, которая наверняка не подойдет для вашего браузера.

Лучше посетим домашнюю страницу проекта LiveReload с описанием установки расширений под каждый из браузеров &#8211; [How do I install and use the browser extensions][4]. Скачиваем по указанной на странице ссылке расширение под нужный браузер (Firefox) и автоматически устанавливаем его.

На панели инструментов браузера появиться значок плагина LiveReload в виде круга из двух стрелок. Однократное нажатие на значок запускает плагин &#8211; он принимает вид, похожий на компас со стрелкой. Еще одно нажатие выключает плагин LiveReload.

### Создание задачи под gulp-livereload

В принципе, плагин `gulp-livereload` не требует для себя создания отдельной задачи. Все, что нужно для него &#8211; это запуск его как локального сервера. Если вы скажете, что не устанавливали сервер LiveReload, то могу успокоить вас &#8211; устанавливали! Инсталляция плагина `gulp-livereload` подразумевает автоматическую установку сервера LiveReload.

Поэтому нам нужно всего лишь предварительно активировать, запустить его. Кстати, если у вас вдруг при попытке включения плагина LiveReload в браузере появляется окно с такой ошибкой:<figure id="attachment_1686" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp-livereload_error_start_server-600x402.png" alt="Ошибка запуска сервера LiveReload" width="600" height="402" class="size-medium wp-image-1686" />][5]<figcaption class="wp-caption-text">Ошибка запуска сервера LiveReload</figcaption></figure> 

&#8230; то это говорит всего лишь о том, что перед этим не был запушен в консоли сам сервер LiveReload. Для этого я создам задачу `watch`, внутрь которой помещу вызов функции `livereload()`:

<pre>// Watch Task
 gulp.task('watch', function(){
  livereload.listen();
  gulp.watch('sass/*.scss', ['sass']).on('change', livereload.changed);
});
</pre>

Все &#8211; мне больше ничего не нужно дописывать для задачи компилирования из Sass в CSS (эта задача приведена здесь в качестве примера использования плагина `gulp-livereload`):

<pre>// Sass Complie Task
 gulp.task('sass', function(){
 gulp.src('sass/*.scss')
  .pipe(sassSCSS())
  .pipe(gulp.dest('build/css'));
});
</pre>

Полностью листинг файла `gulpfile.js` в данном случае будет выглядеть таким образом:

<pre>var gulp = require('gulp'),
    sassSCSS = require('gulp-sass'),
    minifyHTML = require('gulp-minify-html'),
    rename = require('gulp-rename'),
    livereload = require('gulp-livereload');

// Default Task
gulp.task('default', ['sass', 'watch']);

// Watch Task
 gulp.task('watch', function(){
  livereload.listen();
  gulp.watch('sass/*.scss', ['sass']).on('change', livereload.changed);
});

// Sass Complie Task
gulp.task('sass', function(){ 
 gulp.src('sass/*.scss')
  .pipe(sassSCSS())
  .pipe(gulp.dest('build/css'));
});
</pre>

Все готово для тестирования работы плагина `gulp-livereload`.

### Тестирование плагина gulp-livereload

Осталось выполнить две маленькие вещи. Первая &#8211; включаю плагин LiveReload в браузере. Вторая &#8211; запускаю Gulp для мониторинга изменений и работы плагина `gulp-livereload`:

<pre>$ gulp
Using gulpfile ~/Projects/gulp_test/gulpfile.js
Starting 'sass'...
Finished 'sass' after 11 ms
Starting 'watch'...
Finished 'watch' after 17 ms
Starting 'default'...
Finished 'default' after 19 μs
Live reload server listening on: 35729
</pre>

Видим, как последняя строка в консоли говорит нам, что сервер LiveReload запустился и прослушивает порт по умолчанию &#8211; 35729. Вношу изменения в файл стилей `style.scss`:

<pre>figure{
  border: 1px solid #000;
  padding: 5px;
 }
</pre>

&#8230; и смотрю на вывод в консоли:

<pre>$ gulp
Using gulpfile ~/Projects/gulp_test/gulpfile.js
Starting 'sass'...
Finished 'sass' after 10 ms
Starting 'watch'...
Finished 'watch' after 15 ms
Starting 'default'...
Finished 'default' after 11 μs
Live reload server listening on: 35729
style.scss was reloaded.
Starting 'sass'...
Finished 'sass' after 3.58 ms
</pre>

Изменение было отслежено, файл перекомпилирован задачей `sass`. А что же плагин `gulp-livereload` &#8211; он тоже подхватил изменения? Смотрим:<figure id="attachment_1687" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp-livereload_01-600x402.png" alt="Изменения в gulp-livereload" width="600" height="402" class="size-medium wp-image-1687" />][6]<figcaption class="wp-caption-text">Изменения в gulp-livereload</figcaption></figure> 

О, да! Изменение было подхвачено плагином `gulp-livereload` &#8211; &#8220;картинка&#8221; в окне браузера изменилась **без перезагрузки** последнего.

Еще раз проверим и внесем какое-нибудь изменение в файле стилей:

<pre>$ gulp
Using gulpfile ~/Projects/gulp_test/gulpfile.js
Starting 'sass'...
Finished 'sass' after 10 ms
Starting 'watch'...
Finished 'watch' after 15 ms
Starting 'default'...
Finished 'default' after 11 μs
Live reload server listening on: 35729
style.scss was reloaded.
Starting 'sass'...
Finished 'sass' after 3.58 ms
style.scss was reloaded.
Starting 'sass'...
Finished 'sass' after 1.97 ms
</pre><figure id="attachment_1688" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp-livereload_02-600x402.png" alt="Изменения в gulp-livereload" width="600" height="402" class="size-medium wp-image-1688" />][7]<figcaption class="wp-caption-text">Изменения в gulp-livereload</figcaption></figure> 

Отлично! Вот мы и изучили еще одну полезную сторону работы с Gulp &#8211; использование плагина `gulp-livereload`.

 [1]: http://localhost:7788/third/?p=431 "Установка LiveReload в Sublime Text 2"
 [2]: https://www.npmjs.org/package/gulp-livereload "gulp-livereload"
 [3]: https://addons.mozilla.org/en-US/firefox/addon/livereload/ "LiveReload"
 [4]: http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions- "How do I install and use the browser extensions?"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp-livereload_error_start_server.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp-livereload_01.png
 [7]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp-livereload_02.png