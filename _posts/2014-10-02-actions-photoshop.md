---
title: Actions в Photoshop
author: gearmobile
excerpt: Создание операций (actions) для автоматизации рутинных задач в Photoshop. Пример создания простого action в Photoshop для экспортирования изображений в Web.
layout: post
permalink: /actions-photoshop/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Photoshop для кодера
tags:
  - actions
  - photoshop
---
Рассмотрим вопрос **автоматизации действий** в программе Photoshop. Тема статьи перекликается с предыдущей статей &#8220;[Macros в Sublime Text 3][1]&#8220;, посвященной макросам в Sublime Text.

В Adobe Photoshop также имеется инструмент для записи макросов, только называется он по другому &#8211; Actions (Операции). Но от смены названия суть не меняется. С помощью Actions (Операции) в Photoshop можно записать последовательность своих действий, а потом запускать их на выполнение каждый раз, когда это понадобиться.

Для чего нужны Actions (Операции) верстальщику? Не поверите, но это очень удобная вешь, которая значительно ускоряет работу в Photoshop. В частности, можно ускорить нарезку изображений из psd-макета.

Буквально за месяц до этого я приобрел лицензию на плагин PNG Hat для автоматизации вырезания картинок:<figure id="attachment_1883" style="width: 423px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/png_hat-423x600.png" alt="Плагин PNG Hat в Photoshop" width="423" height="600" class="size-medium wp-image-1883" />][2]<figcaption class="wp-caption-text">Плагин PNG Hat в Photoshop</figcaption></figure> 

Так вот &#8211; я просто на тот момент не знал о существовании макросов в Photoshop. Actions &#8211; это намного круче, чем PNG Hat! Узнал о существовании такой возможности благодаря видео Николая Громова.

Но меньше слов, больше дела. Приступим к изучению Actions (Операции) в Photoshop на простом, но очень практичном примере. Создадим макрос для вырезания и экспорта картинок из psd-макета.

### Actions &#8211; где они живут

Все actions в Photoshop проживают по одному адресу &#8211; в меню &#8220;Окно&#8221; &#8211; &#8220;Операции&#8221; (если Photoshop русскоязычный). Или же быстрее и проще &#8211; через **сочетание клавиш Alt+F9**. Как и все другие инструменты в этой программе, actions имеют свою собственную панель:<figure id="attachment_1884" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/actions_panel-600x535.png" alt="Палитра Actions в Photoshop" width="600" height="535" class="size-medium wp-image-1884" />][3]<figcaption class="wp-caption-text">Палитра Actions в Photoshop</figcaption></figure> 

По умолчанию в Photoshop уже есть готовые операции (actions), расположенные в папке &#8220;Операции по умолчанию&#8221;: &#8220;Виньетка (выделенная область)&#8221;, &#8220;Рамка &#8211; 50 пикс.&#8221;, &#8220;Деревянная рамка &#8211; 50 пикс.&#8221; и так далее.

Actions в Photoshop не могут жить вне набора операций (правильно такой набор называется Set). На скриншоте как раз показаны два таких набора (Set) &#8211; один от Photoshop, второй &#8211; мой собственный.

Внизу палитры расположены шесть кнопок управления actions. Перечислю их по порядку, слева направо:

  * остановка записи action
  * запуск записи action
  * воспроизведение записанного action
  * создание нового набора actions
  * создание нового action

### Создаем новую операцию (action)

В палитре &#8220;Операции&#8221; кликаем на кнопке &#8220;Создать новый набор&#8221;. В диалоговом окне вводим название нового набора &#8211; &#8220;Export*Images*to_Web&#8221;, затем сохраняем его. Созданный набор операций (Set) готов, но он пока пустой, в нем нет ни одной операции (action):<figure id="attachment_1885" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/new_set_of_actions-600x535.png" alt="Новый Set для Actions" width="600" height="535" class="size-medium wp-image-1885" />][4]<figcaption class="wp-caption-text">Новый Set для Actions</figcaption></figure> 

В самом левом столбце палитры можно напротив каждого Set&#8217;а ставить или убирать галочки, тем самым включая или отлючая данный набор операций (actions).

Треугольнички напротив названия Set&#8217;а разворачивают или сворачивают данный набор операций (actions). Каждый набор операций (Set) может содержать неограниченное число операций (actions).

Предварительно откроем в Photoshop любой psd-макет, из которого можно экспортировать изображения для будущего HTML-шаблона. В палитре &#8220;Слои&#8221; заранее выделим слой с изображением, которое будем экспортировать (отключим все эффекты данного слоя, если они есть):<figure id="attachment_1886" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/select_layer_with_image-600x455.png" alt="Слой с изображением для экспорта" width="600" height="455" class="size-medium wp-image-1886" />][5]<figcaption class="wp-caption-text">Слой с изображением для экспорта</figcaption></figure> 

И нажмем кнопку &#8220;Создать новую операцию&#8221; в палитре &#8220;Операции&#8221;. Откроется диалоговое окна настройки будущей операции (action):<figure id="attachment_1887" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/setting_new_action-600x326.png" alt="Настройка будущего action" width="600" height="326" class="size-medium wp-image-1887" />][6]<figcaption class="wp-caption-text">Настройка будущего action</figcaption></figure> 

В этом окне указываем имя для будущей операции (action); в какой набор операций (set) она будет входить; назначить &#8220;горячие&#8221; клавиши для данной операции.

Кнопка &#8220;Записать&#8221; запускает процесс записи макроса. Внизу панели &#8220;Операции&#8221; кнопочка &#8220;Запись операции&#8221; станет красной, что напоминает о том, что запись пошла! С этого момента все мои действия будут запоминаться программой Photoshop, поэтому буду внимательным.

Вырезание картинки из выбранного слоя я буду делать пошагово, в следующем порядке:

  * дублирование активного слоя
  * отрезка прозрачных пикселов (trimming)
  * сохранение полученной картинки для Web
  * закрытие нового документа без его сохранения

Не забываем нажать кнопочку &#8220;Остановить запись&#8221;. В принципе, все мои действия очень легко прочитать внутри самой операции (action):<figure id="attachment_1888" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/created_action-600x537.png" alt="Созданная операция (action)" width="600" height="537" class="size-medium wp-image-1888" />][7]<figcaption class="wp-caption-text">Созданная операция (action)</figcaption></figure> 

### Настройка операции (action)

По большому счету, созданная мною операция полностью готова к работе. Можно ради любопытства выбрать любой другой слой с изображением и нажать клавишу F3. Произойдет практически мгновенное экспортирование изображения в этом слоя для Web.

Но что может не устраивать нас в этой операции? Все, кроме одного &#8211; возможность самому выбирать, куда Photoshop должен сохранять экспортируемое изображение.

Для этой цели существует колоночка с пустыми квадратиками напротив каждого действия в записанной мною операции (action). Если навести курсор мыши на любой из них, то всплывающий tooltip подскажет, что это &#8211; &#8220;Возможность установки или отмены установки диалогового окна&#8221;.

К слову сказать, все операции (actions) в Photoshop делятся на два вида:

  * автоматические (без вмешательства пользователя)
  * полуавтоматические (с частичным вмешательством пользователя)

Нам как раз нужно из автоматической операции (action) сделать ее полуавтоматической. На этапе &#8220;Экспортировать&#8221; нужно сделать так, чтобы Photoshop спрашивал нас, куда нужно сохранять изображение.

Делается это очень просто &#8211; достаточно кликнуть мышью в нужном окошке:<figure id="attachment_1889" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/dialog_action-600x425.png" alt="Диалоговое окно экспорта изображения" width="600" height="425" class="size-medium wp-image-1889" />][8]<figcaption class="wp-caption-text">Диалоговое окно экспорта изображения</figcaption></figure> 

Попробуем снова экспортировать изображение по нажатию клавиши F3. Вуаля &#8211; видим, что открылось окно Photoshop, в котором можем задать параметры для экспорта изображения. И в том числе &#8211; куда необходимо сохранять изображение:<figure id="attachment_1890" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/10/action_export_for_web-600x431.png" alt="Экспорт изображения для Web" width="600" height="431" class="size-medium wp-image-1890" />][9]<figcaption class="wp-caption-text">Экспорт изображения для Web</figcaption></figure> 

### Заключение

На этом можно закончить тему создания операций (actions) в Photoshop. На самом деле эта тема большая и достаточно сложная. Я видел даже специальный курс для дизайнеров по написанию actions под Photoshop.

Но для верстальщика нет необходимости создавать большие и сложные операции. Поэтому этого уже достаточно для ускорения и облегчения своей работы. Попробуйте &#8211; оно того стоит!

Оцените статью:  
<span id="post-ratings-1881" class="post-ratings" data-nonce="ccaf21321a"><img id="rating_1881_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1881, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1881_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1881, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1881_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1881, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1881_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1881, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1881_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1881, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1881_text"></span></span><span id="post-ratings-1881-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1850 "Macros в Sublime Text 3"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/10/png_hat.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/10/actions_panel.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/10/new_set_of_actions.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/10/select_layer_with_image.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/10/setting_new_action.png
 [7]: http://localhost:7788/third/wp-content/uploads/2014/10/created_action.png
 [8]: http://localhost:7788/third/wp-content/uploads/2014/10/dialog_action.png
 [9]: http://localhost:7788/third/wp-content/uploads/2014/10/action_export_for_web.png