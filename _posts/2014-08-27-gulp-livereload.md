---
title: "Gulp - плагин gulp-livereload"
layout: post
categories: gulp
tags: [gulp, gulp-livereload]
share: true
---

> Сегодня рассмотрим еще один очень нужный и полезный плагин для web-разработчика. Это плагин `gulp-livereload` под Gulp, который должен иметь каждый веб-разработчик в своей копилке.

Суть плагина `gulp-livereload` в автоматизации обновления страниц в окне браузера. Это тоже самое, что и связка - плагин LiveReload под Sublime Text + плагин LiveReload под браузер. Но в данном случае получается связка - плагин `gulp-livereload` + плагин LiveReload под браузер.

Сказать честно, предыдущий опыт настройки LiveReload, описанный в этой статье - "Установка LiveReload в Sublime Text 2" меня полностью не удовлетворял и я им не пользовался. Причина заключалась в том, что иногда эта связка работала, а иногда - почему-то нет. Нестальность работы плагина под Sublime Text (у меня) отбивала всякое желание иметь с ним дело.

А вот связка плагин `gulp-livereload` + плагин LiveReload под браузер работает стабильно. Кроме того, если Node.js + Gulp уже настроен для текущего проекта, то не возникает никакой проблемы в установке дополнительного плагина `gulp-livereload`.

## Установка плагина gulp-livereload

Плагин `gulp-livereload` проживает по указанному адресу - [gulp-livereload][1]. Установка в проект производиться командой:

{% highlight powershell %}
$ npm install --save-dev gulp-livereload
{% endhighlight %}

В виде зависимостей проекта запись в файле `package.json` должна выглядеть (*как минимум*) так:

{% highlight json %}
{
 "name": "test",
 "version": "0.0.1",
 "devDependencies": {
  "gulp": "~3.8.7",
  "gulp-livereload": "~2.1.1"
 }
}
{% endhighlight %}

Добавляем переменную `livereload` в файл `gulpfile.js` для инициализации плагина `gulp-livereload` и дальнейшей работы с ним:

{% highlight javascript %}
var gulp = require('gulp'),
    livereload = require('gulp-livereload');
{% endhighlight %}

## Установка плагина LiveReload под браузер

Следующим шагом будет установка расширения LiveReload под браузер. В моем случае это будет Mozilla Firefox, однако расширение LiveReload существует и под два других популярных браузера - Google Chrome и Safari.

Для установки расширения под Firefox не стоит искать его на странице расширений Mozilla - [LiveReload 0.6.4][2]. Там находится устаревшая версия плагина, которая наверняка не подойдет для вашего браузера.

Лучше посетим домашнюю страницу проекта LiveReload с описанием установки расширений под каждый из браузеров - [How do I install and use the browser extensions][3]. Скачиваем по указанной на странице ссылке расширение под нужный браузер (Firefox) и автоматически устанавливаем его.

На панели инструментов браузера появиться значок плагина LiveReload в виде круга из двух стрелок. Однократное нажатие на значок запускает плагин - он принимает вид, похожий на компас со стрелкой. Еще одно нажатие выключает плагин LiveReload.

## Создание задачи под gulp-livereload

В принципе, плагин `gulp-livereload` не требует для себя создания отдельной задачи. Все, что нужно для него - это запуск его как локального сервера. Если вы скажете, что не устанавливали сервер LiveReload, то могу успокоить вас - устанавливали! Инсталляция плагина `gulp-livereload` подразумевает автоматическую установку сервера LiveReload.

Поэтому нам нужно всего лишь предварительно активировать, запустить его. Кстати, если у вас вдруг при попытке включения плагина LiveReload в браузере появляется окно с такой ошибкой:

![Ошибка запуска сервера LiveReload]({{site.url}}/images/uploads/2014/08/gulp-livereload_error_start_server.png)

... то это говорит всего лишь о том, что перед этим не был запушен в консоли сам сервер LiveReload. Для этого я создам задачу `watch`, внутрь которой помещу вызов функции `livereload()`:

{% highlight javascript %}
// Watch Task
 gulp.task('watch', function(){
  livereload.listen();
  gulp.watch('sass/*.scss', ['sass']).on('change', livereload.changed);
});
{% endhighlight %}

Все - мне больше ничего не нужно дописывать для задачи компилирования из Sass в CSS (эта задача приведена здесь в качестве примера использования плагина `gulp-livereload`):

{% highlight javascript %}
// Sass Complie Task
 gulp.task('sass', function(){
 gulp.src('sass/*.scss')
  .pipe(sassSCSS())
  .pipe(gulp.dest('build/css'));
});
{% endhighlight %}

Полностью листинг файла `gulpfile.js` в данном случае будет выглядеть таким образом:

{% highlight javascript %}
var gulp = require('gulp'),
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
{% endhighlight %}

Все готово для тестирования работы плагина `gulp-livereload`.

## Тестирование плагина gulp-livereload

Осталось выполнить две маленькие вещи. Первая - включаю плагин LiveReload в браузере. Вторая - запускаю Gulp для мониторинга изменений и работы плагина `gulp-livereload`:

{% highlight powershell %}
$ gulp
Using gulpfile ~/Projects/gulp_test/gulpfile.js
Starting 'sass'...
Finished 'sass' after 11 ms
Starting 'watch'...
Finished 'watch' after 17 ms
Starting 'default'...
Finished 'default' after 19 μs
Live reload server listening on: 35729
{% endhighlight %}

Видим, как последняя строка в консоли говорит нам, что сервер LiveReload запустился и прослушивает порт по умолчанию - 35729. Вношу изменения в файл стилей `style.scss`:

{% highlight css %}
figure{
  border: 1px solid #000;
  padding: 5px;
 }
{% endhighlight %}

... и смотрю на вывод в консоли:

{% highlight powershell %}
$ gulp
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
{% endhighlight %}

Изменение было отслежено, файл перекомпилирован задачей `sass`. А что же плагин `gulp-livereload` - он тоже подхватил изменения?

Смотрим:

![Изменения в gulp-livereload]({{site.url}}/images/uploads/2014/08/gulp-livereload_01.png)

О, да! Изменение было подхвачено плагином `gulp-livereload` - "картинка" в окне браузера изменилась без перезагрузки последнего.

Еще раз проверим и внесем какое-нибудь изменение в файле стилей:

{% highlight powershell %}
$ gulp
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
{% endhighlight %}

![Изменения в gulp-livereload]({{site.url}}/images/uploads/2014/08/gulp-livereload_02.png)

Отлично! Вот мы и изучили еще одну полезную сторону работы с Gulp - использование плагина `gulp-livereload`.

---

[1]: https://www.npmjs.org/package/gulp-livereload "Gulp-livereload"
[2]: https://addons.mozilla.org/en-US/firefox/addon/livereload/ "LiveReload"
[3]: http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions- "How do I install and use the browser extensions?"
