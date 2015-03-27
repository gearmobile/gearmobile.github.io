---
title: 'Photoshop &#8211; как преобразовать градиент в правила CSS3'
author: gearmobile
layout: post
permalink: /photoshop-%d0%ba%d0%b0%d0%ba-%d0%bf%d1%80%d0%b5%d0%be%d0%b1%d1%80%d0%b0%d0%b7%d0%be%d0%b2%d0%b0%d1%82%d1%8c-%d0%b3%d1%80%d0%b0%d0%b4%d0%b8%d0%b5%d0%bd%d1%82-%d0%b2-%d0%bf%d1%80%d0%b0%d0%b2%d0%b8/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 7
ratings_score:
  - 33
ratings_average:
  - 4.71
categories:
  - Photoshop для кодера
tags:
  - photoshop
---
При верстке макета из psd в HTML и CSS может встретиться такая ситуация, когда фоновая заливка какого-либо объекта на макете выполнена в виде градиента. Напомню, что градиентом называется плавный переход одного цвета в другой. Такой прием часто используется в дизайне для придания большей эффектности внешнему виду сайта.

Во времена CSS2.1 поддержки передачи градиента с помощью стилевых правил не было. Поэтому при верстке выходили из положения путем вырезания части фонового изображения из макета. И затем тиражирования этого изображения, используя правило background-image:url() с сопуствующим ему правилом background-repeat.

На сегодняшний день, хотя стандарт CSS3 еше полностью не принят, некоторые из его возможностей активно применяются благодаря поддержке браузеров. Одним из таких свойств является возможность передачи градиента стилевыми правилами.

Но, одно дело знать, как с помощью правил написать градиент в CSS, а другое &#8211; как &#8220;выбрать&#8221; заданный дизайнером градиент из программы Photoshop. Это абсолютно логично &#8211; ведь шаблон создается по макету, с масимальной идентичностью ему.

Каким же образом можно узнать, какой градиент был заложен в объект макета? Все достаточно просто. В этом небольшом руководстве будут пройдены последовательные шаги, детально объясняющие все необходимые действия.

К примеру, имеется макет сайта, у которого фоновоя заливка шапки имеет градент. Просто вырезать из нее фоновое изображение и замостить им шапку на html-странице, может было бы и проще. Но это уже прошлый век. К тому же это заметно утяжеляет html-страницу. Мы поступим по другому:<figure id="attachment_410" style="width: 463px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/fragment-header.jpg" alt="Фрагмент макета с градиентной заливкой" width="463" height="182" class="size-full wp-image-410" />][1]<figcaption class="wp-caption-text">Фрагмент макета с градиентной заливкой</figcaption></figure> 

Еще раз внимательно посмотрим на фрагмент макета. Здесь изображена шапка будущего сайта. Хорошо видно, что фоновая заливка выполнена в виде градиента &#8211; зеленого цвета, плавно переходящего из одного оттенка в другой снизу вверх (или сверху вниз &#8211; это уже как нравиться).

Первое, что необходимо сделать, это открыть слой, отвечающий за прорисовку фонового цвета шапки. Переходим в Панель слоев, находим там такой слой и двойным щелчком мыши открываем его свойства. Появится диалоговое окно, в котором, если для данного объекта установлены какие-либо дополнительные свойства (эффекты), то в списке слева они будут отмечены галочкой. В нашем случае таким свойством будет &#8220;Наложение градиента&#8221;:<figure id="attachment_411" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/properties-layer-600x347.jpg" alt="Дополнительные эффекты слоя" width="600" height="347" class="size-medium wp-image-411" />][2]<figcaption class="wp-caption-text">Дополнительные эффекты слоя</figcaption></figure> 

Щелкаем по нему в списке мышкой, если он не открылся автоматически. И переводим взгляд в правую часть окна. Что мы здесь видим и что нам здесь будет надо? В этом окне это три свойства слоя, которые нам понадобятся при написании стилевых правил. Первое &#8211; тип градиента. Здесь он линейный. Второе &#8211; цвет градиента. И третье &#8211; угол наложения градиентной заливки. В данном случае это вертикальный градиент (90 градусов). Все, больше в этом окне нам больше ничего не потребуется, так как мы узнали то, что необходимо:<figure id="attachment_412" style="width: 464px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/gradient.jpg" alt="Градиентное наложение" width="464" height="478" class="size-full wp-image-412" />][3]<figcaption class="wp-caption-text">Градиентное наложение</figcaption></figure> 

Однако, ведь это еще не все. Необходимы значения стоп-цветов. То есть, начальный цвет и конечный цвет. С помощью них и создается градиент. Для этого щелкаем мыщью прямо на окошке с цветов градиента в этом же окне. Откроется следующее (вложенное) окно, в котором мы сможет узнать точные значения цветов:<figure id="attachment_413" style="width: 480px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/gradient-color.jpg" alt="Цветовая схема градиента" width="480" height="501" class="size-full wp-image-413" />][4]<figcaption class="wp-caption-text">Цветовая схема градиента</figcaption></figure> 

Здесь нам необходима цветовая шкала (выделена рамкой). На ней в наглядном графическом режиме представлен градиент, который используется для заливки шапки макета будущего сайта. Как видно, она представляет из себя цветовую полосу, в начале которой есть один цвет (темно-зеленый), а в конце другой (светло-зеленый). На этой шкале нам потребуются нижние маркеры (отмечены стрелками). С помощью этих маркеров задаются начальный стоп-цвет (крайний левый) и конечный стоп-цвет (крайний правый).

Каким же образом иы узнаем точные значения этих цветов? Все опять просто. Будем последовательны. Наводим куроср мыши на крайний левый маркер и щелкаем по нему. Видим, что сам маркер окрасился в темно-зеленый цвет. А окошко выбора цвета внизу также изменило свой цвет на точно такой же. Это именно тот цвет, который используется в этом градиенте в качестве начального:<figure id="attachment_414" style="width: 464px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/start-stop-marker.jpg" alt="Начальный стоп-маркер" width="464" height="299" class="size-full wp-image-414" />][5]<figcaption class="wp-caption-text">Начальный стоп-маркер</figcaption></figure> 

Щелкаем на окошке выбора цвета и видим его точное значение. Здесь можно выбрать значение цвета как в rbg, так и в hex &#8211; что вы предпочитаете:<figure id="attachment_415" style="width: 574px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/color-start-stop.jpg" alt="Значение начального стоп-цвета" width="574" height="377" class="size-full wp-image-415" />][6]<figcaption class="wp-caption-text">Значение начального стоп-цвета</figcaption></figure> 

Аналогично поступаем с маркером конечного стоп-цвета и получаем точное значение его цвета. Не забываем скопировать значения цветов, чтобы их можно было использовать в дальнейшем:<figure id="attachment_416" style="width: 589px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/color-stop-stop.jpg" alt="Значение конечного стоп-цвета" width="589" height="392" class="size-full wp-image-416" />][7]<figcaption class="wp-caption-text">Значение конечного стоп-цвета</figcaption></figure> 

Теперь мы имеем все данные для того, чтобы создать стилевые правила градиента в CSS3. Приступим к их написанию:

<pre>background: linear-gradient(top, #77c531, #4d722d);
  background: -webkit-gradient(linear, 0 0, 0 100%, from(#77c531), to(#4d722d));
  background: -webkit-linear-gradient(top, #77c531, #4d722d);
  background: -moz-linear-gradient(top, #77c531, #4d722d);
  background: -o-linear-gradient(top, #77c531, #4d722d);
  background: -ms-linear-gradient(top, #77c531, #4d722d);
  filter: progid:dximagetransform.microsoft.gradient(startColorstr='#77c531', endColorstr='#4d722d', GradientType=0);
  -ms-filter: "progid:DXImageTransform.Microsoft.gradient(startColorstr='#77c531',endColorstr='#4d722d')";</pre>

Разберем первую строку:

<pre>background: linear-gradient(top, #77c531, #4d722d);</pre>

Мы хотим (точнее &#8211; так задумал дизайнер), чтобы градиент &#8220;шел&#8221; сверху вниз от светло-зеленого к темно-зеленому. Поэтому в правилах указываем начальную точку отсчета для градиента &#8211; top (верх). Теперь &#8220;отсчет&#8221; градиента пойдет сверху вниз. Затем указываем начальный стоп-цвет (светло-зеленый #77c531) и конечный стоп-цвет (темно-зеленый #4d722d). Также не забываем указать атрибут свойства background &#8211; linear-gradient, говоря тем самым браузеру, что это линейный градиент. Как видим, в этом правиле мы применили все значения, которые получили из Photoshop.

Но данное правило является самым общим. Чтобы на сегодняшний день все браузеры понимали его, ниже мы прописываем почти точно такие же правила, но с учетом специфики каждого из браузеров.

Для браузеров на движке WebKit (Google Chrome, Safari):

<pre>background: -webkit-gradient(linear, 0 0, 0 100%, from(#77c531), to(#4d722d));
  background: -webkit-linear-gradient(top, #77c531, #4d722d);</pre>

Первая строка нужна, чтобы градиент понимал Chrome ниже версии 4. Вторая &#8211; для более новых версий. Как видим, синтаксис под движок webkit более громоздок. Разберем его:

  * background: -webkit-gradient(linear, 0 0, 0 100%, from(#77c531), to(#4d722d));
  * background: -webkit-linear-gradient(top, #77c531, #4d722d);

&#8230; указывают, что это градиент линейный. Дальше &#8211; 0 0, 0 100%, и top, указывают начальную точку отсчета. Причем, если во втором случае все просто &#8211; это верх (top), то в первом несколько сложнее. Первые два нуля указывают положение в процентах начальной точки отсчета. Вместо нулей там могут стоять служебные слова left top, (левый верхний угол), right top (правый верхний угол). В нашем случае это левый верхний угол. Вторая пара чисел &#8211; это положение в процентах конечной точки отсчета. Забыл сказать, что если положение точки отсчета задается в процентах, то первым числом из пары идет значение по горизонтали (ось X), вторым &#8211; значение по вертикали (ось Y). Исходя из этого, можно легко подсчитать, что конечная точка градиента в нашем случае будет в левом нижнем углу, что равнозначно записи &#8211; left bottom. Таким образом мы указали браузеру, что необходимо построить вертикальный градиент, начинающийся в верхней точке и идущий вертикально (90 градусов) вниз до нижней точки. Осталось задать начальный стоп-цвет from(#77c531) и конечный стоп-цвет to(#4d722d).

Следующие три строки предназначены для браузеров Firefox (префикс -moz), Opera (префикс -o), IE (префикс -ms). В них все просто и ничем не отличается от общего правила, за исключнием специфичных префиксов.

Отдельная тема &#8211; это версии IE. Здесь без нестандартных приемов не обойтись, иначе градиент просто не будет отображен. Для них применяется фильтр:

<pre>filter: progid:dximagetransform.microsoft.gradient(startColorstr='#77c531', endColorstr='#4d722d', GradientType=0);
  -ms-filter: "progid:DXImageTransform.Microsoft.gradient(startColorstr='#77c531',endColorstr='#4d722d')";</pre>

На этом процесс преобразования градиента в Photoshop в CSS-правила можно считать законченным.

### P.S.

Забыл упомянуть, что уже довольно давно существуют различные плагины под Photoshop, которые в автоматическом режиме преобразовывают свойства объектов на макете в правила CSS. Звучит очень заманчиво. Однако, в своей практической работе я еще не сталкивался ни с одним из них. Поэтому поводу мне сказать пока нечего.

Оцените статью:  
<span id="post-ratings-409" class="post-ratings" data-nonce="eca1274efa"><img id="rating_409_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(409, 1, '1 Star');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_409_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(409, 2, '2 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_409_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(409, 3, '3 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_409_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(409, 4, '4 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_409_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(409, 5, '5 Stars');" onmouseout="ratings_off(4.7, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>7</strong> votes, average: <strong>4,71</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_409_text"></span></span><span id="post-ratings-409-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/fragment-header.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/properties-layer.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/gradient.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/gradient-color.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2013/11/start-stop-marker.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2013/11/color-start-stop.jpg
 [7]: http://localhost:7788/third/wp-content/uploads/2013/11/color-stop-stop.jpg