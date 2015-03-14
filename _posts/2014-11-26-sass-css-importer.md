---
title: Плагин Sass CSS Importer
author: gearmobile
layout: post
---
Краткий обзор плагина Sass CSS Importer для импортирования файлов CSS в файлы Sass.

В чем заключается вопрос? Как хорошо известно всем, кто постоянно работает с Sass, с помощью директивы `@import` можно подключать одни Sass-файлы в другие Sass-файлы.

Например, подключить файл `typography.scss` в файл `main.scss` можно так:

{% highlight css %}
  @import “_typography”;
{% endhighlight %}

Оба файла `main.scss` и `typography.scss` будут объединены препроцессором в один файл `main.scss`, который уже будет компилироваться в файл `main.css`.

Знак подчеркивания в данном случае является **дополнительной опцией**. Этим знаком препроцессору Sass указывается не выполнять **предварительную компиляцию** файла `typography.scss` в файл `typography.css` перед его подключением в `main.scss`.

Но что, если стоит задача подключения файлов формата CSS в файлы формата Sass? Директива `@import` в этом случае помочь не может. CSS-файл **нельзя просто так подключить** в Sass-файл.

Задача подключения CSS-файлов в Sass-файлы наиболее часто может возникнуть в случае использования различных готовых слайдеров или каруселей, которые зачастую идут “в комплекте” с минимальными правилами на CSS.

Что же делать?

### Плагин Sass CSS Importer

Совсем недавно (*17 июля сего года*) Chris Eppstein [<sup>2</sup>][2]{#return-note-2082-2.simple-footnote} выпустил специальный плагин, задачей которого и является **импортирование CSS-файлов** в Sass-файлы. Страничка с официальной документацией по плагину Sass CSS Importer расположена на GitHub &#8211; [Sass CSS Importer Plugin][3].

Там все описано кратко и предельно ясно. Однако, я был так доволен тем фактом, что теперь могу свободно подключать CSS в Sass, что решил потратить часть своего времени, чтобы описать его своими словами, по-русски.

### Установка Sass CSS Importer

Установка плагина выполняется как обычно, через менеджер пакетов `gem`:

{% highlight powershell %}
  $ sudo gem install --pre sass-css-importer
{% endhighlight %}

### Подключение Sass CSS Importer

При использовании фреймворка Compass нужно добавить строку в конфигурационный файл `config.rb` своего текущего проекта:

{% highlight css %}
  require 'sass-css-importer'
{% endhighlight %}

### Импортирование CSS в Sass

Теперь, чтобы импортировать CSS в Sass, нужно воспользоваться все той же директивой `@import`, но **со специальным синтаксисом**.

В общем случае этот синтаксис выглядит таким образом:

{% highlight css %}
  @import "CSS:имя_директории/имя_css_файла”;
{% endhighlight %}

В частном случае синтаксис будет выглядеть таким образом:

{% highlight css %}
  @import "CSS:carousel";
{% endhighlight %}

> Обратите внимание на важный момент: имя CSS-файла нужно указывать **без расширения**!

Можно запустить процесс компиляции через командную строку:

{% highlight powershell %}
  $ compass watch
{% endhighlight %}

&#8230; и проверить, что CSS-файл будет включен в общий вывод.<figure id="attachment_2086" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-2086" src="http://localhost:7788/third/wp-content/uploads/2014/11/sass-css-importer-600x312.png" alt="Плагин Sass CSS Importer" width="600" height="312" />][4]<figcaption class="wp-caption-text">Плагин Sass CSS Importer</figcaption></figure> 

### Заключение

В принципе, вот и все, что можно сказать о Sass CSS Importer.

 [1]: #note-2082-1 "Sass &#8211; мощный препроцессор для CSS"
 [2]: #note-2082-2 "Chris Eppstein &#8211; один из двух создателей Compass"
 [3]: https://github.com/chriseppstein/sass-css-importer "Sass CSS Importer"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/11/sass-css-importer.png