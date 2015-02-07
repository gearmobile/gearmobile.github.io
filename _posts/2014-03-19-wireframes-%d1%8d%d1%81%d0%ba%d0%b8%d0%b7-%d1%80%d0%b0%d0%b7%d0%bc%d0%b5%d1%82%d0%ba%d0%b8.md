---
title: 'Wireframes &#8211; визуальный эскиз HTML-разметки'
author: gearmobile
layout: post
permalink: /wireframes-%d1%8d%d1%81%d0%ba%d0%b8%d0%b7-%d1%80%d0%b0%d0%b7%d0%bc%d0%b5%d1%82%d0%ba%d0%b8/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - wireframes
---
Перед созданием HTML-разметки часто бывает необходимым и полезным сделать визуальный набросок будущего макета сайта (`wireframes`). Особенно это необходимо для начинающих HTML-верстальщиков, так как такой эскиз помогает понять, какие блоки и каким образом должны располагаться внутри будущей HTML-разметки. Когда я только начинал самостоятельно изучать практику верстки, я просто не мог обойтись без того, чтобы не нарисовать схематичное расположение будущих блоков.

Рисовал их где придется и как придется &#8211; в простом Paint или на листе бумаги карандашом или ручкой. Тут главное не до красоты &#8211; чтобы схема была доступной и понятной, это основное. Если схема не нарисована, то я элементарно не мог приставить себе &#8220;в голове&#8221;, как должна выглядеть блочная структура будущего сайта. А если я не мог представить, как должен выглядеть каркас здания, то о каком дальнейшем строительстве могла идти речь?<figure id="attachment_1039" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/mockup_notepad-600x430.jpg" alt="Wireframes в Notepad" width="600" height="430" class="size-medium wp-image-1039" />][1]<figcaption class="wp-caption-text">Wireframe в Notepad</figcaption></figure> 

Но вот когда блок-схема нарисована, то уже становится ясным, что делать дальше с точки зрения HTML-программирования. Я уже видел, что здесь нужно создать блок-обертку `div.wrap`, вверху поместить блок-шапку `div.header`, по центру должен располагаться большой блок `div.main` с основным контентом и внутренними блоками `div.sidebar` + `div.content`. Ну, а внизу должен находиться блок-подвал `div.footer`.

Другими словами, я просто повторял свои действия, выполненные на бумаге; но уже на компьютере и с помощью программного кода, в HTML-редакторе. Конечно, когда опыта у меня появилось немного побольше, я смог чисто &#8220;на глаз&#8221; определять основную структуру будущей HTML-разметки. Открывал готовый PSD-макет в Photoshop, &#8220;пробегал&#8221; его глазами и сразу &#8220;вычленял&#8221; составные части; которые должны были становиться основными блоками будущей HTML-страницы.

Но один я знаю, сколько времени у меня ушло на то, чтобы так &#8220;с лету&#8221; видеть структуру сайта. Я не хочу сказать, что это трудное дело. Совсем нет! Но в каждом деле нужен опыт и сноровка; а если ее нет, то дело движется тяжело и медленно (*сразу вспомнилась любимая книжка детства &#8211; Робинзон Крузо*).

К тому же, речь идет только о дизайне сайтов с простой структурой. Если же это сложный и большой сайт, то тут и опыт не поможет, так как одновременно держать &#8220;в голове&#8221; структуру и &#8220;ваять&#8221; код будет затруднительно. Тут без предварительной блок-схемы, разработанной на чем угодно и где угодно, не обойтись. Например, оцените вот такой пример готового наброска, сделанный на сайте [Mockup Builder][2]:<figure id="attachment_1040" style="width: 517px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/mockup_silverlight-517x600.jpg" alt="Mockup Builder" width="517" height="600" class="size-medium wp-image-1040" />][3]<figcaption class="wp-caption-text">Mockup Builder</figcaption></figure> 

Чуть позже, по мере чтения статей и книг, посвященных верстке, я познакомился с **тремя способами создания эскиза** HTML-разметки.

### Первый подход &#8211; аскетичный

Одни верстальщики идут по минималистичному пути и используют **стандартный лист бумаги и карандаш**. На бумаге делается набросок будущей схемы сайта, в котором расположены основные и дополнительные блоки HTML-страницы. Быстро, просто и со вкусом, что называется.

### Второй подход &#8211; wireframes

Другие верстальщики используют специальные программы для создания эскизов HTML-разметки. Такие программы относятся к классу *wireframes*. Они бывают разных типов: **online-сервисы** (*платные или бесплатные*) или **desktop-приложения** (*платные или бесплатные*). Мое личное предпочтение к использованию именно таких программ, ибо мне кажется смешным рисовать карандашом на бумаге, сидя перед компьютером.

Вообще-то, существуют **три класса программ для создания эскиза** будущего сайта: **wireframes**, **mockup**, **prototype**. **Wireframes** &#8211; для создания простого эскиза дизайна, ничего больше. **Mockup** &#8211; это тот же wireframes, но в нем добавлены визуальные отрисовки для всех элементов управления (кнопки, картинки и т. д.). **Prototype** &#8211; это самый продвинутый тип; это mockup с возможностью программирования элементов интерфейса (кнопок) прямо в программе.

Преимущество *wireframes* в том, что у них есть уже готовый набор инструментов для создания набросков HTML-разметки &#8211; блоки, кнопки, текстовые поля. Результат получается быстро, просто и красиво. Продвинутые программы этого класса используются разработчиками даже для создания набросков, которые можно предоставлять заказчику в качестве предварительно выполненной работы.

### Третий подход &#8211; Photoshop или Illustrator

Промежуточным звеном между первыми и вторыми верстальщиками являются кодеры, которые умеют и любят использовать для создания визуального HTML-макета программы редактирования графики, такие как Adobe Photoshop, Adobe Illustrator или Adobe Firework. И они в чем-то правы &#8211; в этих программах есть все необходимое для создания эскиза сайта и ничего лишнего.

## Wireframes &#8211; выбор инструмента

Что выбрать для работы &#8211; целиком зависит от предпочтений. Если в поисковой строке Google (Yandex) набрать `wireframes`, то результат превзойдет все ожидания &#8211; выбор просто огромен! На любой вкус и цвет &#8211; мощные программы для прототипирования (например, старейшая и известнейшая [Axure][4]), популярный [Balsamiq][5], готовый PNG-набор под Photoshop под названием [Stencil Kit][6] от команды Yahoo. Этот список можно продолжать и продолжать.<figure id="attachment_1041" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/axure_pr_prototype-600x414.jpg" alt="Axure PR - пример создания макета" width="600" height="414" class="size-medium wp-image-1041" />][7]<figcaption class="wp-caption-text">Axure PR &#8211; пример создания макета</figcaption></figure> <figure id="attachment_1042" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/balsamiq_mockup_web-600x562.jpg" alt="Официальный пример от Balsamiq" width="600" height="562" class="size-medium wp-image-1042" />][8]<figcaption class="wp-caption-text">Официальный пример от Balsamiq</figcaption></figure> 

Лично для меня интерес представляют программы класса `wireframes`, бесплатные online-версии с минималистичным интерфейсом и возможностями. Чтобы открыл ее, за пару минут разобрался, как работать и создавать. И только `wireframes`, ничего больше.

Наверное, в этом плане можно упомянуть online-сервисы [Cacoo][9] или [MockFlow][10]. Очень нравиться Balsamiq, но он платный (хотя есть бесплатная online-demo версия &#8211; [Balsamiq Demo][11]).<figure id="attachment_1043" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/cacoo-600x316.jpg" alt="Cacoo" width="600" height="316" class="size-medium wp-image-1043" />][12]<figcaption class="wp-caption-text">Cacoo</figcaption></figure> 

### Источники вдохновения

  * [Wireframes: A Beginner’s Guide][13]
  * [A Beginner&#8217;s Guide to Wireframing][14]

Вот такая получилась статья. На мой взгляд, не совсем информативная, наполовину &#8211; свои собственные мысли. Но может быть, кому и понадобиться, понравиться.

Оцените статью:  
<span id="post-ratings-1037" class="post-ratings" data-nonce="a859406cde"><img id="rating_1037_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1037, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1037_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1037, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1037_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1037, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1037_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1037, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1037_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1037, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1037_text"></span></span><span id="post-ratings-1037-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/03/mockup_notepad.jpg
 [2]: http://mockupbuilder.com/ "Mockup Builder"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/03/mockup_silverlight.jpg
 [4]: http://www.axure.com/ "Axure"
 [5]: http://balsamiq.com/ "Balsamiq"
 [6]: http://developer.yahoo.com/ypatterns/about/stencils/ "Stencil Kit"
 [7]: http://localhost:7788/third/wp-content/uploads/2014/03/axure_pr_prototype.jpg
 [8]: http://localhost:7788/third/wp-content/uploads/2014/03/balsamiq_mockup_web.jpg
 [9]: http://cacoo.com/ "Cacoo"
 [10]: http://www.mockflow.com/ "MockFlow"
 [11]: http://builds.balsamiq.com//b/mockups-web-demo/ "Balsamiq Demo"
 [12]: http://localhost:7788/third/wp-content/uploads/2014/03/cacoo.jpg
 [13]: http://psd.fanextra.com/tutorials/wireframes/ "Wireframes: A Beginner’s Guide"
 [14]: http://webdesign.tutsplus.com/articles/a-beginners-guide-to-wireframing--webdesign-7399 "A Beginner's Guide to Wireframing"