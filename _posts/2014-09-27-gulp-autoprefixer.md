---
title: "Gulp-autoprefixer, gulp-rename, gulp-notify"
layout: post
categories: gulp
tags: [gulp, gulp-rename, gulp-notify, gulp-autoprefixer]
share: true
---

> В статье рассмотрены три модуля для работы под Gulp - `gulp-rename`, `gulp-notify`, `gulp-autoprefixer`.

Все три модуля слишком маленькие и слишком простые, чтобы их рассматривать в отдельности. Все приведенные в статье примеры являются базовыми и служат задаче показать принцип работы каждого из модулей.

## Подготовка проекта

Подготовим проект, создав его базовую основу. Первым файлом создадим файл `package.json` и наполним его таким содержимым:

{% highlight powershell %}
$ touch package.json
  $ cat package.json
  {
    "name" : "three_modules",
    "version" : "0.0.1"
  }
{% endhighlight %}

Затем установим *локально* Gulp.js и укажем `npm`, чтобы он внес этот пакет в качестве зависимостей в файл `package.json`:

{% highlight powershell %}
$ sudo npm install --save-dev gulp
  $ cat package.json
  {
    "name": "four_modules",
    "version": "0.0.1",
    "devDependencies": {
      "gulp": "~3.8.8"
    }
  }
{% endhighlight %}

Создаем js-файл, в котором будем прописывать задачи для Gulp:

{% highlight powershell %}
$ touch gulpfile.js
  $ cat gulpfile.js
  var gulp = require('gulp');

  // Default Task
  gulp.task('default', function(){
    // body...
  });
{% endhighlight %}

Основа для тестирования отдельных модулей готова.

## Gulp-rename - переименование файлов

Задача модуля `gulp-rename` предназначена для одной маленькой цели - *переименования файлов*. Установим модуль с указанием зависимостей:

{% highlight powershell %}
$ sudo npm install --save-dev gulp-rename
  $ cat package.json
  {
    "name": "four_modules",
    "version": "0.0.1",
    "devDependencies": {
      "gulp": "~3.8.8",
      "gulp-rename": "~1.2.0"
    }
  }
{% endhighlight %}

И создадим задачу в файле `gulpfile.js` для установленного модуля `gulp-rename`:

{% highlight powershell %}
$ cat gulpfile.js
  var gulp = require('gulp'),
      rename = require('gulp-rename');

  // Rename Task
  gulp.task('rename', function(){
    gulp.src('css/style.css')
    .pipe(rename('pretty_styles.css'))
    .pipe(gulp.dest('build/css/'));
  });
{% endhighlight %}

В задаче под именем `rename` для Gulp "говориться" следующее: найти файл `style.css` - `gulp.src('css/style.css')`; переименовать его в имя `pretty_styles` - `.pipe(rename('pretty_styles.css'))`; переименованный файл положить в папку по пути `build/css/` - `.pipe(gulp.dest('build/css/'))`.

Запускаю задачу `rename` в консоли и вижу, что процесс прошел успешно:

{% highlight powershell %}
$ gulp rename
  Using gulpfile /media/aaron/application/develop/training/gulp_connect/gulpfile.js
  Starting 'rename'...
  Finished 'rename' after 11 ms
{% endhighlight %}

Проверяю, "положил" ли Gulp переименованный файл `pretty_styles.css` по пути `build/css/`:

{% highlight powershell %}
$ ls build/css/
  pretty_styles.css
{% endhighlight %}

Да, все верно, файл `pretty_styles.css` находиться там, где он и должен находиться.

Рассмотренный выше пример очень прост. Более сложные и интересные возможности модуля `gulp-rename` показаны на его официальной странице - [gulp-rename][1]. А именно - возможности переименования с помощью *функций* или с помощью *префиксов\суффиксов*.

## Gulp-notify - уведомление о событиях

Установка модуля `gulp-notify` выполняется как обычно:

{% highlight powershell %}
$ sudo npm install --save-dev gulp-notify
  $ cat package.json
  {
    "name": "four_modules",
    "version": "0.0.1",
    "devDependencies": {
      "gulp": "~3.8.8",
      "gulp-rename": "~1.2.0",
      "gulp-notify": "~1.6.0"
    }
  }
{% endhighlight %}

Затем создаю задачу `notify`, которая будет отслеживать все изменения в файле `css/style.css`. Задача информирования об изменениях подразумевает ее использование в *фоновом режиме*.

Поэтому, создаю еще одну задачу для мониторинга - `watch`, которую помещаю в дефолтную задачу `default`. В общем случае файл `gulpgile.js` будет выглядеть следующим образом:

{% highlight javascript %}
var gulp = require('gulp'),
  rename = require('gulp-rename'),
  notify = require('gulp-notify');

  // Default Task
  gulp.task('default', ['watch']);

  // Notify Task
  gulp.task('notify', function(){
    gulp.src('css/style.css')
    .pipe(notify('File style.css was changed!'));
  });

  // Watch Task
  gulp.task('watch', function(){
    gulp.watch('css/style.css', ['notify']);
  });
{% endhighlight %}

В консоли запускаю Gulp с дефолтной задачей `default`:

{% highlight powershell %}
$ gulp
  Using gulpfile /media/aaron/application/develop/training/gulp_connect/gulpfile.js
  Starting 'watch'...
  Finished 'watch' after 8.79 ms
  Starting 'default'...
  Finished 'default' after 7.97 μs
{% endhighlight %}

Теперь вношу в файл `css/style.css` изменения и сохраняю их. На Рабочем столе мгновенно появляется всплывающее окно с уведомлением о внесенных в файл `css/style.css` изменениях. Не знаю, как в других системах, но на Linux Mint 17 Cinnamon это окошко выглядит очень симпатично.

На [странице GitHub][2] автора модуля представлены *более интересные примеры* создания и использования `gulp-notify`.

## Gulp-autoprefixer - браузерные префиксы

Интересный модуль `gulp-autoprefixer` для управления *браузерными префиксами* в проекте. Задача у него - не просто устанавливать префиксы для тех CSS3-свойств, которые нуждаюся в этом на данный момент (*другими словами - для включения их поддержки в браузерах*).

С помощью `gulp-autoprefixer` можно управлять "глубиной" версий браузеров, которые должны поддерживать работу конкретного проекта. Другими словами, можно указать модулю `gulp-autoprefixer`, что необходимо отслеживать поддержку префиксов только в двух последних версиях каждого (*из всех существующих*) браузера - `last 2 versions` (*кстати, это значение по умолчанию для данного модуля*).

Или же учитывать только две последние версии браузера Google Chrome - `last 2 Chrome versions`. При задании префиксов можно учитывать глобальную статистику использования браузера - `> 5%` (если брузер используют больше 5% населения Интернет).

Модуль `gulp-autoprefixer` использует собственные имена для браузеров при задании параматров работы своей работы. С полным списком еще более интересных возможностей для задания выборки браузеров можно (*и нужно*) ознакомиться на [странице GitHub][3].

Работа модуля `gulp-autoprefixer` основана на известном ресурсе [Can I Use][4]. Именно оттуда он берет инормацию о поддержке браузерами того или иного CSS3-свойства на данный момент. Кстати, известный фреймворк Compass также основывается на [Can I Use][4] при работе со своими миксинами (mixin).

![Сервис Can I Use]({{site.url}}/images/uploads/2014/09/gulp-autoprefixer_caniuse.png)

Помимо этого, модуль `gulp-autoprefixer` умеет красиво форматировать CSS-свойства с браузерными префиксами в виде [визульного каскада][5]:

{% highlight css %}
a {
-webkit-box-sizing: border-box;
   -moz-box-sizing: border-box;
        box-sizing: border-box;
}
{% endhighlight %}

За такую возможность отвечает параметр `cascade`, который включен по умолчанию в данном модуле. Вообще, по умолчанию модуль `gulp-autoprefixer` имеет такие параметры в виде массива (array): `> 1%, last 2 versions, Firefox ESR, Opera 12.1`.

Вступление было достаточно долгим и подробным - это потому, что модуль `gulp-autoprefixer` интересный и нужный. Приступаю к его установке:

{% highlight powershell %}
$ sudo npm install --save-dev gulp-autoprefixer
  $ cat package.json
  {
    "name": "four_modules",
    "version": "0.0.1",
    "devDependencies": {
      "gulp": "~3.8.8",
      "gulp-rename": "~1.2.0",
      "gulp-notify": "~1.6.0",
      "gulp-autoprefixer": "~1.0.0"
    }
  }
{% endhighlight %}

Создаю задачу `autoprefixer` с описанием того, что нужно отслеживать изменения в файле `css/style.css` и при добавлении в него CSS3-свойств преобразовывать их в свойства с браузерными префиксами. При этом учитывать только две последние версии браузеров и результат помещать по пути `build/css/`.

{% highlight javascript %}
var gulp = require('gulp'),
  autoprefixer = require('gulp-autoprefixer');

  // Autoprefixer Task
  gulp.task('autoprefixer', function(){
    gulp.src('css/style.css')
    .pipe(autoprefixer({
      browsers: ['last 2 versions']
    }))
    .pipe(gulp.dest('build/css/'));
  });
{% endhighlight %}

Внесу в файл `css/style.css` CSS3-свойство `transform`, которое заведомо нужно использовать с префиксами (для этого я заранее "[подглядел][6]" его на "Can I Use"):

{% highlight css %}
.block {
  width: 100px;
  height: 100px;
  background-color: #778899;
  transform: rotate(7deg);
  }
{% endhighlight %}

Запускаю задачу `autoprefixer` и смотрю результат:

{% highlight css %}
.block {
  width: 100px;
  height: 100px;
  background-color: #778899;
  -webkit-transform: rotate(7deg);
          transform: rotate(7deg);
  }
{% endhighlight %}

Все четко - под условие "не ниже второй версии" попали только браузеры на движке Webkit - можно свериться [здесь][6].

Можно немного "углубить" условие и "опуститься" до третьей версии всех браузеров:

{% highlight javascript %}
// Autoprefixer Task
  gulp.task('autoprefixer', function(){
    gulp.src('css/style.css')
    .pipe(autoprefixer({
      browsers: ['last 3 versions']
    }))
    .pipe(gulp.dest('build/css/'));
  });
{% endhighlight %}

... и посмотреть результат:

{% highlight css %}
.block {
  width: 100px;
  height: 100px;
  background-color: #778899;
  -webkit-transform: rotate(7deg);
      -ms-transform: rotate(7deg);
          transform: rotate(7deg);
  }
{% endhighlight %}

Вывод в `build/css/style.css` красивый благодаря `cascade`, который можно и отключить, установив `cascade: false`.

---

[1]: https://www.npmjs.org/package/gulp-rename "gulp-rename"
[2]: https://github.com/mikaelbr/gulp-notify/blob/master/examples/gulpfile.js "gulp-notify"
[3]: https://github.com/postcss/autoprefixer#browsers "gulp-autoprefixer - Browsers"
[4]: http://caniuse.com/ "Can I Use"
[5]: https://github.com/postcss/autoprefixer#visual-cascade "Visual Cascade"
[6]: http://caniuse.com/#feat=transforms2d "CSS3 Transforms"
