---
title: 'Foundation &#8211; button group и button bar'
author: gearmobile
excerpt: 'Продолжение темы Foundation, в которой рассмотрен вопрос создания группы кнопок (button group) и панели кнопок (button bar). В предыдущем обзоре я с вами научился создавать кнопки на Foundation. В этой статье мы научимся создавать группы кнопок (button group) - несколько кнопок, объединенных в группу. Такие кнопки могут применяться на странице для самых различных целей.'
layout: post
permalink: /foundation-button-group-button-bar/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - button bar
  - button group
  - foundation
---
Продолжение темы Foundation, в которой рассмотрен вопрос создания группы кнопок (button group) и панели кнопок (button bar). В предыдущем обзоре я с вами научился создавать кнопки на Foundation &#8211; [Foundation &#8211; создаем кнопки][1]. В этом обзоре мы научимся создавать **группы кнопок** (button group) &#8211; несколько кнопок, объединенных в группу. Такие кнопки могут применяться на странице для самых различных целей.

### Группы кнопок (button group) на Foundation

С точки зрения HTML струкрута такой группы представляет из себя обычный маркированный список с вложенными ссылками. Все дело в CSS-классах фреймворка Foundation, которые применяются к этому списку. Ссылку мы создаем с помощью класса `.button`, как и в предыдущей статье. А для элемента `ul` мы присваиваем класс `.button-group`:

<pre><ul class="button-group">
  <li>
    <a href="#" class="button">Link 1</a>
  </li>
      
  
  <li>
    <a href="#" class="button">Link 2</a>
  </li>
      
  
  <li>
    <a href="#" class="button">Link 3</a>
  </li>
    
</ul>
  </pre>

В результате получаем группу с набором кнопок внутри:<figure id="attachment_1415" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_group-600x281.png" alt="Button group на Foundation" width="600" height="281" class="size-medium wp-image-1415" />][2]<figcaption class="wp-caption-text">Button group на Foundation</figcaption></figure> 

### Видоизменение группы кнопок (button group) на Foundation

Созданную таким образом группу кнопок можно видоизменять с помощью дополнительных классов, как это делалось ранее. К примеру создадим две группы кнопок и применим к ним дополнительные классы. `.radius`, `.round`, `.alert`, `.secondary`, `.success` Кстати, дополнительные классы можно применять не только к элементам `a`, но и к элементу `ul`:

<pre><ul class="button-group radius">
  <li>
    <a href="#" class="button alert">Link 1</a>
  </li>
      
  
  <li>
    <a href="#" class="button secondary">Link 2</a>
  </li>
      
  
  <li>
    <a href="#" class="button success">Link 3</a>
  </li>
    
</ul>

  

<ul class="button-group round">
  <li>
    <a href="#" class="button alert">Link 1</a>
  </li>
      
  
  <li>
    <a href="#" class="button secondary">Link 2</a>
  </li>
      
  
  <li>
    <a href="#" class="button success">Link 3</a>
  </li>
    
</ul>
  </pre>

Результат будет что-то в виде цветов итальянского флага:<figure id="attachment_1416" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_groups_additional-600x281.png" alt="Button group с дополнительными классами" width="600" height="281" class="size-medium wp-image-1416" />][3]<figcaption class="wp-caption-text">Button group с дополнительными классами</figcaption></figure> 

### Панели кнопок (button bar) на Foundation

Группы кнопок, в свою очередь, можно объединять между собой, создавая **панели кнопок** (button bar). Для этой цели применяется элемент `div` в классом `.button-bar`:

<pre><div class="button-bar">
  <ul class="button-group">
    <li>
      <a href="#" class="button success small round">Link 1</a>
    </li>
          
    
    <li>
      <a href="#" class="button success small round">Link 2</a>
    </li>
          
    
    <li>
      <a href="#" class="button success small round">Link 3</a>
    </li>
        
  </ul>
      
  
  <ul class="button-group round">
    <li>
      <a href="#" class="button alert small">Link 1</a>
    </li>
          
    
    <li>
      <a href="#" class="button alert small">Link 2</a>
    </li>
          
    
    <li>
      <a href="#" class="button alert small">Link 3</a>
    </li>
        
  </ul>
    
</div>
  </pre>

Результат будет примерно таким:<figure id="attachment_1417" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_bar-600x281.png" alt="Button bar на Foundation" width="600" height="281" class="size-medium wp-image-1417" />][4]<figcaption class="wp-caption-text">Button bar на Foundation</figcaption></figure> 

### Видоизменение панели кнопок (button bar) на Foundation

Точно также, как и группу кнопок с классом `.button-group`, панель кнопок `.button-bar` можно видоизменять с помощью все тех же дополнительных классов, как показано на примере выше.

### Создание группы кнопок (button group) и панели кнопок (button bar) c помощью Sass

Ну и по становящейся уже традиции переходим к вопросу создания панели кнопок (button bar) на Foundation c помощью Sass. Для этой цели служат два миксина:

  * `button-group-container`
  * `button-group-style`

Создаю HTML-разметку с произвольным именем класса \`.horizontal:

<pre><ul class="horizontal">
  <li>
    <a href="#">Link 1</a>
  </li>
      
  
  <li>
    <a href="#">Link 2</a>
  </li>
      
  
  <li>
    <a href="#">Link 3</a>
  </li>
      
  
  <li>
    <a href="#">Link 4</a>
  </li>
      
  
  <li>
    <a href="#">Link 5</a>
  </li>
    
</ul>
  </pre>

В файле `app.scss` прописываю для него следующие правила:

<pre>.horizontal{
    @include button-group-container;
    a{
      @include button;
    }
    &#038;>li{
      @include button-group-style;
    }
  } /* end horizontal */
  </pre>

Результат получается таким:<figure id="attachment_1418" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_bar_sass-600x281.png" alt="Button bar с помощью Sass на Foundation" width="600" height="281" class="size-medium wp-image-1418" />][5]<figcaption class="wp-caption-text">Button bar с помощью Sass на Foundation</figcaption></figure> 

У миксинов `button-group-container` и `button-group-style` имеются дополнительные параметры для тонкой настройки. Пример использования данных параметров показан на странице официальной документации &#8211; [Button groups][6].

### Редактирование файла app.scss

До этого момента так и не удосужился рассмотреть вопрос редактирования файла `app.scss`. Точнее, я уже упоминал о нем в начале обзора Foundation как о пользовательской таблице стилей, куда можно и нужно писать свои собственные CSS-правила. Вот теперь решил, что как раз настало время исправить свой недочет.

В начале файла `app.scss` имеются две строки:

<pre>@import "settings";
  @import "foundation";
  </pre>

Назначение их должно быть понятно:

  * строка `@import "settings";` импортирует Sass-переменные и их значения в проект
  * строка `@import "foundation";` импортирует сам фреймворк Foundation в проект

Однако, по аналогии с библиотекой Compass под препроцесор Sass, фреймворк Foundation позволяет выборочно импортировать в проект те свои возможности, которые необходимы на данный момент. Все эти возможности оформлены в виде отдельных модулей и прописаны каждый в отдельной строке файла `app.scss` в виде длинного закоментированного списка:

<pre>@import "settings";
  @import "foundation";

  // Or selectively include components
  //   @import
  //   "foundation/components/accordion",
  //   "foundation/components/alert-boxes",
  //   "foundation/components/block-grid",
  //   "foundation/components/breadcrumbs",
  ...
  </pre>

Допустим, на данный момент нам необходим модуль фреймворка Foundation для создания групп (button group) и панелей (button bar) кнопок. Такой модуль располагается в строке (легко найти по названию!):

<pre>// "foundation/components/button-groups";
  </pre>

И чтобы подключить только его, нужно выключить весь фреймворк Foundation целиком &#8211; закоментировать строку:

<pre>// @import "foundation";
  </pre>

и раскомментировать нижележащие строки следующим образом (только не забыть заменить запятую на точку с запятой в конце):

<pre>@import "settings";
  // @import "foundation";

  // Or selectively include components
  @import
  //   "foundation/components/accordion",
  //   "foundation/components/alert-boxes",
  //   "foundation/components/block-grid",
  //   "foundation/components/breadcrumbs",
  "foundation/components/button-groups";
  // @import "foundation/components/buttons";
  //   "foundation/components/clearing",
  </pre>

Вуаля! Все работает и не нужно &#8220;тащить&#8221; за собой целый воз плюшек, которые не нужны на данный момент.

Оцените статью:  
<span id="post-ratings-1411" class="post-ratings" data-nonce="4ae0b1ec15"><img id="rating_1411_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1411, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1411_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1411, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1411_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1411, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1411_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1411, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1411_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1411, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1411_text"></span></span><span id="post-ratings-1411-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1399 "Foundation - создаем кнопки"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_group.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_groups_additional.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_bar.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/06/foundation_button_bar_sass.png
 [6]: http://foundation.zurb.com/docs/components/button_groups.html "Button groups"