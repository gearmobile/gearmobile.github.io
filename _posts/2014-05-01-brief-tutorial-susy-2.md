---
title: Краткое руководство по Susy 2
author: gearmobile
layout: post
permalink: /brief-tutorial-susy-2/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 5
ratings_score:
  - 22
ratings_average:
  - 4.4
categories:
  - Статьи по CSS
tags:
  - compass
  - susy
---
Susy является вспомогательным инструментом, с помощью которого можно создавать гибкие настраиваемые CSS-сетки буквально на лету. На момент написания статьи состоялся релиз Susy 2. Если у вас есть опыт работы с предыдущей версией этого фреймворка &#8211; Susy 1, то вам наверняка еще больше понравиться работа в Susy 2, так как эта версия предоставляет веб-разработчику еще большую гибкость.

Данное руководство по Susy 2 состоит из двух частей; в этой первой части будет показан процесс создания шаблона в фреймворке Susy 2.

## Почему именно Susy 2

Как я уже упоминал ранее, Susy является вспомогательным инструментом, благодаря которому можно создавать гибкие сетки практически любого вида, без необходимости производить многочисленные рутинные вычисления. Преимуществом Susy в отделении CSS от HTML.

Если у вас до прочтения этой статьи был опыт работы с такими традиционными фреймворками, как Foundation или Bootstrap, то вы должны знать, что в этих фреймворках ширина колонок и контрольные точки breakpoints имеют фиксированные значения. Для изменения разметки необходимо добавлять классы к элементам в HTML-код (*прим. переводчика &#8211; забыл, как называется случай, когда HTML-структура засорена чрезмерным количеством классов*).

Фреймворк Susy лишен такого недостатка &#8211; классы создаются непосредственно под необходимый случай и применяются к конкретной сетке.

Как мне кажется, этот момент довольно трудно понять сразу, так как является достаточно абстрактным понятием. Вместо того, чтобы пытаться бесконечно объяснять теорию, мне кажется гораздо лучшим для понимания воспользоваться практическим примером. Для этого создадим с помощью Susy 2 10-колоночный тестовый макет, нарисованный Arnaud Guera (AG) для официального сайта Susy 2:<figure id="attachment_1150" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/susy2-1-600x344.png" alt="Тестовый шаблон Arnaud Guera" width="600" height="344" class="size-medium wp-image-1150" />][1]<figcaption class="wp-caption-text">Тестовый шаблон Arnaud Guera</figcaption></figure> 

## Установка Susy 2

### Если Susy вообще не установлен

Фреймворк Susy для своей работы нуждается в препроцессоре Sass. Поэтому, если у вас на локальном компьютере еще не установлены как Sass, так и Susy, то необходимо это сделать:

<pre>sudo gem install sass
sudo gem install susy
</pre>

### Если Susy уже установлен

Если фреймворк Susy уже установлен на вашем компьютере и также имеется Ruby RVM (Ruby Version Manager), то можно произвести обновление с помощью команды:

<pre>sudo gem update</pre>

Если у вас эта команда не сработала, то это означает, что нужно попробовать другой способ или же сначала [установить Ruby RVM][2].

Второй способ установки фреймворка Susy версии 2 несколько более &#8220;ручной&#8221;. Он предполагает, что сначала нужно деинсталлировать предыдущие версии Sass\Susy, а затем установить их снова. Этот способ является наилучшим, если необходимо избежать ошибок при обновлении (как в первом случае).

<pre>sudo gem uninstall susy
sudo gem uninstall sass

sudo gem install sass
sudo gem install susy
</pre>

После успешной установки фреймворка Susy 2 на локальной машине, приступим к его базовой настройке.

## Базовая настройка Susy 2

Точно также, как и в первой версии, необходимо в конфигурационном файле config.rb указать, что фреймворк Susy должен быть включен в текущий проект:

<pre># Require any additional compass plugins here.
require 'susy'
</pre>

Затем нужно импортировать фреймворк Susy 2 в таблицы стилей:

<pre>// Importing Susy
@import "susy";
</pre>

Версия 2 фреймворка Susy имеет [список глобальных переменных][3], встроенных в него. Эти переменные можно изменить прямо в таблице стилей:

<pre>// Configuring Susy 2 Global Defaults
  $susy: (
    key : value
);
</pre>

Можно поэкспериментировать с переменными и их значениями по умолчанию, чтобы посмотреть, ккая из них и за что отвечает. Более детальный обзор этих переменных будет произведен во второй части данного руководства. Однако, можно смело использовать Susy 2 с настройками по-умолчанию. В моем случае, так как я предпочитаю работать с моделью border-box и единицами измерения rem, то я изменю некоторые из переменных:

<pre>$susy: (
  global-box-sizing: border-box,
  use-custom: (rem: true)
);
</pre>

Обратите внимание на то, что Susy 2 использует по умолчанию &#8220;резиновый&#8221; шаблон. Это означает, что ширина всех внешних блоков-контейнеров задана в 100%.

Если же вы предпочитаете работать в Susy с фиксированными ширинами элементов и контрольными точками (*breakpoints*), то просто измените значение переменной `math` на `static`. Главное отличие между двумя этими методами проявляется только тогда, когда настает потребность в превращении дизайна в RWD. Однако, этот вопрос будет рассмотрен позже, во второй части данного руководства.

Также обратите внимание, что необходимо подключить к текущему проекту библиотеку Compass и файл нормализации стилей `normalize.css` (*в первых двух строках*):

<pre>@import "normalize";
@import "compass";
@import "susy";

// Настройка переменных Susy
$susy:(
  global-box-sizing: border-box;
  use-custom: (rem: true)
);

@include border-box-sizing;
</pre>

## Базовый HTML и CSS для шаблона AG

HTML-каркас для данного шаблона будет выглядеть следующим образом:

<pre><div class="container">
  <h1>
    10-колоночный шаблон с вложенностью блоков
  </h1>
  
    
  
  <!-- Column 1 -->
    
  
  <div class="column_1">
    <h2>
      Колонка 1
    </h2>
      
  </div>
  
    
  
  <!-- Column 2 -->
    
  
  <div class="column_2">
    <h2>
      Колонка 2
    </h2>
    
        
    
    <div class="column_2_1_1">
      <h2>
        Колонка 2-1-1
      </h2>
          
    </div>
        
    
    <div class="column_2_1_2">
      <h2>
        Колонка 2-1-2
      </h2>
          
    </div>
    
        
    
    <div class="column_2_2_1">
      <h2>
        Колонка 2-2-1
      </h2>
          
    </div>
        
    
    <div class="column_2_2_2">
      <h2>
        Колонка 2-2-2
      </h2>
            
      
      <div class="column_2_3_1">
        <h2>
          Колонка 2-3-1
        </h2>
              
      </div>
            
      
      <div class="column_2_3_2">
        <h2>
          Колонка 2-3-2
        </h2>
              
      </div>
            
      
      <div class="column_2_4">
        <h2>
          Колонка 2-4
        </h2>
              
      </div>
          
    </div>
      
  </div>
  
  <!-- end Column 2 -->
  
    
  
  <!-- Column 3 -->
    
  
  <div class="column_3">
    <h2>
      Колонка 3
    </h2>
      
  </div>
  
  
</div>
</pre>

В этом примере показан довольно сложный случай вложенности одних блоков в другие блоки.

Ниже представлен простой SCSS-код для сетки:

<pre>.container{
  background-color: #fbeecb;
  .column_1,.column_3{
    background-color: #71dad2;
  }
  .column_2{
    background-color: #fae7b3;
    .column_2_1_1,.column_2_1_2{
      background-color: #ee9e9c;
    }
    .column_2_2_1{
      background-color: #f09671;
    }
    .column_2_2_2{
      background-color: #f6d784;
      .column_2_3_1,.column_2_3_2{
        background-color: #ee9e9c;
      }
      .column_2_4{
        background-color: #ea9fc3;
      }
    }
  }
  h1,h2{
    text-align: center;
    font-size: 1rem;
    font-weight: bold;
    padding: 1.8rem 0;
  }
}
</pre>

Все готово для погружения в плагин Susy. Но перед началом необходимо немного остановиться на деталях этого плагина.

### Наиболее важные функции и миксины плагина Susy

Прежде чем приступать к созданию сеток с помощью Susy, стоит кратко рассказать о трех наиболее важных функциях и миксинах данного плагина. Если вам удастся сразу же разобрать с этими тремя вопросами, вы сможете создавать с помощью Susy сетки практически любого вида и сложности.

#### Миксин Container

Первое, что необходимо сделать в разметке &#8211; это включить миксин `.container`. Тем самым подключаются все возможности плагина Susy для расчета и построения CSS-сеток.

Синтаксис этого миксина прост:

<pre>@include container( [&lt;lenght>] );
</pre>

Необязательный параметр `lenght` позволяет указать для блока-обертки максимальную ширину `max-width`. Если параметр не указан, то плагин Susy будет принимать значение максимальной ширины по умолчанию &#8211; `max-widht: 100%`.

Рабочий пример миксина `container`:

<pre>@include container;
</pre>

#### Миксин span

Миксин span является основой плагина Susy. Обычно используется стандартный способ для вызова данного миксина:

<pre>@include span( &lt;width> [&lt;wide / wider>] of &lt;layout> [&lt;last>] );
</pre>

Если до этого момента вы использовали плагин Susy версии 1, то должны были обратить внимание, что синтаксис этого миксина очень похож на синтаксис миксина `span-column`, с очень незначительными отличиями.

Давайте подробно остановимся на всех тонкостях синтаксиса миксина `span`:

  * width &#8211; количество колонок с создаваемой разметке;
  * wide / wider &#8211; необязательный параметр, который позволяет разделить колонку с помощью одного или двух gutter;
  * of &#8211; указывает Susy, что дальше идут параметры, связанные с разметкой;
  * layout &#8211; показывает ширину блока-обертки;
  * last &#8211; необязательный параметр, который говорит о том, что это последний элемент в ряду.

Пример создания колонки с помощью миксина `span`:

<pre>@include span( 3 wide of 9 last);
</pre>

#### Функция span {#span_1}

Функция `span` во многом очень похожа на одноименный миксин `span`, за тем исключением, что она только лишь возвращает ширину элемента. В случае использования функции span потребуются только параметры ширины колонки, ширины `gutter` и всего блока-обертки в целом.

<pre>.column{
    width: span(3 of 9);
  }
</pre>

Прелесть использования функции `span` в том, что в этом случае нет необходимости в запоминании миксинов для работы в `margin` или `padding` в плагине Susy, как это было в предыдущей его версии. Теперь можно использовать функцию `span` для установки точного значения ширины отступа:

<pre>.paddingLeft{
    padding-left: span(1 of 9);
  }
</pre>

#### Функция gutter

Функция gutter принимает только один аргумент:

<pre>margin-right: gutter(9);
</pre>

Это и все основные функции и миксины плагина Susy, которые необходимо знать для работы с ним.

### Создание разметки с помощью плагина Susy

Первый шаг, который мы сделаем для превращения HTML-кода в нужную разметку, это подключим миксин `container`:

<pre>.container{
    background-color: #fbeecb;
    @include container;
    @include clearfix;
    ...
</pre>

Помимо миксина `container`, мы подключили еще один миксин &#8211; `clearfix`, так как внутри блока-обертки будут располагаться плавающие блоки. Если взглянуть на результат компиляции в CSS, то все станет очевидным: миксин `container` генерирует строки:

<pre>max-width: 100%;
  margin-left: auto;
  margin-right: auto;
</pre>

а миксин `clearfix` создает CSS-строки:

<pre>overflow: hidden;
  *zoom: 1;
</pre>

Прим. переводчика: я бы воспользовался более современной версией миксина для очистки потока &#8211; `pie-clearfix`. Данный миксин построен на методе, о котором говориться в статье известного CSS-гуру Никаласа Галлахера &#8211; [A new micro clearfix hack][4].

Теперь перейдем к более мелким деталям разметки. Предположительно, вся ширина блока-контейнера будет у нас состоять из 10 колонок. На рисунке-эскизе будущий макет сайта должен состоять из трех колонок &#8211; двух узких боковых и одной центральной широкой. Такую HTML-разметку мы и создали ранее в этой статье. Поэтому предположим, что две боковые колонки будут у нас шириной в 2 стобца из 10, а центральная колонка &#8211; из 6 столбцов из 10 ( 10 &#8211; (2 + 2) ).

Следовательно, блок с классами `.column_1` и `.column_3` дописываем миксин:

<pre>.column_1,.column_3{
    ...
    @include span(2 of 10);
  }
</pre>

Помимо этого, блоку с классом `.column_3` дописываем еще один миксин `last`, так как этот блок является последним в данном ряду:

<pre>.column_3{
    @include last;
  }
</pre>

Если заглянем в скомпилированный CSS-код, то увидим простую картину. Всем блокам задается одинаковая ширина в процентах, правый `margin` также в процентах. А вот если применен миксин `last`, то плавание блока меняется на противоположное и убирается правый `margin`:

<pre>.container .column_1, .container .column_3 {
    ...
    width: 18.36735%;
    float: left;
    margin-right: 2.04082%;
  }
  .container .column_3 {
    float: right;
    margin-right: 0;
  }
</pre>

Центральная колонка должна иметь у нас ширину в шесть столбцов и плавающие блоки внутри себя, поэтому задаем для нее два миксина:

<pre>.column_2{
    ...
    @include span(6 of 10);
    @include clearfix;
</pre>

&#8230; что дает в результате CSS-код:

<pre>.container .column_2 {
    ...
    width: 59.18367%;
    float: left;
    margin-right: 2.04082%;
    overflow: hidden;
    *zoom: 1;
  }
</pre>

Отлично! Рассмотрим далее наш пример. Внутри центральной колонки в одном ряду расположены два блока, которые в сумме занимают всю ширину блока-контейнера (в данном случае это центральная колонка). Поэтому для двух этих блоков зададим одинаковый миксин:

<pre>.column_2_1_1,.column_2_1_2{
    ...
    @include span(3 of 6);
  }
</pre>

&#8230; и не забудем добавить для блока с классом `.column_2_1_2` миксин `last`, так как он последний в своем ряду и с ним будут происходить толчно такие же метаморфозы, как и в предыдущем случае:

<pre>.column_2_1_2{
    @include last;
  }
</pre>

Смотрим на готовый CSS-код и видим, что ничего необычного не произошло &#8211; все предсказуемо:

<pre>.container .column_2 .column_2_1_1, .container .column_2 .column_2_1_2 {
    background-color: #ee9e9c;
    width: 48.27586%;
    float: left;
    margin-right: 3.44828%;
  }
  .container .column_2 .column_2_1_2 {
    float: right;
    margin-right: 0;
  }
</pre>

В следующем ряду располагаются еще два блока, но уже с разной шириной: блок с классом `.column_2_2_1` будет занимать 2 колонки из 6, а блок с классом `column_2_2_2` &#8211; 4 колонки из 6. Кроме того, в блоке с классом `column_2_2_2`, в свою очередь, размещены еще два плавающих блока `column_2_3_1`, `column_2_3_2`, поэтому к нему нужно применить опять миксин `clearfix`:

<pre>.column_2_2_1{
    ...
    @include span(2 of 6);
  }
  .column_2_2_2{
    ...
    @include span(4 of 6 last);
    @include clearfix;
    .column_2_3_1,.column_2_3_2{
      ...
      @include span(2 of 4);
    }
    .column_2_3_2{
      @include last;
    }
</pre>

CSS-результат применения этих миксинов показан ниже:

<pre>.column_2_2_1 {
  ...
  width: 31.03448%;
  float: left;
  margin-right: 3.44828%;
}
.column_2_2_2 {
  ...
  width: 65.51724%;
  float: right;
  margin-right: 0;
  overflow: hidden;
  *zoom: 1;
}
.column_2_3_1, .column_2_3_2 {
  ...
  width: 47.36842%;
  float: left;
  margin-right: 5.26316%;
}
.column_2_3_2 {
  float: right;
  margin-right: 0;
}
</pre>

Последним у нас идет блок, который занимает всю ширину своего блока-родителя. В нему мы применим миксин `span(full)` и одновременно очистку через CSS-свойство `clear: both;`.

<pre>.column_2_4{
    ...
    @include span(full);
    clear: both;
  }
</pre>

&#8230; чтобы получился CSS-результат:

<pre>.container .column_2 .column_2_2_2 .column_2_4 {
    ...
    width: 100%;
    float: left;
    margin-left: 0;
    margin-right: 0;
    clear: both;
  }
</pre>

Вот, в принципе, и все несложное построение разметки. Давайте взглянем на результат наших трудов в окне браузера:<figure id="attachment_1152" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/05/susy_result-600x353.png" alt="Готовый шаблон, созданный с помощью Susy" width="600" height="353" class="size-medium wp-image-1152" />][5]<figcaption class="wp-caption-text">Готовый шаблон, созданный с помощью Susy</figcaption></figure> 

Полный вариант кода можно посмотреть здесь &#8211; [Susy Part 1][6]

Думаю, на cегодня можно закруглиться с изучением Susy. Но, вообще эта тема очень интересная и положительная. В том плане, что для практической работы применение плагина Susy мне видится &#8211; в самый раз. Это вам не неуклюжие [960gs][7] или [Blueprint][8]. Тут все гибко и настраиваемо прямо на лету. Хочешь такую разметку &#8211; пожалуйста. А хочешь другую &#8211; да пожалуйста, Susy тебе пересчитает все в мгновение ока! ))

Думается мне, это не последняя статья, посвященная плагину Susy под библиотеку Compass.

Данная статья является вольным переводом и осмыслением статьи, написанной американским fornt-end &#8211; самоучкой, расположенным по адресу &#8211; [A Complete Tutorial to Susy 2][9]

Оцените статью:  
<span id="post-ratings-1148" class="post-ratings" data-nonce="a2095182a7"><img id="rating_1148_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1148, 1, '1 Star');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1148_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1148, 2, '2 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1148_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1148, 3, '3 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1148_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1148, 4, '4 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1148_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1148, 5, '5 Stars');" onmouseout="ratings_off(4.4, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>5</strong> votes, average: <strong>4,40</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1148_text"></span></span><span id="post-ratings-1148-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/05/susy2-1.png
 [2]: http://rvm.io/rvm/install "установить Ruby RVM"
 [3]: http://susydocs.oddbird.net/en/latest/settings/#global-defaults "список глобальных переменных"
 [4]: http://nicolasgallagher.com/micro-clearfix-hack/
 [5]: http://localhost:7788/third/wp-content/uploads/2014/05/susy_result.png
 [6]: http://sassmeister.com/gist/11450132
 [7]: http://localhost:7788/third/?p=1096 "Фреймворк 960 Grid System"
 [8]: http://localhost:7788/third/?p=1136 "Фреймворк Blueprint"
 [9]: http://www.zell-weekeat.com/susy2-tutorial/