---
title: Установка Node.js, npm и Bower под Linux Mint
author: gearmobile
excerpt: 'Статья посвящена вопросу установки Node.js и пакетного менеджера npm под операционную систему Linux Mint 17 “Qiana” Cinnamon (64-bit). Также рассмотрен вопрос установки пакетного менеджера Bower в этой же операционной системе'
layout: post
permalink: /install-nodejs-npm-bower-in-linux-mint/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 7
ratings_score:
  - 35
ratings_average:
  - 5
categories:
  - OS Linux
tags:
  - bower
  - node.js
  - npm
---
> Статья посвящена вопросу установки Node.js и пакетного менеджера npm под операционную систему Linux Mint 17 “Qiana” Cinnamon (64-bit). Также рассмотрен вопрос установки пакетного менеджера Bower в этой же операционной системе.

Почему выбрана система Linux Mint - об этом не стоит говорить долго. Это система гораздо удобнее для задач кодинга, нежели Windows. Пакеты Node.js и пакетный менеджер npm необходим для дальнейшего изучения ремесла верстальщика. Дело в том, что популярный фреймворк Foundation для своей корректной работы требует первоначальной установки Node.js. Автор планирует в дальнейшем познакомиться с фреймворком Foundation, поэтому ему потребовалась установка вышеназванных пакетов.

О том, что такое Node.js, в этой статье также не будет описано. Во-первых, автор статьи имеет лишь поверхностное представление об этом сервере. А во-вторых, в Интернете есть немало хороших материалов по данному вопросу.

### Установка Node.js

Для установки пакета Node.js под систему Linux Mint можно воспользоваться официальным сайтом проекта - [Node.js][1]. В разделе [Download][2] имеется табличка для скачивания различных версий пакета Node.js. В случае системы Linux в этой таблице нужно найти строку Linux Binaries.

Однако я не буду "заморчиваться" установкой из исходного кода. В Linux Mint есть прекрасный менеджер пакетов `apt-get`, которым можно и нужно воспользоваться для быстрой и безопасной установки Node.js под Linux. Единственный минус такого подхода - в результате у меня на машине будет стоять не самая свежая версия сервера Node.js. Однако в данном случае это абсолютно не критично.

В терминале ввожу команду:

{% highlight powershell %}
$ sudo apt-get install nodejs
{% endhighlight %}

... пару секунд терпения и у меня под Linux Mint 17 “Qiana” Cinnamon (64-bit) установлен пакет Node.js версии:

{% highlight powershell %}
$ nodejs -v
v0.10.25
{% endhighlight %}

На момент написания статьи самая свежая версия Node.js (*как указано на официальном сайте*) - это 0.10.28. Как видим, разница в версиях небольшая, так что я поступил правильно, воспользовавшись `apt-get`.

### Установка npm под Linux Mint

Как хорошо известно, у данного сервера имеется свой собственный менеджер пакетов npm (Node Packaged Modules), для установки дополнительных модулей под Node.js. Другими словами, с помощью менеджера npm можно установить под сервер Node.js любой модуль, имеющийся в наличии на репозитории GitHub. Модуль расширяет возможности сервера Node.js в зависимости от того, какой это модуль (*тавтология*). С кратким описанием и списком всех модулей под Node.js можно ознакомиться на официальном сайте проекта npm - [Node Packaged Modules][3].

При установке в свою систему Linux Mint через `apt-get` у меня был установлен только сам сервер Node.js. При этом менеджер пакетов npm отстуствовал в системе. Не знаю, как это происходит при установке пакета Node.js из исходников, но при использовании `apt-get` у меня получилось именно так. Поэтому следующим шагом будет инсталляция менеджера пакетов npm под систему Linux Mint.

В терминале Linux ввожу команду:

{% highlight powershell %}
$ sudo apt-get install npm
{% endhighlight %}

Пробежит много-много строк, но в результате в системе появиться пакет npm:

{% highlight powershell %}
$ npm -v
1.3.10
{% endhighlight %}

Использование менеджера npm очень похоже на использование менеджеров пакетов a-la Linux: `apt-get`, `emerge`, `pacman` и так далее. npm также является консольной командой и у него схожие ключи, поэтому пользователи Linux без труда разберутся с ним:

{% highlight powershell %}
$ npm -h
{% endhighlight %}

Давайте проверим работу установленного менеджера npm. Для этого я в специально отведенной директории Projects создам поддиректорию npm, перейду в нее для дальнейшего удобства работы и установлю в этой поддиректории модуль `underscore` из репозитория npm:

{% highlight powershell %}
$ mkdir -p Projects/npm
$ cd Projects/npm
$ npm install underscore
{% endhighlight %}

Если теперь посмотреть содержимое поддиректории npm c помощью команды `ls`, то обнаружим появление папки `node_modules`, внутри которой располагается подпапка `underscore` c содержимым одноименного модуля:

{% highlight powershell %}
$ ls node_modules/underscore/
LICENSE  package.json  README.md  underscore.js  underscore-min.js
{% endhighlight %}

Модуль Underscore успешно установлен и менеджер npm также успешно справился со своей задачей.

### Установка менеджера Bower под Linux Mint

Переходим к заключительному (*и продолжительному*) вопросу данной статьи и рассмотрим установку менеджера пакетов Bower. Могу предвидеть у читателей логичный вопрос: "Как - еще один менеджер пакетов?! Но зачем? Разве не хватает npm, c которым мы только что познакомились?"

Все правильно! npm - это менеджер пакетов. И Bower - тоже менеджер пакетов. Отличие первого от второго заключается в том, что npm - это менеджер пакетов для сервера Node.js (*и только*). А Bower (*хотя сам является модулем под Node.js*) - это менеджер пакетов для всего проекта в целом.

Npm понимает и может работать только с JavaScript-приложениями (*модулями под Node.js, написанными на этом языке*). Bower умеет работать с пакетами на JavaScript, HTML, CSS. C помощью него можно одним движением добавить в разрабатываемый проект все, что нужно: библиотеку jQuery, фреймворк Foundation, модуль Underscore, сброс стилей Normalize.css и так далее.

Не нужно самому "вручную" выискивать на безбрежных просторах Интернет пакет и подключать его в проект - Bower это сделает сам. Заманчиво, не правда ли? На официальной странице проекта [Bower][4] можно почитать подробную информацию о данном менеджере (правда, на английском языке). В разделе [Search Packages][5] можно поискать нужный пакет для установки.

Я же приступлю к установке Bower на свою локальную машину. Так как Bower является модулем для Node.js, то его можно установить с помощью менеджера npm:

{% highlight powershell %}
$ sudo npm install -g bower
{% endhighlight %}

Однако, если запустить после этого в терминале команду просмотра версии, то увидим такой результат:

{% highlight powershell %}
$ bower -v
/usr/bin/env: node: No such file or directory
{% endhighlight %}

Исправить ситуацию можно созданием ссылки:

{% highlight powershell %}
$ sudo ln -s /usr/bin/nodejs /usr/bin/node
{% endhighlight %}

Теперь если снова посмотреть версию установленного пакета, увидим следующее:

{% highlight powershell %}
$ bower -v
1.3.3
{% endhighlight %}

Создаю специальную поддиректорию `bower` в директории Projects, перехожу туда и запускаю менеджер bower на установку пакета jquery:

{% highlight powershell %}
$ mkdir -p Projects/bower
$ cd Projects/bower
$ bower install jquery
{% endhighlight %}

Если до этого момента на локальной машине (*как у меня*) не был установлен пакет `git`, то самое время это сделать, иначе bower не сможет установить указанный пакет jquery:

{% highlight powershell %}
$ bower install jquery
bower jquery#*  ENOGIT git is not installed or not in the PATH
{% endhighlight %}

Все пакеты для скачивания и установки менеджер bower берет с GitHub, поэтому без пакета git этот менеджер не сможет обойтись.

Установка Git на Linux производится простой командой:

{% highlight powershell %}
$ sudo apt-get install git
{% endhighlight %}

После этого, повторив команду установки jquery через bower, получаю следующий отзыв в консоли:

{% highlight powershell %}
$ bower install jquery
  bower jquery#*              not-cached git://github.com/jquery/jquery.git#*
  bower jquery#*                 resolve git://github.com/jquery/jquery.git#*
  bower jquery#*                download https://github.com/jquery/jquery/archive/2.1.1.tar.gz
  bower jquery#*                 extract archive.tar.gz
  bower jquery#*                resolved git://github.com/jquery/jquery.git#2.1.1
  bower jquery#~2.1.1            install jquery#2.1.1
{% endhighlight %}

Если посмотреть на содержимое поддиректории `bower`, то увидим, что там появилась директория `bower_components`, в которой находится поддиректория `jquery` c установленным пакетом:

{% highlight powershell %}
$ ls bower_components/jquery/
bower.json  dist  MIT-LICENSE.txt  src
{% endhighlight %}

В результате была установлена **последняя версия** библиотеки jQuery - 2.1.1. Если нужна какая-то конкретная версия пакета (jQuery, в частности), то нужно это указать с помощью тега:

{% highlight powershell %}
$ bower install jquery#1.9.1
{% endhighlight %}

Внимательный читатель мог заметить, менеджер пакетов Bower также (как и npm) является консольным. Список доступных для него команд можно получить вызовом:

{% highlight powershell %}
$ bower -h
{% endhighlight %}

В частности, для обновления уже установленного пакета существует команда:

{% highlight powershell %}
$ bower update [name_package]
{% endhighlight %}

Для удаления установленного пакета имеется команда:

{% highlight powershell %}
$ bower uninstall [name_package]
{% endhighlight %}

Посмотреть информацию о пакете:

{% highlight powershell %}
$ bower info [name_package]
{% endhighlight %}

Этой командой можно воспользоваться при настройке файла пакетной установки `bower.json`

#### Плагин Bower под Sublime Text

Под редактор Sublime Text имеется одноименный плагин Bower, который в точности повторяет все возможности менеджера Bower. Все преимущество использования плагина Bower заключается в том, что производить инсталляцию, обновление или удаление пакетов можно прямо в редакторе Sublime Text, не переходя в консоль.

Установка плагина Bower выполняется стандартно - через менеджер пакетов Sublime Text: нажимаем сочетание клавиш **Shift+Ctrl+P**, введем в строке **Install** и выбираем из появившегося списка пакет **Bower**.

Теперь попробуем установить какой-либо пакет, не выходя из Sublime Text, c помощью плагина Bower. Для этого снова нажмем сочетание клавиш **Shift+Ctrl+P**, вводим **Bower:Install** и из появившегося списка выбираем пакет Foundation (*к примеру*).

Видим, как в панели проектов Sublime Text, в папке `bower_components` появилась целая куча подпапок, являющихся частью единого целого - фреймворка Foundation:

![Установленный через Bower пакет Foundation в Sublime Text]({{ http://zencoder.ru/ }}/images/uploads/2014/06/st-bower_components.png)
{: .center-image .responsive-image }

#### Настройка плагина Bower

Поддиректория `bower_components`, в которую плагин Bower производит установку пакетов, не является чем-то постоянным. То есть, можно легко изменить имя и расположение этой директории. Делается это следующим образом - в Sublime Text нажимаем сочетание клавиш **Shift+Ctrl+P** и вводим **Bower: Configure project** (*никто не запрещает создать файл конфигурации вручную*).

В текущую директорию автоматически добавиться файл `.bowerrc` типа json, в котором будет всего лишь одна строка - имя директории, в которую производится установка пакетов через плагин Bower:

![Файл настроек пакета Bower]({{ http://zencoder.ru/ }}/images/uploads/2014/06/st-bower_configure_project.png)
{: .center-image .responsive-image }

Для эксперимента изменим имя папки с:

{% highlight powershell %}
"directory": "components"
{% endhighlight %}

на:

{% highlight powershell %}
"directory": "apps"
{% endhighlight %}

... удалим старую директорию `bower_components` с пакетом foundation и установим через Bower другой пакет - underscore. В результате получим следущее:

![Новое имя директории с пакетами в Bower]({{ http://zencoder.ru/ }}/images/uploads/2014/06/st-bower_configure_project_new_name.png)
{: .center-image .responsive-image }

#### Пакетная установка в менеджере Bower

У менеджера пакетов Bower есть еще одна замечательная особенность. Это возможность пакетной установки через специально созданный конфигурационный файл. Другими словами, создается специальный файл формата json (`component.json`), в котором прописываются имена всех пакетов, которые необходимы для установки в данном проекте. Затем в консоли запускается менеджер Bower c одной командой:

{% highlight powershell %}
$ bower install
{% endhighlight %}

... менеджер bower прочитает файл `component.json` и автоматически установит все пакеты, перечисленные в нем. Отлично, не правда ли?

**Примечание**: начиная с Bower v.0.9 файл конфигурации `component.json` был переименован в файл `bower.json`, который я буду использовать в дальнейшем.

Файл `bower.json` имеет следующий формат:

{% highlight powershell %}
{
"name": "name_of_project",
"version": "1.0.0",
  "dependencies": {
    "name_package": "version_package",
    "name_package": "version_package"
  }
}
{% endhighlight %}

... где `name` - это имя проекта, `version` - версия проекта, `dependencies` - зависимости проекта. Под зависимостями проекта подразумевается список сторонних пакетов (к примеру - foundation, backborne, jquery и так далее), которые используются при создании данного проекта.

Прописав в этом списке нужные пакеты, тем самым мы заставим Bower автоматически отслеживать наличие указанных пакетов для текущего проекта. Но, от слов к делу - давайте попрактикуемся и создадим примерный файл `bower.json` для текущего "проекта" bower. Для этого я удалю все ранее установленные в этой поддиректории пакеты:

{% highlight powershell %}
$ bower uninstall [name_of_package]
{% endhighlight %}

... создам в этой директории пустой файл `bower.json` и наполню его следующим содержимым:

{% highlight powershell %}
{
"name": "bower",
"version": "0.0.1",
  "dependencies": {
     "jquery": "1.9.1",
     "foundation": "latest"
   }
}
{% endhighlight %}

... где `latest` - самая последняя версия пакета. Сохраняю изменения, перехожу в консоль и запускаю команду:

{% highlight powershell %}
$ bower install
{% endhighlight %}

В результате будет произведена автоматическая установка всех перечисленных в файле пакетов. Кроме того, Bower умеет **отслеживать зависимости пакетов**. В моем примере в консоль была выведена следующая информация:

{% highlight powershell %}
...
Unable to find a suitable version for jquery, please choose one:
    1) jquery#1.9.1 which resolved to 1.9.1 and is required by bower
    2) jquery#>= 2.1.0 which resolved to 2.1.1 and is required by foundation#5.2.3
    3) jquery#>=1.2 which resolved to 2.1.1 and is required by jquery.cookie#1.4.1

Prefix the choice with ! to persist it to bower.json

[?] Answer:
...
{% endhighlight %}

... то есть, Bower отследил, что я устанавливаю библиотеку jQuery версии 1.9.1; но при этом самая последняя версия фреймворка Foundation 5.2.3 требует для своей работы jQuery версии 2.1.1. Вот менеджер и спрашивает у меня - как быть дальше? Ай да Bower! ))

#### Добавление зависимостей в файл bower.json

После создания пакетного файла `bower.json` в менеждере Bower можно **автоматически добавлять в него запись** при ручной установке отдельного пакета. Допустим, в ходе работы срочно потребовалась установка пакета backbone.

Тогда выполняем следующую команду:

{% highlight powershell %}
$ bower install backbone --save
{% endhighlight %}

... пакет backbone (и его зависимость underscore) успешно установились. Но нас интересует факт добавления записи в файл `bower.json`, поэтому смотрим:

{% highlight powershell %}
$ cat bower.json
{
"name": "bower",
"version": "0.0.1",
  "dependencies": {
    "jquery": "1.9.1",
    "foundation": "latest",
    "backbone": "~1.1.2"
  }
}
{% endhighlight %}

#### Автоматическое создание файла bower.json

Помимо ручного создания и настройки файла `bower.json`, у данного менеджера предусмотрена команда для автоматического создания и настройки этого файла. Для этого необходимо в консоли запустить команду:

{% highlight powershell %}
$ bower init
{% endhighlight %}

... тогда менеджер проведет нас "за ручку" через все этапы создания настроек файла `bower.json` путем задания серии вопросов. Взгляните на примерный результат вышеназванной команды:

{% highlight powershell %}
$ cat bower.json
{
  "name": "bower",
  "version": "0.0.1",
  "dependencies": {
    "jquery": "1.9.1",
    "foundation": "latest",
    "backbone": "~1.1.2"
  },
  "description": "my firts project",
  "moduleType": [
    "amd"
  ],
  "authors": [
    "zencoder"
  ],
  "license": "MIT",
  "homepage": "http://localhost:7788/third/",
  "ignore": [
    "**/.*",
    "node_modules",
    "bower_components",
    "apps",
    "test",
    "tests"
  ]
}
{% endhighlight %}

### Плагин AutoFileName в Sublime Text

Редактор Sublime Text имеет неизмеримое количество полезных плагинов. Одним из них является [AutoFileName][6] - незаменимая вещь для автодополнения путей файлов в проекте. Кто имел мало-мальский опыт работы в Dreamveawer (или подобные ему IDE), могут сразу догадаться, о чем идет речь.

Поэтому данный плагин must have в коллекции под рабочую версию Sublime Text любого верстальщика.

### Заключение

Завершаю обзор установки пакетов Node.js, npm и Bower под систему Linux Mint. Надеюсь, статья оказалась достаточно полной, точной и грамотной. В ее написании неоценимую помощь оказало видео " [Bower - Обзор пакетного менеджера][7] " Sorax&#8217;а.

 [1]: http://nodejs.org/ "Node.js"
 [2]: http://nodejs.org/download/ "Download"
 [3]: https://www.npmjs.org/ "Node Packaged Modules"
 [4]: http://bower.io/ "Bower"
 [5]: http://bower.io/search/ "Search Packages"
 [6]: https://sublime.wbond.net/packages/AutoFileName "AutoFileName"
 [7]: http://youtu.be/swUFx9p0M7g "Bower - Обзор пакетного менеджера"
