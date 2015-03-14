---
title: 'Parallax Scrolling с помощью Stellar.js'
author: gearmobile
layout: post
---
> Отличный пример создания parallax scrolling с помощью Stellar.js. Оригинал статьи размещен здесь &#8211; [An Introduction to Parallax Scrolling Using Stellar.js][1].

Одним из наиболее обсуждаемых трендов в web-дизайне последние несколько лет является эффект parallax scrolling. Нравиться он вам или нет, но этот эффект сегодня применяется на очень многих сайтах. В этой статье будет дано краткое описание принципа parallax scrolling и будет показано, как применить этот эффект на странице с помощью jQuery-плагина под названием Stellar.js.

### Что такое parallax scrolling

Основная идея parallax scrolling заключается в том, что при прокрутке страницы вниз фоновое изображение **движется с меньшей скоростью**, нежели содержимое страницы. Таким образом создается иллюзия 3D на странице. Этот эффект является прекрасным дополнением к web-странице, однако он становиться навязчивым при чрезмерном злоупотреблении им. Время от времени вы встречаете на просторах Сети сайты, перегруженные подобными эффектами. И вам не всегда может такое понравиться. Потому что в основном при реализации такого эффекта используется анимация фоновых изображений, что значительно увеличивает вес страницы, в результате чего она очень медленно загружается в браузере.

Примерами сайтов со **злоупотреблением** таких эффектов, на мой взгляд, могут послужить [Saucony Kinavara 3][2] и [Oakley Airbrake MX][3]. Первый сайт &#8220;весит&#8221; 50Mb(!), второй сайт &#8211; около 20Mb.

Теперь, когда вы имеете представление о том, как на деле выглядит эффект parallax scrolling, давайте попробуем реализовать его с помощью плагина Stellar.js.

### Что такое Stellar.js

[Stellar.js][4] &#8211; это jQuery-плагин, с помощью которого можно легко реализовать эффект parallax scrolling на web-странице. Несмотря на то, что этот плагин **уже не поддерживается разработчиком**, он все еще **остается очень надежным**, **совместим с самыми последними версиями библиотеки jQuery** и часто применяется web-разработчиками в проектах (*что является показателем*). Stellar.js в списке популярных плагинов [The jQuery Plugin Registry][5] находится на высших позициях, поэтому вы наверняка о нем слышали или же читали упоминание о нем.

Отлично, вкратце мы познакомились, что такое Stellar.js и можно приступать к процессу создания parallax scrolling на странице с его помощью.

### Stellar.js &#8211; начинаем работу

Начать работать с плагином Stellar.js очень просто. Для начала нужно **скачать** этот плагин и **подключить** к странице. Получить плагин Stellar.js можно двумя способами &#8211; из [Git-репозитория][6] или с помощью менеджера пакетов **Bower**. Если остановится на использовании Bower, то в консоли нужно набрать такую команду:

{% highlight powershell %}
  bower install jquery.stellar
{% endhighlight %}

Когда плагин Stellar.js получен любым из вышеописанных способов, необходимо подключить его к странице как обычно.

<p>После подключения плагина Stellar.js все готово для того, чтобы применить эффект parallax scrolling на странице. Этот плагин позволяет применить данный эффект к любому scrolling-элементу на странице, будь то объект <code>window` или любой другой. Для этого нужно выполнить выборку нужного элемента с помощью jQuery, а затем применить к выбранному элементу метод `stellar()`.

Самый простой пример применения плагина Stellar.js к объекту показан ниже:

{% highlight javascript %}
  $('#someElement').stellar();
{% endhighlight %}

Для объекта `window` можно использовать и более краткий синтаксис вышеприведенного примера:

{% highlight javascript %}
  $.stellar();
{% endhighlight %}

В этом коде производится поиск фоновых изображений или элементов, к которым применяется эффект parallax; и для этих элементов выполняется пересчет их расположения на web-странице при ее прокрутке.

Если вам хочется взглянуть хотя бы на один готовый пример страницы с parallax scrolling, созданной с помощью Stellar.js, то можете посетить эту ссылку - [Stellar.js Backgrounds Demo][7].

### Настройки Stellar.js

[Stellar.js][4], как и большинство других плагинов подобного рода, достаточно гибок в настройке. В нем есть несколько параметров, с помощью которых можно **задать нужный вариант работы**. В Stellar.js все настройки делятся на два типа - глобальные (*оказывают влияние на все элементы*) и локальные, имеющие отношение только к конкретному элементу.

Глобальные настройки передаются методу `stellar()` в качестве аргументов, в момент вызова этого метода. Специфичные для элемента настройки передаются в виде `data-*`-атрибутов. В этом разделе статьи я не буду подробно останавливаться на рассмотрении всех возможных параметров плагина Stellar.js. Если у вас возникнет желание детально ознакомиться с ними, то можно обратиться к разделу, посвященному этому вопросу - [Configuring Everything][8].

Одной из **основных настроек плагина**, которая может понадобиться в первую очередь, является **выбор направления**, в котором будет осуществляться эффект. Классическим вариантом parallax scrolling является направление **parallax по вертикали** - сверху вниз или же наоборот. Однако, с помощью настроек можно задать **parallax по горизонтали** - слева направо и наоборот. И даже можно задать **сразу два направления** - по вертикали и по горизонтали. Для управления направлением parallax в плагине Stellar.js имеются два параметра Boolean-типа:

  * `horizontalScrolling` - для управления parallax **по горизонтали**
  * `verticalScrolling` - для управления parallax **по вертикали**

По умолчанию оба параметра имеют значение `true`.

Другим интересным параметров плагина Stellar.js является `responsive`. Данная настройка отвечается за возможность обновления содержимого блока с эффектом parallax при наступлении событий `load` и `resize` объекта `window`. Значением по умолчанию является `false`.

Последним (достойным внимания) глобальным параметром плагина Stellar.js является `hideDistantElements`. Значением по умолчанию этого параметра является `true`. Данный параметр отвечает за **эффект скрытия объекта** в том случае, когда он выходит на границы viewport. Если такое поведение вам не нужно, то можно поставить значение `hideDistantElements` в `false`.

Единственным специфичным для элемента параметром плагина Stellar.js, о котором я расскажу в этой статье, является `data-stellar-background-ratio`. Расскажу только потому, что он **используется очень часто** при работе с плагином Stellar.js. Параметр принимает в качестве значения положительное число и управляет **скоростью parallax для выбранного элемента**.

Например, `data-stellar-background-ratio="0.5"` означает, что скорость перемещения элемента при scrolling будет **в два раза меньше обычной**. Если вы будете использовать данный параметр со значением, меньшим 1, то, согласно документации, для элемента с parallax необходимо применить CSS-правило `background-attachment: fixed;`.

Теперь, когда мы познакомились с плагином Stellar.js и научились управлять им с помощью параметров, самое время посмотреть его в действии.

### Demo

В этом разделе статьи мы создадим пример кода, в котором применим плагин Stellar.js и настроим его с помощью параметров, рассмотренных ранее. Первым делом нам понадобиться HTML-разметка. Для этого создадим шесть блоков `div`, внутри которых будет содержаться некоторый текст:

{% highlight html %}
<div class="content" id="content1">
  <p>
    text here
  </p>
</div>

<div class="content" id="content2">
  <p>
    text here
  </p>
</div>

<div class="content" id="content3" data-stellar-background-ratio="0.5">
  <p>
    text here
  </p>
</div>

<div class="content" id="content4" data-stellar-background-ratio="0.5">
  <p>
    text here
  </p>
</div>

<div class="content" id="content5" data-stellar-background-ratio="0.5">
  <p>
    text here
  </p>
</div>

<div class="content" id="content6" data-stellar-background-ratio="0.5">
  <p>
    text here
  </p>
</div>
{% endhighlight %}

Для представленной выше HTML-разметки необходимо написать некоторые CSS-стили для задания фоновых изображений. В нашем примере будут использоваться три изображения, при этом каждое из них будет использоваться дважды. Так как к последним трем блокам `div` применен атрибут `data-stellar-background-ratio`, то в CSS-стилях также необходимо прописать правило `background-attachment: fixed;`.

Финальный вариант CSS-кода будет выглядеть таким образом:

{% highlight css %}
  @import "compass";
  @import "compass/reset";

  $white: #fff;
  $black: #000;

  body {
    font-size: 20px;
    color: $white;
    text-shadow: 0 1px 0 $black, 0 0 5px $black;
  }

  p {
    padding: 0 .5em;
    margin: 0;
  }

  .content {
    background-attachment: fixed;
    height: 400px;
    line-height: 400px;
    text-align: center;
  }

  #content1 {
    background-image: url("http://www.tamperlock.com/blog/wp-content/uploads/2014/08/london-england.jpg");
  }

  #content2 {
    background-image: url("http://ocdn.eu/images/pulscms/ZjU7MDQsMCwzMiwzODQsMWZhOzA2LDMyMCwxYzI_/1eb29a70dabd0994cdefaad01ca3c884.jpg");
  }

  #content3 {
    background-image: url("http://www.zeus.aegee.org/magazine/wp-content/uploads/napoli-golfo-vesuvio.jpg");
  }

  #content4 {
    background-image: url("http://www.tamperlock.com/blog/wp-content/uploads/2014/08/london-england.jpg");
  }

  #content5 {
    background-image: url("http://ocdn.eu/images/pulscms/ZjU7MDQsMCwzMiwzODQsMWZhOzA2LDMyMCwxYzI_/1eb29a70dabd0994cdefaad01ca3c884.jpg");
  }

  #content6 {
    background-image: url("http://www.zeus.aegee.org/magazine/wp-content/uploads/napoli-golfo-vesuvio.jpg");
  }
{% endhighlight %}

Последний шаг, который нужно выполнить, это запустить эффект, вызвав метод `stellar()`. Этому методу также передадим **несколько аргументов**:

{% highlight javascript %}
  $.stellar({
    horizontalScrolling: false,
    responsive: true
  });
{% endhighlight %}

<figure id="attachment_2031" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/stellar-600x382.png" alt="Stellar.js - parallax scrolling with jQuery" width="600" height="382" class="size-medium wp-image-2031" />][9]<figcaption class="wp-caption-text">Stellar.js - parallax scrolling with jQuery</figcaption></figure> 

Готовый Live-Demo пример parallax scrolling на Stellar.js можно посмотреть здесь - [Stellar.js][10].

### Заключение

В данной статье был рассмотрен плагин Stellar.js для создания эффекта parallax на web-странице. Мною не были рассмотрены **все настройки и возможности этого плагина**. Но целью этой статьи было заинтересовать читателей плагином Stellar.js для того, чтобы продолжить его изучение самостоятельно.

Что вы думаете о плагине Stellar.js? Вы слышали о таком или же используете его давно?

 [1]: http://www.sitepoint.com/introduction-parallax-scrolling-using-stellar-js/ "An Introduction to Parallax Scrolling Using Stellar.js"
 [2]: http://community.saucony.com/kinvara3/ "Saucony Kinavara 3"
 [3]: http://moto.oakley.com/ "Oakley Airbrake MX"
 [4]: https://github.com/markdalgleish/stellar.js/ "Stellar.js"
 [5]: http://plugins.jquery.com/ "The jQuery Plugin Registry"
 [6]: https://github.com/markdalgleish/stellar.js/ "Git-репозиторий Stellar.js"
 [7]: http://markdalgleish.com/projects/stellar.js/demos/backgrounds.html "Stellar.js Backgrounds Demo"
 [8]: https://github.com/markdalgleish/stellar.js#configuring-everything "Configuring Everything"
 [9]: http://localhost:7788/third/wp-content/uploads/2014/11/stellar.png
 [10]: http://stellar.zencoder.ru/ "Stellar.js"