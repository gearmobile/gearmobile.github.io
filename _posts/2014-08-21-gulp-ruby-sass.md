---
title: "Gulp - плагин gulp-ruby-sass"
layout: post
categories: gulp
tags: [gulp, gulp-ruby-sass]
share: true
---

> Рассмотрим очень нужный и полезный плагин `gulp-ruby-sass` под Gulp для компиляции файлов Sass в файлы формата CSS. Для разработчиков, которые пользуются препроцессором Sass данный плагин `gulp-ruby-sass` просто необходим.

Для компиляции Sass в CSS под Gulp имеется несколько плагинов. Например, `gulp-sass` или `gulp-ruby-sass`. Более стабильным плагином является `gulp-ruby-sass`. Вот его мы и установим.

## Установка плагина gulp-ruby-sass

Команда установки уже стандартная для нас:

{% highlight powershell %}
$ sudo npm install --save-dev gulp-ruby-sass
{% endhighlight %}

В директории `sass` заранее помещены мною два scss-файла `main.scss` и `style.scss`:

{% highlight powershell %}
$ ls sass/
main.scss  style.scss
{% endhighlight %}

После этого создаю именованную задачу `sass` для плагина `gulp-ruby-sass`:

{% highlight javascript %}
// Sass Compile Task
gulp.task('sass', function() {
  gulp.src('sass/**/*.scss')
  .pipe(sass())
  .pipe(gulp.dest('build/css'))
});
{% endhighlight %}

И запускаем задачу `sass`:

{% highlight powershell %}
$ gulp sass
  [14:31:48] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [14:31:48] Starting 'sass'...
  [14:31:48] Finished 'sass' after 12 ms
  [14:31:49] gulp-ruby-sass: directory
  [14:31:49] gulp-ruby-sass: write main.css
  [14:31:49] gulp-ruby-sass: write style.css
{% endhighlight %}

Оба файла скомпилированы `main.scss` и `style.scss` и помещены по пути `build/css`:

{% highlight powershell %}
$ ls build/css/
  main.css  one.css  style.css
{% endhighlight %}

Взглянем на содержимое хотя бы одного из них (пускай это будет `main.css`), чтобы убедиться в том, что это уже CSS-файл, а не SCSS-файл:

![Компиляция Sass в CSS с помощью gulp-ruby-sass]({{site.url}}/images/uploads/2014/08/gulp-ruby-sass_plugin.png)

Да, действительно, перед нами CSS-файл!

## Добавление опций к плагину gulp-ruby-sass

До этого момента все плагины, которые мы устанавливали и настраивали в виде задач, были без опций. То есть, в потоке мы просто вызывали плагин через переменную и передавали ему данные для обработки. На этом работа плагина заканчивалась.

Однако внимательный читатель мог уже при первом знакостве с плагинами заметить, что в руководстве почти к каждому из них, помимо описания установки, есть раздел, посвященный опциям данного плагина. Другими словами, плагин может не просто обрабатывать данные, а обрабатывать так, как нам это нужно.

Что касается плагина `gulp-ruby-sass`, то данный плагин может производить компиляцию из Sass в CSS **несколькими способами**. Достаточно почитать раздел **API** к документации к нему - [gulp-ruby-sass][1].

Мы же воспользуемся всего одной опцией из этого списка и сделаем так, чтобы результат компиляции был **более сжатым**. Для этого немного изменим созданную ранее задачу `sass` и добавим опцию `style: 'compressed'` к переменной `sass`:

{% highlight javascript %}
// Sass Compile Task
gulp.task('sass', function() {
  gulp.src('sass/**/*.scss')
  .pipe(sass({
    style: 'compressed'
  }))
  .pipe(gulp.dest('build/css'))
});
{% endhighlight %}

Снова запустим задачу `sass` из консоли:

{% highlight powershell %}
$ gulp sass
  [14:52:57] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [14:52:57] Starting 'sass'...
  [14:52:57] Finished 'sass' after 8.68 ms
  [14:52:58] gulp-ruby-sass: directory
  [14:52:58] gulp-ruby-sass: write main.css
  [14:52:58] gulp-ruby-sass: write style.css
{% endhighlight %}

И взглянем на результат компиляции файла `main.scss` в файл `main.css`:

![Компиляция gulp-ruby-sass с опцией compressed]({{site.url}}/images/uploads/2014/08/gulp-ruby-sass_plugin_compressed.png)

Отлично! Видим, что плагин `gulp-ruby-sass` действительно отработал с опцией `compressed` и произвел не просто компиляцию из SCSS в CSS, но и сжатие CSS-файла `main.css` - удалены все лишние пробелы и табуляция, выкинуты лишние точки с запятой, а все CSS-правила размещены в одну строку.

## Объединение нескольких плагинов в одной задаче

До недавнего момента при работе в Gulp мы всегда поступали таким образом - "один плагин - одна задача". Однако, Gulp гораздо гибче и мощнее, чем можно было бы подумать. В частности, в одной задаче можно объединить несколько ранее установленных плагинов именно благодаря поточности Gulp.

Чтобы было более понятно, разберем все вышесказанное на живом примере. Дополним задачу `sass` плагином конкатенации, чтобы "склеить" два результирующих файла `main.css` и `style.css` в один файл `compile.css`. Как вы уже догадались, для этой цели мы воспользуемся уже установленным ранее плагином `gulp-concat`.

Видоизменим задачу `sass`, добавив строку `.pipe(concat('compile.css'))` после строки с вызовом плагина `gulp-ruby-sass`:

{% highlight javascript %}
// Sass Compile Task
  gulp.task('sass', function() {
    gulp.src('sass/**/*.scss')
    .pipe(sass({
      style: 'compressed'
    }))
    .pipe(concat('compile.css'))
    .pipe(gulp.dest('build/css'))
  });
{% endhighlight %}

Вновь запустим в консоли задачу `sass`:

{% highlight powershell %}
$ gulp sass
  [15:14:44] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [15:14:44] Starting 'sass'...
  [15:14:44] Finished 'sass' after 9.05 ms
  [15:14:45] gulp-ruby-sass: directory
  [15:14:45] gulp-ruby-sass: write main.css
  [15:14:45] gulp-ruby-sass: write style.css
{% endhighlight %}

Посмотрим содержимое по пути `build/css`:

{% highlight powershell %}
aaron@zmk ~/Projects/gulp_test $ ls build/css/
  compile.css  one.css
{% endhighlight %}

Файл `compile.css` появился по указанному пути. Взглянем на его содержимое в редакторе Sublime Text:

![Компиляция gulp-ruby-sass и конкатенация Sass в CSS под Gulp]({{site.url}}/images/uploads/2014/08/gulp-ruby-sass_plugin_compressed_concat.png)

Пример получился не совсем удачный, но, тем не менее, наглядный. Видим, чтобы оба плагина отработали. Была произведена компиляция, а затем "склейка" двух файлов в один.

Конечно, благодаря поточности в Gulp, в одну задачу можно добавлять не два плагина, а гораздо больше.

---

[1]: https://www.npmjs.org/package/gulp-ruby-sass "Gulp-Ruby-Sass"
