---
title: "Фреймворк Foundation - Знакомство"
layout: post
categories: css
tags: [foundation, css]
share: true
---

> Начинаем изучение фреймворка Foundation. Этот фреймворк входит в двойку самых популярных и распространенных CSS-фреймворков на момент написания статьи (еще один - Twitter Bootstrap).

Можно по разному относиться к фреймворкам - любить их или не любить. Однако, они есть и ими пользуются при создании сайтов. Данный факт говорит о том, что фреймворки - это все-таки не такое уж и Зло. Скорее всего, нужно выработать для себя такое отношение к фреймворкам, что это быстрый способ создать что-либо непритязательное - не слишком оригинальное по дизайну, со стандартизированными элементами и не слишком оптимизированным кодом (*читай - с большой долей мусора*). А вот если к шаблону предъявляются повышенные требования, вот тогда нужно писать весь код вручную.

Но, как говорилось уже выше, фреймворки - они есть, и факт их существования говорит сам за себя. А поэтому, любой профессиональный веб-разработчик обязан знать и уметь работать с ними. В этой статье будет положено начало посильного знакомства с одним из двух популярных фреймворков - ZURB Foundation.

## Сайт проекта Foundation

Официальный сайт проекта находится по этому адресу - [Foundation][1]. Если внимательно присмотреться, то можно заметить, что на странице проекта и в других местах часто мелькает слово [ZURB][2] - это название дизайнерской фирмы, которая и создала фреймворк.

Если бегло пробежаться по документации, то можно увидеть множество "плюшек" у данного фреймворка:

* фирменную консольную утилитку foundation для разворачивания или обновления проекта на Foundation
* коллекцию [сниппетов под Sublime Text][3] для быстрого создания различных компонент HTML-страницы
* тесная интерграция с препроцессором Sass

Естественно, Foundation заявляется как полностью адаптивный фреймворк, нацеленный прежде всего на создание мобильных версий сайтов (Mobile First).

## Способы установки Foundation

Как говориться на [странице документации][4], существует три способа установки фреймворка на локальном компьютере:

* [Getting Started With Foundation CSS][5] - самый простой и быстрый способ установки и начала работы. Нужно просто скачать и распаковать архив с готовым фреймворком
* [Getting Started With Sass][6] - разворачивание фреймворка c поддержкой Sass/Compass. Установка на локальный компьютер производится автоматически, с помощью уже упоминавшейся консольной утилиты foundation
* [Applications][7] - это что-то связано с разработкой приложений под Foundation. В общем, для front-end это не интересно

В дальнейшей статье приступим в установке Foundation вторым способом, так как мы уже хорошо знаем и умеем пользоваться препроцессором Sass и его библиотекой Compass.

## Установка Foundation c поддержкой Sass

Для установки фреймворка на локальный компьютер с поддержкой Sass/Compass потребуется предварительное начилие на нем таких программных продуктов, как:

* Git - нужен для работы Bower
* Ruby - нужен для работы Sass/Compass
* Nodejs - нужен для работы Grunt

Foundation версии 5 использует для установки своих компонентов, а также для обновления себя самого в целом менеджер пакетов Bower, поэтому его наличие также жизненно необходимо в системе. Помимо этого, фреймворк может работать совместно с менеджером задач Grunt для конкатенации файлов; но наличие Grunt не является обязательным.

Проверяю наличие трех вышеназванных пакетов в своей системе Linux Mint 17. Все три пакета были установлены мною гораздо раньше. Как выполнить установку Git, Ruby, Nodejs, Grunt и Bower под Linux Mint 17, можно почитать в этой статье - "Установка Node.js, npm и Bower под Linux Mint":

{% highlight powershell %}
$ git --version
git version 1.9.1
$ ruby --version
ruby 1.9.3p484 (2013-11-22 revision 43786) [x86_64-linux]
$ nodejs --version
v0.10.25
$ bower --version
1.3.3
{% endhighlight %}

Установка Bower и Grunt, если они еще не были инсталлированы в системе, производится простой командой:

{% highlight powershell %}
$ npm install -g bower grunt-cli
{% endhighlight %}

Все готово для установки консольной утилиты `foundation`. Вы спросите - что это еще за утилита такая и зачем она нужна? Все просто - это фирменная утилитка от Foundation и ее задача - автоматизированное разворачивание готового проекта на локальной машине.

Устанавливаем утилиту foundation:

{% highlight powershell %}
$ gem install foundation
{% endhighlight %}

Сама утилитка foundation очень проста. Вызову команду `help` и все станет понятно без слов:

{% highlight powershell %}
$ foundation help
Commands:
  foundation help [COMMAND]  # Describe available commands or one specific command
  foundation new             # create new project
  foundation update          # update an existing project
  foundation upgrade         # Upgrade your Foundation 4 compass project
  foundation version         # Display CLI version
{% endhighlight %}

## Разворачивание Foundation c поддержкой Compass

C помощью утилиты foundation можно развернуть на локальной машине фреймворк c поддержкой:

* Grunt и Libsass
* Compass

Я воспользуюсь вторым вариантом и запущу установку Foundation c поддержкой Compass. Для этого нужно выполнить команду:

{% highlight powershell %}
$ foundation new new_project_name
{% endhighlight %}

В моем случае имя нового проекта было оригинальным - foundation )) Пару секунд ожидания и я получаю папку с таким содержимым:

{% highlight powershell %}
$ ls -l
drwxr-xr-x bower_components
-rw-r--r-- bower.json
-rw-r--r-- config.rb
-rw-rw-rw- Foundation.md
-rw-r--r-- humans.txt
-rw-r--r-- index.html
drwxr-xr-x js
-rw-r--r-- README.md
-rw-r--r-- robots.txt
drwxr-xr-x scss
{% endhighlight %}

![Новый проект на Foundation]({{site.url}}/images/uploads/2014/06/new_project_in_foundation.png)

![Новый проект на Foundation]({{site.url}}/images/uploads/2014/06/new_project_in_foundation.png)

Видим здесь файлы `config.rb`, `bower.json`, `index.html`; папки `bower_components`, `js`, `scss`. Другими словами - это готовый проект!

Немного подредактирую файл `config.rb` и запускаю Compass на мониторинг изменений в текущем проекте:

{% highlight powershell %}
$ compass watch .
{% endhighlight %}

Проект готов для работы! В следующем обзоре будет рассмотрен самый простой пример работы с данным фреймворком - я с вами научусь создавать кнопки на Foundation.

---

 [1]: http://foundation.zurb.com/ "Foundation"
 [2]: http://www.zurb.com/ "ZURB"
 [3]: https://github.com/zurb/foundation-5-sublime-snippets "сниппеты под Sublime Text"
 [4]: http://foundation.zurb.com/docs/ "Getting Started"
 [5]: http://foundation.zurb.com/docs/css.html "Getting Started With Foundation CSS"
 [6]: http://foundation.zurb.com/docs/sass.html "Getting Started With Sass"
 [7]: http://foundation.zurb.com/docs/applications.html "Applications"
