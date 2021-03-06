---
title: 'Ubuntu Linux - установка WebStorm'
layout: post
categories: linux
tags: [linux, webstorm, install]
share: true
---

С недавних пор на практике оценил преимущества использования профессиональных IDE для задач кодинга. К таким IDE я отношу [WebStorm](https://www.jetbrains.com/webstorm/ 'WebStorm'), [Visual Studio Code](https://code.visualstudio.com/ 'Visual Studio Code'), [Aptana Studio](http://www.aptana.com/ 'Aptana Studio').

До недавнего времени я пользовался отличным [Sublime Text](http://www.sublimetext.com/ 'Sublime Text') (к поклонникам [Atom](https://atom.io/ 'Atom') я себя не отношу) и все меня устраивало. Но в последнее время я все больше и больше начинаю заниматься с JavaScript (_надо сказать - не без удовольствия, особенно впечатлил Canvas_).

И вот тут произошло так, что в один прекрасный день я просто попробовал поработать в WebStorm с JavaScript. И все! Я уже не мог вернуться на Sublime Text!

Описать конкретно, что именно мне понравилось в WebStorm vs Sublime Text, я так вот в двух словах и не могу. Но скажу только одно - работа в WebStorm действительно удобная; в этом IDE есть много продуманных и отшлифованных вещей, которые сильно облегчают жизнь кодера.

После того, как я оценил работу в WebStorm на Mac OS X, мне захотелось иметь этот IDE и на ноутбуке с [Linux Mint 17.2 Cinnamon](https://linuxmint.com/ 'Linux Mint'). Не могу сказать точно, почему так, но мне работать под Linux как-то комфортнее, чем под Mac OS X. Наверное, просто сказывается сила привычки - я linuxoid со стажем.

Но вот незадача - под Linux я привык пользоваться супер-удобными менеджерами пакетов, такими как `apt-get` или `pacman`.

А вот что касается Visual Studio Code, Aptana Studio или WebStorm - то официальных портов этих IDE в Debian \ Ubuntu-репозиториях нет (_поправьте меня, если я ошибаюсь_).

На официальных сайтах этих IDE описывается только процесс установки под операционную систему Linux **вручную**. Не сказать, что там плохо описан этот процесс, но мне он не помог совсем.

Как результат, я решил вкратце описать процесс **ручной установки** IDE WebStorm под Linux Mint 17.2 Cinnamon \ Xfce. Две другие IDE - Aptana Studio и Visual Studio Code устанавливаются **абсолютно аналогично**.

- **Шаг первый** - с официального сайта [скачивается](https://www.jetbrains.com/webstorm/download/#section=linux-version 'WebStorm Linux') пакет под Linux (32 или 64 бита - на выбор)

- **Шаг второй** - делается копия скачанного архива с IDE WebStorm и помещается в любое удобное место (например, пусть это будет Desktop)

- **Шаг третий** - распаковывается архив с IDE WebStorm (который в Desktop)

- **Шаг четвертый** - в терминале запускается Midnight Commander с правами _root_: `sudo mc`; если вы вдруг не знаете, что такое [Midnight Commander](http://www.midnight-commander.org/ 'Midnight Commander') - то в самое время узнать о нем, так как это программа из разряда **must have** под системой Linux

- **Шаг пятый** - в Midnight Commander копируем распакованный архив WebStorm по пути `~/opt/`; в итоге в `~/opt/` должна появиться папка примерно такого вида - "WebStorm-141.456" (`~/opt/WebStorm-141.456`)

- **Шаг шестой** - на любом пустом месте Desktop делаем правый клик мыши (ПКМ), чтобы вызвать _контекстное меню_

- **Шаг седьмой** - в контекстном меню находим строку "Create Launcher"; текст строки может отличаться в зависимости от того, что именно используется на конкретном Linux - [Cinnamon](https://en.wikipedia.org/wiki/Cinnamon_%28software%29 'Cinnamon') или [Xfce](http://www.xfce.org/ 'Xfce'); тут главное - увидеть знакомое слово "Launcher"; в результате должно открыться примерно такое окно (в данном случае это Xfce):

![Create Launcher]({{site.url}}/images/uploads/2016/04/create-launcher.png 'Create Launcher')

- **Шаг восьмой** - вводим значения в поля этого окна; во все поля вводить данные необязательно; нужно ввести только **имя приложения** в поле "Name" - WebStorm; в поле "Command" вручную вводить **путь к исполняемому файлу приложения** нет необходимости - достаточно нажать на значок рядом с полем и откроется диалоговое окно "Select an Application"; дальше можно легко и удобно найти IDE WebStorm по пути: `~/opt/WebStorm-141.456/bin/webstorm.sh`

- **Шаг девятый** - в поле "Icon" добавляем фирменную иконку приложения WebStorm (_чтобы легко углядеть WebStorm на Desktop_); снова жмем на значок (уже в поле "Icon"); откроется диалоговое окно "Select an Icon"; в этом окне в выпадающем списке поля "Select icon from" выбираем самую нижнюю строку - "Image Files"; снова идем по пути `~/opt/WebStorm-141.456/bin/webide.png`

Если все шаги выполнены правильно, то в результате должно получиться примерно такое окно с заполненными полями:

![Create Launcher Ready]({{site.url}}/images/uploads/2016/04/create-launcher-ready.png 'Create Launcher Ready')

Это минимальная конфигурация, достаточная для нормального запуска приложения из Desktop. При первом запуске WebStorm-приложения Linux-система задаст вопрос - сделать ли запускаемый файл _исполняемым_. Естественно, соглашаемся - ведь нам нужно запустить и работать в WebStorm-приложении.

Как я уже упоминал ранее, установка двух других IDE - Aptana Studio и Visual Studio Code ничем не отличается от установки WebStorm. Единственный момент - для Visual Studio Code нужно покопаться с поисках фирменной иконки, которая расположена по пути: `~/opt/VSCode-linux-x64/resources/app/resources/linux/code.png`, а исполняемый файл приложения - по пути: `~/opt/VSCode-linux-x64/code`.

К слову сказать, лично я был приятно удивлен Visual Studio Code и разочарован Aptana Studio. WebStorm - вне конкуренции!

## WebStorm темы

Хочу немного отклониться в сторону выбора темы оформления под IDE WebStorm. В Sublime Text это была однозначно - [Material Theme](https://github.com/equinusocio/material-theme 'Material Theme').

Под WebStorm есть порт этой темы - [Material Theme JetBrains](https://github.com/ChrisRM/material-theme-jetbrains 'Material Theme JetBrains').

Документация хорошо расписана и автор даже постарался создать возможность легкой и "кошерной" установки темы - через репозиторий JetBrains, из самого WebStorm.

Но, как мне кажется, эта тема заметно уступает своему "оригиналу" из-под Sublime Text (автор сам об этом [упоминает](https://github.com/ChrisRM/material-theme-jetbrains#contribution 'Material Theme JetBrains')).

Хорошая коллекция тем под WebStorm расположена по этим адресам:

- [Color Themes for WebStorm](http://color-themes.com/?view=index 'Color Themes for WebStorm')
- [11 тем для WebIDE (PHPStorm & WebStorm)](https://habrahabr.ru/sandbox/36027/ '11 тем для WebIDE (PHPStorm & WebStorm)')
- [PHPStorm Themes](http://www.phpstorm-themes.com/ 'PHPStorm Themes')

В дополнение можно еще установить модный шрифт [Hack](http://sourcefoundry.org/hack/) (_на любителя_). Или покопаться здесь - [Top 11 Programming Fonts](http://wesbos.com/programming-fonts/ 'Top 11 Programming Fonts'), чтобы выбрать что-то подходящее.

К примеру, автор блога [WesBos](http://wesbos.com/ 'WesBos') долго пользовался OpenSource-шрифтом [Inconsolata](http://www.levien.com/type/myfonts/inconsolata.html 'Inconsolata'), а потом взял и [купил](http://wesbos.com/uses/ 'WesBos - Uses') шрифт [Operator Mono](http://www.typography.com/fonts/operator/overview/ 'Operator Mono') за \$200.

### PS

Еще в тему установки программных пакетов для разработки под системой Linux стоит сказать, что под Ubuntu существует удобный пакет [Ubuntu Make](https://wiki.ubuntu.com/ubuntu-make title="Ubuntu Make") (_он же Ubuntu Developer Tools Center в прошлом_).

Задача пакета Ubuntu Make - **быстрая и легкая установка** общих потребностей разработчика в Ubuntu. Ubuntu Make может устанавливать:

- [Android Studio](https://developer.android.com/sdk/index.html 'Android Studio')
- [PyCharm Community Edition](http://jetbrains.ru/products/pycharm/ 'PyCharm Community Edition')
- [IntelliJ Idea Community Edition](https://www.jetbrains.com/idea/download/#section=linux 'IntelliJ Idea Community Edition')
- и многие другие IDE.

На Хабрахабр есть небольшая обзорная статья об этом пакете - [Ubuntu Make — разработчику в помощь](https://habrahabr.ru/post/248249/ 'Ubuntu Make — разработчику в помощь').

Лично от себя могу сказать, что первый раз установка WebStorm при помощи Ubuntu Make на моем ноутбуке с Linux Mint 17.2 прошла "на ура".

А вот во-второй раз что-то не заладилось и Ubuntu Make "не хочет" ставить WebStorm - выдает какую-то ошибку, с которой мне нет желания разбираться.

---

На этом все.
