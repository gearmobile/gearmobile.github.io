---
title: "Знакомимся с Pixel Perfect"
layout: post
categories: web-development
tags: [pixel perfect]
share: true
---

> Обзор плагинов и скриптов для работы в технике Pixel Perfect.

Для начала - что такое техника Pixel Perfect? Все просто и можно догадаться по названию - это техника верстки, при которой сверстанный HTML-шаблон в точности (пиксель-в-пиксель) совпадает с оригиналом, PSD-макетом.

Другими словами, если наложить "картинку" сверстанного HTML-шаблона на картинку оригинального PSD-макета, то обе картинки должны совпасть. Совместиться должны все элементы картинок - текст, изображения, графические элементы.

По современным требованиям к верстке Pixel Perfect уже чуть ли не стандарт де-факто. Так что изучить этот вопрос жизненно необходимо, если есть желание и стремление иметь много заказов и заказчиков.

На момент написания статьи реализация техники Pixel Perfect осуществляется при помощи соответствующих плагинов под браузеры или же с помощью специализированных скриптов. Ниже будут кратко рассмотрены два плагина и два скрипта, однако во всех случаях шаги для проверки Pixel Perfect одинаковы.

Первоначально в программе Photoshop оригинальный PSD-макет сохраняется как изображение в формате `.png`. Затем в браузере открывается сверстанный по этому макету HTML-шаблон. При помощи плагина PNG-копия макета накладывается на сверстанную страницу. И становится видна разница в расположении элементов на HTML-странице и на PNG-копии.

В этом и заключается вся несложная процедура Pixel Perfect проверки сверстанной страницы. Там, где на странице элементы не совпадают с оригиналом, производится коррекция значений в файлах стилей.

## Pixel Perfect под Firefox

Для браузера Firefox имеется плагин [Pixel Perfect][1] для одноименной проверки сверстанной страницы.

После установки плагина Pixel Perfect его значок появиться в панели инструментов браузера Firefox. Стоит сказать, что плагин Pixel Perfect *поддерживает только последние версии браузера Firefox* (к примеру, в версии v.31 этот плагин не будет работать).

Теперь нужно открыть в Photoshop оригинальный PSD-макет и сохранить его целиком как изображение в формате `.png` через "Save for Web…".

**Важно!** Перед экспортом в PNG-изображение PSD-макет необходимо **привести к оригинальному размеру**! Для этого в Photoshop зарезервирована комбинация hotkeys: <kbd>Ctrl+1</kbd> - под Windows\Linux, <kbd>Cmd+1</kbd> - под Mac OS X.

Как только PNG-копия PSD-макета подготовлена и сохранена, открываем в окне браузера Firefox сверстанную по этому макету HTML-страницу.

Запускаем плагин Pixel Perfect щелчком мыши по его иконке в панели инструментов браузера. Сразу же появится окно плагина, в котором он предложит нам выбрать заранее подготовленное PNG-изображение (копию PSD-макета):

![Pixel Perfect Add Layer]({{site.url}}/images/uploads/2015/04/pixel_perfect_01.png "Pixel Perfect Add Layer")

Жмем на кнопку "Add Layer", выбираем подготовленное PNG-изображение и получаем результат - наложение двух слоев (сверстанного и оригинального):

![Pixel Perfect Compare Layers]({{site.url}}/images/uploads/2015/04/pixel_perfect_02.png "Pixel Perfect Compare Layers")

Видим, как не совпадают текст и кнопка HTML-страницы c PNG-оригиналом. Поэтому открываем в Firebug (этот плагин активируется автоматически при запуске плагина Pixel Perfect) вкладку со стилями и начинаем правку\подгонку:

![Pixel Perfect Correct CSS Styles]({{site.url}}/images/uploads/2015/04/pixel_perfect_03.png "Pixel Perfect Correct CSS Styles")

Обратите внимание на режим "Invert" плагина Pixel Perfect - с помощью него можно очень точно корректировать элементы HTML-страницы.

В описанном выше процессе и заключается работа с плагином Pixel Perfect, а также Pixel Perfect верстка как таковая. Все предельно просто.

Ниже приведен видео-ролик, в котором показан процесс работы с плагином Pixel Perfect (видео не мое, поэтому за качество во всех смыслах ответственности не несу) - для наглядности работы пойдет:

<iframe width="560" height="315" src="https://www.youtube.com/embed/E9R-dhu2g_E" frameborder="0"> </iframe>

Рассмотрение плагина Pixel Perfect под браузер Firefox закончено.

## PerfectPixel под Google Chrome

Плагин [PerfectPixel][2] под браузер Chrome очень похож по назначению и функционалу (и названию!) на плагин Pixel Perfect под браузер Firefox.

После установки PerfectPixel необходимо зайти в настройки расширений браузера Chrome - [chrome://extensions/](chrome://extensions/) и активировать для плагина галочку "Allow access to  file URLs", тем самым разрешив плагину доступ к локальным HTML-страницам:

![PerfectPixel Activate]({{site.url}}/images/uploads/2015/04/perfectpixel_01.png "PerfectPixel Activate")

**Важно!** Перед экспортом в PNG-изображение PSD-макет необходимо **привести к оригинальному размеру**! Для этого в Photoshop зарезервирована комбинация hotkeys: <kbd>Ctrl+1</kbd> - под Windows\Linux, <kbd>Cmd+1</kbd> - под Mac OS X.

После этого запускаем плагин PerfectPixel, добавляем в нем новый слой (PNG-копию оригинала) и проверяем:

![PerfectPixel Work]({{site.url}}/images/uploads/2015/04/perfectpixel_02.png "PerfectPixel Work")

Функционал и работа плагина PerfectPixel ничем не отличается от функционала и работы плагина Pixel Perfect.

Ниже приведен видео-ролик с официальной страницы плагина PerfectPixel для демонстрации работы в нем:

<iframe width="560" height="315" src="https://www.youtube.com/embed/jxzcKRRgfCg" frameborder="0"> </iframe>

Рассмотрение плагина PerfectPixel можно на этом закончить.

## X-Precise

Если в двух предыдущих случаях были рассмотрены бесплатные плагины под два популярных браузера Firefox и Chrome, то в данном случае речь пойдет о платном ($5 на момент написания статьи) скрипте [X-Precise][3], написанном на JavaScript и использующем библиотеку jQuery.

### Подключение X-Precise

Для того, чтобы получить наложение картинки-оригинала на сверстанную страницу нужно подключить скрипт X-Precise к этой странице. Для этого необходимо скачать архив X-Precise.

Затем нужно распаковать папку `_xprecise`в корневую директорию проекта. И подключить скрипт `xprecise.min.js` к HTML-странице для запуска интерсейса скрипта X-Precise.

Обратите внимание, что скрипт для своей работы использует библиотеку jQuery (v1.3.2), поэтому подключение X-Precise должно выглядеть таким образом:

{% highlight html %}
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js" type="text/javascript"></script>
<script src="_xprecise/xprecise.min.js" type="text/javascript"></script>
{% endhighlight %}

Затем нужно создать копии PSD-оригиналов в формате JPG и сохранить под тем же именем, что и файл оригинала в директории `/_xprecise/` скрипта X-Precise.

При сохранении в формате JPG рекомендуется выбирать режим оттенков серого, так как при таком варианте лучше видна разница между сверстанной копией и оригиналом (помните об опции "Invert" плагина Pixel Perfect?).

Скрипт X-Precise попытается автоматически загрузить JPG-изображение из директории `/_xprecise/` по имени файла этого изображения, считая, что имя файла иображения идентично имени файла открытой HTML-страницы (index.html -> index.jpg).

Но это не означает, что нельзя загрузить файл изображения с другим именем. Для этого достаточно задать другой путь к файлу в интерфейсе скрипта X-Precise.

### Использование X-Precise

Основным достоинством скрипта X-Precise является его способность автоматически запоминать и хранить все настройки.

В целом, интерфейс скрипта X-Precise и его применение ничем не отличается от плагинов Pixel Perfect или PerfectPixel. Для желающих - можно ознакомиться со скриншотами по [ссылке][4] на главной странице проекта.

## pixLayout

pixLayout - еще один плагин (наподобие X-Precise) под библиотеку jQuery, предназначенный для попиксельной верстки. Однако, в отличие от предыдущего скрипта, pixLayout бесплатный (интересная особенность - скрипт создан отечественным разработчиком).

Для своей работы скрипт pixLayout может использовать изображение в двух популярных форматах - JPG или PNG.

Домашняя страничка проекта расположена здесь - [pixLayout][5]. Скрипт прекрасно документирован как на родном (русском), так и на языке Уильяма Шекспира. Полюбоваться и поиграться можно на демо-страничке скрипта - [pixLayout Test][6].

Для подключения к тестируемой странице необходимо прописать базовый набор строк:

{% highlight html %}
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript" src="jquery.pixlayout.js"></script>
<script type="text/javascript">
  $(function(){
    $.pixlayout("/path_to_picture/picture.ext");
  });
</script>
{% endhighlight %}

Можно дополнить базовый набор, указав в скрипте параметры (*взято с официального сайта*):

{% highlight javascript %}
$(function(){
  $.pixlayout({
    src: "/img/layout.jpg",
    opacity: 0.8,
    top: 50,
    center: true,
    clip: true,
    show: true
  }, ".wrapper");
});
{% endhighlight %}

### Краткая справка по использованию скрипта pixLayout

Краткая справка по использованию скрипта pixLayout приведена в двух абзацах ниже (*также взята с официального сайта*):

#### Перемещение

  * кнопки: 'влево', 'вправо', 'вверх', 'вниз'
  * кнопки: <kbd>W</kbd>, <kbd>A</kbd>, <kbd>S</kbd>, <kbd>D</kbd>, когда картинка видима
  * кнопки панели навигации

#### Операции

  * **Уничтожить** (*удалить весь html и css код pixLayout со страницы*) - крестик в правом верхнем углу панели;
  * **Закрепить панель** - иконка в правом верхнем углу панели;
  * **Краткая справка** - знак вопроса в правом верхнем углу панели;
  * **Свернуть параметры** - стрелка "вверх"" внизу панели;
  * **Показать\убрать картинку** - центральная кнопка панели навигации или <kbd>Shift + E</kbd>.

Ниже приведено официальное видео, демонстрирующее работу со скриптом pixLayout:

<iframe width="560" height="315" src="https://www.youtube.com/embed/mc2d7xT-alo" frameborder="0"> </iframe>

## Заключение

В этом небольшом обзоре мы познакомились с четырьмя инструментами для попиксельной (pixel perfect) верстки. Два из них - это бесплатные плагины под браузеры. Другие два - скрипты на JavaScript для подключения к HTML-странице.

Что выбирать для своей работы - решать каждому.

В пользу плагинов под браузеры можно сказать, что они бесплатные, их легко установить и просто использовать.

В минус скрипту X-Precise можно сказать, что он платный ($5), требует подключения к проверяемой HTML-странице и зависит от библиотеки jQuery. В минус pixLayout также можно сказать, что для своей работы он требует дополнительной "возни" с подключением к HTML-странице.

Однако в плюс обоим скриптам можно привести тот неоспоримый факт, что это кроссбраузерное решение, абсолютно не зависящее от какого-либо браузера (Firefox, Chrome, Opera, Safari) или версии конкретного браузера. Скрипты будут работать одинаково во всех случаях.

На этом все.

***
[1]: https://addons.mozilla.org/ru/firefox/addon/pixel-perfect/ "Pixel Perfect"
[2]: https://chrome.google.com/webstore/detail/perfectpixel-by-welldonec/dkaagdgjmgdmbnecmcefdhjekcoceebi "PerfectPixel"
[3]: http://codecanyon.net/item/xprecise/78685 "X-Precise"
[4]: http://codecanyon.net/theme_previews/78685-xprecise?index=0&url_name=xprecise "X-Precise Screenshots"
[5]: http://pixlayout.polycreative.ru/ "pixLayout"
[6]: http://pixlayout.polycreative.ru/test.html "pixLayout Test"