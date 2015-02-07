---
title: Верстаем с помощью модульной сетки 960gs
author: gearmobile
layout: post
permalink: /module-grid-960gs/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 9
ratings_score:
  - 44
ratings_average:
  - 4.89
categories:
  - Статьи по CSS
tags:
  - 960gs
---
Вот плавно и постепенно, стараясь без рывков и пробелов в познаниях front-end, я подошел к теме модульных сеток на CSS. Очередные мысли по поводу верстки для начинающего верстальщика ))

Зачем я подошел к этой теме? Для чего нужны модульные сетки для верстальщика? Ответ прост &#8211; сегодня по крайней мере половина всех дизайнов верстается по такой сетке. Зачем это делается? Для быстроты процесса верстки и стандартизации этого же самого процесса. Сама идея модульной сетки далеко и далеко не новая &#8211; в типографии она была разработана еще в прошлом веке (*если я не ошибаюсь*). Благодаря такой сетке упорядочивается расположение всех элементов текста (изображений) на странице журнала, газеты и т. д.

Чтобы воочию представить себе модульную сетку в типографии, возьмите любой журнал или статью и внимательно посмотрите на любую его(ее) страницу. Вы сразу обратите внимание, что колонки текста, заголовки, фотографии на странице располагаются не хаотично, а *в некотором порядке*. Если попытаться начертить границы между блоками контента, то можно увидеть **определенную блочную структуру**:<figure id="attachment_1098" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/journal_grid_example-600x399.jpg" alt="Выдуманный пример разметки журнальной страницы" width="600" height="399" class="size-medium wp-image-1098" />][1]<figcaption class="wp-caption-text">Выдуманный пример разметки журнальной страницы</figcaption></figure> 

Рисунок выше &#8211; самый что ни на есть истинный пример модульной сетки. Блоки на этом рисунке могут быть блоками текста или изображениями. И такое расположение блоков информации на странице вполне может иметь место быть в реальной жизни.

Кстати, а почему модульные? Откуда такое название? Все просто &#8211; под модулем в таких сетках подразумевается &#8220;кирпичик&#8221;, основа сетки. Минимальная единица &#8220;измерения&#8221;, которая является основой этой сетки. 

Обыкновенная кирпичная стена &#8211; это тоже модульная структура, модулем у которой является &#8211; **кирпич**. Стена увеличивается в размерах в высоту и ширину на шаг, равный высоте и ширине кирпича. Поэтому такая структура и называется модульной.

Сетка в электронной таблице MS Excel тоже является модульной структурой, в основе которой лежит **ячейка** этой сетки. Таблица в Excel может увеличиваться или уменьшаться с шагом, равным размеру ячейки этой таблицы.

Как очень хорошо известно, CSS &#8211; это типография, перешедшая в Интернет. Многие термины и понятия также перекочевали из типографии в технологию CSS: размер шрифта, межстрочное расстояние и т. д. Не стала исключением модульная сетка.

В один прекрасный момент веб-дизайнеры поняли, что не стоит изобретать велосипед. Что создание макета веб-страницы в коде HTML&CSS гораздо удобнее, проще и быстрее выполнять по модульной сетке, нежели &#8220;тасовать&#8221; блоки произвольно. Кроме того, сам дизайн страницы получается более стандартизированным, унифицированным; **подчиненным одним и тем же, единым правилам**.

С помощью кода на CSS была сделана попытка воспроизвести модульную сетку в Веб и применить ее на практике. Первой такой (*насколько я знаю*) попыткой была система **960 Grid System**:<figure id="attachment_1100" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid-600x379.jpg" alt="Модульная сетка на CSS" width="600" height="379" class="size-medium wp-image-1100" />][2]<figcaption class="wp-caption-text">Модульная сетка на CSS</figcaption></figure> 

При первом взгляде на рисунок (*не знаю, как у вас*), у меня сразу возник вопрос &#8211; &#8220;а где же здесь сетка?&#8221; Сетка, сетка &#8211; **это и есть сетка, спроектированная под особенности Веб**! Ведь вы хорошо знаете, что в макете веб-страницы имеет значение только ширина блоков контента; высота же блоков является *величиной переменной*, она меняется в зависимости от количества контента, наполняющего эти блоки; она почти никогда не задается жестко, фиксировано. Поэтому в данном случае строки сетки совсем ни к чему &#8211; **остаются только колонки**.

Как уже упоминалось выше, модульная сетка пришла в CSS из типографии; понятия, связанные с модульной сеткой, также пришли из типографии.

В модульной сетке имеются всего **три параметра**:

  * **container** (*контейнер*)
  * **column** (*колонка*)
  * **gutter** (*канавка*)<figure id="attachment_1102" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_structure-600x410.jpg" alt="Структура модульной сетки на CSS" width="600" height="410" class="size-medium wp-image-1102" />][3]<figcaption class="wp-caption-text">Структура модульной сетки на CSS</figcaption></figure> 

Видим, что основной блок-обертка (**container**) содержит в себе 12 колонок (**column**). Содержимое (</em>контент</em>) располагается в этих колонках. Колонок может быть не обязательно 12; другими популярными величинами являются **16 колонок** и **24 колонки**:<figure id="attachment_1103" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_16_columns-600x379.jpg" alt="Модульная CSS-сетка из 16 колонок" width="600" height="379" class="size-medium wp-image-1103" />][4]<figcaption class="wp-caption-text">Модульная CSS-сетка из 16 колонок</figcaption></figure> <figure id="attachment_1104" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_24_columns-600x375.jpg" alt="Модульная CSS-сетка из 24 колонок" width="600" height="375" class="size-medium wp-image-1104" />][5]<figcaption class="wp-caption-text">Модульная CSS-сетка из 24 колонок</figcaption></figure> 

Откуда такие величины &#8211; 12, 16 и 24 колонки? Во-первых, они взяты из математических расчетов, на которых основана модульная сетка. А во-вторых, такие значения наиболее применимы на практике.

Колонки разделяются между собой промежутками (**gutter**). Как правило, самые крайние отступы от колонок равны половине **gutter** &#8211; **gutter/2**. 

Колонки можно объединять между собой &#8211; две колонки объединить в одну, три колонки объединить в одну и так далее. В результате получаются ячейки сетки &#8211; блоки с контентом. Чтобы визуально разъяснить (*если еще непонятно*) этот вопрос, посмотрите на рисунок ниже:<figure id="attachment_1105" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/css_module_grid-600x377.jpg" alt="Пример блочной верстки на основе CSS-сетки" width="600" height="377" class="size-medium wp-image-1105" />][6]<figcaption class="wp-caption-text">Пример блочной верстки на основе CSS-сетки</figcaption></figure> 

Вот и получается примерный вид блочной верстки страницы на основе модульной CSS-сетки. 

Ну, это было краткое теоретическое введение в модульные CSS-сетки. Задачей данной статьи не являются теоретические основы подобных сеток, так как уже давно написаны прекрасные материалы (*с не менее прекрасными иллюстрациями*) по этой теме другими людьми. В этой же статье мы попытаемся осуществить практическое применение таких сеток и воспользуемся одной из старейший из них &#8211; **960 Grid System** (сокращенное название &#8211; 960gs).

### Получение модульной сетки 960gs

Первым шагом необходимо получить копию заготовки (шаблон) данной модульной CSS-сетки. Для этого заходим на сайт проекта [960gs][7] и скачиваем оттуда заготовку, нажав большую кнопку посередине с надписью &#8211; **&#8216;Big ol&#8217;DOWNLOAD button :)&#8217;**. Получаем на свой компьютер архив с именем `960-Grid-System-master.zip`.

Кстати, а почему такое название у этой модульной сетки &#8211; 960 Grid System? Все просто, здесь цифра 960 &#8211; это ширина блока-обертки **container** в 960px, наиболее приемлемая ширина страницы сайта для мониторов с разрешением 1024x768px. На время создания этой модульной CSS-сетки большинство сайтов делалось фиксированной ширины для наиболее популярного разрешения мониторов &#8211; 1024x768px.

Разархивируем этот пакет и взглянем на его содержимое:

  * app_plugins
  * code
  * licenses
  * logo_files
  * sketch_sheets
  * templates
  * .gitignore
  * README.txt

В папке **app_plugins** находятся плагины под два графических редактора &#8211; Fireworks и Photoshop. Цель плагинов &#8211; будучи установленными в эти программы, помогать создавать макеты сайтов на основе модульной сетки 960gs. Это помощь для дизайнеров, которые рисуют макеты будущих сайтов.

В папке **licenses** располагаются тексты лицензий, под которыми распространяется данная модульная сетка.

В директории **logo_files** находятся логотип 960 Grid System в разных форматах &#8211; `.ai`, `.eps`, `.png` и `.psd`. Как пишется сам автор 960gs &#8211; Nathan Smith, этот логотип был создан и предоставлен в бесплатное пользование всем желающим по многочисленным просьбам &#8220;трудящихся&#8221; ))

Есть также заготовки модульной сетки в виде **линованной бумаги с колонкой для комментариев**. Эти заготовки помещены в папку **sketch_sheets** в формате `.pdf` и готовы для того, чтобы их распечатать и пользоваться. Видимо, это тоже было сделано по просьбам &#8220;трудящихся&#8221;, которые любят создавать наброски макета на бумаге с помощью ручки или карандаша.

А вот для настоящих IT-ов имеется директория **templates**, в которой расфасованы точно такие же макеты, но в электронном виде, под самые разные wireframe-программы. Количество впечатляет &#8211; тут и Balsamiq, и Photoshop, Firework и Illustrator; под Gimp на Linux и под Omnigraffle на Mac OS X; пользуйся не хочу, что называется.

Но мы вернемся к самой главной папке, которую мы пропустили &#8211; **code**. Там находится то, ради чего мы и затеялись с этой модульной сеткой 960gs &#8211; готовые файлы с кодом этой самой сетки. Файлы формата HTML (`demo.html`, `demo_24_col.html`, `demo_24_col_rtl.html`, `demo_rtl.html`) можно посмотреть, но интереса они представляют мало &#8211; как понятно из их названия, это всего лишь демо-файлы. В папке **img** находятся три файла формата `.gif`: `12_col.gif`, `16_col.gif`, `24_col.gif`. Задача этих файлов &#8211; &#8220;подкладывать&#8221; их в виде фона для блока `.container_12` (или `.container_16` или `.container_24`) для того, чтобы удобно было визуально видеть эту самую сетку при верстке.

Папка **CSS** имеет список файлов формата CSS:

  * 960.css
  * 960*12*col.css
  * 960*12*col_rtl.css
  * 960*16*col.css
  * 960*16*col_rtl.css
  * 960*24*col.css
  * 960*24*col_rtl.css
  * 960_rtl.css
  * demo.css
  * reset.css
  * reset_rtl.css
  * text.css
  * text_rtl.css

&#8230; и подпапку **min**, в которой содержится точно такой же список файлов. Разница между первым и вторым списком в том, что первый список &#8211; это **developer**-версия, а второй &#8211; **production**-версия.

Внимательный читатель спросит &#8211; а что это за суффикс странный у некоторых файлов CSS &#8211; rtl. Ну, даже новичкам (которые в теме) должно быть понятно, что это right-to-left, стили для создания дизайна, в котором текст пишется и располагается справа налево. Таки если вы не собираетесь иммигрировать на историческую родину, то эти стили вам никогда не пригодятся, по большому счету!

Эти файлы формата CSS является тем самым, ради чего мы заходили на оф. сайт &#8211; это и сеть модульная сетка 960gs! Можно открыть их в HTML-редакторе и просмотреть исходный код &#8211; он очень короткий и простой.

Построение верстки на основе модульной сетки 960gs производится с помощью классов, расположенных в главном файле `960_12_col.css` (или `960_16_col.css`, или `960_24_col.css`). Классов в модульной сетке 960gs не так уж много &#8211; точнее, их совсем мало:

  * .container*12 (.container*16, .container_24)
  * .grid_х
  * .push_х
  * .pull_х
  * .alpha
  * .omega
  * .prefix_х
  * .suffix_х
  * .clear

Эти классы &#8211; своего рода рычаги, с помощью которых можно управлять созданием верстки:

  * **Класс** `.container_12` создает блок-обертку шириной 960px, расположенную по центру окна браузера, состоящую из 12 колонок. Аналогично классы `.container_16` и `.container_24` также создают обертку шириной 960px, но состоящую из 16 и 24 колонок, соответственно.
  * **Класс** `.grid_х` &#8211; это общее представление (*можно сказать &#8211; формула*) для создания ячеек модульной сетки. В качестве `х` может быть значение от 1 до 12 (в 12-колоночной сетке), от 1 до 16 (в 16-колоночной сетке), от 1 до 24 (в 24-колоночной сетке). Задав значение вместо `х`, создается ячейка шириной `х` колонок. То есть, `.grid_2` создает ячейку шириной 2 колонки; `.grid_10` &#8211; создает ячейку шириной в 10 колонок. Естественно, значение `х` не может превышать общее число колонок в контейнере. То есть, в контейнере с классом `.container_12` может быть класс `.grid_12`, но не больше. В контейнере с классом `.container_16` может быть класс `.grid_16`, но не больше. Аналогично с контейнером класса `.container_24`.
  * **Класс** `.push_х` &#8220;сдвигает&#8221; ячейку вправо на указанное количество колонок. То есть, класс `.push_4` &#8220;отодвигает&#8221; ячейку вправо на 4 колонки.
  * **Класс** `.pull_х` &#8220;сдвигает&#8221; ячейку влево на указанное количество колонок. Например, `.pull_3` сдвинет ячейку влево на три колонки.
  * **Классы** `.alpha` и `.omega` просты &#8211; они убирают отступы у ячейки слева и справа, соответственно.
  * **Классы** `.prefix_х` и `.suffix_х` добавляют пустое пространство (расширяют) ячейку слева и справа, соответственно.
  * **Класс** `.clear` служит для &#8220;очистки&#8221; содержимого после плавающего блока.

Давайте от теории перейдем к практике и создадим каркас обычного трех-колоночного макета, в котором &#8220;шапка&#8221; и &#8220;подвал&#8221; будут занимать всю ширину страницы:<figure id="attachment_1107" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/css_module_grid_simple_mockup-600x304.jpg" alt="Пример простого трех-колоночного макета" width="600" height="304" class="size-medium wp-image-1107" />][8]<figcaption class="wp-caption-text">Пример простого трех-колоночного макета</figcaption></figure> 

Из скачанного архива `960-Grid-System-master.zip` нам потребуются файлы:

  * **text.css** (*в нем находятся все правила по типографике*)
  * **reset.css** (*файл сброса стилей для браузеров*)
  * **960\_24\_col.css** (*модульная CSS-сетка на 24 колонок*)
  * **24_col.gif** (фоновая картинка, рисующая 24 колонок в основном блоке `.container_24`)

Выбираем их оттуда и раскладываем по папкам нашего собственного проекта:

  * **css**: 
      * text.css
      * reset.css
      * 960*24*col.css
  * **img**: 
      * 24_col.gif

В шапке `header` файла `index.html` производим последовательное подключение полученных файлов. Только один из них &#8211; `style.css` &#8211; мы создадим самостоятельно, для написания своих собственных CSS-стилей. Все остальные файлы оставим без изменения &#8211; так и нужно поступать с файлами данного фреймворка (и не только этого):

<pre><link rel="stylesheet" type="text/css" href="css/reset.css" />

<link rel="stylesheet" type="text/css" href="css/text.css" />

<link rel="stylesheet" type="text/css" href="css/960_24_col.css" />

<link rel="stylesheet" type="text/css" href="css/style.css" />
</pre>

Затем создадим HTML-структуру страницы, применив знания классов, которые были рассмотрены выше. Шапке сайта задаем класс `.grid_24`, чтобы она заняла всю ширину 24-колоночного блока. Затем создаем левый блок шириной в 8 колонок с помощью класса `.grid_8`, центральный блок шириной в 13 колонок с помощью класса `.grid_13`, правый блок шириной в 3 колонки через класс `.grid_3`. И внизу помещаем &#8220;подвал&#8221; сайта опять на всю ширину страницы с помощью класса `.grid_24`:

<pre><div class="container_24">
  <!-- header -->
    &lt;header class="grid_24">&lt;/header>
  
  
  
  <!-- content -->
    &lt;aside class="grid_8 leftSideBar">&lt;/aside>
    &lt;main class="grid_13">&lt;/main>
    &lt;aside class="grid_3 rightSideBar">&lt;/aside>
  
  
  
  <!-- footer -->
    &lt;footer class="grid_24">&lt;/footer>
  
  
</div>

<!-- end container -->
</pre>

Все, совсем несложными движениями мы создали структуру страницы сайта. Осталось применить некоторое оформление к блокам, чтобы визуально их отличать:

<pre>.container_24{
  background: url(../img/24_col.gif) top left repeat;
  margin-top: 10px;
}

header{
  background-color: hsla(120,100%,50%,.4);
  min-height: 100px;
  margin-bottom: 10px;
}

.leftSideBar, .rightSideBar, main{
  min-height: 300px;
  margin-bottom: 10px;
}

.leftSideBar{
  background-color: hsla(240,100%,50%,.5);
}

main{
  background-color: hsla(180,100%,50%,.4);
}

.rightSideBar{
  background-color: hsla(300,100%,50%,.3);
}

footer{
  background-color: hsla(60,100%,50%,.7);
  min-height: 50px;
}
</pre>

На официальном сайте проекта 960gs имеется ссылка на слайд-шоу, в котором есть несколько интересных примеров создания разметки с помощью 960gs. Давайте разберем их &#8211; кусочки кода, которые можно применить на практике (кстати, именно такое предназначение имеют сниппеты).

### Простой пример колонок

Очень простой пример создания двух рядов с тремя и двумя ячейками на всю ширину страницы.<figure id="attachment_1109" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_several_grids-600x206.jpg" alt="Два ряда с колонками на всю ширину страницы" width="600" height="206" class="size-medium wp-image-1109" />][9]<figcaption class="wp-caption-text">Два ряда с колонками на всю ширину страницы</figcaption></figure> 

Для этого создаем такую разметку:

<pre><div class="container_12">
  <!-- header -->
  
  
  
  <div class="grid_4">
    <p>
      1/3 ширины блока .container
    </p>
    
  </div>
  
  
  
  <div class="grid_4">
    <p>
      1/3 ширины блока .container
    </p>
    
  </div>
  
  
  
  <div class="grid_4">
    <p>
      1/3 ширины блока .container
    </p>
    
  </div>
  
  
  
  <div class="clear">
    
  </div>
  
  <!-- гадость! -->
  
  
  
  <!-- footer -->
  
  
  
  <div class="grid_6">
    <p>
      1/2 ширины блока .container
    </p>
    
  </div>
  
  
  
  <div class="grid_6">
    <p>
      1/2 ширины блока .container
    </p>
    
  </div>
  
  
</div>

<!-- end container -->
</pre>

&#8230; и CSS-код:

<pre>.container_12{
  background: url(../img/12_col.gif) top left repeat;
  margin-top: 10px;
}

div[class^="grid"]{
  min-height: 100px;
  text-align: center;
  line-height: 100px;
}

div[class="grid_4"]{
  background-color: hsla(120,100%,50%,.4);
}

div[class="grid_6"]{
  background-color: hsla(240,100%,50%,.4);
}
</pre>

### Ячейки, обернутые другой ячейкой

Простой пример обертывания ячеек с сетке еще одной &#8211; общей ячейкой, которая может служить для придания общего фона для всех элементов внутри блока. Стоит обратить внимание на применение двух классов `alpha` и `omega` для первого и последнего блоков. С помощью этих классов убираются отступы слева и справа от этих крайних блоков. Если не добавить эти классы, то верстка поломается.<figure id="attachment_1110" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_wrap_grids-600x49.jpg" alt="Обертывание ячеек в 960gs" width="600" height="49" class="size-medium wp-image-1110" />][10]<figcaption class="wp-caption-text">Обертывание ячеек в 960gs</figcaption></figure> 

HTML-код:

<pre><div class="container_12">
  <!-- content -->
  
    
  
  <div role="wrap" class="grid_12">
    <div class="grid_3 alpha">
      <p>
        Part_1
      </p>
          
    </div>
    
        
    
    <div class="grid_3">
      <p>
        Part_2
      </p>
          
    </div>
    
        
    
    <div class="grid_3">
      <p>
        Part_3
      </p>
          
    </div>
    
        
    
    <div class="grid_3 omega">
      <p>
        Part_4
      </p>
          
    </div>
    
      
  </div>
  
  
</div>

<!-- end container -->
</pre>

&#8230; и CSS-код:

<pre>.container_12{
  background: url(../img/12_col.gif) top left repeat;
}

div[role="wrap"]{
  background-color: hsla(120,100%,50%,.3);
  padding: 10px 0;
  margin-top: 10px;
}

div[class^="grid_3"]{
  background-color: hsla(240,100%,50%,.4);
}
</pre>

### Смещение ячеек в 960gs<figure id="attachment_1113" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_rearrangement_grids-600x80.jpg" alt="Перемещение ячеек в сетке 960gs" width="600" height="80" class="size-medium wp-image-1113" />][11]<figcaption class="wp-caption-text">Перемещение ячеек в сетке 960gs</figcaption></figure> 

Интересный пример перемещения ячеек в модульной сетке 960gs. Если внимательно посмотреть на пример, то станет заметно, что фиолетовый блок с надписью Last (последний) стоит на первом месте в ряду. Достигнуто это благодаря двум классам `.push` и `.pull`. Если не вдаваться в код, стоящий за этими двумя классами, то их назначение запомнить легко: `push` &#8211; толкать (толкаем, двигаем ячейки слева направо), `pull` &#8211; тянуть (тянем, двигаем ячейки справа налево). В этом примере было произведено взаимное замещение двух ячеек &#8211; они поменялись местами.

HTML-код:

<pre><div class="container_12">
  <!-- header -->
  
    
  
  <div role="first" class="grid_6 push_6">
    <div class="grid_2 alpha">
      <p>
        Grid_1
      </p>
          
    </div>
    
        
    
    <div class="grid_2">
      <p>
        Grid_2
      </p>
          
    </div>
    
        
    
    <div class="grid_2 omega">
      <p>
        Grid_3
      </p>
          
    </div>
    
      
  </div>
  
    
  
  <!-- content -->
    
  
  <div role="last" class="grid_6 pull_6">
    Last
  </div>
  
  
</div>

<!-- end container -->
</pre>

&#8230; CSS-код:

<pre>.container_12{
  background: url(../img/12_col.gif) top left repeat;
  margin-top: 10px;
}

div[class^="grid"]{
  min-height: 100px;
}

div[role="first"]{
  background-color: hsla(120,100%,50%,.3);
}

div[role="last"]{
  background-color: hsla(240,100%,50%,.3);
}

div[class^="grid_2"]{
  background-color: hsla(180,100%,50%,.2);
}
</pre>

### Создание рамки вокруг ячейки в 960gs

Также интересный пример создания рамки вокруг ячейки с изображением. Такая рамка с помощью обычного CSS-кода создается очень легко и просто; а вот в системе 960gs это достаточно непростая задача. Для этого придется в одну ячейку вложить блок, для которого установить границу, которая будет служить рамкой для картинки.<figure id="attachment_1112" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_border_grids-600x205.jpg" alt="Ячейка с рамкой в 960gs" width="600" height="205" class="size-medium wp-image-1112" />][12]<figcaption class="wp-caption-text">Ячейка с рамкой в 960gs</figcaption></figure> 

HTML-код:

<pre><div class="container_12">
  <!-- content -->
  
      
  
  <div role="top" class="grid_7">
    <div role="border">
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vitae, voluptatum, minus dolor eaque officiis quis placeat commodi unde minima recusandae amet velit dolorem perferendis quibusdam dolorum! Saepe iste nisi nobis!
      </p>
              
      
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Architecto, iusto, id veniam non quas nesciunt laborum error debitis ipsam delectus sequi incidunt sunt et iste nulla deserunt vitae aut beatae.
      </p>
              
      
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Recusandae, ab, totam, labore, odio accusamus excepturi repellendus porro deserunt ut nisi molestiae molestias quibusdam accusantium saepe doloribus perspiciatis aliquid voluptatum sit?
      </p>
            
    </div>
        
  </div>
  
      
  
  <div role="top" class="grid_5">
    <div role="border" class="banner">
      
    </div>
        
  </div>
  
    
</div>

<!-- end container -->
</pre>

&#8230; CSS-код:

<pre>.container_12{
  margin-top: 10px;
}

div[role="top"]{
  background-color: hsla(120,100%,50%,.3);
}

div[role="border"]{
  border: 10px solid #e5e5e6;
  height: 280px;
}

  div[role="border"] p{
    margin: 10px;
    padding: 5px;
    background-color: hsla(0,0%,0%,.3);
    border-radius: 5px;
  }

  div[role="border" ][class="banner"]{
    background: url(../img/weiss.jpg) top left no-repeat;
  }

</pre>

### Ячейка с обтеканием в 960gs

И напоследок еще один пример, на этот раз с примером отмены обтекания. Обратите внимание на два последних ряда. В предпоследнем намеренно сделано три ячейки, чтобы ширина страницы не была заполнена до конца. После этого ряда добавлен блок с классом `clear`, чтобы предотвратить смещение ячеек следующего ряда в это пустое пространство. Это одно из предназначений класса `clear` в системе 960gs.<figure id="attachment_1111" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_clear_grids-600x312.jpg" alt="Отмена обтекания ячейки в 960gs" width="600" height="312" class="size-medium wp-image-1111" />][13]<figcaption class="wp-caption-text">Отмена обтекания ячейки в 960gs</figcaption></figure> 

<pre><div class="container_24">
  <!-- header -->
      
  
  <div class="grid_24 navbar">
    <div class="grid_12 push_2 alpha header">
      
    </div>
          
    
    <div class="grid_6 push_5 omega header">
      
    </div>
        
  </div>
  
      
  
  <!-- content -->
      
  
  <div class="grid_24 content">
    &lt;aside class="grid_10 alpha leftColumn">&lt;/aside>
          
    
    <div class="grid_4 pull_9 label">
      
    </div>
          
    
    <div class="grid_11 push_3 rightColumn omega">
      
    </div>
        
  </div>
      
      
  
  <!-- subtopics -->
      
  
  <div class="grid_6 topic">
    
  </div>
      
  
  <div class="grid_6 topic">
    
  </div>
      
  
  <div class="grid_6 topic">
    
  </div>
      
  
  <div class="clear">
    
  </div>
  
  <!-- вот он зачем здесь, этот странный блок! -->
  
      
  
  <!-- subtopics -->
      
  
  <div class="grid_6 subtopic">
    
  </div>
      
  
  <div class="grid_6 subtopic">
    
  </div>
      
  
  <div class="grid_6 subtopic">
    
  </div>
      
  
  <div class="grid_6 subtopic">
    
  </div>
  
    
</div>

<!-- end container -->
</pre>

&#8230; CSS-код:

<pre>.container_24{
  background: url(../img/24_col.gif) top left repeat;
}

.navbar{
  margin-top: 5px;
  margin-bottom: 10px;
  padding: 10px 0;
  background-color: hsla(240,100%,50%,.2);
}

.header{
  min-height: 50px;
  background-color: hsla(120,100%,50%,.7);
}

.content{
  background-color: hsla(60,100%,50%,.2);
  padding: 15px 0;
  margin-bottom: 10px;
}

.leftColumn{
  background-color: hsla(300,100%,50%,.5);
  min-height: 100px;
}

.rightColumn{
  background-color: hsla(180,100%,50%,.3);
  min-height: 150px;
  margin-top: -60px;
}

.label{
  background-color: hsla(0,0%,0%,.5);
  min-height: 50px;
  margin-top: 10px;
}

.news{
  background-color: hsla(0,0%,0%,.3);
}

.topic{
  background-color: hsla(0,0%,0%,.5);
  min-height: 80px;
}

.subtopic{
  background-color: hsla(30,100%,50%,.4);
  min-height: 80px;
}

.border{
  padding: 0 10px;
}
</pre>

Вот и все. Объемной получилась статейка! ))

Оцените статью:  
<span id="post-ratings-1096" class="post-ratings" data-nonce="f293e017c3"><img id="rating_1096_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1096, 1, '1 Star');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1096_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1096, 2, '2 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1096_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1096, 3, '3 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1096_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1096, 4, '4 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1096_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1096, 5, '5 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>9</strong> votes, average: <strong>4,89</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1096_text"></span></span><span id="post-ratings-1096-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/04/journal_grid_example.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_structure.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_16_columns.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_24_columns.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/04/css_module_grid.jpg
 [7]: http://960.gs/ "960gs"
 [8]: http://localhost:7788/third/wp-content/uploads/2014/04/css_module_grid_simple_mockup.jpg
 [9]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_several_grids.jpg
 [10]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_wrap_grids.jpg
 [11]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_rearrangement_grids.jpg
 [12]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_border_grids.jpg
 [13]: http://localhost:7788/third/wp-content/uploads/2014/04/module_grid_960_clear_grids.jpg