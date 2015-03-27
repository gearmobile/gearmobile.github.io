---
title: Hexagon на CSS
author: gearmobile
layout: post
---
В этой статье будет детально рассмотрен вопрос создания фигуры шестиугольника (hexagon) на CSS. Материал целиком основан на замечательной статье [CSS Hexagon Tutorial][1]. В Сети имеется хорошая статья по примерам создания различных видов фигур на CSS, и располагается эта статья на блоге известного CSS-гуру Chris Coyier &#8211; [Shapes of CSS][2]. Среди прочих фигур там есть и желанный шестиугольник `hexagon` с готовым CSS-кодом &#8211; что называется, &#8220;бери и пользуйся&#8221;. Но ведь такой подход для нас не интересен, правда? Это потом, когда мы изучим вопрос создания шестиугольника, мы будем делать так &#8211; нашел готовый код, скопировал к себе, подредактировал и готово! А сейчас мы пошагово пройдем весь путь, от начала и до конца &#8211; это даст нам понимание процесса.

### Как будем строить hexagon

Фигура hexagon изначально кажется неприступной &#8211; не понятно, с какого боку к ней подойди, чтобы начать постороение шестиугольника на CSS. Однако, если внимательно присмотреться, то hexagon можно разделить на три простые фигуры:<figure id="attachment_1552" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_origin-600x437.jpg" alt="Три части фигуры hexagon" width="600" height="437" class="size-medium wp-image-1552" />][3]<figcaption class="wp-caption-text">Три части фигуры hexagon</figcaption></figure> 

Видно, что фигура состоит из двух одинаковых треугольников и одного прямоугольника. Построение треугольников на CSS выполняется очень просто &#8211; [CSS – почему треугольник это треугольник][4], прямоугольника &#8211; вообще в два движения.

Поэтому, построение шестиугольника hexagon на CSS сводится к двух задачам:

  * создать два треугольника
  * создать один прямоугольник

### Построение треугольников на CSS

Задачу создания треугольников на CSS начнем с **построения обычного квадрата** со стороной в 100px и широкой границей (30px) определенного цвета (#778899):

<pre><div class="hexagon">
  
</div>

  .hexagon{
    width: 100px;
    height: 100px;
    border: 30px solid #778899;
  }
  </pre><figure id="attachment_1553" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square-600x541.jpg" alt="Квадрат на CSS" width="600" height="541" class="size-medium wp-image-1553" />][5]<figcaption class="wp-caption-text">Квадрат на CSS</figcaption></figure> 

**&#8220;Раскрасим&#8221;** границы квадрата для того, чтобы можно было визуально отличать их друг от друга:

<pre><div class="hexagon hexagon_colors">
  
</div>

  .hexagon_colors{
    border-top-color: lighten(#778899,5%);
    border-right-color: lighten(#778899,10%);
    border-bottom-color: darken(#778899,10%);
    border-left-color: darken(#778899,5%);
  }
  </pre><figure id="attachment_1555" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_colors-600x541.jpg" alt="Квадрат на CSS с границами разного цвета" width="600" height="541" class="size-medium wp-image-1555" />][6]<figcaption class="wp-caption-text">Квадрат на CSS с границами разного цвета</figcaption></figure> 

Затем **обнулим** высоту (`height`) и ширину (`width`) нашего квадрата. Он &#8220;схлопнется&#8221;, оставив для нас видимой только его широкую границу со всех четырех сторон:

<pre><div class="hexagon hexagon_colors hexagon_zero">
  
</div>

  .hexagon_zero{
    width: 0;
    height: 0;
  }
  </pre><figure id="attachment_1556" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_zero-600x541.jpg" alt="Квадрат на CSS с нулевой высотой и шириной" width="600" height="541" class="size-medium wp-image-1556" />][7]<figcaption class="wp-caption-text">Квадрат на CSS с нулевой высотой и шириной</figcaption></figure> 

Теперь превратим полученную фигуру в настоящий треугольник. Для этого обнулим (уберем) у нее верхнюю границу (`border-top`), а обе боковые границы (`border-left`, `border-right`) сделаем прозрачного (`transparent`) цвета:

<pre><div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up">
  
</div>

  .hexagon_triangle_up{
    border-top-width: 0;
    border-right-color: transparent;
    border-left-color: transparent;
  }
  </pre><figure id="attachment_1557" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_to_triangle-600x541.jpg" alt="Трегольник на CSS" width="600" height="541" class="size-medium wp-image-1557" />][8]<figcaption class="wp-caption-text">Треугольник на CSS</figcaption></figure> 

У получившегося треугольника все стороны равны &#8211; высота и ширина по 30px каждая. Нам же необходимо &#8220;растянуть&#8221; треугольник в ширину, чтобы он у него появился тупой угол. Для этого нужно увеличить ширину боковых границ (`border-left`, `border-right`) треугольника, а ширину нижней границы (`border-bottom`) оставить прежней:

<pre><div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
  
</div>

  .hexagon_triangle_up_large{
    border-left-width: 52px;
    border-right-width: 52px;
  }
  </pre><figure id="attachment_1558" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_to_triangle_large-600x541.jpg" alt="Удлиненный треугольник на CSS" width="600" height="541" class="size-medium wp-image-1558" />][9]<figcaption class="wp-caption-text">Удлиненный треугольник на CSS</figcaption></figure> 

Задача создания треугольника нами выполнена. Теперь необходимо получить точно такой треугольник, только &#8220;направленный&#8221; вниз. Это просто &#8211; достаточно поменять нулевое значение между верхней и нижней границей фигуры. Все остальные значения останутся неизменными. Чуть не забыл сказать, что для &#8220;повернутого&#8221; треугольника придется создать в HTML-коде **новый блок**:

<pre><div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
  
</div>
  

<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
  
</div>

  ...

  .hexagon_triangle_down{
    border-bottom-width: 0;
    border-right-color: transparent;
    border-left-color: transparent;
  }

  .hexagon_triangle_down_large{
    border-left-width: 52px;
    border-right-width: 52px;
  }
  </pre><figure id="attachment_1559" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_to_two_triangles-600x541.jpg" alt="Два треугольника на CSS" width="600" height="541" class="size-medium wp-image-1559" />][10]<figcaption class="wp-caption-text">Два треугольника на CSS</figcaption></figure> 

Первый шаг по созданию шестиугольника hexagon на CSS выполнен &#8211; у нас есть два одинаковых разнонаправленных треугольника. Теперь нужно создать &#8220;тело&#8221; для шестиугольника &#8211; прямоугольник.

#### Построение прямоугольника на CSS

Для создания прямоугольника на CSS достаточно прописать для нового блока три величины &#8211; высоту, ширину и фоновый цвет. Новый блок я размещу между двумя блоками-треугольниками.

А вот с размерами для прямоугольника нужно разобраться немного подробнее. У него ширина должна быть равна **удвоенной ширине боковой границы треугольника**:

<pre>border-left-width: 52px + border-right-width: 52px = 104px
  </pre>

А высота должна быть равна удвоенной высоте треугольника (или ширине верхней\нижней границы &#8211; кому как нравиться):

<pre>border-top: 30px * 2 = 60px
  </pre>

В результате код будет следующим:

<pre><div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
  
</div>
  

<div class="inside">
  
</div>
  

<div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
  
</div>

  ...

  .inside{
    width: 104px;
    height: 60px;
    background-color: #778899;
  }
  </pre><figure id="attachment_1560" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon-600x541.jpg" alt="Hexagon на CSS" width="600" height="541" class="size-medium wp-image-1560" />][11]<figcaption class="wp-caption-text">Hexagon на CSS</figcaption></figure> 

Все &#8211; задача построения шестиугольника hexagon на CSS выполнена &#8211; все оказалось достаточно просто!

## Создание сетки из hexagon

Теперь можно усложнить задачу и создать из фигур hexagon своеобразную сетку, а-ля пчелиные соты. Задача тривиальная и весь вопрос сводиться к нескольким CSS-свойствам: `float`, `overflow`, `margin`, `padding`.

Создаю первый ряд сетки:

<pre><div class="row">
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
    
</div>

<!--  end row  -->

  ...

  .inside{
    width: 104px;
    height: 60px;
    background-color: #778899;
  }

  .hexa{
    float: left;
    margin: 0 3px 0 0;
  }

  .row{
    overflow: hidden;
  }
  </pre><figure id="attachment_1561" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_first_row-600x541.jpg" alt="Первый ряд сетки из hexagons" width="600" height="541" class="size-medium wp-image-1561" />][12]<figcaption class="wp-caption-text">Первый ряд сетки из hexagons</figcaption></figure> 

Второй ряд сетки строиться аналогично, за тем лишь исключением, что его необходимо сдвинуть влево и вверх:

<pre><!--  ROW  -->
  

<div class="row left_padding top_margin">
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_up hexagon_triangle_up_large">
      
    </div>
          
    
    <div class="inside">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_down hexagon_triangle_down_large">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
    
</div>

<!--  end row  -->

  .left_padding{
    padding-left: 53px;
  }

  .top_margin{
    margin-top: -28px;
  }
  </pre><figure id="attachment_1562" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_first-second_rows-600x541.jpg" alt="Первый и второй ряды сетки из hexagons" width="600" height="541" class="size-medium wp-image-1562" />][13]<figcaption class="wp-caption-text">Первый и второй ряды сетки из hexagons</figcaption></figure> 

Дальше продолжать не имеет смысла &#8211; все остальные ряды строятся аналогично. Нужно только управлять ими с помощью соотвествующих классов, смещая влево или вверх:<figure id="attachment_1563" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_full_stack-600x542.jpg" alt="Несколько рядов сетки из hexagons" width="600" height="542" class="size-medium wp-image-1563" />][14]<figcaption class="wp-caption-text">Несколько рядов сетки из hexagons</figcaption></figure> 

Лучше перейдем к другому интересному вопросу &#8211; созданию такого же шестиугольника hexagon, но несколько иной формы, &#8220;повернутого&#8221;. У которого углы развернуты по-горизонтали, а не по-вертикали.

### Построение повернутого hexagon на CSS

Задача создания развернутого hexagon почти ничем не отличается от задачи построения обычного шестиугольника. Только потребуется несколько дополнительных строчек кода. Дело в том, что в этом случае нужны углы, которые будут располагаться горизонтально и &#8220;смотреть&#8221; влево или вправо. Помимо этого, понадобиться &#8220;плавание&#8221; влево `float: left;`.

Для блока &#8211; &#8220;тела&#8221; hexagon нужно будет изменить значения высоты или ширины на прямопротивоположные.

Но не буду голословным, а лучше создам один такой hexagon:

<pre><div class="hexa">
  <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left">
    
  </div>
      
  
  <div class="inside_rotate left">
    
  </div>
      
  
  <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left">
    
  </div>
    
</div>

<!--  end hexa  -->

  /*  LEFT ARROW  */

  .hexagon_triangle_left{
    border-left-width: 0;
    border-top-color: transparent;
    border-bottom-color: transparent;
  }

  .hexagon_triangle_left_large{
    border-top-width: 52px;
    border-bottom-width: 52px;
  }

  /*  RIGHT ARROW  */

  .hexagon_triangle_right{
    border-right-width: 0;
    border-top-color: transparent;
    border-bottom-color: transparent;
  }

  .hexagon_triangle_right_large{
    border-top-width: 52px;
    border-bottom-width: 52px;
  }

  .inside_rotate{
    width: 60px;
    height: 104px;
    background-color: #778899;
  }

  .left{
    float: left;
  }
  </pre><figure id="attachment_1564" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated-600x542.jpg" alt="Развернутый hexagon" width="600" height="542" class="size-medium wp-image-1564" />][15]<figcaption class="wp-caption-text">Развернутый hexagon</figcaption></figure> 

Добавлю несколько таких шестиугольников, чтобы получился полный ряд:<figure id="attachment_1565" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_row-600x542.jpg" alt="Несколько развернутых hexagons в ряд" width="600" height="542" class="size-medium wp-image-1565" />][16]<figcaption class="wp-caption-text">Несколько развернутых hexagons в ряд</figcaption></figure> 

Отлично! Теперь нужно добавить еще один ряд &#8211; нижний. При этом опять придется немного модифицировать код, чтобы произвести смещение фигур влево и вверх:

<pre><!--  ROW  -->
  

<div class="row top_margin_double">
  <div class="hexa left_padding_double_middle">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left">
      
    </div>
          
    
    <div class="inside_rotate left">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa left_padding_double">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left">
      
    </div>
          
    
    <div class="inside_rotate left">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
      
  
  <div class="hexa left_padding_double">
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_left hexagon_triangle_left_large left">
      
    </div>
          
    
    <div class="inside_rotate left">
      
    </div>
          
    
    <div class="hexagon hexagon_colors hexagon_zero hexagon_triangle_right hexagon_triangle_right_large left">
      
    </div>
        
  </div>
  
  <!--  end hexa  -->
    
</div>

<!--  end row  -->

  .left_padding_double{
    padding-left: 64px;
  }

  .left_padding_double_middle{
    padding-left: 94px;
  }

  .top_margin_double{
    margin-top: -50px;
  }
  </pre><figure id="attachment_1566" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_several_rows-600x423.jpg" alt="Развернутые hexagons в два ряда" width="600" height="423" class="size-medium wp-image-1566" />][17]<figcaption class="wp-caption-text">Развернутые hexagons в два ряда</figcaption></figure> 

Можно продолжать постороние рядов до бесконечности, получая сетку из hexagons все большего размера:<figure id="attachment_1567" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_more_rows-600x423.jpg" alt="Развернутые hexagons в несколько рядов" width="600" height="423" class="size-medium wp-image-1567" />][18]<figcaption class="wp-caption-text">Развернутые hexagons в несколько рядов</figcaption></figure> 

### 3D-проекция hexagons

Можно видоизменить внешний вид сетки из hexagons, воспользовавшись CSS3-свойством `transform`. Создаю отдельный класс, в котором прописываю такие свойстсва:

<pre>.hexa_transform{
    -webkit-transform: perspective(600px) rotateX(60deg);
    -moz-transform: perspective(600px) rotateX(60deg);
    -ms-transform: perspective(600px) rotateX(60deg);
    -o-transform: perspective(600px) rotateX(60deg);
    transform: perspective(600px) rotateX(60deg);
  }
  </pre>

&#8230; и проверяю в окне браузера:<figure id="attachment_1568" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_transform-600x353.jpg" alt="3D-проекция сетки из hexagons" width="600" height="353" class="size-medium wp-image-1568" />][19]<figcaption class="wp-caption-text">3D-проекция сетки из hexagons</figcaption></figure> 

## Hexagons с помощью псевдо-классов

Рассмотренный выше способ создания hexagons хорош, но имеет один недостаток &#8211; слишком много дополнительных блоков, одними из которых являются блоки для создания треугольников. Можно (и нужно) значительно сократить код, воспользовавшись для этой цели псевдо-классами `:before` и `:after`. Давайте я так и поступлю, при этом возьму код из примера, не буду ничего выдумывать:

<pre>.hex:before {
      content: " ";
      width: 0; height: 0;
      border-bottom: 30px solid #778899;
      border-left: 52px solid transparent;
      border-right: 52px solid transparent;
      position: absolute;
      top: -30px;
  }

  .hex {
      margin-top: 30px;
      width: 104px;
      height: 60px;
      background-color: #778899;
      position: relative;
      float: left;
  }

  .hex:after {
      content: "";
      width: 0;
      position: absolute;
      bottom: -30px;
      border-top: 30px solid #778899;
      border-left: 52px solid transparent;
      border-right: 52px solid transparent;
  }
  </pre><figure id="attachment_1569" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_pseudo-600x353.jpg" alt="Hexagon на CSS с помощью псевдо-классов :before и :after" width="600" height="353" class="size-medium wp-image-1569" />][20]<figcaption class="wp-caption-text">Hexagon на CSS с помощью псевдо-классов :before и :after</figcaption></figure> 

### CSS Hexagon

Рассмотренный выше способ неплох, причем оба его варианта. Но для практического применения оба они достаточно трудоемкие. В Сети, помимо многих других подобного рода, имеется online CSS-генератор для создания hexagon в считанные минуты.

Адрес сервиса располагается здесь &#8211; [CSS Hexagon][21]. Помимо создания самого hexagon, там можно &#8220;прикрутить&#8221; к фигуре тень и границу, что просто великолепно!

Все &#8211; на этом обзор закончен.

 [1]: http://jtauber.github.io/articles/css-hexagon.html "CSS Hexagon Tutorial"
 [2]: http://css-tricks.com/examples/ShapesOfCSS/ "Shapes of CSS"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_origin.jpg
 [4]: http://localhost:7788/third/?p=153 "CSS – почему треугольник это треугольник"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_colors.jpg
 [7]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_zero.jpg
 [8]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_to_triangle.jpg
 [9]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_to_triangle_large.jpg
 [10]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_square_to_two_triangles.jpg
 [11]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon.jpg
 [12]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_first_row.jpg
 [13]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_first-second_rows.jpg
 [14]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_full_stack.jpg
 [15]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated.jpg
 [16]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_row.jpg
 [17]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_several_rows.jpg
 [18]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_more_rows.jpg
 [19]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_rotated_transform.jpg
 [20]: http://localhost:7788/third/wp-content/uploads/2014/07/hexagon_pseudo.jpg
 [21]: http://csshexagon.com/ "CSS Hexagon"