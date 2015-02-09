---
title: 'Nib &#8211; библиотека миксинов под Stylus'
author: gearmobile
excerpt: Знакомство с библиотекой миксинов Nib под препроцессор Stylus. Установка Nib с помощью npm, подключение директивой @import. Применение миксинов в проекте.
layout: post
permalink: /nib-stylus/
ratings_users:
  - 3
ratings_score:
  - 13
ratings_average:
  - 4.33
categories:
  - Статьи по CSS
tags:
  - nib
  - stylus
---
> Легкое знакомство с библиотекой Nib под препроцессор Stylus. Эта библиотека является тем же самым, что Compass или Bourbon под препроцессор Sass.

Библиотека миксинов Nib написана под препроцессор Stylus и является аналогом более известных библиотек Compass или Bourbon под препроцессор Sass. С самим препроцессором Stylus я с вами познакомился немного раньше &#8211; скажем так, это было краткое и легкое знакомство.

Библиотека Nib проживает по адресу &#8211; [Nib GitHub][1]. Она маленькая и легкая, но должна быть полезной. Поэтому мне необходимо с ней познакомиться поближе.

### Установка библиотеки Nib

В Сети мною было найдено два способа установки данной библиотеки:

  * с использованием GitHub
  * с использованием менеджера пакетов npm

Второй способ мне кажется более удобным, так как в этом случае библиотека устанавливается **глобально** и доступна для любого проекта из любого места файловой системы. В первом же случае придется устанавливать библиотеку каждый раз &#8211; **локально** в каждый отдельный проект.

Если вдруг в системе еще не установлен препроцессор Stylus, то первоначально необходимо установить его командой:

<pre>// Command Line

    $ sudo npm install stylus --global
  </pre>

Не забудьте добавить ключ `--global`, чтобы препроцессор **установился глобально** в системе.

**Установка библиотеки Nib** почти ничем не отличается от установки препроцессора и выполняется командой:

<pre>// Command Line

    $ sudo npm install nib --global
  </pre>

Отлично! Все, что теперь осталось сделать &#8211; это **подключить библиотеку** в текущий проект (текущий рабочий Stylus-файл).

Это выполняется директивой `@import`:

<pre>// Stylus

    @import 'nib'
  </pre>

Проверим, что библиотека подключена без ошибок и отрабатывает в проекте\файле. Для этого запишем в файле `style.styl` несколько миксинов этой библиотеки и &#8220;натравим&#8221; на файл `style.styl` утилиту `stylus` с несколькими ключами:

<pre>// Command Line

    $ stylus -u nib -w style.styl
  </pre>

здесь:

  * `-u nib` &#8211; говорит о том, что при компиляции в CSS должно учитываться наличие библиотеки Nib
  * `-w style.styl` &#8211; мониторить изменения в файле `style.styl` и своевременно выполнять его компиляцию в CSS

Посмотрим на результат компиляции Stylus в CSS &#8211; очень уж любопытно, получилось ли?<figure id="attachment_2163" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/12/nib-600x440.png" alt="nib" width="600" height="440" class="size-medium wp-image-2163" />][2]<figcaption class="wp-caption-text">Библиотека Nib в действии</figcaption></figure> 

Отлично! Все работает четко &#8211; миксины преобразуются в готовый CSS-код. Правда, выглядит он немного неприглядно &#8211; не причесанный и не почищенный.

Ну это решается просто &#8211; достаточно на этот CSS-файл натравить Gulp-плагины [gulp-csscomb][3] и [gulp-autoprefixer][4].

Главное &#8211; библиотека подключена и работает!

### Nib &#8211; как подружить с Gulp

До этого момента мною использовалась нативная утилита `stylus` для компиляции из формата Stylus в формат CSS. И в том числе &#8211; с поддержкой библиотеки Nib.

Однако, на практике такой способ вряд-ли будет использоваться. Я имею ввиду, что использование лишь одной утилиты `stylus` &#8211; я сомневаюсь, что кому-либо пригодиться.

Гораздо практичнее использование Gulp, у которого есть соответствующий плагин [gulp-stylus][5] для компиляции из формата Stylus в CSS.

Этот плагин имеет поддержку библиотеки Nib, достаточно только настроить таковую в своем проекте.

Ниже я рассмотрю процесс подключения и настройки Nib (а заодно &#8211; и Stylus) в моем любимом Gulp.

#### Установка плагинов gulp-stylus и nib

В своем рабочем проекте необходимо установить два плагина (*с помощью консоли*):

<pre>// Command Line

  $ sudo npm install gulp-stylus nib --save-dev
  </pre>

В результате оба пакета установятся в проект и добавятся в файл package.json в качестве зависимостей:

<pre>// Javascript

  ...
  "gulp-stylus": "^1.3.4",
  "nib": "^1.0.4"
  ...
  </pre>

#### Настройка файла gulpfile.js

В файле gulpfile.js необходимо внести несколько правок. Первым делом &#8211; добавляем в начало файла две с строки:

<pre>// Javascript

  var gulp = require('gulp'),
    stylus = require('gulp-stylus'),
    nib = require('nib'),
  ...
  </pre>

Затем создаем задачу task для компиляции из Stylus в CSS. В качестве параметра у метода `stylus` будет дополнительная строка `use:[nib()]`, говорящая о том, что необходимо использовать библиотеку Nib:

<pre>// Javascript

  gulp.task('stylus', function () {
    gulp.src('app/styles/common.styl')
      .pipe(plumber())
      .pipe(stylus({use:[nib()]}))
      .pipe(prefixer({
        browsers: ['last 2 versions']
      }))
      .pipe(csscomb())
      .pipe(gulp.dest('dist/assets/styles/'));
  });
  </pre>

Вот это и все (*необходимый минимум*), чтобы подружить библиотеку Nib c Gulp.

Не забываем подключить в stylus-файл проекта библиотеку:

<pre>// Stylus

@import 'nib'
</pre>

### Миксины библиотеки Nib

С подключением библиотеки Nib разобрались. Остался вопрос &#8211; а что там внутри, под капотом у Nib?

С малой толикой миксинов я уже познакомился, когда создавал тестовую страничку подключения и компиляции (*см. изображение выше*).

На [официальной странице Nib][6] есть ссылка на документацию по миксинам &#8211; [Документация миксинов Nib][7].

Там все описано просто и понято, с подробными примерами. Осталось только читать и пользоваться.

В принципе, больше и сказать мне нечего (*по крайней мере &#8211; мне*) по поводу миксинов в Nib. Дальше только &#8211; брать их и использовать на практике.

На этом все &#8211; оцените статью:  
<span id="post-ratings-2162" class="post-ratings" data-nonce="d796592aba"><img id="rating_2162_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2162, 1, '1 Star');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2162_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2162, 2, '2 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2162_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2162, 3, '3 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2162_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2162, 4, '4 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2162_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2162, 5, '5 Stars');" onmouseout="ratings_off(4.3, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>4,33</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2162_text"></span></span><span id="post-ratings-2162-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: https://github.com/tj/nib "Nib"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/12/nib.png
 [3]: https://www.npmjs.com/package/gulp-csscomb "gulp-csscomb"
 [4]: https://www.npmjs.com/package/gulp-autoprefixer "gulp-autoprefixer"
 [5]: https://www.npmjs.com/package/gulp-stylus "Stylus plugin for gulp"
 [6]: https://github.com/tj/nib "Nib GitHub"
 [7]: http://tj.github.io/nib/ "Документация миксинов Nib"