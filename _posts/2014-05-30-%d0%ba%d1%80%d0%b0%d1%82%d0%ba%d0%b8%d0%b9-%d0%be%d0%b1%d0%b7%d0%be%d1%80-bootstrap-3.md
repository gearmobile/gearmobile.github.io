---
title: Краткий обзор Bootstrap 3
author: gearmobile
excerpt: '<p>Еще один фреймворк из бесчисленного на сегодняшний день полка фреймворков - Bootstrap 3. Точнее было бы сказать, что не еще один - а флагман CSS-фреймворков! Версия 2 вышла давно и на сегодня является устаревшей. Сегодня самая современная версия - это версия 3. Поэтому ее мы и будем рассматривать. Вопрос данной статьи будет посвящен основе данной фреймворка - CSS-сетке и особенностям ее создания в версии 3.</p>'
layout: post
permalink: /%d0%ba%d1%80%d0%b0%d1%82%d0%ba%d0%b8%d0%b9-%d0%be%d0%b1%d0%b7%d0%be%d1%80-bootstrap-3/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 8
ratings_score:
  - 39
ratings_average:
  - 4.88
categories:
  - Статьи по CSS
tags:
  - bootstrap
---
Еще один фреймворк из бесчисленного на сегодняшний день полка фреймворков &#8211; Bootstrap 3. Точнее было бы сказать, что не еще один &#8211; а флагман CSS-фреймворков! Версия 2 вышла давно и на сегодня является устаревшей. Сегодня самая современная версия &#8211; это версия 3. Поэтому ее мы и будем рассматривать. Вопрос данной статьи будет посвящен основе данной фреймворка &#8211; CSS-сетке и особенностям ее создания в версии 3.

### Установка и настройка Bootstrap 3

Ничего сложного и необычного в установке фреймворка Bootstrap 3 нет. Для этого скачиваем дистрибутив с официального сайта [Bootstrap 3][1], распаковываем архив в готовый проект-директорию.

Затем с официального сайта берем готовый шаблон HTML-документа &#8211; [Basic template][2] и создаем свой собственный индексный файл HTML:

<pre>
  
    
    
      
      
    
  
  </pre>

В этом файле проверяем правильность путей для CSS и JS-файлов:

<pre><link href="css/bootstrap.css"        rel="stylesheet" />

<link href="css/bootstrap-theme.css"  rel="stylesheet" />
...
    
  </pre>

Все готово для дальнейшей работы.

### Система сеток Bootstrap 3

Важнейшей составляюшей любого CSS-фреймворка является система CSS-сетки (grid). Как и в предыдущей версии Bootstrap 2, в версии 3 используется 12-ти колоночная система.

Однако, в Bootstrap 3 применяются четыре типа классов для создания адаптивной (responsive) сетки. На официальном сайте Bootstrap 3 имеется таблица с побробным и наглядным описанием этих классов &#8211; [Grid Options][3].<figure id="attachment_1301" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/bootstrap3_grid-options-600x356.png" alt="Таблица классов для CSS-сетки Bootstrap 3" width="600" height="356" class="size-medium wp-image-1301" />][4]<figcaption class="wp-caption-text">Таблица классов для CSS-сетки Bootstrap 3</figcaption></figure> 

В этой таблице представлены четыре ширины экрана устройства, на котором будет отображена страница. Колонка &#8220;Extra small devices&#8221; с шириной менее 768px обозначает **мобильные устройства**. Колонка &#8220;Small devices&#8221; с шириной равной или больше 768px представляет **планшетные компьютеры** (планшеты). Две остальные колонки представляют **обычный настольный монитор** через колонку &#8220;Medium devices&#8221; с шириной равной или больше 992px и **широкоформатный монитор** через колонку &#8220;Large devices&#8221; с шириной равной или больше 1200px.

Вышеназванные величины 768px, 992px и 1200px являются контрольными точками (breakpoints), служащими для обработки медиа-запросов в адаптивном дизайне страницы.

В данной таблице строка &#8220;Class prefix&#8221; является чуть ли не самой важной, так как в ней содержатся имена (префиксы) классов фреймворка Bootstrap 3 для каждого из четырех типов устройств. Для мобильного устройства имя (префикс) класса будет `.col-xs-`, для планшетного компьютера префикс будет `.col-sm-`, для обычного монитора &#8211; `.col-md-` и для широкоформатного монитора &#8211; `.col-lg-`. Для видно из названия префиксов, они являются сокращениями от названия самих устройств, поэтому их легко запомнить.

Вот и все, что необходимо знать о системе CSS-сеток в фреймворке Bootstrap 3. Дальше можно легко домыслить ход построения адаптивной сетки для конкретного сайта.

### Пример создания CSS-сетки в Bootstrap 3

Допустим, необходимо создать следующий макет:

  * для широкоформатного монитора в макете должно быть 2 столбца &#8211; один шириной 10 колонок и второй шириной 2 колонки;
  * для обычного монитора 2 столбца &#8211; один шириной 8 колонок и второй шириной 4 колонки;
  * для планшета 2 столбца &#8211; один шириной 6 колонок и второй шириной также 6 колонок;
  * для мобильного устройства макет должен остаться, как и для планшета &#8211; два столбца одинаковой ширины.

То есть, при изменении ширины монитора устройства ширина столбцов в макете должна меняться, как показано выше. Для этого создадим простую разметку и добавим в нее классы Bootstrap 3:

<pre><div class="container">
  <div class="row">
    <div class="col-lg-10  col-md-8  col-sm-6">
      
    </div>
          
    
    <div class="col-lg-2   col-md-4  col-sm-6">
      
    </div>
        
  </div>
    
</div>
  </pre>

Если открыть созданную страницу в окне браузера и попробовать менять ширину его окна, то в диспечере свойств страницы увидим метаморфозы, связанные с работой медиа-запросов (media-queries). При ширине окна больше 1200px будем наблюдать левый столбец шириной в 10 колонок и правый столбец шириной в 2 колонки.

Уменьшив ширину окна до 992px, получим левый столбец шириной в 8 колонок и правый стлбец шириной в 4 колонки. Еще уменьшив окно до 768px, получим два одинаковых столбца шириной в 6 колонок. Если окно окончательно уменьшится (менее 768px), ширина столбцов останется прежней, но они расположаться вертикально, друг под другом (*поведение по умолчанию*).

### Видимость элементов сетки в Bootstrap 3

Немного усложним задачу и сделаем ее интереснее ради теоретического примера работы фреймворка Bootstrap 3. Допустим, нам необходим такой макет:

  * широкоформатный монитор &#8211; 12 колонок;
  * обычный монитор &#8211; 3 колонки;
  * планшетный монитор &#8211; 3 колонки;
  * мобильный монитор &#8211; 2 колонки.

Тогда HTML-разметка и классы фреймворка Bootstrap 3 следующими:

<pre><div class="container">
  <div class="row">
    <div class="col-lg-2  col-md-4   col-sm-4   col-xs-6">
      
    </div>
          
    
    <div class="col-lg-2  hidden-md  hidden-sm  hidden-xs">
      
    </div>
          
    
    <div class="col-lg-2  col-md-4   col-sm-4   col-xs-6">
      
    </div>
          
    
    <div class="col-lg-2  hidden-md  hidden-sm  hidden-xs">
      
    </div>
          
    
    <div class="col-lg-2  col-md-4   col-sm-4   hidden-xs">
      
    </div>
          
    
    <div class="col-lg-2  hidden-md  hidden-sm  hidden-xs">
      
    </div>
        
  </div>
    
</div>
  </pre>

В данном случае при измении ширины окна браузера будет меняться количество колонок внутри макета. При ширине большей 1200px число колонок будет равняться шести. При уменьшении окна до ширины в 992px число колонок изменится до 4-х и будет оставаться таковым при ширине окна 768px. Если окно еще уменьшится ниже 768px, то количество колонок измениться до двух.

Подобные метаморфозы возможны благодаря классу `hidden-x`, который вы могли заметить в разметке. Задача этого класса скрыть указанный элемент при достижении окном браузера определенной контрольной точки. Для каждого из предполагаемых состояний окна браузера необходимо указать класс &#8211; `hidden-lg`, `hidden-md`, `hidden-sm`, `hidden-xs`.<figure id="attachment_1304" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/bootstrap3_available-classes-600x452.png" alt="Сравнительная таблица классов hidden и visible в Bootstrap 3" width="600" height="452" class="size-medium wp-image-1304" />][5]<figcaption class="wp-caption-text">Сравнительная таблица классов hidden и visible в Bootstrap 3</figcaption></figure> 

Противоположностью класса `hidden-x` является класс `visible-x`. Несмотря на то, что действие этих классов должно быть прямо противоположным друг другу, на практике это различие уловить не так просто и тут может помочь сравнительная таблица с официального файта Bootstrap 3 &#8211; [Responsive utilities][6]. В этой таблице (*см. таблицу выше*) хорошо видно различие между этими классами. В то время как класс `hidden-x` производит скрытие элемента в определенной контрольной точке (breakpoint), во всех остальных состояниях элемент **видимый**. Класс `visible-x` делает элемент видимым только в определенном состоянии &#8211; во всех остальных состояниях элемент **невидимый**.

### Вложенность (nesting) сетки в Bootstrap 3

CSS-сетка в фреймворке Bootstrap 3 позволяет выполнять вложение одних ячеек в другие. Такое явление называется nesting. К примеру, необходим создать такую HTML-разметку:

<pre><div class="container">
  <div class="row primo">
    <div class="col-lg-4">
      
    </div>
          
    
    <div class="col-lg-4">
      
    </div>
          
    
    <div class="col-lg-4">
      
    </div>
        
  </div>
  
      
  
  <div class="row secondo">
    <div class="col-lg-8">
      <div class="row">
        <div class="col-lg-6">
          
        </div>
                  
        
        <div class="col-lg-6">
          
        </div>
                
      </div>
            
    </div>
          
    
    <div class="col-lg-4">
      
    </div>
        
  </div>
  
      
  
  <div class="row tetro">
    <div class="col-lg-6">
      <div class="row">
        <div class="col-lg-6">
          
        </div>
                  
        
        <div class="col-lg-6">
          
        </div>
                
      </div>
            
    </div>
          
    
    <div class="col-lg-6">
      <div class="row">
        <div class="col-lg-6">
          
        </div>
                  
        
        <div class="col-lg-6">
          
        </div>
                
      </div>
            
    </div>
        
  </div>
  
      
  
  <div class="row quattro">
    <div class="col-lg-2">
      
    </div>
          
    
    <div class="col-lg-2">
      
    </div>
          
    
    <div class="col-lg-2">
      
    </div>
          
    
    <div class="col-lg-2">
      
    </div>
          
    
    <div class="col-lg-2">
      
    </div>
          
    
    <div class="col-lg-2">
      
    </div>
        
  </div>
  
    
</div>
  </pre>

Для наглядности примера оставим для элементов только один класс `.col-lg-`. Блок с классом `primo` имеет три обычные колонки `col-lg-4`. Блок с классом `secondo` имеет две колонки &#8211; `col-lg-8` и `col-lg-4`. Внутри колонки `col-lg-8` размещено еще два блока равной ширины &#8211; две колонки с классом `col-lg-6`. Это пример вложенности (nesting) одних ячеек CSS-сетки Bootstrap 3 в другие ячейки.

Аналогичная ситуация с блоком класса `tetro`, но в нем в оба &#8220;первичных&#8221; блока вложены еще два блока. Всего получается четыре блока. С блоком класса `quattro` все просто &#8211; там &#8220;обычные&#8221; (не вложенные) шесть блоков класса `col-lg-2`.

При этом нужно обратить внимание (если еще не догадались), что при вложении одних блоков в другие ширина блока-родителя принимается по умолчанию равной 12-колонкам.

### Смещение (offsetting) колонок в Bootstrap 3

В Bootstrap 3 можно смещать колонки вправо с помощью класса `.col-*-offset-*`, который добавляет margin-left для указанной колонки. Смещение производится на ширину колонки, кратную указанному количеству.

Приведу пример, чтобы было наглядно понятно:

<pre><div class="container">
  <div class="row">
    <div class="col-lg-8">
      
    </div>
          
    
    <div class="col-lg-2 col-lg-offset-2 right">
      
    </div>
        
  </div>
    
</div>
  </pre>

В этом примере колонка с классом `right` имеет ширину в два столбца и смещается вправо опять таки на два столбца &#8211; `col-lg-offset-2`. При этом стоит также заметить, что данное смещение будет выполняться только при ширине экрана больше 1200px (breakpoint), на что указывает имя класса &#8211; `col-lg-`. Если необходимо, чтобы такое смещение сохранялось при меньших размерах окна браузера, необходимо явно указать это в коде:

<pre><div class="container">
  <div class="row">
    <div class="col-lg-8">
      
    </div>
          
    
    <div class="col-lg-2 col-lg-offset-2 col-md-offset-2 col-sm-offset-2 col-xs-offset-2 right">
      
    </div>
        
  </div>
    
</div>
  </pre>

### Адаптивная (responsive) сетка в Bootstrap 3

Переключать ширину сетки с фиксированной на резиновую в Bootstrap 3 можно точно также, как и во 2-й версии. Для этого нужно заменить для блока-контейнера имя класса с `container` на `container-fluid`:

<pre><div class="container-fluid">
  <div class="row">
    ...
        
  </div>
    
</div>
  </pre>

### Заключение

На этом обзор CSS-сетки в фреймворке Bootstrap 3 можно считать законченным. Субъективно для меня был интересен именно этот вопрос. Что касается рассмотрения остальных классов, предназначенных для оформления различных элементов на странице, то мне они кажутся не такими интересныи и важными.

Может быть, в дальнейшем я и вернусь к расмотрению деталей фреймворка Bootstrap 3.

Оцените статью:  
<span id="post-ratings-1297" class="post-ratings" data-nonce="0f40764630"><img id="rating_1297_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1297, 1, '1 Star');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1297_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1297, 2, '2 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1297_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1297, 3, '3 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1297_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1297, 4, '4 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1297_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1297, 5, '5 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>8</strong> votes, average: <strong>4,88</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1297_text"></span></span><span id="post-ratings-1297-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://getbootstrap.com/ "Bootstrap 3"
 [2]: http://getbootstrap.com/getting-started/#template "Basic template"
 [3]: http://getbootstrap.com/css/#grid "Grid Options"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/05/bootstrap3_grid-options.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/05/bootstrap3_available-classes.png
 [6]: http://getbootstrap.com/css/#responsive-utilities "Responsive utilities"