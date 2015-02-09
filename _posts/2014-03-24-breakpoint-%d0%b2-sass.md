---
title: Медиа-запросы Breakpoint в Sass
author: gearmobile
layout: post
permalink: /breakpoint-%d0%b2-sass/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 20
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - breakpoint
  - sass
---
Прочитал одну статью, посвященную проблеме создания кода в CSS и Sass. Статья мне чрезвычайно понравилась &#8211; можно даже сказать, я был в восхищении о нее и от того, что написал ее автор. В ней вкратце описывались основные &#8220;опорные&#8221; моменты при написании кода в CSS/Sass. Одним из таких &#8220;опорных&#8221; моментов упоминались Breakpoint в Sass. Так как я большой поклонник этого препроцессора, то мне интересны все вопросы, связанные с ним. Поэтому мимо такой технологии, как Breakpoint &#8211; я просто не мог пройти мимо.

Итак, давайте знакомиться с Breakpoint в препроцессоре Sass. Прежде всего, Breakpoint &#8211; это расширение (модуль) для хорошо известной и популярной библиотеки-фреймворка Compass. Создан он двумя web-разработчиками Mason Wendell и Sam Richard. Основная идея и цель создания этого модуля &#8211; **сократить к одной строке создание медиа-запроса** и **возможность задавать для медиа-запросов осмысленные имена**.

### Установка модуля Breakpoint

Первое, что необходимо сделать, это установить в систему сам модуль `breakpoint`. Делается это обычной командой Ruby-окружения:

<pre>gem install breakpoint</pre>

Но тут могут быть несколько подводных камней, с которыми лично мне пришлось столкнуться (не знаю, как уж читателям). Первое &#8211; если у вас уже установлены `sass` и `compass` обычным способом, через команды:

<pre>gem install sass
gem install compass
</pre>

&#8230; то велика вероятность, что у вас в системе стоят Sass версии 3.2.18 и Compass версии 0.12.4. Поверить этот факт можно командой в терминале:

<pre>gem list</pre>

Однако, на момент написания статьи разрабатывается библиотека Compass под версией `1.0.0.alpha.19`, которую уже можно использовать несмотря на ее экспериментальный вид. Более того, модуль `breakpoint` совместим только с библиотекой Compass этой версии (1.0.0.alpha.19).

Поэтому, при запуске команды:

<pre>gem install breakpoint</pre>

&#8230; будет произведено автоматическое обновление пакетов `sass` и `compass` до версий Sass 3.3.4 и Compass 1.0.0.alpha.19. После успешной установки модуля `breakpoint` можно создать через Compass новый проект, указав при этом, что в проекте требуется поддержка (required) модуля `breakpoint`:

<pre>compass create newProject -r breakpoint</pre>

Заходим в созданную директорию и пробуем запустить Compass на мониторинг изменений во всех файлах проекта. Но не тут то было:<figure id="attachment_1067" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/sass_wdm-600x347.png" alt="Ошибка при запуске библиотеки Compass - нет модуля wdm" width="600" height="347" class="size-medium wp-image-1067" />][1]<figcaption class="wp-caption-text">Ошибка при запуске библиотеки Compass &#8211; нет модуля wdm</figcaption></figure> 

Compass пишет в терминале, что ему не хватает модуля `wdm` и не запускается в режим мониторинга. Что такое `wdm`, я не знаю (я не Ruby-разработчик), но подозреваю, что это какой-то модуль. И его придется установить.

Для этого необходимо скачать с оф. сайта Ruby пакет разработчика Development Kit (Device). Мною скачивалась версия `DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe`. Ее нужно распаковать в любое (постоянное) место &#8211; папку, но при этом не туда же, где уже стоит у вас Ruby. Затем в терминале зайти в эту папку и запустить последовательно три команды (не обращая внимание, что они там пишут в ответ):

<pre>ruby dk.rb init
ruby dk.rb review
ruby dk.rb install
</pre><figure id="attachment_1069" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/ruby_devkit-600x347.png" alt="Установка пакета DevKit" width="600" height="347" class="size-medium wp-image-1069" />][2]<figcaption class="wp-caption-text">Установка пакета DevKit</figcaption></figure> 

А затем в этом же терминале снова запустить установку загадочного (для меня) модуля `wdm`:

<pre>gem install wdm</pre>

После этого процесс пройдет успешно и Compass, наконец-то, &#8220;заткнется&#8221; и станет делать то, что от него требуют &#8211; мониторинг содержимого папки:<figure id="attachment_1068" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/sass_install_wdm-600x347.png" alt="Успешная установка пакета wdm" width="600" height="347" class="size-medium wp-image-1068" />][3]<figcaption class="wp-caption-text">Успешная установка пакета wdm</figcaption></figure> 

Теперь открывает уже созданный Compass файл `screen.scss` и дописываем в его начало строчку:

<pre>@import "breakpoint";</pre>

&#8230; говоря те самым, что в наш проект необходимо включить модуль `breakpoint`. Если проект создавался не с нуля, а уже был готовым, то поддержку Breakpoint в него можно добавить, дописав в конфигурационный файл `config.rb` строчку:

<pre>require 'breakpoint'</pre>

### Дальнейшее знакомство с Breakpoint

Можно приступать к дальнейшему знакомству с Breakpoint.

Breakpoint &#8211; дословно с английского языка переводится как &#8220;опорная точка&#8221;. Медиа-запросы фактически и являются такими опорными точками. В правилах CSS мы указываем браузеру &#8211; при ширине *viewport* равной 480px сделать такой-то элемент таким-то; а при ширине *viewport* равной 768px сделать такой элемент другим! То есть, мы через CSS-правила определяем для браузера подобные опорные точки. Модуль Breakpoint позволяет создавать опорные точки в коде SCSS с помощью одной строки &#8211; через миксин (mixin) **breakpoint**.

Простейший пример применения миксина **breakpoint** приведен ниже:

<pre>$high-tide: 500px;

.johnny-utah {
  @include breakpoint($high-tide) {
    content: 'Whoa.';
  }
}
</pre>

То есть, сначала инициализируется переменная `$high-tide` со значением 500px. Затем селектору класса `.johnny-utah` задается CSS-правило через подключение миксина `@include breakpoint`, аргументом которому передается значение переменной `$high-tide`. В теле миксина пишется, что нужно сделать браузеру &#8211; создать контент `Whoa.` (в данном случае).

Результатом генерации в CSS будет следующий код:

<pre>@media (min-width: 500px) {
  .johnny-utah {
    content: 'Whoa.';
  }
}
</pre>

Предельно просто! ОК, немного усложним задачу и продвинемся дальше, чтобы на примере лучше понять, что из себя представляют Breakpoint:

<pre>$bkpt-login-small: 370px;
$bkpt-login-medium: 490px;
$bkpt-login-large: 865px;

body{
  background-color: hsl(0,100%,25%);
}

@include breakpoint($bkpt-login-small){
  body{
    background-color: hsl(30,100%,50%);
  }
}

@include breakpoint($bkpt-login-medium){
  body{
    background-color: hsl(60,100%,50%);
  }
}

@include breakpoint($bkpt-login-large){
  body{
    background-color: hsl(120,100%,50%);
  }
}
</pre>

Здесь мы создали три переменные `$bkpt-login-small`, `$bkpt-login-medium`, `$bkpt-login-large` с помощью которых установили три опорные точки для адаптивного дизайна. А затем в SCSS-правилах через подключение миксина `@include breakpoint` для каждой опорной точки задаем правило для элемента `body`, последовательно указывая этому миксину переменные в качестве аргументов. Результат работы этого кода приводить не буду &#8211; вы можете сами набрать его в редакторе и проверить!

### Варианты аргументов миксина Breakpoint

Миксин `breakpoint` в качестве аргумента может принимать **не только одно значение**, как в примере выше.

#### Два числа в качестве значений

Переменной можно задать **два числа в качестве значений**:

<pre>$ex-presidents: 600px 800px;</pre>

В этом случае модуль Breakpoint автоматически распознает и преобразует их в пару значений **min-width/max-width**:

<pre>.nixon {
   @include breakpoint($ex-presidents) {
   content: 'Ex-Presidents';
   }
 }

@media (min-width: 600px) and (max-width: 800px) {
   .nixon {
     content: 'Ex-Presidents';
   }
 }
</pre>

#### Имя и значение этого имени

Переменной можно задать **имя и значение этого имени**:

<pre>$surfboard-width: max-width 1000px;</pre>

Модуль Breakpoint распознает его следующим образом:

<pre>.johnson {
   @include breakpoint($surfboard-width) {
     content: 'Surfboard Width';
   }
 }

 @media (max-width: 1000px) {
   .johnson {
     content: 'Surfboard Width';
   }
 }
</pre>

#### Расширенный вариант имени и значения

И можно пойти еще дальше:

<pre>$surfboard-height: (min-height 1000px) (orientation portrait);</pre>

Breakpoint воспримет это таким образом:

<pre>.carter {
   @include breakpoint($surfboard-height) {
     content: 'Surfboard Height, Portrait';
   }
 }

@media (min-height: 1000px) and (orientation: portrait) {
   .carter {
     content: 'Surfboard Height, Portrait';
   }
 }
</pre>

### Настройки модуля Breakpoint

Модуль Breakpoint имеет совсем немного настроек, которые выражаются **в четырех переменных**, которые можно легко переопределить в рамках разрабатываемого проекта:

  * **$breakpoint-default-media** &#8211; **тип медиа-запроса**. По умолчанию его значение равно &#8220;**all**&#8220;, то есть медиа-запрос применим ко всем типам устройств: мониторы, телефизоры и так далее.
  * **$breakpoint-default-feature** &#8211; по умолчанию установлено в значение &#8220;**min-width**&#8221; как наиболее часто используемое на практике. То есть, это запрашиваемая **характеристика типа устройства**.
  * **$breakpoint-default-pair** &#8211; установлено в значение **min-width/max-width** по умолчанию. То есть, при передаче миксину `breakpoint` пары чисел (к примеру &#8211; 400px и 500px) он распознает их как **min-width: 400px** и **max-width: 500px**.
  * **$breakpoint-to-ems** &#8211; по умолчанию установлено в значение **false**. Если перевести этот параметр в значение **true**, то при передаче миксину `breakpoint` аргументов в любых единицах измерения (px, pt, %) они будут автоматически переконвертированы в **em**! Круто!

Чтобы не быть голословным, приведу пример настройки последнего параметра &#8211; **$breakpoint-to-ems**:<figure id="attachment_1070" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/breakpoint-to-ems-600x384.png" alt="Параметр модуля Breakpoints - breakpoint-to-ems" width="600" height="384" class="size-medium wp-image-1070" />][4]<figcaption class="wp-caption-text">Параметр модуля Breakpoints &#8211; breakpoint-to-ems</figcaption></figure> 

Авторами модуля Breakpoint была сделана еще одна дополнительная &#8220;плюшка&#8221; &#8211; поддержка кроссбраузерности для экранов повышенного разрешения (так называемых Retina-экранов). Чтобы не писать по отдельности медиа-запрос для каждого из движков браузеров:

<pre>-webkit-device-pixel-ratio
-moz-device-pixel-ratio
-o-device-pixel-ratio
</pre>

&#8230; можно писать краткий медиа-запрос:

<pre>device-pixel-ratio</pre>

&#8230; который преобразует полученное браузером значение в стандартное разрешение экрана.

### Заключение

Перечисленные возможности модуля Breakpoint являются основными, [но не единственными][5]. Однако, как мне кажется, этих основных возможностей хватит для 90% случаев на практике. Если же кто желает углубить свои познания в модуле Breakpoint, это легко можно сделать на оф. сайте проекта.

При написании этой статьи активно использовались два бесценных источника (*а примеры кода вообще были скопированы оттуда самым наглым образом*):

  * [INTRODUCING BREAKPOINT; MEDIA QUERIES MADE EASY][6]
  * [Breakpoint Really Simple, Organized, Media Queries with Sass][7]

Очень вольный перевод и компиляция этих двух статей была сделана с энтузиазмом и на одном дыхании. ))

Оцените статью:  
<span id="post-ratings-1065" class="post-ratings" data-nonce="99d0ea7811"><img id="rating_1065_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1065, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1065_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1065, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1065_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1065, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1065_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1065, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1065_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1065, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1065_text"></span></span><span id="post-ratings-1065-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/03/sass_wdm.png
 [2]: http://localhost:7788/third/wp-content/uploads/2014/03/ruby_devkit.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/03/sass_install_wdm.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/03/breakpoint-to-ems.png
 [5]: http://breakpoint-sass.com/#advanced "Breakpoint - Advanced Features"
 [6]: http://snugug.com/musings/introducing-breakpoint-media-queries-made-easy "INTRODUCING BREAKPOINT; MEDIA QUERIES MADE EASY"
 [7]: http://breakpoint-sass.com/ "Breakpoint Really Simple, Organized, Media Queries with Sass"