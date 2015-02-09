---
title: Как управлять положением gutters в Susy
author: gearmobile
excerpt: Как управлять расположением отступов gutter в разметке, созданной с помощью Susy. Четыре варианта расположения gutter, устанавливаемые через ключевые слова before, after, split и inside для параметра gutter-position. Местоположение gutter оказывает ключевое влияние на всю разметку в целом, кардинально меняя ее вид и свойства.
layout: post
permalink: /gutter-susy/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Статьи по CSS
tags:
  - gutter
  - susy
---
При изучении Susy одним из вопросов, который всегда стоял передо мной, заключался в следующем: &#8220;Как удалить `padding` или `margin` у первого и последнего столбца `column` в разметке Susy без применения CSS-свойств `first-child` и `last-child?`&#8220;.

Этот вопрос является один из самых главных для всех, кто только начинает изучение Susy. Если посмотреть в корень данного вопроса, то его основную суть можно свести к следующему (*если судить по многочисленным постам в Интернет*): необходимо использовать значение `inside` вместо значения `after`. Для того, чтобы точно ответить на этот вопрос, необходимо хорошо понимать, каким образом положение отступов `gutter` в целом оказывает влияние на всю разметку, созданную в Susy.

Как мне кажется, вопрос о расположении отступов `gutter` в разметке Susy является **самой важной настройкой**, поскольку он **оказывает влияние на весь код в целом**. Если у вас перед прочтением статьи существовал такой вопрос, то данная статья именно для вас.

### Что такое &#8211; расположение отступов gutter

Расположение отступа `gutter` позволяет полностью менять всю разметку страницы, созданную в Susy. Данный параметр определяет, где должны находиться отступы `gutter` относительно столбцов `columns`. Также данная настройка определяет, будут ли отступы `gutter` являться CSS-свойством `padding` или `margin`.

Эта параметр находиться среди **глобальных настроек** переменной `$susy`. Как вариант, данный параметр можно использовать **локально**, внутри миксина `span`. Давайте начнем с рассмотрения случая, когда расположение отступа `gutter` управляется из глобальной переменной `$susy`.

По умолчанию, расположение отступов в Susy определено ключевым словом `after`. Помимо этого, существуют еще варианты: `before`, `split`, `inside` и `inside-static`. Ниже представлен полный вариант синтаксиса параметра `gutter-position` в глобальной переменной `$susy`:

<pre>// SCSS

  $susy: (
    gutter-position: after ( before | after | split | inside | inside-static )
  );
  </pre>

Ключевые слова в круглых скобках являются **возможными вариантами** значения параметра `gutter-position`.

Для ясности понимания тонкостей разметки в Susy при использовании параметра `gutter-position` необходимо создать простую структуру:<figure id="attachment_1968" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_01-600x346.png" alt="Базовая разметка в Susy" width="600" height="346" class="size-medium wp-image-1968" />][1]<figcaption class="wp-caption-text">Базовая разметка в Susy</figcaption></figure> 

### Gutter-position: after

Значением по умолчанию для параметра `gutter-position` является ключевое слово `after`. Данное значение заставляет Susy располагать отступы gutters **после каждого столбца** разметки. В этом режиме необходимо **удалить отступ у последнего столбца** в разметке. В этом случае отступы gutters являются CSS-свойством margin и размещаются в разметке следующим образом:<figure id="attachment_1969" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_02-600x160.png" alt="Gutter-position: after" width="600" height="160" class="size-medium wp-image-1969" />][2]<figcaption class="wp-caption-text">Gutter-position: after</figcaption></figure> 

При использовании значения по умолчанию для параметра `gutter-position` миксин `span` создает три CSS-правила &#8211; `width`, `margin-right` и `float: left`:

<pre>// SCSS

  .test {
    @include span(3 of 4);
  }
  </pre>

Результирующий CSS-код:

<pre>// CSS</p>

  

<p>
  .test {
      width: 73.68421%;
      float: left;
      margin-right: 5.26316%;
    }
    </pre>
  
  
  <p>
    В этом коде свойство <code>margin-right</code> &#8211; это отступ <code>gutter</code>, созданный Susy в данной разметке.
  </p>
  
  
  <p>
    Можно использовать ключевое слово <code>last</code> для удаления крайнего <code>margin</code> у столбца:
  </p>
  
  
  <pre>
  // SCSS

  .last {
    @include span(1 of 4 last);
  }
  </pre>
  
  
  <p>
    В результате получим результат в виде <code>margin-right: 0</code>:
  </p>
  
  
  <pre>
  // CSS

  .last {
    width: 21.05263%;
    float: right;
    margin-right: 0;
  }
  </pre>
  
  
  <p>
    В рассматриваемой нами разметке область контента занимает 3 столбца из 4. При этом область боковой панели размещается в одном столбце из 4-х. Кроме того, боковая панель является последним элементом разметки, поэтому код для подобного случая будет таким:
  </p>
  
  
  <pre>
  // SCSS

  .content {
    @include span(3 of 4);
  }
  .sidebar {
    @include span(1 of 4 last);
  }
  </pre>
  
  
  <p>
    <strong>Краткое заключение</strong>: значение <code>after</code> параметра <code>gutter-position</code> является наиболее интуитивно понятным случаем создания разметки в Susy. При использовании значения по умолчанию единственный момент, о котором следует помнить &#8211; это убрать отступ у последнего столбца разметки с помощью ключевого слова <code>last</code>.
  </p>
  
  
  <h3>
    Gutter-position: before
  </h3>
  
  
  <p>
    Значение <code>before</code> является одним из вариантов предыдущего значения &#8211; <code>after</code>. Суть этого значения также простая. Вместо размещения отступов gutter после столбцов (как в случае с <code>after</code>), при значении <code>before</code> отступы gutters размещаются перед столбцами. В этом случае необходимо удалить отступ у первого столбца в разметке. Отступы gutter также являются в данном случае CSS-свойством <code>margin</code>:
  </p>
  <figure id="attachment_1970" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_03.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_03-600x161.png" alt="Gutter-position: before" width="600" height="161" class="size-medium wp-image-1970" /></a><figcaption class="wp-caption-text">Gutter-position: before</figcaption></figure>
  
  
  <p>
    При использовании значения <code>before</code> для параметра <code>gutter-position</code> миксин <code>span</code> генерирует три CSS-правила: <code>width</code>, <code>margin-left</code> и <code>float: left</code> с помощью кода:
  </p>
  
  
  <pre>
  // SCSS

  .test {
    @include span(3 of 4);
  }
  </pre>
  
  
  <p>
    Результирующий CSS-код будет выглядеть таким образом:
  </p>
  
  
  <pre>
  // CSS

  .test {
    width: 73.68421%;
    float: left;
    margin-left: 5.26316%; /* Notice this is margin left, not right */
  }
  </pre>
  
  
  <p>
    Так как значение <code>before</code> является прямой противоположностью значения <code>after</code>, то его очень легко понять, если до этого вы хорошо разобрались с <code>after</code>. Вместо использования ключевого слова <code>last</code> для <strong>удаления отступа у последнего столбца</strong> разметки, в данном случае нужно использовать ключевое слово <code>first</code> для <strong>удаления отступа у первого столбца</strong> разметки:
  </p>
  
  
  <pre>
  // SCSS

  .content {
    @include span(3 of 4 first);
  }

  .sidebar {
    @include span(1 of 4);
  }
  </pre>
  
  
  <p>
    В результате получим точно такую же разметку, что и в предыдущем случае.
  </p>
  
  
  <p>
    <strong>Краткое заключение</strong>: при использовании значения <code>before</code> разметка получается точно такой же, как и в предыдущем случае. Единственное отличие заключается в применении ключевого слова <code>first</code> для первого столбца разметки.
  </p>
  
  
  <h3>
    Gutter-position: split
  </h3>
  
  
  <p>
    Значение <code>split</code> параметра <code>gutter-position</code> кардинально отличается от двух предыдущих значений  <code>before</code> и <code>after</code>. Если установлено значение <code>split</code>, то ширина отступа <code>gutter</code> делиться пополам (надвое) и обе половинки отступа располагаются по обеим сторонам одного столбца. В этом режиме отступы <code>gutters</code> генерируются в CSS-коде в виде CSS-свойства <code>margin</code>. В этом случае нет необходимости удалять отступы для крайних столбцов разметки:
  </p>
  <figure id="attachment_1971" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_04.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_04-600x274.png" alt="Gutter-position: split" width="600" height="274" class="size-medium wp-image-1971" /></a><figcaption class="wp-caption-text">Gutter-position: split</figcaption></figure>
  
  
  <p>
    Если, как в нашем случае, имеются только два блока (с классом <code>.content</code>  и <code>.sidebar</code>), то создание такой разметки выполняется просто. Для этого достаточно воспользоваться функцией <code>span</code>, как обычно:
  </p>
  
  
  <pre>
  // SCSS

  .content {
    @include span(3 of 4);
  }

  .sidebar {
    @include span(1 of 4);
  }
  </pre>
  <figure id="attachment_1972" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_05.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_05-600x335.png" alt="Разметка с двумя блоками" width="600" height="335" class="size-medium wp-image-1972" /></a><figcaption class="wp-caption-text">Разметка с двумя блоками</figcaption></figure>
  
  
  <p>
    Однако, ситуация становиться не такой ясной, если блок <code>.content</code> или блок <code>.sidebar</code> будут содержать внутри себя блоки-потомки.
  </p>
  
  
  <p>
    Давайте добавим два блока <code>div</code> с классом <code>.child-one</code> и классом <code>.child-two</code> внутрь блока <code>.content</code> для того, чтобы проиллюстрировать эту ситуацию:
  </p>
  
  
  <pre>
  // HTML

  

<div class="content">
  <h2>
    Content
  </h2>
      
  
  <div class="child-one">
    <h2>
      Child One
    </h2>
  </div>
      
  
  <div class="child-two">
    <h2>
      Child Two
    </h2>
  </div>
    
</div>
  </pre>
  
  
  <p>
    Для обоих вновь созданных блока применим тот же подход, что и ранее. Блок с классом <code>.child-one</code> будет иметь ширину 2-х столбцов из 3-х; блок с классом <code>.child-two</code> будет иметь ширину 1-го столбца из 3-х.
  </p>
  
  
  <pre>
  // SCSS

  .content {
    @include span(3 of 4);
  }

  .child-one {
    @include span(2 of 3);
  }

  .child-two {
    @include span(1 of 3);
  }
  </pre>
  <figure id="attachment_1973" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_06.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_06-600x334.png" alt="Разметка с двумя дополнительными блоками" width="600" height="334" class="size-medium wp-image-1973" /></a><figcaption class="wp-caption-text">Разметка с двумя дополнительными блоками</figcaption></figure>
  
  
  <p>
    Обратите внимание на тот факт, что границы обоих блоков <code>.child-one</code> и <code>.child-two</code> <strong>не совпадают с границами фоновой сетки</strong>!
  </p>
  
  
  <p>
    Это происходит потому, что при задании для параметра <code>gutter-position</code> значения <code>split</code> нужно <strong>учитывать взаимосвязь</strong> между блоками-родителями и блоками-потомками. В данном конкретном случае блоком-родителем является <code>.content</code>, а блоками-потомками являются <code>.child-one</code> и <code>.child-two</code>.
  </p>
  
  
  <p>
    Для создания правильной разметки в данном случае необходимо добавить для блока-родителя ключевое слово <code>nest</code> для того, чтобы показать, что этот блок как раз и является блоком-родителем:
  </p>
  
  
  <pre>
  // SCSS

  .content {
    @include span(3 of 4 nest); // Добавлен ключ nest
  }

  .child-one {
    @include span(2 of 3);
  }

  .child-two {
    @include span(1 of 3);
  }
  </pre>
  <figure id="attachment_1974" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_07.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_07-600x438.png" alt="Применение ключевого слова nest" width="600" height="438" class="size-medium wp-image-1974" /></a><figcaption class="wp-caption-text">Применение ключевого слова nest</figcaption></figure>
  
  
  <p>
    Теперь посмотрите, как точно оба блока .child-one<code>и</code>.child-two` вписались в границы сетки, &#8220;нарисованной&#8221; фоновым изображением!
  </p>
  
  
  <p>
    На первый взгляд, ситуация является немного запутанной. Для того, чтобы не путаться, нужно всегда помнить, что в случае необходимости вписать блоки-потомки точно в границы сетки, нужно использовать ключевое слово для их блока-родителя.
  </p>
  
  
  <p>
    Если &#8220;копнуть&#8221; поглубже и проанализировать сгенерированный CSS-код, то можно заметить, что для блоков <code>.child-one</code> и <code>.child-two</code> он совершенно различный:
  </p>
  
  
  <pre>
  // CSS

  .content {
    width: 75%;
    float: left;
  }

  .child-one {
    width: 60%;
    float: left;
    margin-left: 3.33333%;
    margin-right: 3.33333%;
  }

  .child-two {
    width: 26.66667%;
    float: left;
    margin-left: 3.33333%;
    margin-right: 3.33333%;
  }
  </pre>
  
  
  <p>
    Блок-родитель имеет плавание влево <code>float: left</code> и ширину, которая указана в процентах; при этом ширина отступов <code>gutters</code> этого блока не учитывается (75% равно 3/4).
  </p>
  
  
  <p>
    Блоки-потомки имеют все те же свойства, что и блок-родитель. Но при этом отступы gutters имеют место быть для этих блоков.
  </p>
  
  
  <p>
    <strong>Краткое заключение</strong>: значение <code>split</code> кардинально отличается от двух рассмотренных ранее значений <code>before</code> и <code>after</code>. При использовании значения <code>split</code> необходимо добавлять ключевое слово <code>nest</code> к блоку-родителю и использовать миксин <code>span</code> для всех блоков-потомков.
  </p>
  
  
  <h3>
    Gutter-position: inside/inside-static
  </h3>
  
  
  <p>
    Оба значения <code>inside</code> и <code>inside-static</code> очень похожи на предыдущее значение <code>split</code>. Отступы gutters также делятся пополам (надвое) и обе половинки располагаются по обеим сторонам каждого столбца. Однако, в этом случае в CSS-выводе отступы являются свойством <code>padding</code>, а не <code>margin</code>. Также в этом случае <strong>нет необходимости удалять отступы</strong> у крайних столбцов в разметке:
  </p>
  <figure id="attachment_1975" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_08.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_08-600x270.png" alt="Gutter-position: inside" width="600" height="270" class="size-medium wp-image-1975" /></a><figcaption class="wp-caption-text">Gutter-position: inside</figcaption></figure>
  
  
  <p>
    Отступы gutters в случае <code>gutter-position: inside</code> имеют тот же принцип, что и при значении <code>split</code>. Если для блока-родителя не будет указано ключевое слово <code>nest</code>, то блоки-потомки выйдут за границы разметки.
  </p>
  
  
  <pre>
    // SCSS

    .content {
      @include span(3 of 4);
    }

    .child-one {
      @include span(2 of 3);
    }

    .child-two {
      @include span(1 of 3);
    }
  </pre>
  <figure id="attachment_1976" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_09.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_09-600x156.png" alt="Блоки-потомки выходят за границы разметки" width="600" height="156" class="size-medium wp-image-1976" /></a><figcaption class="wp-caption-text">Блоки-потомки выходят за границы разметки</figcaption></figure>
  
  
  <p>
    Если просто добавить ключевое слово <code>nest</code> для блока-родителя <code>.content</code>, то в результате получим следующее:
  </p>
  
  
  <pre>
    // SCSS

    .content {
      @include span(3 of 4 nest); // The nest key is needed
    }

    .child-one {
      @include span(2 of 3);
    }

    .child-two {
      @include span(1 of 3);
    }
  </pre>
  <figure id="attachment_1977" style="width: 600px;" class="wp-caption aligncenter">
  
  <a href="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_10.png"><img src="http://localhost:7788/third/wp-content/uploads/2014/11/gutters_10-600x154.png" alt="Блоки-потомки в границах разметки" width="600" height="154" class="size-medium wp-image-1977" /></a><figcaption class="wp-caption-text">Блоки-потомки в границах разметки</figcaption></figure>
  
  
  <p>
    Значение <code>inside-static</code> работает точно также, как и значение <code>inside</code>. Единственное исключение заключается в том, что отступы gutters получаются в фиксированных единицах измерения, а не в процентах. Кроме этого, в глобальной переменной <code>$susy</code> необходимо задать параметр <code>column-width</code> с указанием ширины столбца <code>column</code>.
  </p>
  
  
  <p>
    <strong>Краткое заключение</strong>: значение <code>inside</code> работает точно также, как и значение <code>split</code>. При использовании значения <code>inside</code> необходимо добавлять ключевое слово <code>nest</code> к блоку-родителю и использовать миксин <code>span</code> для всех блоков-потомков.
  </p>
  
  
  <p>
    Значение <code>inside</code> и <code>split</code> имеют одинаковый сгенерированный CSS-код, поэтому можно с легкостью менять между собой эти значения в глобальной переменной <code>$susy</code> для параметра <code>gutter-position</code>.
  </p>
  
  
  <h2>
    Заключение
  </h2>
  
  
  <p>
    Различные типы разметки в Susy создаются с помощью выбора расположения отступов <code>gutters</code>. Различное местоположение отступов <code>gutters</code> в каждом случае имеет свои тонкости и требует понимания процесса, если вы хотите эффективно их использовать.
  </p>
  
  
  <p>
    Существует два основных способа создания разметки при содействии отступов <code>gutters</code>:
  </p>
  
  
  <ul>
    <li>
      значения <code>before</code> и <code>after</code> имеют создают отступы <code>gutters</code> <strong>с одной стороны каждого столбца</strong> <code>column</code>; для крайнего столбца необходимо удалить отступ <code>gutter</code> с помощью ключевого слова <code>first</code> или <code>last</code>.
    </li>
    
    
    <li>
      значения <code>inside</code>, <code>inside-static</code>, <code>split</code> разделяют каждый отступ <code>gutter</code> на две равные половины, которые располагаются по обе сторны каждого столбца <code>column</code>. Такие отступы не нуждаются в удалении.
    </li>
    
  </ul>
  
  
  <p>
    Эта статья является небольшой выдержкой из книги <a href="http://zell-weekeat.com/learnsusy" title="Learning Susy">Learning Susy</a>, а точнее &#8211; из главы 8, посвященной позиционированию отступов <code>gutter</code> в разметке Susy. В книге вопрос позиционирования рассмотрен подробнее на основе более сложного примера. Если материал, поданный в статье, вм понравился, то книга понравиться еще больше.
  </p>
  
  
  <p>
    <strong>Примечание переводчика</strong>: данный пост является переводом статьи <a href="http://www.zell-weekeat.com/susy-gutter-positions/" title="Understanding Gutter Positions in Susy">Understanding Gutter Positions in Susy</a>, созданным мною с любезного разрешения ее автора Zell Liew.
  </p>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/11/gutters_01.png
 [2]: http://localhost:7788/third/wp-content/uploads/2014/11/gutters_02.png