---
title: "Медиа-запросы Breakpoint в Sass"
layout: post
categories: css
tags: [breakpoint, sass, css]
share: true
---

Прочитал одну статью, посвященную проблеме создания кода в CSS и Sass. Статья мне чрезвычайно понравилась - можно даже сказать, я был в восхищении о нее и от того, что написал ее автор. В ней вкратце описывались основные "опорные" моменты при написании кода в CSS/Sass. Одним из таких "опорных" моментов упоминались Breakpoint в Sass. Так как я большой поклонник этого препроцессора, то мне интересны все вопросы, связанные с ним. Поэтому мимо такой технологии, как Breakpoint - я просто не мог пройти мимо.

Итак, давайте знакомиться с Breakpoint в препроцессоре Sass. Прежде всего, Breakpoint - это расширение (модуль) для хорошо известной и популярной библиотеки-фреймворка Compass. Создан он двумя web-разработчиками Mason Wendell и Sam Richard. Основная идея и цель создания этого модуля - **сократить к одной строке создание медиа-запроса** и **возможность задавать для медиа-запросов осмысленные имена**.

## Установка модуля Breakpoint

Первое, что необходимо сделать, это установить в систему сам модуль `breakpoint`. Делается это обычной командой Ruby-окружения:

{% highlight powershell %}
gem install breakpoint
{% endhighlight %}

Но тут могут быть несколько подводных камней, с которыми лично мне пришлось столкнуться (не знаю, как уж читателям). Первое - если у вас уже установлены `sass` и `compass` обычным способом, через команды:

{% highlight powershell %}
gem install sass
gem install compass
{% endhighlight %}

... то велика вероятность, что у вас в системе стоят Sass версии 3.2.18 и Compass версии 0.12.4. Поверить этот факт можно командой в терминале:

{% highlight powershell %}
gem list
{% endhighlight %}

Однако, на момент написания статьи разрабатывается библиотека Compass под версией `1.0.0.alpha.19`, которую уже можно использовать несмотря на ее экспериментальный вид. Более того, модуль `breakpoint` совместим только с библиотекой Compass этой версии (1.0.0.alpha.19).

Поэтому, при запуске команды:

{% highlight powershell %}
gem install breakpoint
{% endhighlight %}

... будет произведено автоматическое обновление пакетов `sass` и `compass` до версий Sass 3.3.4 и Compass 1.0.0.alpha.19. После успешной установки модуля `breakpoint` можно создать через Compass новый проект, указав при этом, что в проекте требуется поддержка (required) модуля `breakpoint`:

{% highlight powershell %}
compass create newProject -r breakpoint
{% endhighlight %}

Заходим в созданную директорию и пробуем запустить Compass на мониторинг изменений во всех файлах проекта. Но не тут то было:

![Ошибка при запуске библиотеки Compass - нет модуля wdm]({{site.url}}/images/uploads/2014/03/sass_wdm.png)

Compass пишет в терминале, что ему не хватает модуля `wdm` и не запускается в режим мониторинга. Что такое `wdm`, я не знаю (я не Ruby-разработчик), но подозреваю, что это какой-то модуль. И его придется установить.

Для этого необходимо скачать с оф. сайта Ruby пакет разработчика Development Kit (Device). Мною скачивалась версия `DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe`. Ее нужно распаковать в любое (постоянное) место - папку, но при этом не туда же, где уже стоит у вас Ruby. Затем в терминале зайти в эту папку и запустить последовательно три команды (не обращая внимание, что они там пишут в ответ):

{% highlight powershell %}
ruby dk.rb init
ruby dk.rb review
ruby dk.rb install
{% endhighlight %}

![Установка пакета DevKit]({{site.url}}/images/uploads/2014/03/ruby_devkit.png)

А затем в этом же терминале снова запустить установку загадочного (для меня) модуля `wdm`:

{% highlight powershell %}
gem install wdm
{% endhighlight %}

После этого процесс пройдет успешно и Compass, наконец-то, "заткнется" и станет делать то, что от него требуют - мониторинг содержимого папки:

![Успешная установка пакета wdm]({{site.url}}/images/uploads/2014/03/sass_install_wdm.png)

Теперь открывает уже созданный Compass файл `screen.scss` и дописываем в его начало строчку:

{% highlight css %}
@import "breakpoint";
{% endhighlight %}

... говоря те самым, что в наш проект необходимо включить модуль `breakpoint`. Если проект создавался не с нуля, а уже был готовым, то поддержку Breakpoint в него можно добавить, дописав в конфигурационный файл `config.rb` строчку:

{% highlight css %}
require 'breakpoint'
{% endhighlight %}

## Дальнейшее знакомство с Breakpoint

Можно приступать к дальнейшему знакомству с Breakpoint.

Breakpoint - дословно с английского языка переводится как "опорная точка". Медиа-запросы фактически и являются такими опорными точками. В правилах CSS мы указываем браузеру - при ширине `viewport` равной 480px сделать такой-то элемент таким-то; а при ширине `viewport` равной 768px сделать такой элемент другим! То есть, мы через CSS-правила определяем для браузера подобные опорные точки. Модуль Breakpoint позволяет создавать опорные точки в коде SCSS с помощью одной строки - через миксин (mixin) `breakpoint`.

Простейший пример применения миксина `breakpoint` приведен ниже:

{% highlight css %}
$high-tide: 500px;

.johnny-utah {
  @include breakpoint($high-tide) {
    content: 'Whoa.';
  }
}
{% endhighlight %}

То есть, сначала инициализируется переменная `$high-tide` со значением 500px. Затем селектору класса `.johnny-utah` задается CSS-правило через подключение миксина `@include breakpoint`, аргументом которому передается значение переменной `$high-tide`. В теле миксина пишется, что нужно сделать браузеру - создать контент `Whoa.` (в данном случае).

Результатом генерации в CSS будет следующий код:

{% highlight css %}
@media (min-width: 500px) {
  .johnny-utah {
    content: 'Whoa.';
  }
}
{% endhighlight %}

Предельно просто! ОК, немного усложним задачу и продвинемся дальше, чтобы на примере лучше понять, что из себя представляют Breakpoint:

{% highlight css %}
$bkpt-login-small: 370px;
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
{% endhighlight %}

Здесь мы создали три переменные `$bkpt-login-small`, `$bkpt-login-medium`, `$bkpt-login-large` с помощью которых установили три опорные точки для адаптивного дизайна. А затем в SCSS-правилах через подключение миксина `@include breakpoint` для каждой опорной точки задаем правило для элемента `body`, последовательно указывая этому миксину переменные в качестве аргументов. Результат работы этого кода приводить не буду - вы можете сами набрать его в редакторе и проверить!

## Варианты аргументов миксина Breakpoint

Миксин `breakpoint` в качестве аргумента может принимать **не только одно значение**, как в примере выше.

### Два числа в качестве значений

Переменной можно задать **два числа в качестве значений**:

{% highlight css %}
$ex-presidents: 600px 800px;
{% endhighlight %}

В этом случае модуль Breakpoint автоматически распознает и преобразует их в пару значений **min-width/max-width**:

{% highlight css %}
.nixon {
   @include breakpoint($ex-presidents) {
   content: 'Ex-Presidents';
   }
 }

@media (min-width: 600px) and (max-width: 800px) {
   .nixon {
     content: 'Ex-Presidents';
   }
 }
{% endhighlight %}

### Имя и значение этого имени

Переменной можно задать **имя и значение этого имени**:

{% highlight css %}
$surfboard-width: max-width 1000px;
{% endhighlight %}

Модуль Breakpoint распознает его следующим образом:

{% highlight css %}
.johnson {
   @include breakpoint($surfboard-width) {
     content: 'Surfboard Width';
   }
 }

 @media (max-width: 1000px) {
   .johnson {
     content: 'Surfboard Width';
   }
 }
{% endhighlight %}

### Расширенный вариант имени и значения

И можно пойти еще дальше:

{% highlight css %}
$surfboard-height: (min-height 1000px) (orientation portrait);
{% endhighlight %}

Breakpoint воспримет это таким образом:

{% highlight css %}
.carter {
   @include breakpoint($surfboard-height) {
     content: 'Surfboard Height, Portrait';
   }
 }

@media (min-height: 1000px) and (orientation: portrait) {
   .carter {
     content: 'Surfboard Height, Portrait';
   }
 }
{% endhighlight %}

## Настройки модуля Breakpoint

Модуль Breakpoint имеет совсем немного настроек, которые выражаются **в четырех переменных**, которые можно легко переопределить в рамках разрабатываемого проекта:

  * `$breakpoint-default-media` - **тип медиа-запроса**. По умолчанию его значение равно `all`, то есть медиа-запрос применим ко всем типам устройств: мониторы, телефизоры и так далее.
  * `$breakpoint-default-feature` - по умолчанию установлено в значение `min-width` как наиболее часто используемое на практике. То есть, это запрашиваемая **характеристика типа устройства**.
  * `$breakpoint-default-pair` - установлено в значение `min-width/max-width` по умолчанию. То есть, при передаче миксину `breakpoint` пары чисел (к примеру - 400px и 500px) он распознает их как `min-width: 400px` и `max-width: 500px`.
  * `$breakpoint-to-ems` - по умолчанию установлено в значение `false`. Если перевести этот параметр в значение `true`, то при передаче миксину `breakpoint` аргументов в любых единицах измерения (`px`, `pt`, `%`) они будут автоматически переконвертированы в `em`! Круто!

Чтобы не быть голословным, приведу пример настройки последнего параметра - **$breakpoint-to-ems**:

![Параметр модуля Breakpoints - breakpoint-to-ems]({{site.url}}/images/2014/03/breakpoint-to-ems.png)

Авторами модуля Breakpoint была сделана еще одна дополнительная "плюшка" - поддержка кроссбраузерности для экранов повышенного разрешения (так называемых Retina-экранов). Чтобы не писать по отдельности медиа-запрос для каждого из движков браузеров:

{% highlight css %}
-webkit-device-pixel-ratio
-moz-device-pixel-ratio
-o-device-pixel-ratio
{% endhighlight %}

... можно писать краткий медиа-запрос:

{% highlight css %}
device-pixel-ratio
{% endhighlight %}

... который преобразует полученное браузером значение в стандартное разрешение экрана.

## Заключение

Перечисленные возможности модуля Breakpoint являются основными, [но не единственными][1]. Однако, как мне кажется, этих основных возможностей хватит для 90% случаев на практике. Если же кто желает углубить свои познания в модуле Breakpoint, это легко можно сделать на оф. сайте проекта.

При написании этой статьи активно использовались два бесценных источника (*а примеры кода вообще были скопированы оттуда самым наглым образом*):

  * [INTRODUCING BREAKPOINT; MEDIA QUERIES MADE EASY][2]
  * [Breakpoint Really Simple, Organized, Media Queries with Sass][3]

Очень вольный перевод и компиляция этих двух статей была сделана с энтузиазмом и на одном дыхании.

---

 [1]: http://breakpoint-sass.com/#advanced "Breakpoint - Advanced Features"
 [2]: http://snugug.com/musings/introducing-breakpoint-media-queries-made-easy "INTRODUCING BREAKPOINT; MEDIA QUERIES MADE EASY"
 [3]: http://breakpoint-sass.com/ "Breakpoint Really Simple, Organized, Media Queries with Sass"
