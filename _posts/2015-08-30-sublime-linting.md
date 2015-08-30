---
title: "SublimeLinter - обнаружение ошибок в Sublime Text"
layout: post
categories: sublime text
tags: [sublime text, linting]
share: true
---

Термин <em>linting</em> применяется для обозначения процесса обнаружения ошибок в исходных файлах программ, скриптов или документов. Программа такого рода должна иметься в инструментарии каждого разработчика, так как с помощью таких программ можно обнаруживать ошибки в процессе написания кода. Популярный редактор кода Sublime Text не имеет встроенных возможностей для обнаружения ошибок; однако такую ситуацию легко исправить.

При помощи <em>linting</em>'а можно обнаруживать небольшие ошибки кода "на лету", в процессе написания этого кода - например, пропущенную точку с запятой в JavaScript-коде. Возможность обнаружения ошибок в редакторе Sublime Text осуществляется с помощью плагина [SublimeLinter][1], который необходимо установить прежде всего.

Если в какой-либо строке кода этот редактор обнаружит ошибку, то данная строка будет подсвечена в gutter редактора Sublime. Более того, если поместить курсор мыши в строку с ошибкой, то в *status bar* редактора Sublime Text отобразится краткое описание ошибки, что поможет принять меры для ее правильного устранения.

Ниже представлен наглядный пример подсветки ошибок в Sublime Text с помощью плагина SublimeLinter:

![SublimeLinter]({{site.url}}/images/uploads/2015/08/linter-fill.jpg "SublimeLinter")

Плагин [SublimeLinter][1] сам по себе не выполняет процесса "отлавливания" ошибок в коде, так как является всего-лишь фреймворком, основой для других плагинов (linter), каждый из которых создан для обнаружения ошибок в каком-то определенном языке - JavaScript, PHP, Ruby, Python, HTML, CSS и так далее.

## SublimeLinter в Sublime Text

Как уже упоминалось ранее, плагин SublimeLinter является фреймворком, основой для более маленьких плагинов (linter), которые осуществляют непосредственный поиск синтаксических ошибок в программном коде.

Поэтому первоначально необходимо установить этот фреймворк (как плагин) в редактор Sublime Text и самый простой способ это сделать - воспользоваться менеджером пакетов [Package Control][2]. Для этого нажимаем сочетание клавиш <kbd>Shift+Ctrl+P</kbd> (Linux \ Windows) или <kbd>Shift+Cmd+P</kbd> (Mac OSX). В поле поиска вводим название устанавливаемого пакета - [SublimeLinter][3]. Далее - производим установку.

Теперь необходимо определиться с тем, в каких языках программирования необходимо "отлавливать" ошибки. Другими словами, на каких языках программирования вы пишете и в каких из них вам необходима поддержка SublimeLinter.

Допустим, это серверный язык PHP. Тогда для включения возможности обнаружения ошибок в Sublime Text необходимо установить плагин [Sublime​Linter-php][4], так же через менеджер пакетов [Package Control][2]. Стоит оговориться, что дополнительной зависимостью этого плагина является язык PHP, который предустановлен в операционных системах Linux\MacOSX, но который необходимо заранее установить отдельно в операционной системе Windows.

Примером работы связки Sublime​Linter + Sublime​Linter-php в редакторе Sublime Text может послужить нижеследующее изображение:

![SublimeLinter PHP]({{site.url}}/images/uploads/2015/08/linter-php-error.jpg "SublimeLinter PHP")

Рассмотрим другой случай, когда в редакторе Sublime Text используется язык программирования JavaScript. Тогда для возможности отлавливания ошибок в JS-коде необходимо установить плагин [Sublime​Linter-jshint][5]. В этом случае вопрос зависимостей этого пакета выглядит несколько сложнее. Плагин Sublime​Linter-jshint основывает свою работу на [JSHint][7], который необходимо установить в виде пакета под [Node.js][6] и устанавливается с помощью менеджера пакетов <abbr>npm</abbr>. Поэтому в операционной системе заранее должны быть установлены Node.js, <abbr>npm</abbr> и JSHint.

Примером работы плагина Sublime​Linter-jshint может послужить нижеследующее изображение:

![Sublime​Linter JSHint]({{site.url}}/images/uploads/2015/08/linter-js-error.jpg "Sublime​Linter JSHint")

Рассмотрим еще один случай, когда в редакторе Sublime Text используется язык таблиц каскадных стилей CSS (куда же без него?). Тогда необходимо доустановить в Sublime Text плагин [Sublime​Linter-csslint][8].

Рассмотрение подобных плагинов (linter) можно продолжать еще долго. Поэтому ограничимся только тремя вышеприведенными. Стоит сказать, что для поиска какого-либо конкретного плагина (linter) удобно воспользоваться online-сервисом [Package Control][2], в поисковой строке которого достаточно ввести начало названия искомого пакета, например, так - "SublimeLinter-". Система автоматически выдаст список все плагинов под фреймворк SublimeLinter.

Как нетрудно заметить, окончание (суффикс) в названии каждого из плагинов является подсказкой, для поддержки какого языка был создан этот плагин. Например, для языка Ruby существует плагин Sublime​Linter-ruby, для препроцессора Haml имеется плагин Sublime​Linter-haml.

Также стоит сказать, что необходимо внимательно читать описание к каждому из тех плагинов, которые планируется установить, так как каждый из них имеет разные зависимости. Наглядный пример зависимостей у плагинов Sublime​Linter-php и Sublime​Linter-jshint был приведен выше.

## Настройка SublimeLint

В плагине SublimeLint имеется большое количество настроек. Однако, с большинством из них не составит труда разобраться. Ниже приведено краткое описание некоторых из них.

### Linting Modes

Эта настройка отвечает за поведение плагина SublimeLinter - когда плагин должен оповещать об обнаруженной ошибке в коде программы или документа.

 * **Background** - это поведение по умолчанию плагина SublimeLinter. Сообщения об обнаруженных ошибках будут появляться по мере их обнаружения (другими словами - по мере написания строк кода) и будут обновляться каждый раз, когда будет производиться исправление обнаруженных ошибок. Такой режим может показаться излишне назойливым, так как иногда сообщение об ошибке может появиться прежде, чем будет дописана до конца инструкция, в которой вкралась ошибка.
 * **Load\Save** - в этом случае сообщения об ошибках будут отображаться плагином только после сохранения или загрузки сохраненного документа.
 * **Save Only** - сообщения об обнаруженных ошибках будут отображаться только при сохранении документа.
 * **Manual** - ручной вызов проверки на ошибки, из командной панели редактора Sublime Text.

Лично я предпочитаю режим **Load\Save**, так как в этом случае плагин SublimeLinter не мешает работать с кодом до тех пор, пора не будет выполнено сохранение этого кода в файле. Режим **Background** может показаться излишне назойливым, так как сообщения об ошибках будут появляться постоянно, мешая работе.

Для того, чтобы изменить поведение плагина SublimeLinter через настройку Linting Modes, необходимо зайти в командную панель редактора Sublime Text с помощью сочетания клавиш (<kbd>Shift+Ctrl+P</kbd> или <kbd>Shift+Cmd+P</kbd>) и ввести в строке поиска следующее:

<strong>sublimelinter lint mode</strong>

... откроется выпадающий список со всеми настройками плагина SublimeLinter, из которого необходимо выбрать **SublimeLinter: Choose Lint Mode**:

![SublimeLinter Lint Mode]({{site.url}}/images/uploads/2015/08/choose-lint-mode.jpg "SublimeLinter Lint Mode")

### Mark Style

Настройка **Mark Style** отвечает за внешний вид выделения ошибки в строке кода. Значением по умолчанию является **outline**. Но можно выбрать любое другое значение из предустановленных настроек.

В соответствии с [официальной документацией][9] SublimeLinter имеются несколько вариантов выделения ошибок в строке кода:

 * fill
 * outline
 * solid underline
 * squiggly underline
 * stippled underline

Аналогично с режимом **Linting Modes**, режим **Mark Style** настраивается через командную панель редактора Sublime Text - <kbd>Shift+Ctrl+P</kbd> (Linux \ Windows) или <kbd>Shift+Cmd+P</kbd> (Mac OSX). В выпадающм списке нужно выбрать строку **Sublime Linter: Choose Mark Style**.

Ниже представлены скриншоты всех пяти режимов выделения ошибок в строке, чтобы можно было сравнить и выбрать наиболее подходящий вариант.

#### Fill

![Mark Style Fill]({{site.url}}/images/uploads/2015/08/linter-mode-fill.jpg "Mark Style Fill")

#### Outline

![Mark Style Outline]({{site.url}}/images/uploads/2015/08/linter-mode-outline.jpg "Mark Style Outline")

#### Solid Underline

![Mark Style Solid Underline]({{site.url}}/images/uploads/2015/08/linter-mode-solid-underline.jpg "Mark Style Solid Underline")

#### Squiggly Underline

![Mark Style Squiggly Underline]({{site.url}}/images/uploads/2015/08/linter-mode-squiggly-outline.jpg "Mark Style Squiggly Underline")

#### Stippled Underline

![Mark Style Stippled Underline]({{site.url}}/images/uploads/2015/08/linter-mode-stippled-outline.jpg "Mark Style Stippled Underline")

### Gutter Themes

В дополнение к настройке выделения ошибок в строке кода, можно выполнить настройку иконок, который помещаются в области gutter редактора Sublime Text напротив строки с обнаруженной ошибкой. Такое выделение строки служит для большей информативности.

В плагине SublimeLinter имеется [набор предустановленных иконок][10], наглядное изображение которых представлено ниже.

#### Blueberry – cross

![SublimeLinter Gutter Blueberry Cross]({{site.url}}/images/uploads/2015/08/linter-gutter-blueberry-cross.jpg "SublimeLinter Gutter Blueberry Cross")

#### Blueberry – round

![SublimeLinter Gutter Blueberry Round]({{site.url}}/images/uploads/2015/08/linter-gutter-blueberry-round.jpg "SublimeLinter Gutter Blueberry Round")

#### Circle

![SublimeLinter Gutter Blueberry Circle]({{site.url}}/images/uploads/2015/08/linter-gutter-circle.jpg "SublimeLinter Gutter Blueberry Circle")

#### Danish Royalty

![SublimeLinter Gutter Danish Royalty]({{site.url}}/images/uploads/2015/08/linter-gutter-danish-royalty.jpg "SublimeLinter Gutter Danish Royalty")

#### Hands

![SublimeLinter Gutter Hands]({{site.url}}/images/uploads/2015/08/linter-gutter-hands.jpg "SublimeLinter Gutter Hands")

#### Knob – simple

![SublimeLinter Gutter Knob Simple]({{site.url}}/images/uploads/2015/08/linter-gutter-knob-simple.jpg  "SublimeLinter Gutter Knob Simple")

#### Knob – symbol

![SublimeLinter Gutter Knob Symbol]({{site.url}}/images/uploads/2015/08/linter-gutter-knob-symbol.jpg  "SublimeLinter Gutter Knob Symbol")

#### Koloria

![SublimeLinter Gutter Koloria]({{site.url}}/images/uploads/2015/08/linter-gutter-koloria.jpg  "SublimeLinter Gutter Koloria")

#### ProjectIcons

![SublimeLinter Gutter Project Icons]({{site.url}}/images/uploads/2015/08/images/linter-gutter-projecticons.jpg "SublimeLinter Gutter Project Icons")

Изменить настройки отображения иконок можно, зайдя в командную панель редактора Sublime Text и выбрав в выпадающем списке строку **Sublime Linter: Choose Gutter Theme**.

## Заключение

Плагин SublimeLinter является очень мощным и гибким, а количество поддерживаемых им язык - очень большое. Вы можете посетить [страницу поддерживаемых языков][11], чтобы убедиться в богатом выборе поддерживаемых языков программирования, разметки и многих других.

Рассмотренные в этой статье возможности плагина SublimeLinter являются далеко не исчерпывающими. На [официальной странице документации][1] вы всегда найдете для себя что-то новое. Для этого нужно только периодически просматривать эту документацию.

***
[1]: http://www.sublimelinter.com/en/latest/about.html "SublimeLinter"
[2]: https://packagecontrol.io/ "Package Control"
[3]: https://packagecontrol.io/packages/SublimeLinter "SublimeLinter Package Control"
[4]: https://packagecontrol.io/packages/SublimeLinter-php "Sublime​Linter-php"
[5]: https://packagecontrol.io/packages/SublimeLinter-jshint "Sublime​Linter-jshint"
[6]: https://nodejs.org/ "Node.js"
[7]: http://jshint.com/about/ "JSHint"
[8]: https://packagecontrol.io/packages/SublimeLinter-csslint "Sublime​Linter-csslint"
[9]: http://www.sublimelinter.com/en/latest/mark_styles.html "SublimeLinter Mark Style"
[10]: http://www.sublimelinter.com/en/latest/gutter_themes.html#standard-gutter-themes "Standard gutter themes"
[11]: https://packagecontrol.io/search/sublimelinter "Package Control Sublime Linter List"
