---
title: "Режим эмуляции мобильных устройств в Chrome"
layout: post
categories: css
tags: [css, browser, emulate]
share: true
---

На сегодняшний день тестирование страниц становиться непростой задачей. Времена, когда проверка работоспособности сайта ограничивалась парой браузеров, давно прошли. Сегодня ваше творение необходимо тщательно проверять в целом диапазоне мобильных телефонов, планшетов и настольных систем с различными операционными системами, разрешениями экранов и возможностями. В особо серьезных случаях процесс тестирования может занять столько же времени, сколько и разработка проекта.

Процесс тестирования также усложняется благодаря устройствам с сенсорным экраном и мониторов с высоким разрешением. Если вы ведете разработку проекта на обычном PC с помощью таких же обычных мыши и клавиатуры, то вам будет трудно оценить работоспособность вашего кода в реальных условиях (на всех вышеперечисленных устройствах). Такая возможность, как событие мыши `hover` может не работать и ваше приложение становиться неработоспособным. Но тогда каким же образом можно протестировать программу и избежать при этом необходимости переключения между различными устройствами?

К счастью, сегодня выход из этой ситуации есть. В браузер Chrome версии 32 был добавлен **режим эмуляции**. С помощью него можно решить многие вышеназванные проблемы, не покидая комфортного окружения PC.

Первое, что необходимо сделать, это заполучить сам браузер Chrome v.32. Если последние шесть лет вы жили на обратной стороне Луны, то тогда вы можете сделать это по ссылке [google.com/chrome][1].

Запустите установленный Chrome, откройте в нем страницу, которую хотите протестировать и откройте **Developer Tools** (**Menu - Tools - Developer Tools**, <kbd>Cmd+Opt+I</kbd> на Mac или <kbd>F12/Ctrl+Shift+I</kbd> под Windows и Linux). Кликните мышью на значке-шестеренке **Settings** в правом верхнем углу окна браузера, затем откройте раздел **Overrides** для того, чтобы включить показ эмуляции в браузере - **Show Emulation view in console drawer** (*в версии 33 эта возможность активирована по умолчанию*):

![Режим Settings в браузере Chrome]({{site.url}}/images/uploads/2014/03/settings.png)

![Show Emulation view in console drawer]({{site.url}}/images/uploads/2014/03/emulation_show.png)

Закрываем окно **Settings** и открываем "Console Drawer" (это не тоже самое, что общая "Console") - для этого кликаем мышью на иконке (расположенной слева от иконки **Settings**) или нажав клавишу <kbd>Esc</kbd>. У вас должна открыться вкладка **Emulate** в "Console Drawer" (если этого не произошло, перезапустите браузер Chrome):

## Режим эмуляции - раздел Device

Раздел **Device** предоставляет несколько дюжин готовых предустановок для большинства популярных мобильных устройств, включая iPhone, iPad, Kindles, планшеты Nexus, смартфоны Samsung Galaxy и т. д. Выбор одного из устройств приводит к изменениям настроек в остальных разделах.

Выбираем из списка нужное устройство и жмем кнопочку "Emulate" внизу этого списка:

![Выбор эмулируемого устройства]({{site.url}}/images/uploads/2014/03/emulation_device.png)

> Обратите внимание! Инструкция, представленная выше, описывает включение режима эмуляции в стабильной версии v.32 браузера Chrome. Если вы используете последнюю версию браузера Chrome Canary, эта опция будет располагаться в разделе "Settings" во вкладке "General" под вкладкой "Appearance". (*прим. переводчика: кто не знает, браузер Chrome Canary - это самая свежая и нестабильная версия браузера Chrome.*)

![Режим эмуляции в Chrome Canary]({{site.url}}/images/uploads/2014/03/emulation_chrome_canary.png)

## Режим эмуляции - раздел Screen

В разделе **Screen** можно самостоятельно установить настройки экрана эмулируемого устройства:

  * **Resolution** - произвольный размер экрана устройства
  * **Device pixel ratio** - то есть для дисплеев Retina от Apple нужно ставит 2, чтобы производилось удваивание размера объектов в области просмотра
  * font-scaling factor (*прим. переводчика: неизвестный для меня параметр*)

![Настройка экрана в режиме эмуляции]({{site.url}}/images/uploads/2014/03/emulation_screen.png)

## Режим эмуляции - раздел User Agent

В этом разделе настраивается режим агента пользователя. То есть, устанавливается модель взаимодействия между эмулируемыми клиентом и сервером:

![Эмуляция агента пользователя]({{site.url}}/images/uploads/2014/03/emulation_user_agent.png)

## Режим эмуляции - раздел Sensors

В этом разделе настраивается режим эмуляции сенсорного экрана:

![Эмуляция сенсорного экрана устройства]({{site.url}}/images/uploads/2014/03/emulation_touch_screen.png)

В режиме эмуляции сенсорного экрана курсор мыши приобретает вид отпечатка пальца на экране устройства:

![Эмуляция отпечатка пальца на экране устройства]({{site.url}}/images/uploads/2014/03/emulation_touch_screen_finger.png)

Эмуляция multi-touch может быть выполнена при помощи зажатой клавиши <kbd>Shift</kbd> и движения мыши в нужную сторону. Этот режим задействует соответствующие JavaScript-события, такие как `touchstart`, `touchend`, `touchmove`. Также делается попытка полностью соответствовать мобильным браузерам благодаря реализации JavaScript-события `mouseover`, но это событие возникает только тогда, когда будет произведено "нажатие" на элемент интерфейса. Эмулятор корректно игнорирует событие `mouseover`, возникающее, когда курсор сенсорного устройства просто движется поверх элемента интерфейса.

## Возвращение браузера в обычный режим

Для того, чтобы завершить режим эмуляции и возвратиться в обычный режим просмотра, нужно перейти обратно в раздел **Device** и нажать кнопку <kbd>Reset</kbd>.

## Мне больше не нужны устройства

Рассмотренный выше эмулятор браузера Chrome является полезным инструментом, но он не может в точности реализовать поведение настоящих устройств с сенсорным экраном, во всех их тонкостях.

Стоит также обратить внимание, что эмулятор несовершенен в следующих вопросах:

  * вы можете столкнуть с некоторыми необъяснимыми ошибками в работе эмулятора
  * CSS-событие `:hover` все еще в действии и
  * для него нет механизма эмуляции; страница будет сгенерирована браузером Chrome вне зависимости от того, все ли устройства поддерживают возможности, заложенные в ней

Будем надеяться, что команда Google обратит внимание на эти недостатки и исправит их в последующих релизах.

Если подвести итог, то можно сказать, что режим эмуляции в браузере Google Chrome является простым и быстрым способом протестировать страницу, без необходимости проверки на реальных устройствах, таких как смартфоны или планшеты. Кроме того, у вас есть полный набор инструментов разработчика, что может сэкономить несколько часов вашего труда.

Автор статьи: Craig Buckler, [How to Use Mobile Emulation Mode in Chrome][2]

## От переводчика

Хочется от себя немного добавить в эту тему. В книге Б. Фрейна "HTML5 и CSS3. Разработка сайтов для любых браузеров и устройств" автор приводит краткий список плагинов для тестирования страниц в различных браузерах. Эти плагины не такие "продвинутые", как режим эмуляции в браузере Chrome. Их задача сводиться только к одному - проверке работоспособности страниц на экранах различных устройств, с разными размерами области просмотра. Цель такой проверки - создание полностью рабочего **адаптивного дизайна сайта**.

Для браузера Safari автор рекомендует расширение **Resize** или **ResizeMe**. Под браузер Mozilla Firefox имеется плагин **Firesizer**. А под браузер Google Chrome автором рекомендуется использовать расширение **Windows Resizer**.

Например, после установки и активизации расширения **Windows Resizer** под Chrome при щелчке мыши на иконке появиться окно с предустановленными размерами экранов устройств:

![Расширение Windows Resizer под Chrome]({{site.url}}/images/uploads/2014/03/windows-_resizer_chrome.png)

В дальнейших объяснениях работа с плагином не нуждается, как мне кажется.

На этом все.

---

[1]: google.com/chrome "Google Chrome"
[2]: http://www.sitepoint.com/use-mobile-emulation-mode-chrome/ "How to Use Mobile Emulation Mode in Chrome"