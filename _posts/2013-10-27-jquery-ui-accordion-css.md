---
layout: post
title: "Создаем меню-аккордеон на jQuery UI"
author: gearmobile
tags: [accordion, css, jquery ui]
---

В этой статье будем создавать меню-аккордеон с помощью jQuery UI. Что такое jQuery, знают все - это библиотека Javascript. То есть, это собрание готовых модулей для самых разнообразный действий на сайте, таких как применение анимации, динамического изменения свойств HTML-элементов и многое другое. С помощью jQuery подобные действия можно "прикрутить" к страничке легко и быстро. jQuery UI - это библиотека для библиотеки jQuery. Другими словами, если jQuery - это надстройка над Javascript, то jQuery UI - это надстройка над jQuery. Пирамида получается в некотором смысле этого слова.

Предназначение jQuery UI - создание интерфейсов пользователя на HTML-странице. UI - это аббревиатура User Interface (Интерфейс Пользователя), а именно - это **меню навигации**, **вкладки**, **полоса прогресса**, **календарь**, **автопроверка вводимых данных** и другое.

Меню-аккордеон *можно сделать на чистом CSS*, но сегодня рассмотрим самый **простой и надежный способ** - на Javascript, так как он заведомо будет работать во всех браузерах, если в них не отключена поддержка этого языка.

Первое, что нужно сделать - это набросать каркас HTML-страницы, то есть `doctype`, кодировку, `head`, `body`:

{% highlight html %}
<!doctype html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <title>Document</title>
    </head>
    <body>
    </body>
  </html>
{% endhighlight %}

Затем подключаем библиотеку jQuery и ее надстройку jQuery UI, причем делать это нужно в указанном порядке: сначала основная библиотека, затем ее надстройка. Так как мы будем делать меню со своими собственными стилями, то необходимо выполнить следующие шаги. Переходим на страницу загрузки http://jqueryui.com/download/ и здесь выполним компиляцию ядра и только необходимых нам модулей (возможностей) jQuery UI. Что это значит? Полный комплект библиотеки jQuery UI содержит в себе возможность создания самых различный интерфейсов - вкладок, ползунков, календарей, полос прогресса, автозаполнения и так далее. Нам же необходима только одна из них - меню-аккордеон. Зачем скачивать и использовать библиотеку целиком, когда можно применять в работе только малую ее часть? Выигрыш в загрузке страницы в окне браузера очевиден.

Другая, менее очевидная причина такого выбора заключается в том, что во время работы движок jQuery UI создает свои собственные классы стилизации для меню, в частности. Эти классы напрямую соотносятся с файлом стилизации, таким как smoothness/jquery-ui.css. Когда мы будем создавать правила CSS для нашего аккордеона, мы будет прописывать свои собственные классы. В итоге те классы, которые "вмонтированы" в связку jQuery UI + Theme будут только ненужным балластом и мусором.

Итогом всех вышеперечисленных умозаключений является следующая последовательность шагов. Заходим, как было уже сказано, на страницу http://jqueryui.com/download/ и видим там три больших раздела: Version, Components, Theme. В первом разделе Version выбирается версия библиотеки jQuery. На момент написания статьи это `v.1.10.3`. Это нас устраивает, поэтому оставляем все как есть.

Переходим во второй раздел Components. Здесь из длинного списка модулей выберем только то, что нам необходимо. Но сначала снимаем галочку со всех выбранных по умолчанию опций - "Toggle All". Пролистываем список вниз и находим нужную нам строчку - "Accordion", ставим против нее галочку. Обращаем внимание, что автоматически активировались еще две галочки в подразделе UI Core - "Core" и "Widget". Это два основных компонента ядра jQuery UI, без которых не будет работать ни один модуль.

Опускаемся вниз страницы в раздел Theme. Здесь по умолчанию выбрана тема UI lightness, это набор CSS-стилей для оформления меню-аккордеон, созданный командой разработчиков jQuery UI. Список готовых тем не ограничивается только этим файлом, на самом деле таких тем около 24, из которых можно выбрать понравившуюся. Помимо этого, можно воспользоваться визуальным конструктором ThemeRoller, перейдя по ссылке "design a custom theme". Но нас оба эти выбора не интересуют, так как мы будем создавать свои собственные стили. Поэтому в выпадающем списке тем данного раздела выбираем "No Theme".

Осталось нажать кнопку "Download", чтобы скачать скомпилированную библиотеку, которая будет носить имя jquery-ui-1.10.3.custom.zip и весить 461 Kb. Сравните - полная версия jQuery UI весит 2.37 Mb, разница ощутимая! Теперь распаковываем архив и вытаскиваем из него необходимые нам файлы, которые распихиваем в соответствующие им папки: `jquery-1.9.1.js` и `jquery-ui-1.10.3.custom.js` в папку javascripts (я буду создавать меню с помощью SASS/Compass). В папке css скачанного архива есть подпапка no-theme с CSS-файлом `jquery-ui-1.10.3.custom.css`. Пролистав го, я сделал вывод, что данный файл служит для подключения иконок и другого вспомогательного оформления будущего меню. Рискну оставить его в архиве и не использовать.

Подключаю полученные файлы библиотеки jQuery UI в head HTML-документа. Напоминаю, что я буду создавать меню-аккордеон с помощью SASS/Compass, поэтому название папок и синтаксис кода будет отличаться от "общепринятого".

{% highlight html %}
<!doctype html>
  <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Accordion jQuery UI</title>
      <script type="text/javascript" src="javascripts/jquery-1.9.1.js"></script>
      <script type="text/javascript" src="javascripts/jquery-ui-1.10.3.custom.min.js"></script>
      <link rel="stylesheet" type="text/css" href="stylesheets/screen.css">
    </head>
{% endhighlight %}

Создаем HTML-разметку для будущего меню аккордеон. Для чистоты эксперимента просто скопируем ее с сайта проекта jQuery UI, со страницы примера "Accordion" (http://jqueryui.com/accordion/). Как написано на этой странице, разметка выполнена в виде заголовков третьего уровня `h3` и блоков `div` для того, чтобы контент был доступен на странице даже при отключенной поддержке Javascript в браузере пользователей.

Ниже приведена точная копия оригинальной разметки от разработчиков jQuery. Видим, что роль пунктов меню выполняют заголовки, а контент меню обернут в блоки `div`, внутри которых может располагаться все что угодно - текст, список, картинки. Принцип создания меню на основе h3 и div немного не стандарный, так как обычно такие меню строятся на основе маркированных списков ul.

{% highlight html %}
<div id="accordion">
  <h3>Section 1</h3>
    <div>
      <p>
        Mauris mauris ante, blandit et, ultrices a, suscipit eget, quam. Integer
        ut neque. Vivamus nisi metus, molestie vel, gravida in, condimentum sit
        amet, nunc. Nam a nibh. Donec suscipit eros. Nam mi. Proin viverra leo ut
        odio. Curabitur malesuada. Vestibulum a velit eu ante scelerisque vulputate.
        </p>
    </div>
  <h3>Section 2</h3>
    <div>
      <p>
        Sed non urna. Donec et ante. Phasellus eu ligula. Vestibulum sit amet
        purus. Vivamus hendrerit, dolor at aliquet laoreet, mauris turpis porttitor
        velit, faucibus interdum tellus libero ac justo. Vivamus non quam. In
        suscipit faucibus urna.
      </p>
    </div>
  <h3>Section 3</h3>
    <div>
      <p>
        Nam enim risus, molestie et, porta ac, aliquam ac, risus. Quisque lobortis.
        Phasellus pellentesque purus in massa. Aenean in pede. Phasellus ac libero
        ac tellus pellentesque semper. Sed ac felis. Sed commodo, magna quis
        lacinia ornare, quam ante aliquam nisi, eu iaculis leo purus venenatis dui.
      </p>
      <ul>
        <li>List item one</li>
        <li>List item two</li>
        <li>List item three</li>
      </ul>
    </div>
  <h3>Section 4</h3>
    <div>
      <p>
        Cras dictum. Pellentesque habitant morbi tristique senectus et netus
        et malesuada fames ac turpis egestas. Vestibulum ante ipsum primis in
        faucibus orci luctus et ultrices posuere cubilia Curae; Aenean lacinia
        mauris vel est.
      </p>
      <p>
        Suspendisse eu nisl. Nullam ut libero. Integer dignissim consequat lectus.
        Class aptent taciti sociosqu ad litora torquent per conubia nostra, per
        inceptos himenaeos.
      </p>
    </div>
</div>
{% endhighlight %}

Все готово для написания своих собственных стилей для нашего меню. Сброс стилей (reset) мне выполнять не нужно, так как Compass автоматически подключил его к моему проекту:

{% highlight css %}
  @import "compass/reset";
{% endhighlight %}

Устанавливаем самые общие правила для контейнера #accordion:

{% highlight css %}
#accordion{
  width: 500px;
  margin: 10px auto;
  ...
{% endhighlight %}

Создаем правила для заголовков `h3`:

{% highlight html %}
...
  h3 {
    font: 18px/30px Georgia, serif;
    background-color: #778899;
    text-indent: 10px;
    cursor: pointer;
    margin-bottom: 1px;
    &:hover{
    background-color: lighten(#778899, 10%);
  }
    &:focus {
    outline: none;
  }
{% endhighlight %}

... и для контента в меню:

{% highlight html %}
...
  div{
  padding: 10px 20px;
  background-color: lighten(#778899, 20%);
  margin-bottom: 1px;
  font: 14px/20px 'PT Sans', sans-serif;
  text-indent: 1em;
}
{% endhighlight %}

Теперь прикрутим скрипт в head нашего HTML-документа, чтобы меню-аккордеон заработало:

{% highlight javascript %}
<script type="text/javascript">
  $(function(){
    $('#accordion').accordion();
  });
</script>
{% endhighlight %}

Вуаля - все готово! Меню работает на скрытие и раскрытие. Можно немного приукрасить навигацию, сделав заголовки активными - при щелчке мыши на нем содержимое будет сворачивается. При повторном щелчке на этом же заголовке содержимое меню будет вновь разворачивается. Выполняется это передачей нашему скрипту параметра collapsible:

{% highlight javascript %}
<script type="text/javascript">
  $(function(){
    $('#accordion').accordion({
      collapsible: true
    });
  });
</script>
{% endhighlight %}

Все хорошо, но есть один небольшой недочет - по умолчанию скрипт задает для блоков div высоту 120px. В третьем блоке у нас имеются два элемента - параграф p и список ul. При раскрытии этого пункта контент не вмещается по высоте и "налазит" на четвертый пункт. Аналогичная ситуация и с контентом четвертого пункта меню. Решение напрашивается само собой - нужно отрегулировать высоту для контента нашего меню.

Для этого нужно перейти по ссылке "API documentation" (http://api.jqueryui.com/accordion/), где представлен список опций, методов и событий для меню аккордеон на jQuery UI. Нас интересует одна из опций - heightStyle, которая может принимать три значения:

  * "fill" - высота всех блоков с контентом будет высчитана, исходя из высоты всей панели навигации (то бишь - меню-аккордеон). Для тех блоков, содержимое которых не вмещается, добавиться вертикальная полоса прокрутки;
  * "auto" - непонятно, как оно работает. В документации сказано, что при установке данного значения высота для каждого блока содержимого панели будет высчитываться, исходя из высоты самого высокого блока. Однако, работа навигации с этим значением параметра heightStyle аналогична той, когда его вообще нет;
  * "content" - высота каждого из блоков с контентом вычисляется в зависимости от величины его содержимого, то есть - подстраивается под контент.

Ниже представлены скриншоты меню аккордеон с вариантами значений "fill" и "content" для опции heightStyle:

<figure id="attachment_87" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-fill-600x418.jpg" alt="Меню аккордеон с опцией heightStyle: fill" width="600" height="418" class="size-medium wp-image-87" />][1]
  <figcaption class="wp-caption-text">Меню аккордеон с опцией heightStyle: fill</figcaption>
</figure>

<figure id="attachment_88" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-content-600x418.jpg" alt="Меню аккордеон с опцией heightStyle: content" width="600" height="418" class="size-medium wp-image-88" />][2]
  <figcaption class="wp-caption-text">Меню аккордеон с опцией heightStyle: content</figcaption>
</figure>

Есть еще несколько интересных опций для меню на jQuery UI.

Опция `active` - какой пункт меню будет открыт по умолчанию в браузере. Номер пункта устанавливается через целое число, отсчет ведется с нуля.

Например, код:

{% highlight javascript %}
  active: 2
{% endhighlight %}

... заставит браузер раскрыть третий по счету пункт меню.

Событие event назначит, при каком условии будет происходить переключение между пунктами меню. По умолчанию таковым является событие click, то есть щелчок мыши на пункте. Можно изменить событие на mouseover, что заставит скрипт открывать вкладку при наведении курсора мыши на пункт меню.

Можно сказать, что задача выполнена. Меню аккордеон на jQuery UI имеет еще достаточно опций и способов настройки, но здесь представлен самый простой и общий результат. Ниже приведен полный код созданного нами меню.

{% highlight html %}
<!doctype html>
  <html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Accordion jQuery UI</title>
    <script type="text/javascript" src="javascripts/jquery-1.9.1.js"></script>
    <script type="text/javascript" src="javascripts/jquery-ui-1.10.3.custom.min.js"></script>
    <link href='http://fonts.googleapis.com/css?family=PT+Sans' rel='stylesheet' type='text/css'>
    <link rel="stylesheet" type="text/css" href="stylesheets/screen.css">
    <script type="text/javascript">
      $(function(){
        $('#accordion').accordion({
          collapsible: true,
          heightStyle: "content"
        });
      });
    </script>
  </head>
  <body>
    <div id="accordion">
      <h3>Section 1</h3>
        <div>
          <p>
            Mauris mauris ante, blandit et, ultrices a, suscipit eget, quam. Integer
            ut neque. Vivamus nisi metus, molestie vel, gravida in, condimentum sit
            amet, nunc. Nam a nibh. Donec suscipit eros. Nam mi. Proin viverra leo ut
            odio. Curabitur malesuada. Vestibulum a velit eu ante scelerisque vulputate.
          </p>
        </div>
      <h3>Section 2</h3>
        <div>
          <p>
            Sed non urna. Donec et ante. Phasellus eu ligula. Vestibulum sit amet
            purus. Vivamus hendrerit, dolor at aliquet laoreet, mauris turpis porttitor
            velit, faucibus interdum tellus libero ac justo. Vivamus non quam. In
            suscipit faucibus urna.
          </p>
        </div>
      <h3>Section 3</h3>
        <div>
          <p>
            Nam enim risus, molestie et, porta ac, aliquam ac, risus. Quisque lobortis.
            Phasellus pellentesque purus in massa. Aenean in pede. Phasellus ac libero
            ac tellus pellentesque semper. Sed ac felis. Sed commodo, magna quis
            lacinia ornare, quam ante aliquam nisi, eu iaculis leo purus venenatis dui.
          </p>
          <ul>
            <li>List item one</li>
            <li>List item two</li>
            <li>List item three</li>
          </ul>
        </div>
      <h3>Section 4</h3>
        <div>
          <p>
            Cras dictum. Pellentesque habitant morbi tristique senectus et netus
            et malesuada fames ac turpis egestas. Vestibulum ante ipsum primis in
            faucibus orci luctus et ultrices posuere cubilia Curae; Aenean lacinia
            mauris vel est.
          </p>
          <p>
            Suspendisse eu nisl. Nullam ut libero. Integer dignissim consequat lectus.
            Class aptent taciti sociosqu ad litora torquent per conubia nostra, per
            inceptos himenaeos.
          </p>
        </div>
    </div>
  </body>
</html>
{% endhighlight %}

{% highlight css %}
@import "compass/reset";

  #accordion{
  width: 500px;
  margin: 10px auto;
    h3{
      font: 18px/30px Georgia, serif;
      background-color: #778899;
      text-indent: 10px;
      cursor: pointer;
      margin-bottom: 1px;
    &:hover{
      background-color: lighten(#778899, 10%);
    }
    &:focus{
     outline: none;
    }
  }
    div{
      padding: 10px 20px;
      background-color: lighten(#778899, 20%);
      margin-bottom: 1px;
      font: 14px/20px 'PT Sans', sans-serif;
      text-indent: 1em;
    }
  }
{% endhighlight %}

 [1]: http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-fill.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-content.jpg
