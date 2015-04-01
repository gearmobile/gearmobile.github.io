---
title: "LESS Hat - коллекция готовых mixin'ов под LESS"
layout: post
categories: css
tags: [css, less hat]
share: true
---

> Продолжение темы препроцессоров для CSS, которая для меня намного интереснее всех остальных.

На этот раз остановимся на препроцессоре LESS, ибо было бы странно рассказать о SASS (SCSS) и не упомянуть о не менее популярном его аналоге. Преимуществ у LESS столько же, сколько и недостатков.

Эта статья является моей попыткой на личном опыте познакомиться с LESS Hat и сравнить ее с Compass. Про сам LESS и его синтаксис я рассказывать не буду - это глупо, ибо документация для этого препроцессора прекрасно оформлена и переведена на русский язык на оф. сайте проекта.

Плюсы - этот препроцессор развивается более динамично, это более молодой проект. Синтаксис LESS интуитивно понятный и максимально приближен к CSS, поэтому новички могут освоить его совсем без труда. Документация для LESS гораздо более подробная, с примерами и переведена на множество языков, что облегчает его изучение (для SASS это серьезный недостаток, я сам с этим сталкиваюсь постоянно, когда изучаю Compass).

Ну и последний немаловажный момент, который оказывает существенное влияние на распространенность LESS, это тот факт, что он включен в состав модного и известного фреймворка Bootstrap. То есть, все компоненты этого фреймворка созданы с использованием данного препроцессора. А если учесть, что один из трех китов CMS - Joomla 3 - создана на Bootstrap, то можно только гадать, куда заведет этот процесс.

К недостаткам LESS лично я могу отнести такой факт, как большое время для компиляции (хотя на оф. сайте один из создателей Bootstrap отвечал на вопрос, что им выбран препроцессор LESS как раз из-за высокой скорости компиляции, ибо он написан на языке Javascript). Еще один момент в минус LESS - файл с расширением .less компилируется каждый раз при обращении к нему браузера.

В SASS производится создание файла `.css` из `.scss` "раз и навсегда", там не нужно что-то собирать на лету, а он уже готовый подключается в HTML-документ. И последнее - LESS не имеет на сегодня такой продвинутой библиотеки миксинов, как Compass для SASS (SCSS). Точнее - подобная библиотека уже есть и ее название [LESS Hat][1] (глупо было бы, если бы такая библиотека не появилась). Однако она уступает по своим возможностям Compass.

Итак, мы уже выяснили, что LESS Hat - аналог Compass под SASS (SCSS). Библиотека LESS Hat была создана командой, которая разработала плагин под Adobe Photoshop с названием [CSS Hat][1]. Этот плагин выполняет автоматизированные операции по переводу свойств любого элемента на psd-макете в свойства CSS.

То есть, он старается упростить и ускорить задачу верстальщика, которую тот обычно выполняет вручную. Плагин CSS Hat не бесплатный, цену его я не знаю (это нетрудно узнать) и сам им не пользовался ни разу, поэтому ничего не могу сказать по этому поводу.

Проект [LESS Hat][2] на сегодняшний момент является самой большой и популярной библиотекой готовых миксинов под препроцессор LESS. В отличие от плагина [CSS Hat][1], библиотека [LESS Hat][2] бесплатная для использования. На момент написания статьи самая свежая версия этой библиотеки - v2.0.7, которую я и забираю со страницы проекта для своих собственных экспериментов. Архивчик .zip весит около 200Kb, что прилично для подобной библиотеки. Но пугаться не стоит - из всего архива нам потребуется только один файлик, а все остальное - это сопутствующая информация. Если распаковать архив, то увидим следующий список файлов и папок:

{% highlight powershell %}
build\
  mixins\
  .gitignore
  .travis.yml
  bower.json
  Gruntfile.js
  LICENSE
  package.json
  README.md
  README-template.md
{% endhighlight %}

Первая папка `build` - самая нужная, там находятся два файла `lesshat.less` и `lesshat-prefixed.less` (не успел разобраться, для чего нужен этот файл), которые являются готовыми к использованию коллекциями LESS-миксинов.

Вторая папка `mixins` - также содержит всю коллекцию миксинов, но предназначена для разработчиков. Другими словами, если у вас есть соответствующая квалификация и желание что-то подправить в любом из миксинов, то вам сюда. Все остальные файлы можно смело пропустить, они для работы не нужны.

Теперь создаю шаблон для будущей площадки экспериментов под LESS и LESS Hat. Все как обычно - подключаю файл стилей в формате `.less` и файл для автоматической компиляции в CSS на лету - `less-1.3.3.min.js`.

Затем вытаскиваю из папки файлик lesshat.less и кидаю его в папочку `css`, где также расположен файл `style.less` (все до кучи). Кстати, сразу оговорюсь, что все файлы и пример в целом (для этой статьи) у меня крутился под управлением локального сервера XAMPP. С ним у меня отношения сложились с первого раза, в отличие от других популярных серверов, таких как OpenServer, Endels(Denwer), WAMP.

Файл `lesshat.less` подключаю к `style.less` через директиву `@import`. Как говориться в оф. документации к LESS, расширение `.less` можно и не указывать, но оставлю "как есть":

{% highlight css %}
...

/* Imports
------------------*/
@import "lesshat.less";

...
{% endhighlight %}

Все готово для того, чтобы опробовать библиотеку LESS Hat. Применю оттуда готовый миксин `.border-radius(10)` для создания скругленных углов у блока с помощью CSS-свойства `border-radius`. В документации к этому миксину говориться, что он может принимать значения без указания единиц измерения, так как допишет их сам (`px` по умолчанию).

Также вспомним функции для работы с цветами в LESS. И воспользуемся еще двумя миксинами из LESS Hat: `.background-image()` для создания градиентов у блока и `.box-shadow()` для придания внешней тени.

Рабочий файлик `style.less` получиться следующим:

{% highlight css %}
/* Imports
  ------------------*/
  @import "lesshat.less";

  /* Variables
  ------------------*/
  @width: 200px;
  @color: #778899;

  /* Block
  ------------------*/
  div{
    float: left;
    margin: 10px;
    text-align: center;
    width: @width;
    height: @width/2;
    .border-radius(10);
  }

  /* Colors
  ------------------*/
  .color{
    background-color: @color;
  }
  .lighten{
    background-color: lighten(@color, 20%);
  }
  .darken{
    background-color: darken(@color, 20%);
  }
  .saturate{
    background-color: saturate(@color, 20%);
  }
  .desaturate{
    background-color: desaturate(@color, 20%);
  }
  .fadein{
    background-color: fadein(@color, 20%);
  }
  .fadeout{
    background-color: fadeout(@color, 20%);
  }
  .spin-plus{
    background-color: spin(@color, 20);
  }
  .spin-minus{
    background-color: spin(@color, -20);
  }
  .gradient{
    .background-image(linear-gradient(to bottom, lighten(@color, 20%) 0%, darken(@color, 20%) 100%));
    .box-shadow(2, 2, 3, lighten(@color, 10%));
  }
{% endhighlight %}

Результат работы препроцессора LESS и его библиотеки миксинов LESS Hat показан ниже. Вот это да - работает!

![LESS Hat - миксин .border-radius()]({{site.url}}/images/uploads/2013/11/LESSHat_border-radius.png)

Список всех миксинов, доступных в этой библиотеке, представлен в начале файла `lesshat.less`, в разделе "TABLE OF MIXINS". Количество mixin'ов немаленькое (86 штук), но мне кажется, что у Compass оно будет намного больше.

Подробное описание и примеры использования каждого из миксинов библиотеки LESS Hat доступно на GitHub в файле `README.md`. Добро пожаловать ознакомиться - там все хорошо описано.

В принципе - больше и сказать нечего. Подключайте и используйте LESS Hat - только так можно освоить и оценить эту библиотеку. Для себя я сделал вывод, что мне пока удобнее работать с SASS/Compass и возможностей у последнего больше, чем у LESS/LESS Hat.

На этом все.

---

 [1]: www.csshat.com "CSS Hat"
 [2]: http://lesshat.com " LESS Hat"