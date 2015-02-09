---
title: Создаем меню-аккордеон на jQuery UI
author: gearmobile
layout: post
permalink: /%d1%81%d0%be%d0%b7%d0%b4%d0%b0%d0%b5%d0%bc-%d0%bc%d0%b5%d0%bd%d1%8e-%d0%b0%d0%ba%d0%ba%d0%be%d1%80%d0%b4%d0%b5%d0%be%d0%bd-%d0%bd%d0%b0-jquery-ui/
ratings_users:
  - 10
ratings_score:
  - 27
ratings_average:
  - 2.7
cleanretina_sidebarlayout:
  - no-sidebar-full-width
categories:
  - 'Javascript &amp; jQuery'
tags:
  - accordion
  - jquery ui
---
В этой статье будем создавать меню-аккордеон с помощью jQuery UI. Что такое jQuery, знают все &#8211; это библиотека Javascript. То есть, это собрание готовых модулей для самых разнообразный действий на сайте, таких как применение анимации, динамического изменения свойств HTML-элементов и многое другое. С помощью jQuery подобные действия можно &#8220;прикрутить&#8221; к страничке легко и быстро. jQuery UI &#8211; это библиотека для библиотеки jQuery. Другими словами, если jQuery &#8211; это надстройка над Javascript, то jQuery UI &#8211; это надстройка над jQuery. Пирамида получается в некотором смысле этого слова.

Предназначение jQuery UI &#8211; создание интерфейсов пользователя на HTML-странице. UI &#8211; это аббревиатура User Interface (Интерфейс Пользователя), а именно это меню навигации, вкладки, полоса прогресса, календарь, автопроверка вводимых данных и другое.

Меню-аккордеон можно сделать на чистом CSS, но сегодня рассмотрим самый простой и надежный способ &#8211; на Javascript, так как он заведомо будет работать во всех браузерах, если в них не отключена поддержка этого языка.

Первое, что нужно сделать &#8211; это набросать каркас HTML-страницы, то есть doctype, кодировку, head, body

<pre>&lt;!doctype html&gt;
    &lt;html lang="en"&gt;
      &lt;head&gt;
        &lt;meta charset="UTF-8"&gt;
        &lt;title&gt;Document&lt;/title&gt;
      &lt;/head&gt;
    &lt;body&gt;

    &lt;/body&gt;
  &lt;/html&gt;
</pre>

Затем подключаем библиотеку jQuery и ее надстройку jQuery UI, причем делать это нужно в указанном порядке: сначала основная библиотека, затем ее надстройка. Так как мы будем делать меню со своими собственными стилями, то необходимо выполнить следующие шаги. Переходим на страницу загрузки http://jqueryui.com/download/ и здесь выполним компиляцию ядра и только необходимых нам модулей (возможностей) jQuery UI. Что это значит? Полный комплект библиотеки jQuery UI содержит в себе возможность создания самых различный интерфейсов &#8211; вкладок, ползунков, календарей, полос прогресса, автозаполнения и так далее. Нам же необходима только одна из них &#8211; меню-аккордеон. Зачем скачивать и использовать библиотеку целиком, когда можно применять в работе только малую ее часть? Выигрыш в загрузке страницы в окне браузера очевиден.

Другая, менее очевидная причина такого выбора заключается в том, что во время работы движок jQuery UI создает свои собственные классы стилизации для меню, в частности. Эти классы напрямую соотносятся с файлом стилизации, таким как smoothness/jquery-ui.css. Когда мы будем создавать правила CSS для нашего аккордеона, мы будет прописывать свои собственные классы. В итоге те классы, которые &#8220;вмонтированы&#8221; в связку jQuery UI + Theme будут только ненужным балластом и мусором.

Итогом всех вышеперечисленных умозаключений является следующая последовательность шагов. Заходим, как было уже сказано, на страницу http://jqueryui.com/download/ и видим там три больших раздела: Version, Components, Theme. В первом разделе Version выбирается версия библиотеки jQuery. На момент написания статьи это v.1.10.3. Это нас устраивает, поэтому оставляем все как есть.

Переходим во второй раздел Components. Здесь из длинного списка модулей выберем только то, что нам необходимо. Но сначала снимаем галочку со всех выбранных по умолчанию опций &#8211; Toggle All. Пролистываем список вниз и находим нужную нам строчку &#8211; Accordion, ставим против нее галочку. Обращаем внимание, что автоматически активировались еще две галочки в подразделе UI Core &#8211; Core и Widget. Это два основных компонента ядра jQuery UI, без которых не будет работать ни один модуль.

Опускаемся вниз страницы в раздел Theme. Здесь по умолчанию выбрана тема UI lightness, это набор CSS-стилей для оформления меню-аккордеон, созданный командой разработчиков jQuery UI. Список готовых тем не ограничивается только этим файлом, на самом деле таких тем около 24, из которых можно выбрать понравившуюся. Помимо этого, можно воспользоваться визуальным конструктором ThemeRoller, перейдя по ссылке &#8220;design a custom theme&#8221;. Но нас оба эти выбора не интересуют, так как мы будем создавать свои собственные стили. Поэтому в выпадающем списке тем данного раздела выбираем &#8220;No Theme&#8221;.

Осталось нажать кнопку &#8220;Download&#8221;, чтобы скачать скомпилированную библиотеку, которая будет носить имя jquery-ui-1.10.3.custom.zip и весить 461 Kb. Сравните &#8211; полная версия jQuery UI весит 2.37 Mb, разница ощутимая! Теперь распаковываем архив и вытаскиваем из него необходимые нам файлы, которые распихиваем в соответствующие им папки: jquery-1.9.1.js и jquery-ui-1.10.3.custom.js в папку javascripts (я буду создавать меню с помощью SASS/Compass). В папке css скачанного архива есть подпапка no-theme с CSS-файлом jquery-ui-1.10.3.custom.css. Пролистав го, я сделал вывод, что данный файл служит для подключения иконок и другого вспомогательного оформления будущего меню. Рискну оставить его в архиве и не использовать.

Подключаю полученные файлы библиотеки jQuery UI в head HTML-документа. Напоминаю, что я буду создавать меню-аккордеон с помощью SASS/Compass, поэтому название папок и синтаксис кода будет отличаться от &#8220;общепринятого&#8221;.

<pre>&lt;!doctype html&gt;
    &lt;html lang="en"&gt;
      &lt;head&gt;
        &lt;meta charset="UTF-8"&gt;
        &lt;title&gt;Accordion jQuery UI&lt;/title&gt;
        &lt;script type="text/javascript" src="javascripts/jquery-1.9.1.js"&gt;&lt;/script&gt;
        &lt;script type="text/javascript" src="javascripts/jquery-ui-1.10.3.custom.min.js"&gt;&lt;/script&gt;
        &lt;link rel="stylesheet" type="text/css" href="stylesheets/screen.css"&gt;
      &lt;/head&gt;
</pre>

Создаем HTML-разметку для будущего меню аккордеон. Для чистоты эксперимента просто скопируем ее с сайта проекта jQuery UI, со страницы примера &#8220;Accordion&#8221; (http://jqueryui.com/accordion/). Как написано на этой странице, разметка выполнена в виде заголовков третьего уровня h3 и блоков div для того, чтобы контент был доступен на странице даже при отключенной поддержке Javascript в браузере пользователей. Ниже приведена точная копия оригинальной разметки от разработчиков jQuery. Видим, что роль пунктов меню выполняют заголовки, а контент меню обернут в блоки div, внутри которых может располагаться все что угодно &#8211; текст, список, картинки. Принцип создания меню на основе h3 и div немного не стандарный, так как обычно такие меню строятся на основе маркированных списков ul.

<pre>&lt;div id="accordion"&gt;
    &lt;h3&gt;Section 1&lt;/h3&gt;
      &lt;div&gt;
        &lt;p&gt;
          Mauris mauris ante, blandit et, ultrices a, suscipit eget, quam. Integer
          ut neque. Vivamus nisi metus, molestie vel, gravida in, condimentum sit
          amet, nunc. Nam a nibh. Donec suscipit eros. Nam mi. Proin viverra leo ut
          odio. Curabitur malesuada. Vestibulum a velit eu ante scelerisque vulputate.
          &lt;/p&gt;
      &lt;/div&gt;
    &lt;h3&gt;Section 2&lt;/h3&gt;
      &lt;div&gt;
        &lt;p&gt;
          Sed non urna. Donec et ante. Phasellus eu ligula. Vestibulum sit amet
          purus. Vivamus hendrerit, dolor at aliquet laoreet, mauris turpis porttitor
          velit, faucibus interdum tellus libero ac justo. Vivamus non quam. In
          suscipit faucibus urna.
        &lt;/p&gt;
      &lt;/div&gt;
    &lt;h3&gt;Section 3&lt;/h3&gt;
      &lt;div&gt;
        &lt;p&gt;
          Nam enim risus, molestie et, porta ac, aliquam ac, risus. Quisque lobortis.
          Phasellus pellentesque purus in massa. Aenean in pede. Phasellus ac libero
          ac tellus pellentesque semper. Sed ac felis. Sed commodo, magna quis
          lacinia ornare, quam ante aliquam nisi, eu iaculis leo purus venenatis dui.
        &lt;/p&gt;
        &lt;ul&gt;
          &lt;li&gt;List item one&lt;/li&gt;
          &lt;li&gt;List item two&lt;/li&gt;
          &lt;li&gt;List item three&lt;/li&gt;
        &lt;/ul&gt;
      &lt;/div&gt;
    &lt;h3&gt;Section 4&lt;/h3&gt;
      &lt;div&gt;
        &lt;p&gt;
          Cras dictum. Pellentesque habitant morbi tristique senectus et netus
          et malesuada fames ac turpis egestas. Vestibulum ante ipsum primis in
          faucibus orci luctus et ultrices posuere cubilia Curae; Aenean lacinia
          mauris vel est.
        &lt;/p&gt;
        &lt;p&gt;
          Suspendisse eu nisl. Nullam ut libero. Integer dignissim consequat lectus.
          Class aptent taciti sociosqu ad litora torquent per conubia nostra, per
          inceptos himenaeos.
        &lt;/p&gt;
      &lt;/div&gt;
  &lt;/div&gt;
</pre>

Все готово для написания своих собственных стилей для нашего меню. Сброс стилей (reset) мне выполнять не нужно, так как Compass автоматически подключил его к моему проекту:

<pre>@import "compass/reset";</pre>

Устанавливаем самые общие правила для контейнера #accordion:

<pre>#accordion{
  width: 500px;
  margin: 10px auto;
  ...
</pre>

Создаем правила для заголовков h3:

<pre>...
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
</pre>

&#8230; и для контента в меню:

<pre>...
  div{
    padding: 10px 20px;
    background-color: lighten(#778899, 20%);
    margin-bottom: 1px;
    font: 14px/20px 'PT Sans', sans-serif;
    text-indent: 1em;
  }
</pre>

Теперь прикрутим скрипт в head нашего HTML-документа, чтобы меню-аккордеон заработало:

<pre>&lt;script type="text/javascript"&gt;
    $(function(){
      $('#accordion').accordion();
    });
  &lt;/script&gt;
</pre>

Вуаля &#8211; все готово! Меню работает на скрытие и раскрытие. Можно немного приукрасить навигацию, сделав заголовки активными &#8211; при щелчке мыши на нем содержимое будет сворачивается. При повторном щелчке на этом же заголовке содержимое меню будет вновь разворачивается. Выполняется это передачей нашему скрипту параметра collapsible:

<pre>&lt;script type="text/javascript"&gt;
    $(function(){
      $('#accordion').accordion({
        collapsible: true
      });
    });
  &lt;/script&gt;
</pre>

Все хорошо, но есть один небольшой недочет &#8211; по умолчанию скрипт задает для блоков div высоту 120px. В третьем блоке у нас имеются два элемента &#8211; параграф p и список ul. При раскрытии этого пункта контент не вмещается по высоте и &#8220;налазит&#8221; на четвертый пункт. Аналогичная ситуация и с контентом четвертого пункта меню. Решение напрашивается само собой &#8211; нужно отрегулировать высоту для контента нашего меню.

Для этого нужно перейти по ссылке &#8220;API documentation&#8221; (http://api.jqueryui.com/accordion/), где представлен список опций, методов и событий для меню аккордеон на jQuery UI. Нас интересует одна из опций &#8211; heightStyle, которая может принимать три значения:

  * &#8220;fill&#8221; &#8211; высота всех блоков с контентом будет высчитана, исходя из высоты всей панели навигации (то бишь &#8211; меню-аккордеон). Для тех блоков, содержимое которых не вмещается, добавиться вертикальная полоса прокрутки;
  * &#8220;auto&#8221; &#8211; непонятно, как оно работает. В документации сказано, что при установке данного значения высота для каждого блока содержимого панели будет высчитываться, исходя из высоты самого высокого блока. Однако, работа навигации с этим значением параметра heightStyle аналогична той, когда его вообще нет;
  * &#8220;content&#8221; &#8211; высота каждого из блоков с контентом вычисляется в зависимости от величины его содержимого, то есть &#8211; подстраивается под контент.

Ниже представлены скриншоты меню аккордеон с вариантами значений &#8220;fill&#8221; и &#8220;content&#8221; для опции heightStyle:<figure id="attachment_87" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-fill-600x418.jpg" alt="Меню аккордеон с опцией heightStyle: fill" width="600" height="418" class="size-medium wp-image-87" />][1]<figcaption class="wp-caption-text">Меню аккордеон с опцией heightStyle: fill</figcaption></figure> <figure id="attachment_88" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-content-600x418.jpg" alt="Меню аккордеон с опцией heightStyle: content" width="600" height="418" class="size-medium wp-image-88" />][2]<figcaption class="wp-caption-text">Меню аккордеон с опцией heightStyle: content</figcaption></figure> 

Есть еще несколько интересных опций для меню на jQuery UI.

Опция active &#8211; какой пункт меню будет открыт по умолчанию в браузере. Номер пункта устанавливается через целое число, отсчет ведется с нуля. Например, код:

<pre>active: 2
</pre>

&#8230; заставит браузер раскрыть третий по счету пункт меню.

Событие event назначит, при каком условии будет происходить переключение между пунктами меню. По умолчанию таковым является событие click, то есть щелчок мыши на пункте. Можно изменить событие на mouseover, что заставит скрипт открывать вкладку при наведении курсора мыши на пункт меню.

Можно сказать, что задача выполнена. Меню аккордеон на jQuery UI имеет еще достаточно опций и способов настройки, но здесь представлен самый простой и общий результат. Ниже приведен полный код созданного нами меню.

HTML:

<pre>&lt;!doctype html&gt;
    &lt;html lang="en"&gt;
    &lt;head&gt;
      &lt;meta charset="UTF-8"&gt;
      &lt;title&gt;Accordion jQuery UI&lt;/title&gt;
      &lt;script type="text/javascript" src="javascripts/jquery-1.9.1.js"&gt;&lt;/script&gt;
      &lt;script type="text/javascript" src="javascripts/jquery-ui-1.10.3.custom.min.js"&gt;&lt;/script&gt;
      &lt;link href='http://fonts.googleapis.com/css?family=PT+Sans' rel='stylesheet' type='text/css'&gt;
      &lt;link rel="stylesheet" type="text/css" href="stylesheets/screen.css"&gt;
      &lt;script type="text/javascript"&gt;
        $(function(){
          $('#accordion').accordion({
            collapsible: true,
            heightStyle: "content"
          });
        });
      &lt;/script&gt;
    &lt;/head&gt;
    &lt;body&gt;
      &lt;div id="accordion"&gt;
        &lt;h3&gt;Section 1&lt;/h3&gt;
          &lt;div&gt;
            &lt;p&gt;
              Mauris mauris ante, blandit et, ultrices a, suscipit eget, quam. Integer
              ut neque. Vivamus nisi metus, molestie vel, gravida in, condimentum sit
              amet, nunc. Nam a nibh. Donec suscipit eros. Nam mi. Proin viverra leo ut
              odio. Curabitur malesuada. Vestibulum a velit eu ante scelerisque vulputate.
            &lt;/p&gt;
          &lt;/div&gt;
        &lt;h3&gt;Section 2&lt;/h3&gt;
          &lt;div&gt;
            &lt;p&gt;
              Sed non urna. Donec et ante. Phasellus eu ligula. Vestibulum sit amet
              purus. Vivamus hendrerit, dolor at aliquet laoreet, mauris turpis porttitor
              velit, faucibus interdum tellus libero ac justo. Vivamus non quam. In
              suscipit faucibus urna.
            &lt;/p&gt;
          &lt;/div&gt;
        &lt;h3&gt;Section 3&lt;/h3&gt;
          &lt;div&gt;
            &lt;p&gt;
              Nam enim risus, molestie et, porta ac, aliquam ac, risus. Quisque lobortis.
              Phasellus pellentesque purus in massa. Aenean in pede. Phasellus ac libero
              ac tellus pellentesque semper. Sed ac felis. Sed commodo, magna quis
              lacinia ornare, quam ante aliquam nisi, eu iaculis leo purus venenatis dui.
            &lt;/p&gt;
            &lt;ul&gt;
              &lt;li&gt;List item one&lt;/li&gt;
              &lt;li&gt;List item two&lt;/li&gt;
              &lt;li&gt;List item three&lt;/li&gt;
            &lt;/ul&gt;
          &lt;/div&gt;
        &lt;h3&gt;Section 4&lt;/h3&gt;
          &lt;div&gt;
            &lt;p&gt;
              Cras dictum. Pellentesque habitant morbi tristique senectus et netus
              et malesuada fames ac turpis egestas. Vestibulum ante ipsum primis in
              faucibus orci luctus et ultrices posuere cubilia Curae; Aenean lacinia
              mauris vel est.
            &lt;/p&gt;
            &lt;p&gt;
              Suspendisse eu nisl. Nullam ut libero. Integer dignissim consequat lectus.
              Class aptent taciti sociosqu ad litora torquent per conubia nostra, per
              inceptos himenaeos.
            &lt;/p&gt;
          &lt;/div&gt;
      &lt;/div&gt;
    &lt;/body&gt;
  &lt;/html&gt;
</pre>

CSS (SASS):

<pre>@import "compass/reset";

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
</pre>

Оцените статью:  
<span id="post-ratings-11" class="post-ratings" data-nonce="a8d1c9ff75"><img id="rating_11_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(11, 1, '1 Star');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_11_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(11, 2, '2 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_11_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(11, 3, '3 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_11_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(11, 4, '4 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_11_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(11, 5, '5 Stars');" onmouseout="ratings_off(2.7, 3, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>10</strong> votes, average: <strong>2,70</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_11_text"></span></span><span id="post-ratings-11-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-fill.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/10/jquery-ui_heightStyle-content.jpg