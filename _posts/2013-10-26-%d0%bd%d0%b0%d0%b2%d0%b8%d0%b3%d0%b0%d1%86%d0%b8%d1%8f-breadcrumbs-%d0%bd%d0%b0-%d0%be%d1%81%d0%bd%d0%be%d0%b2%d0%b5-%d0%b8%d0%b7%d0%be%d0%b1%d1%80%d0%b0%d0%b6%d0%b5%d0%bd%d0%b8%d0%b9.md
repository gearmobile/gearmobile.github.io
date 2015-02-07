---
title: Навигация breadcrumbs на основе изображений
author: gearmobile
layout: post
permalink: /%d0%bd%d0%b0%d0%b2%d0%b8%d0%b3%d0%b0%d1%86%d0%b8%d1%8f-breadcrumbs-%d0%bd%d0%b0-%d0%be%d1%81%d0%bd%d0%be%d0%b2%d0%b5-%d0%b8%d0%b7%d0%be%d0%b1%d1%80%d0%b0%d0%b6%d0%b5%d0%bd%d0%b8%d0%b9/
ratings_users:
  - 1
ratings_score:
  - 1
ratings_average:
  - 1
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - breadcrumbs
---
В предыдущей статье &#8220;[Навигация breadcrumbs с помощью треугольников на CSS][1]&#8221; описывался способ создания меню с помощью чистого CSS, без использования графики. Метод всем хорош, за исключением одного &#8211; поддержка такого меню в старых браузерах сомнительна. Но при переводе этой статьи упоминалась ссылка на способ создания навигации с помощью графики. Статья написана достаточно давно, но метод абсолютно рабочий. Автор статьи Veerle Pieters, а сам пост называется &#8220;Simple scalable CSS based breadcrumbs&#8221;. Ниже привожу даже не вольный его перевод, а вольный пересказ.

Несколько дней назад у меня стояла задача создать навигационное меню в стиле &#8220;хлебные крошки&#8221; (breadcrumbs) для сайта, над которым я работал. Я не думаю, что такое меню необходимо для каждого сайта, но в некоторых случаях оно очень полезно и практично. Это послужило поводом для меня написать статью для своего блога. Тот пример, которым я хочу поделиться с вами, является очень простым, при его создании применяется только один графический файл. Остальная часть навигации создается с помощью CSS-кода. Однако этот пример является как бы основой, которую можно расширять и применять на практике. Меню будет создаваться при помощи обычного маркированного списка ul.

Но сначала посмотрим на образец, с которым будем работать:<figure id="attachment_101" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/breadcrumbs-images-600x41.gif" alt="Навигационное меню хлебные крошки" width="600" height="41" class="size-medium wp-image-101" />][2]<figcaption class="wp-caption-text">Навигационное меню хлебные крошки</figcaption></figure> 

Меню достаточно простое, как и код, с помощью которого мы будем его создавать.

### HTML код &#8211; маркированный список ul

<pre>&lt;ul class="crumbs"&gt;
    &lt;li&gt;&lt;a href="#"&gt;Home&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Main section&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Sub section&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;&lt;a href="#"&gt;Sub sub section&lt;/a&gt;&lt;/li&gt;
    &lt;li&gt;The page you are on right now&lt;/li&gt;
  &lt;/ul&gt;</pre>

Все пункты меню имеют ссылки, кроме последнего &#8211; &#8220;The page you are on right now&#8221; (Страница, на которой вы сейчас находитесь). При работе над меню я задавался вопросом &#8211; является ли список наиболее подходящей структурой для создания меню? Я полагаю, что применение списка в этом случае не является строгим правилом, но мне кажется &#8211; это наиболее семантичный и правильный вариант.

### CSS код &#8211; создаем стили для меню

Задаем общие стили для меню &#8211; убираем маркеры и обнуляем отступы в браузерах Firefox, IE:

<pre>ul, li {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }</pre>

Далее для меню задаем класс с именем crumbs, устанавливаем границу толщиной в 1px и фиксированную ширину 30px:

<pre>.crumbs {
    border: 1px solid #dedede;
    height: 30px;
  }</pre>

Все &#8220;крошки&#8221; должны располагаться горизонтально, в одну линию, поэтому элементы li делаем плавающими через свойство float:left. Текст меню должен быть отцентрирован точно по вертикали, для этого устанавливаем для него значение свойства line-height равное высоте всего меню &#8211; 30px. Помещаем слева каждого пункта небольшое пространство для отступа с помощью padding-left:10px. И задаем цвет текста #777:

<pre>.crumbs li {
    float: left;
    line-height: 30px;
    padding-left: 10px;
    color: #777;
  }</pre>

Нам необходимо, чтобы вся область пункта меню была кликабельной, поэтому делаем ее блочным элементом display:block. Далее помещаем для ссылки фоновое изображение, вырезанное из макета. Для этого нужно вырезать только саму &#8220;стрелку&#8221;:<figure id="attachment_102" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/breadcrumbs-images_cut-600x41.gif" alt="Вырезание стрелки из навигации" width="600" height="41" class="size-medium wp-image-102" />][3]<figcaption class="wp-caption-text">Вырезание стрелки из навигации</figcaption></figure> 

&#8230; которую &#8220;задвигаем&#8221; вправо (100%) и размещаем точно по вертикали (50%). Также делаем у ссылки отступ справа padding-left:15px, в котором будет как раз и находиться фоновое изображение (вырезанная стрелка):

<pre>.crumbs li a {
    display: block;
    padding: 0 15px 0 0;
    background: url(img/crumbs.gif) 100% 50% no-repeat;
  }</pre>

Уже практически все сделано. Осталось задать стили для текста ссылок. Уберем стандартное подчеркивание и изменим ее цвет:

<pre>.crumbs li a:link, .crumbs li a:visited {
    text-decoration: none;
    color: #777;
  }</pre>

Придадим ссылкам небольшую анимацию с помощью псевдо-класса :hover и :focus. При наведении курсора мыши или получения фокуса с клавиатуры цвет текста ссылки будет меняться:

<pre>.crumbs li a:hover, .crumbs li a:focus {
    color: #dd2c0d;
  }</pre>

Результат нашей работы представлен здесь:<figure id="attachment_103" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/breadcrumbs-images_result-600x67.gif" alt="Готовая навигация хлебные крошки" width="600" height="67" class="size-medium wp-image-103" />][4]<figcaption class="wp-caption-text">Готовая навигация хлебные крошки</figcaption></figure> 

*Примечание переводчика:*

> Автор статьи максимально упростил пример и сам код соответственно, насколько я понимаю. Дело в том, что на примере хорошо виден линейный горизонтальный градиент для каждого из пунктов меню. Однако в коде это никак отображено не было. Ну, не беда &#8211; разве это проблема создать линейный градиент на CSS3? Сама задача ведь выполнена!

Оцените статью:  
<span id="post-ratings-100" class="post-ratings" data-nonce="289db54d78"><img id="rating_100_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(100, 1, '1 Star');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_100_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(100, 2, '2 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_100_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(100, 3, '3 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_100_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(100, 4, '4 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_100_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(100, 5, '5 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>1,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_100_text"></span></span><span id="post-ratings-100-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=91 "Навигация breadcrumbs с помощью треугольников на CSS"
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/breadcrumbs-images.gif
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/breadcrumbs-images_cut.gif
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/breadcrumbs-images_result.gif