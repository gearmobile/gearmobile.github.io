---
title: Создание Asymmetric Layout в Susy
author: gearmobile
excerpt: 'Цель статьи - на простом примере показать, каким образом можно создавать ассиметричную разметку (asymmetric layout) с помощью Susy 2. Обзор ни в коей мере не является каким-либо пособием - это просто очень краткий экскурс по возможностям Susy 2 в области (asymmetric layout).'
layout: post
permalink: /asymmetric-layout-susy/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - asymmetric layout
  - susy
---
**От переводчика**. Данная статья является вольным переводом поста [Creating Asymmetric Layouts With Susy][1] автора Zell Liew. Цель статьи &#8211; на простом примере показать, каким образом можно создавать **ассиметричную разметку** (asymmetric layout) с помощью Susy 2. Обзор ни в коей мере не является каким-либо пособием &#8211; это просто очень краткий экскурс по возможностям Susy 2 в области (asymmetric layout). Далее &#8211; вольный перевод с разрешения автора.

Когда я впервые услышал об **ассиметричной разметке** (asymmetric layout), на тот момент такую можно было сделать только с помощью фреймворка [Singularity GS][2]. Подобная разметка была чем-то невероятно крутым и я очень захотел сделать подобную же &#8211; с неравной шириной столбцов `columns`. Но на тот момент я был полностью доволен системой Susyone и мне очень не хотелось переключаться на другой инструмент.

Можете представить мой восторг, когда вышла новая версия Susy 2, в которой была включена поддержка **ассиметричной разметки** (asymmetric layout).

В этой статье я покажу, как просто можно создавать **ассиметричную разметку** (asymmetric layout) с помощью Susy 2.

### Что мы будем делать

В этой статье мы будем создавать с помощью Susy простую fluid-разметку. В этой разметке есть две боковых панели и два вложенных блока-потомка внутри центрального блока с контентом.<figure id="attachment_1985" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/asym-grid-1-basic-setup-600x237.png" alt="Asymmetric Layout Basic Setup" width="600" height="237" class="size-medium wp-image-1985" />][3]<figcaption class="wp-caption-text">Asymmetric Layout Basic Setup</figcaption></figure> 

### Глобальные переменные Susy

Для того, чтобы использовать возможность создания **ассиметричной разметки** (asymmetric layout) в Susy, в ее глобальной переменной `$susy`нужно внести два параметра: `columns` и `output`. Параметр `columns` должен быть Sass-списком для того, чтобы можно было работать с **ассиметричной разметкой** (asymmetric layouts).

**Sass-список** является **строкой значений**, разделенных пробелом и выглядит он примерно таким образом:

<pre>// SCSS
$list : 1 2 3 2 1;
</pre>

Внутри данного списка `$list` располагаются пять значений: `1`, `2`, `3`, `2`, `1`. Если поместить этот список в качестве параметра в глобальную переменную `$susy`, то в результате получим **ассиметричную разметку** (asymmetric layout), состоящую из пяти столбцов.

Также же необходимо добавить еще один параметр `output: isolate`:

<pre>// SCSS
$susy : (
  columns: 1 2 3 2 1,
  output: isolate
)
</pre>

После установки этих параметров все готово для создания заметки с помощью Susy.

### Создание ассиметричной разметки (asymmetric layout)

Как правило, первым важным шагом является добавление миксина `container` для блока-обертки. Помимо этого, в данном примере для блока-обертки добавим еще высоту на 100% viewport, так как внутри блока нет содержимого и иначе мы его просто не увидим:

<pre>.wrap {
  @include container(1140px);
  height: 100vh;
}
</pre><figure id="attachment_1986" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/asym-grid-1-600x92.png" alt="Asymmetric Layout" width="600" height="92" class="size-medium wp-image-1986" />][4]<figcaption class="wp-caption-text">Asymmetric Layout</figcaption></figure> 

Прежде чем продолжить создание разметки, необходимо разобраться с еще одним вопросом.

Так как в глобальных настройках Susy используется параметр `output: isolate`, необходимо уточнить **месторасположение каждой отдельной части разметки**. Для этой цели нужно использовать параметр `$location`.

Параметр `$location` **указывает месторасположение** каждого отдельного `span` и может принимать следующие значения:

  * first
  * last
  * at <number>

Если какой-либо отдельный блок по разметке располагается первым, то для него необходимо использовать ключевое слово `first`. Если блок располагается последним, то для него нужно использовать слово `last`. Если же блок располагается в разметке, к примеру, начиная со 2-го столбца, то в миксине `span` нужно использовать ключевое слово `at 2`.

Теперь, обладая всеми этими знаниями, можно создать разметку для трех блоков: `.sidebar-one`, `.content` и `.sidebar-two`.

Блок `.sidebar-one` по нашей схеме располагается первым и занимает ширину в один столбец:

<pre>// SCSS
  .sidebar-one {
    @include span(1 first);
  }
</pre>

Блок `.sidebar-two` является последним в схеме разметки и также занимает ширину в один столбец:

<pre>// SCSS
  .sidebar-two {
    @include span(1 last);
  }
</pre>

Блок `.content` имеет ширину в три столбца и начинается со второго столбца:

<pre>// SCSS
  .content {
    @include span(3 at 2);
  }
</pre>

Теперь все три блока должны точно расположиться в создаваемой нами **ассиметричной разметке** (asymmetric layout). Два оставшися блока `.nest-one` и `.nest-two` временно опустим для более ясной картины:<figure id="attachment_1987" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/asym-grid-2-600x116.png" alt="Созданная Asymmetric Layout" width="600" height="116" class="size-medium wp-image-1987" />][5]<figcaption class="wp-caption-text">Созданная Asymmetric Layout</figcaption></figure> 

Создание разметки для вложенных блоков `.nest-one` и `.nest-two` немного сложнее, нежели для основных блоков разметки. Имеется ввиду, что при разметке блоков-потомков необходимо учитывать факт их вложенности.

Оба наших блока расположены внутри блока `.content`, а мы знаем, что данный блок имеет структуру (2 3 2), которая также является **ассиметричной разметкой** (asymmetric layout).

Поэтому, при создании разметки для вложенных элементов необходимо включить эти значения в качестве аргументов для миксина `span`.

Блок с классом `.nest-one` является первым блоком в разметке и занимает ширину в один (1) столбец **ассиметричной сетки** (asymmetric layout). Блок с классом `.nest-two` является последним блоком в разметке и занимает ширину в два (2) столбца.

Такая разметка создается с помощью следующего кода:

<pre>.nest-one{
  @include span(1 of (2 3 2) first);
}
.nest-two{
  @include span(2 of (2 3 2) last);
}
</pre>

Как видим по исходному коду, при создании разметки нет необходимости указывать точную ширину (px,%) каждого блока. Благодаря Susy создание **ассиметричной разметки** (asymmetric layout) выполняется просто, с применением той теории, о которой только что говорилось. Достаточно только указать число столбцов, которое должен занимать каждый блок.

### Более сложный пример разметки

Пример ассиметричной разметки, представленный в этой статье, достаточно простой. Более сложным случаем является создание **адаптивной ассиметричной разметки** (asymmetric layout).

В качестве примера могу привести [образец ассиметричной разметки][6], созданной Nathan Ford с применением приложения [GridsetApp][7]. Этот образец является хорошим примером адаптивной страницы, которая дает представление о том, что может Susy.

**Примечание переводчика**: на этом самое существенное и интересное в этой статье заканчивается. Дальше идет реклама книги автора. Собственно, данная статья для этого и писалась, конечно. Но ради даже такого простого примера ассиметричной разметки (asymmetric layout) на Susy стоило превести этот пост.

Оцените статью:  
<span id="post-ratings-1984" class="post-ratings" data-nonce="1f089ca70b"><img id="rating_1984_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1984, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1984_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1984, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1984_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1984, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1984_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1984, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1984_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1984, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1984_text"></span></span><span id="post-ratings-1984-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://www.zell-weekeat.com/asymmetric-layouts-with-susy/ "Creating Asymmetric Layouts With Susy"
 [2]: http://singularity.gs/ "Singularity GS"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/11/asym-grid-1-basic-setup.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/11/asym-grid-1.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/11/asym-grid-2.png
 [6]: https://gridsetapp.com/specs/typekit-demos/chaparral.html?gridset=show "образец ассиметричной разметки"
 [7]: https://gridsetapp.com/ "GridsetApp"