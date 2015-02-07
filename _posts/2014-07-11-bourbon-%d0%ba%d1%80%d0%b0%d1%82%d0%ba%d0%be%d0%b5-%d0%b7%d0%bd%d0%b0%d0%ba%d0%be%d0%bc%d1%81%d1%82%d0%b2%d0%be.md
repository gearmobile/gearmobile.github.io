---
title: 'Bourbon + Sass &#8211; краткое знакомство'
author: gearmobile
excerpt: 'Библиотека миксинов под препроцессор Sass с названием Bourbon - вот о чем будет сегодняшний краткий обзор. Данная статья не могла не появиться по нескольким причинам. Первая - я являюсь большим поклонником препроцессора Sass и библиотеки миксинов Compass под него. А библиотека Bourbon является аналогом Compass, но обладает некоторыми расширенными возможностями по сравнению с последней.'
layout: post
permalink: /bourbon-%d0%ba%d1%80%d0%b0%d1%82%d0%ba%d0%be%d0%b5-%d0%b7%d0%bd%d0%b0%d0%ba%d0%be%d0%bc%d1%81%d1%82%d0%b2%d0%be/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 10
ratings_average:
  - 3.33
categories:
  - Статьи по CSS
tags:
  - bourbon
  - sass
---
Библиотека миксинов (mixin) под препроцессор Sass под названием [Bourbon][1] &#8211; вот о чем будет сегодняшний краткий обзор. Данная статья не могла не появиться по нескольким причинам. Первая &#8211; я являюсь большим поклонником препроцессора Sass и библиотеки миксинов Compass под него. Библиотека Bourbon является аналогом Compass, просто она меньше по размеру и возможностям. Но это не значит, что она хуже &#8211; она обладает некоторыми возможностями, которых нет в Compass.

Помимо этого, существует прекрасная сравнительная статья Sass-гуру [Hugo Giraudel][2], посвященная этим двум библиотекам под один препроцессор. Оригинал статьи находиться здесь &#8211; [Sass Frameworks: Compass or Bourbon?][3], а посильный перевод этой статьи размещен здесь &#8211; [Что выбрать &#8211; Compass или Bourbon?][4]. В этой статье Юг Жиродель (Hugo Giraudel) приводит преимущества использования библиотеки Bourbon и сопутствующих ему пакетов, таких как Neat для создания адаптивной CSS-сетки (grid).

Однако, после прочтения вышеназванной статьи один вопрос остается открытым &#8211; а как установить библиотеку Bourbon? Что можно в ней делать и как это делать? На эти вопросы я постараюсь ответить самому себе (*и возможно &#8211; вам, уважаемый читатель*).

### Установка библиотеки Bourbon

Инсталляцию библиотеки миксинов Bourbon я буду производить под операционной системой Linux Mint 17 Cinnamon, просто потому что мне так интереснее. Под OS Windows процесс ничем не отличается от того, который будет описан здесь. Единственное условие &#8211; на момент установки Bourbon в системе уже должны стоять и нормально работать **Ruby + Sass**.

Установка библиотеки сводиться к одной вещи &#8211; установке пакета `bourbon` под Ruby. Выполняется это одной командой:

<pre>$ sudo gem install bourbon
  </pre>

Проверяю, какая версия этой библиотеки &#8220;попала&#8221; ко мне:

<pre>$ bourbon -v
  Bourbon 4.0.2
  </pre>

Отлично! Теперь можно приступать к разворачиванию проекта с поддержкой Bourbon.

### Создание проекта Bourbon

Перехожу в директорию с опытными (подопытными?) образцами всего разного и создаю там папку с именем `bourbon`:

<pre>$ cd ~/Projects/
  $ mkdir bourbon
  $ cd bourbon/
  </pre>

&#8230; и запускаю там команду:

<pre>$ bourbon install
  Bourbon files installed to bourbon/
  </pre>

Не знаю, как вы, а я сразу после этого задал себе вопрос &#8211; &#8220;А что это было?&#8221; Что это за команда и зачем она нужна? Все оказалось просто.

В библиотеке Compass в таблице стилей конкретно указывается, какой модуль необходимо подключить к проекту. К примеру, таким образом:

<pre>@import "compass/reset";
  @import "compass/utilities/general/clearfix";
  @import "compass/css3/transition";
  @import "compass/css3/border-radius";
  </pre>

В результате Compass **выборочно подгружает по сети** только указанные модули. И ничего больше.

Библиотека Bourbon поступает прямо противоположно &#8211; она устанавливает локально, в отдельную папку проекта (имя этой папки всегда &#8211; `bourbon`) **все миксины сразу**, на все случаи жизни. Если посмотреть на содержимое папки `bourbon`, то увидим такую картину:

<pre>$ ls -l bourbon/
  drwxr-xr-x 2 addons
  -rw-r--r-- 1 _bourbon-deprecated-upcoming.scss
  -rw-r--r-- 1 _bourbon.scss
  drwxr-xr-x 2 css3
  drwxr-xr-x 2 functions
  drwxr-xr-x 2 helpers
  drwxr-xr-x 2 settings
  </pre>

Видим, что все миксины &#8220;расфасованы&#8221; по папкам в зависимости от их назначения. Давайте &#8220;заглянем&#8221; в одну из этих подпапок &#8211; пусть это будет `css3`:<figure id="attachment_1491" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/bourbon-600x377.png" alt="Содержимое папки Bourbon" width="600" height="377" class="size-medium wp-image-1491" />][5]<figcaption class="wp-caption-text">Содержимое папки Bourbon</figcaption></figure> 

Видим здесь готовые миксины для создания самых различных CSS3-эффектов &#8211; `border-radius`, `gradient`, `transform`, `transition` и так далее. Ну, теперь все понятно, не правда ли?

### Включение библиотеки Bourbon в проект

Дело осталось за малым &#8211; включить поддержку миксинов библиотеки в таблицу стилей. Выполняется это обычно, директивой `@import`. Для этого создаю структуру папок и файлов будущего проекта (*однако, Compass это может делать одной командой!*):

<pre>$ mkdir sass
  $ mkdir css
  $ touch sass/style.scss
  $ touch css/style.css
  $ touch index.html
  </pre>

&#8230; и помещаю одну строку в таблице стилей `style.scss`:

<pre>@import "bourbon/bourbon";
  </pre>

### Мониторинг изменений в проекте Bourbon

Чтобы автоматически отслеживать изменения в файле таблиц стилей `style.scss` и выполнять компиляцию в CSS-стили, запускаю команду мониторинга:

<pre>$ sass --watch sass/style.scss:css/style.css
  </pre>

### Использование библиотеки Bourbon

Ну и что, скажете вы? Что дальше? А ничего &#8211; дальше только пользоваться библиотекой Bourbon. Для этого с главной страницы проекта [Bourbon][1] переходим на страницу документации, нажав кнопочку <a href="http://bourbon.io/docs/" title="Bourbon Documentation" target="_blank">DOCS</a>. В правом верхнем углу есть две ссылки, одна из которых **View Spec** &#8211; ведет на страницу CSS-документации MDN, а вторая **View Source** &#8211; на страницу GitHub c рабочими примерами миксинов.

Также видим, что миксинов здесь даже на беглый взгляд значительно меньше, чем в библиотеке <a href="http://beta.compass-style.org/reference/compass/" title="Compass Core Framework" target="_blank">Compass</a>. Ну это ничего.

#### Bourbon &#8211; создаем кнопки

Давайте для начала создадим на Bourbon что-нибудь простенькое. Пусть это будут кнопки. Для этого перейдем на страницу документации по созданию кнопок &#8211; [Button][6].

Видим, что в библиотеке Bourbon есть три готовых миксина для создания кнопок:

  * simple
  * pill
  * shiny

Поэтому в HTML-коде создаю кнопку:

<pre><button class="simple" type="button"></button>
  </pre>

&#8230; и прописываю для нее миксин в таблице стилей `style.scss`:

<pre>.simple{
    @include button;
  }
  </pre>

Смотрим результат в браузере &#8211; готовая красивая синенькая кнопочка! Точно также можно создать еще две другие кнопки, с помощью миксинов `pill` и `shiny`. При этом можно передать в качестве аргумента фоновый цвет создаваемой кнопки:

<pre>.pill{
    @include button(pill);
  }

  .shiny{
    @include button(shiny, #ff9900);
  }
  </pre>

Ради любопытства посмотрите на скомпилированный CSS-код этих кнопок в файле `style.css` &#8211; вы будете поражены однозначно! ))

#### Bourbon &#8211; создаем треугольники

Кто из внимательных читателей может на память создать треугольник на чистом CSS? Конечно, там нет ничего сложного, но уверен &#8211; время у вас все равно уйдет на то, чтобы вспомнить все тонкости этого процесса &#8211; обнулить ширину и высоту, задать ширину и цвет границы, убрать ее с трех остальных сторон и так далее.

А вот в библиотеке Bourbon эта задача выполняется в одну строку, для этого достаточно миксину `triangle` передать всего лишь три аргумента &#8211; ширину границы, цвет границы, **направление треугольник**а:

<pre>@include triangle(2em, #ff9900, up);
  </pre>

Все &#8211; треугольник готов! Самые разные варианты создания теругольников хорошо описаны на странице документации &#8211; [Triangle][7].

### Заключение

На этом задачу ознакомления с библиотекой Bourbon считаю законченной. Читайте документацию &#8211; там все хорошо описано!

Оцените статью:  
<span id="post-ratings-1483" class="post-ratings" data-nonce="195840ba41"><img id="rating_1483_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1483, 1, '1 Star');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1483_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1483, 2, '2 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1483_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1483, 3, '3 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1483_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1483, 4, '4 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1483_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1483, 5, '5 Stars');" onmouseout="ratings_off(3.3, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>3,33</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1483_text"></span></span><span id="post-ratings-1483-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://bourbon.io/ "Bourbon"
 [2]: http://hugogiraudel.com/ "Hugo Giraudel"
 [3]: http://www.sitepoint.com/compass-or-bourbon-sass-frameworks/ "Sass Frameworks: Compass or Bourbon?"
 [4]: http://localhost:7788/third/?p=1340 "Что выбрать - Compass или Bourbon?"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/07/bourbon.png
 [6]: http://bourbon.io/docs/#buttons "Button"
 [7]: http://bourbon.io/docs/#triangle "Triangle"