---
title: Что такое библиотека Modernizr
author: gearmobile
layout: post
permalink: /modernizr/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 6
ratings_score:
  - 29
ratings_average:
  - 4.83
categories:
  - Статьи по CSS
tags:
  - modernizr
---
Добрался до такой достаточно интересной темы, как JavaScript-библиотека Modernizr. Что это за библиотека и для чего она предназначена? Немного отвлекусь &#8211; на этом сайтике уже есть статья, посвященная библиотеке Modernizr &#8211; [Как использовать Modernizr][1]. Но эта статья является переводом чужой статьи. Кроме того, тема библиотеки Modernizr отдаленно схожа с предыдущей темой, посвященной условным комментариям &#8211; [Что такое условные комментарии][2]. В ней также упоминается способ выборки возможностей браузера, но условные комментарии &#8220;нацелены&#8221; на один конкретный браузер &#8211; IE; в то время как библиотека Modernizr более универсальная и с широким возможностями.

Начнем с предназначения &#8211; тут все предельно просто. Modernizr служит для автоматизации определения возможностей конкретного браузера. Другими словами, заходит посетитель на страницу `http://localhost:7788/third/` с помощью браузера Chrome версии 32, а Modernizr, установленный на этой странице, сразу же определяет: &#8220;*ага, этот браузер и этой версии поддерживает CSS-свойства `box-shadow`, `text-shadow`, `box-sizing`, `flexbox`, `rgba`, `hsla`, `background-size` и многое другое*&#8220;. Поэтому для этого браузера можно создавать на странице эффекты с помощью этих свойств &#8211; пользователь их увидит и оценит (может быть оценит). А вот технологию `touch` этот браузер не поддерживает, поэтому создавать на странице поддержку этой технологии и для этого браузера бесполезно &#8211; все равно работать не будет.

А вот если посетитель зайдет на эту же страницу с помощью браузера Firefox версии 22, то Modernizr обнаружит факт, что данный браузер не поддерживает модель `flexbox`, поэтому бесполезно (*и даже нельзя*) создавать страницу с помощью этой технологии для данного браузера.

Если же мы попробуем (ради эксперимента) зайти на эту страницу с помощью браузера IE7, то картина будет еще более печальной &#8211; там целая куча CSS-свойств не будет поддерживаться.

Надеюсь, мы разобрались тем, для чего предназначена библиотека Modernizr. Следовательно, ответили и на первый вопрос &#8211; что это за библиотека. Плавно переходим к вопросу &#8211; как воспользоваться этой библиотекой.

### Подключение библиотеки Modernizr

Чтобы подключить библиотеку Modernizr к HTML-странице и воспользоваться ее возможностями, необходимо сначала скачать файл библиотеки с официального сайта проекта &#8211; [Modernizr][3]. При попытке скачивания на сайте откроется конструктор, с помощью которого можно выбрать CSS3 или HTML5 свойства, поддержка которых требуется в проекте. Преимущество такого подхода в минимизации самой библиотеки &#8211; зачем загружать и использовать Modernizr, если из всех его возможностей используется только одна или две?

После получения файла библиотеки Modernizr подключаем его к HTML-странице, как самый обычный файл JavaScript. При этом обратите внимание, что для элемента `html` дописан класс `"no-js"` &#8211; он необходим для работы самой библиотеки:

<pre>


...
</pre>


<h3>
  Пример библиотеки Modernizr
</h3>


<p>
  После подключения библиотеки Modernizr открываем HTML-страницу в браузере и запускаем инспектор кода. И наблюдаем следующие &#8220;картины&#8221;:
</p>


<ul>
  <li>
    браузер Google Chrome v32:
  </li>
  
  
  <pre>
    <head>
  </pre>
  
  
  <li>
    браузер Mozilla Firefox v22:
  </li>
  
  
  <pre>
    <head>
  </pre>
  </ul>
  
  
  <p>
    Первое, что бросается в глаза &#8211; класс <code>"no-js"</code> поменялся на <code>"js"</code>! Это сделала библиотека Modernizr. А дальше идут совсем непонятные слова, отдаленно похожие на названия CSS3-свойств или HTML5-свойств. Ничего сложного в этих служебных словах нет &#8211; это собственные классы библиотеки Modernizr, с помощью которых она отмечает, что поддерживается конкретным браузером, а что &#8211; нет.
  </p>
  
  
  <p>
    К примеру, если браузер поддерживает CSS-свойство <code>box-shadow</code>, то это отмечается собственным классом библиотечки &#8211; <code>boxshadow</code>. А вот если CSS-свойство (<code>flexbox</code>) не поддерживается, то библиотека Modernizr &#8220;прикрепляет&#8221; к названию своего класса префикс <code>"no-"</code> и получается <code>no-flexbox</code>. Поэтому, смотрим на вывод в инспекторе кода и сразу видим, что браузер Firefox v.22 (<em>например</em>) поддерживает очень много HTML5 и CSS3-свойств, но вот модель <code>flexbox</code>, сенсорный экран, базы данных в веб или же CSS-reflections &#8211; этого данный браузер выполнить не может: <code>no-flexbox</code>, <code>no-touch</code>, <code>no-websqldatabase</code>, <code>no-cssreflections</code>.
  </p>
  
  
  <h3>
    Пример работы Modernizr
  </h3>
  
  
  <p>
    Все хорошо, скажете вы &#8211; определили возможности конкретного браузера. Но что нам это даст в практическом плане, при верстке страницы? Давайте рассмотрим небольшой пример. На странице в порядке эксперимента создан квадрат с фоновой заливкой зеленого (<code>hsl(120,100%,50%)</code>) цвета:
  </p>
  
  
  <pre>
p{
  width: 200px;
  height: 200px;
  border: 1px solid #000;
  background-color: hsl(120,100%,50%);
  margin: 20px auto;
}
</pre>
  <figure id="attachment_1089" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_simple_page.jpg"><img src="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_simple_page-600x272.jpg" alt="Пример обычного квадрата на CSS" width="600" height="272" class="size-medium wp-image-1089" /></a><figcaption class="wp-caption-text">Пример обычного квадрата на CSS</figcaption></figure>
  
  
  <p>
    Допустим, мы хотим, чтобы для браузеров, в которых отсутствует поддержка сенсорного экрана, фоновая заливка этого квадрата была не зеленым (<code>hsl(120,100%,50%)</code>) цветом, а синим (<code>hsl(240,100%,50%)</code>). Для этого мы немного переделаем код, представленный выше и посмотрим на результат:
  </p>
  
  
  <pre>
p{
  width: 200px;
  height: 200px;
  border: 1px solid #000;
  background-color: hsl(120,100%,50%);
  margin: 20px auto;
}

.no-touch p{
  background-color: hsl(240,100%,50%);
}
</pre>
  <figure id="attachment_1090" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_class_no-touch.jpg"><img src="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_class_no-touch-600x272.jpg" alt="Стилизованный с помощью библиотеки Modernizr квадрат" width="600" height="272" class="size-medium wp-image-1090" /></a><figcaption class="wp-caption-text">Стилизованный с помощью библиотеки Modernizr квадрат</figcaption></figure>
  
  
  <p>
    Фантастика! А что-же произошло, что наш квадрат стал из зеленого синим? Все просто &#8211; это обыкновенная <strong>CSS-специфичность</strong>. Библиотека Modernizr автоматически &#8220;прицепила&#8221; к элементу <code>html</code> класс <code>no-touch</code> (<em>в числе многих других &#8211; стоит отметить</em>). И вот получается, что наш браузер не поддерживает сенсорный экран, у родителя (<code>html</code>) ВСЕХ элементов страницы появляется класс <code>no-touch</code>, который по правилам CSS-специфичности (10+1=11 явно больше, чем 1) переопределяет значение правила <code>background-color</code> для элемента <code>p</code> с <code>hsl(120,100%,50%)</code> на <code>hsl(240,100%,50%)</code>. Вот и вся &#8220;хитрость&#8221; работы библиотеки Modernizr! ))
  </p>
  
  
  <p>
    Теперь, зная принцип работы Modernizr, можно легко создавать CSS-правила под определенные возможности браузера. К примеру, зная, что IE6 не умеет работать с градиентами через CSS, можно прописать два правила:
  </p>
  
  
  <pre>
.goo{
  background-image: -webkit-linear-gradient(bottom,#000,#fff);
  background-image:   -moz-background-image-linear-gradient(bottom,#000,#fff);
  background-image:     -o-background-image-linear-gradient(bottom,#000,#fff);
  background-image:                         linear-gradient(bottom,#000,#fff); 
}

.no-cssgradients .goo{
  background: url(../img/bg.jpg) top left repeat-x;
}
</pre>
  
  
  <h3>
    Загрузчик библиотеки Modernizr
  </h3>
  
  
  <p>
    Отлично! Но писать по два условия на одно правило &#8211; это утомительно и не рационально (представьте, насколько раздуется код!). Поэтому в библиотеке Modernizr придумали специальный механизм для тестирования CSS-свойств и применения соответствующих CSS-правил. Заключается оно в следующем &#8211; при рендеринге HTML-страницы создается один большой JavaScript-объект с именем Modernizr.
  </p>
  
  
  <p>
    У этого объекта есть свойства:
  </p>
  
  
  <ul>
    <li>
      Modernizr.flexbox
    </li>
    
    
    <li>
      Modernizr.canvas
    </li>
    
    
    <li>
      Modernizr.backgroundsize
    </li>
    
    
    <li>
      &#8230;
    </li>
    
    
    <li>
      Modernizr.boxshadow
    </li>
    
    
    <li>
      Modernizr.borderradius
    </li>
    
  </ul>
  
  
  <p>
    &#8230; и так далее. В библиотеке Modernizr встроен загрузчик, который загружает указанное в условии проверки свойство и применяет к нему правила в зависимости от того, <code>true</code> или <code>false</code> получится в результате проверки.
  </p>
  
  
  <p>
    Например, давайте сделает так, чтобы наш квадрат имел фоновую заливку голубого (cyan) цвета, если браузер <strong>поддерживает</strong> модель <code>flexbox</code>, и фиолетового (magenta) цвета, если <strong>не поддерживает</strong> модель <code>flexbox</code>. Для этого создадим два разных CSS-файла:
  </p>
  
  
  <ul>
    <li>
      flexbox.css
    </li>
    
    
    <li>
      no_flexbox.css
    </li>
    
  </ul>
  
  
  <p>
    &#8230; в первом (<code>flexbox.css</code>) из которых пропишем:
  </p>
  
  
  <pre>
p{
  background-color: hsl(180,100%,50%);
}
</pre>
  
  
  <p>
    &#8230; во втором (<code>no_flexbox.css</code>) пропишем:
  </p>
  
  
  <pre>
p{
  background-color: hsl(300,100%,50%);
}
</pre>
  
  
  <p>
    &#8230; и затем создадим еще один JavaScript-файл <code>check.js</code> (подключается к HTML-странице как обычно, тегом <code>script</code>), в котором запишем следующее:
  </p>
  
  
  <pre>
Modernizr.load({
  test: Modernizr.flexbox,
  yep:  'css/flexbox.css',
  nope: 'css/no_flexbox.css'
});
</pre>
  
  
  <p>
    Здесь:
  </p>
  
  
  <ul>
    <li>
      строка <code>Modernizr.load</code> &#8211; это загрузчик библиотеки Modernizr;
    </li>
    
    
    <li>
      строка <code>test: Modernizr.flexbox</code>    &#8211; условие проверки (какое свойство объекта Modernizr проверяем);
    </li>
    
    
    <li>
      строка <code>yep: 'css/flexbox.css'</code>     &#8211; загрузить файл <code>flexbox.css</code>, если условие выполняется (<em>yep &#8211; да</em>);
    </li>
    
    
    <li>
      строка <code>nope: 'css/no_flexbox.css'</code> &#8211; загрузить файл <code>no_flexbox.css</code>, если условие не выполняется (<em>nope &#8211; нет</em>).
    </li>
    
  </ul>
  
  
  <p>
    Результат работы вышеприведенного кода в браузере Chrome (поддерживает модель <code>flexbox</code>) и браузере Firefox (не поддерживает модель <code>flexbox</code>):
  </p>
  <figure id="attachment_1091" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_yep_flexbox.jpg"><img src="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_yep_flexbox-600x272.jpg" alt="Modernizr - поддержка flexbox" width="600" height="272" class="size-medium wp-image-1091" /></a><figcaption class="wp-caption-text">Modernizr &#8211; поддержка flexbox</figcaption></figure>
  <figure id="attachment_1092" style="width: 600px;" class="wp-caption aligncenter"><a href="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_nope_flexbox.jpg"><img src="http://localhost:7788/third/wp-content/uploads/2014/03/modernizr_nope_flexbox-600x445.jpg" alt="Modernizr - отсутствие поддержки flexbox" width="600" height="445" class="size-medium wp-image-1092" /></a><figcaption class="wp-caption-text">Modernizr &#8211; отсутствие поддержки flexbox</figcaption></figure>
  
  
  <h3>
    Заключение
  </h3>
  
  
  <p>
    В пользу применения библиотеки Modernizr можно сказать еще то, что такой полезный файлик, как <code>html5shiv.js</code> уже автоматически включен в состав этой библиотеки. Поэтому, при подключении Modernizr можно смело переходить на doctype html5 и не заморачиваться поиском и подключением файла <code>html5shiv.js</code>.
  </p>
  
  
  <p>
    На этом краткий обзор библиотеки Modernizr можно закончить.
  </p>
  
  
  <p>
    Оцените статью:<br />
    <span id="post-ratings-1087" class="post-ratings" data-nonce="58bccfa909"><img id="rating_1087_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1087, 1, '1 Star');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1087_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1087, 2, '2 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1087_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1087, 3, '3 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1087_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1087, 4, '4 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1087_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1087, 5, '5 Stars');" onmouseout="ratings_off(4.8, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>6</strong> votes, average: <strong>4,83</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1087_text"></span></span><span id="post-ratings-1087-loading" class="post-ratings-loading">
    			<img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>
  </p>

 [1]: http://localhost:7788/third/how-to-use-modernizr/ "Как использовать Modernizr"
 [2]: http://goo.gl/FGdZyl "Что такое условные комментарии"
 [3]: http://modernizr.com/ "Modernizr"