---
title: 'Photoshop &#8211; пример нарезки макета для верстки'
author: gearmobile
layout: post
permalink: /photoshop-%d0%bf%d1%80%d0%b8%d0%bc%d0%b5%d1%80-%d0%bd%d0%b0%d1%80%d0%b5%d0%b7%d0%ba%d0%b8-%d0%bc%d0%b0%d0%ba%d0%b5%d1%82%d0%b0-%d0%b4%d0%bb%d1%8f-%d0%b2%d0%b5%d1%80%d1%81%d1%82%d0%ba%d0%b8/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 41
ratings_score:
  - 186
ratings_average:
  - 4.54
categories:
  - Photoshop для кодера
tags:
  - photoshop
---
В Интернете существует мало материалов с примерами как нарезать макет в Photoshop. Для новичков-верстальщиков этот факт является камнем преткновения. И хотя на форумах, посвященных web-дизайну, много говориться о том, что &#8220;да там все просто &#8211; нечего учить&#8221;, &#8220;в сети полно информации по этому вопросу&#8221;, но на самом деле это не совсем так. Я могу судить об этом по самом себе. Мне потребовалось некоторое время, чтобы самому разобраться и докопаться до процесса нарезки.

В этой статье я постараюсь описать нарезку макета на примере одного из его объектов и тем самым внести посильную помощь в процесс освоения верстки. Думаю, данная статья будет полезна для новичков, каким я был совсем недавно сам.

Итак, у нас имеется psd-макет, созданный неким &#8220;гением&#8221; web-дизайна:<figure id="attachment_480" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/polo360-600x600.jpg" alt="Макет сайта" width="600" height="600" class="size-medium wp-image-480" />][1]<figcaption class="wp-caption-text">Макет сайта</figcaption></figure> 

Как и положено, макет представлен в формате psd (в исходном коде) со всеми слоями так, как нарисовал его дизайнер.

Нам необходимо вырезать логотип будущего сайта. В данном случае это красивая цветастая напись POLO360. Видим, что логотип состоит из двух текстов &#8211; самого POLO360 и нижней строки &#8220;My kind of business blog&#8221;. Также имеется некое графическое изображение (слева от надписи), которое также является частью логотипа. В сумме все эти объекты являются одним целым и представляют логотип сайта.

Вот нам и предстоит задача вырезать его. Первым и самым трудным делом является нахождение всех слоев, отвечающих за прорисовку логотипа. Для этого нужно выбрать инструмент &#8220;Move Tool (V)&#8221;. В панели инструментов Photoshop необходимо проверить, что стоит галочка в разделе &#8220;Auto &#8211; Select&#8221;:<figure id="attachment_481" style="width: 536px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/auto-select_photoshop.png" alt="auto-select photoshop" width="536" height="36" class="size-full wp-image-481" />][2]<figcaption class="wp-caption-text">auto-select photoshop</figcaption></figure> 

Это необходимо для того, чтобы при выделении объекта на макете в Палитре слоев автоматически выделились все слои, отвечающие за отрисовку данного объекта. Другими словами &#8211; так проще искать нужные слои при нарезке.

Теперь начинается самое интересное. Если дизайнер человек ответственный и пунктуальный, то перед передачей макета на верстку он рассортирует все слои по папкам. Каждая из папок будет однозначно указывать и содержать в себе все слои, отвечающие за отрисовку только одного объекта. И жизнь верстальщика значительно упрощается.

Но такое бывает редко и слои разбросаны по палитре как попало. нам необходимо методом &#8220;научного тыка&#8221; найти нужные нам.

Для этого открываем (если еще не открыли) Палитру слоев и пробуем отключать или включать отображение слоя, щелкая мышью на значке &#8220;глаза&#8221; слева от названия слоя. Тем самым, мы проверяем, входит ли этот слой в состав нужного объекта или нет. Как только находим нужный слой, то отмечаем его цветом, чтобы потом не потерять (как это делается, рассказано в статье &#8220;[Photoshop &#8211; как объединить несколько слоев в один слой][3]&#8220;).

Когда все слои найдены, картина в Палитре слоев будет примерно такой:<figure id="attachment_482" style="width: 239px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/selected_layers1.png" alt="selected layers" width="239" height="473" class="size-full wp-image-482" />][4]<figcaption class="wp-caption-text">selected layers</figcaption></figure> 

Теперь объединяем отмеченные нами слои. Для этого держим зажатой клавишу Ctrl и выделяем каждый из слоев одинарным щелчком мыши. Получаем следующую картину:<figure id="attachment_483" style="width: 239px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/ready_layers.png" alt="Выделенные слои" width="239" height="473" class="size-full wp-image-483" />][5]<figcaption class="wp-caption-text">Выделенные слои</figcaption></figure> 

Далее необходимо объединить выделенные слои в один. Другими словами, мы сведем нужные нам слои в один и в результате изображение (в нашем случае &#8211; логотип) будет цельным. Только так мы можем вырезать его впоследствии. Для объединения слоев щелкаем правой кнопкой мыши на любом из выделенных слоев и в открывшемся контекстном меню выбираем &#8220;Merge Layers&#8221;:<figure id="attachment_484" style="width: 177px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/merge_layers1.png" alt="merge layers" width="177" height="435" class="size-full wp-image-484" />][6]<figcaption class="wp-caption-text">merge layers</figcaption></figure> 

Видим такую картину:<figure id="attachment_485" style="width: 239px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/merged_layers.png" alt="Объединенный слой" width="239" height="473" class="size-full wp-image-485" />][7]<figcaption class="wp-caption-text">Объединенный слой</figcaption></figure> 

Несколько слоев слились в один. Все, теперь мы готовы к нарезке.

Выбираем в панели инструментов &#8220;Rectangular Marquee Tool(M)&#8221; и обводим логотип произвольным прямоугольником:<figure id="attachment_486" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/selected_logo-600x229.png" alt="Выделенный логотип" width="600" height="229" class="size-medium wp-image-486" />][8]<figcaption class="wp-caption-text">Выделенный логотип</figcaption></figure> 

Теперь копируем выделенную нами область &#8211; нажимаем на клавиатуре комбинацию клавиш Ctrl+C.

Создаем в Photoshop новый документ &#8211; нажимаем Ctrl+N. Откроется новая вкладка с диалоговым окном настройки создаваемого документа:<figure id="attachment_487" style="width: 555px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/photoshop_new-document.png" alt="Photoshop - создание нового документа" width="555" height="406" class="size-full wp-image-487" />][9]<figcaption class="wp-caption-text">Photoshop &#8211; создание нового документа</figcaption></figure> 

Здесь самым важным является поле &#8220;Preset&#8221;. В его значении должно стоять &#8220;Clipboard (Буфер обмена)&#8221;. Если все было сделано правильно, то Photoshop автоматически создаст новый документ с размерами той области, которую мы скопировали. Размеры программа возмет из &#8220;Буфера обмена&#8221;, куда была помещена выделенная нами область. Остальные параметры для нас неважны. Нажимаем ОК.

Появится новая вкладка, но пока еще пустая. Точнее, в ней уже будет создан документ с указанными в диалоговом окне размерами. Но ничего, кроме белого фонового изображения, этот документ содержать не будет:<figure id="attachment_488" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/photoshop_new-document_ready-600x401.png" alt="Photoshop - новый документ почти создан" width="600" height="401" class="size-medium wp-image-488" />][10]<figcaption class="wp-caption-text">Photoshop &#8211; новый документ почти создан</figcaption></figure> 

Нам осталось вставить в этот документ выделенную область, которая все еще находится в &#8220;Буфере обмена&#8221;. Для этого нажимаем на клавиатуре Ctrl+V. Результат:<figure id="attachment_489" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/ready_logo-600x422.png" alt="Вставленная в новый документ область" width="600" height="422" class="size-medium wp-image-489" />][11]<figcaption class="wp-caption-text">Вставленная в новый документ область</figcaption></figure> 

Как видим, Photoshop автоматически обрезал изображение так, чтобы не было пустых областей вокруг него (ведь при выделении мы создали произвольный прямоугольник &#8211; лишь бы выделить логотип).

Однако, белый фон остался. А он нам совсем не нужен. Это делается очень просто. Переводим взгляд на &#8220;Палитру слоев&#8221;&#8221; и видим там всего два слоя: &#8220;Layer 1&#8243; и &#8220;Background&#8221;. Слой &#8220;Layer 1&#8243; &#8211; это вставленная нами область, а &#8220;Background&#8221; &#8211; фоновое изображение. Щелкаем мышью на значке &#8220;глазика&#8221; напротив слоя &#8220;Background&#8221;:<figure id="attachment_490" style="width: 239px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/deactivated_layer.png" alt="Отключенный фоновый слой" width="239" height="473" class="size-full wp-image-490" />][12]<figcaption class="wp-caption-text">Отключенный фоновый слой</figcaption></figure> 

Само изображение в окне Photoshop изменилось &#8211; вместо белого фона появилась шахматная &#8220;доска&#8221;. Это говорит о том, что фоновый слой у нас теперь прозрачный.

Теперь нам осталось только сохранить отредактированное изображение. Переходим в меню &#8220;File &#8211; Save for Web &#8230;&#8221;:<figure id="attachment_491" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/03/save_for_web-600x439.png" alt="Сохранение для Web" width="600" height="439" class="size-medium wp-image-491" />][13]<figcaption class="wp-caption-text">Сохранение для Web</figcaption></figure> 

Здесь нам нужны два поля.

Верхнее &#8211; для выбора формата сохраняемого файла. В Интернете имеются подробные описания, как выбрать нужный формат. На самом деле все просто. Формат GIF имеет поддержку прозрачного фона, но не имеет поддержки передачи градиентов. Формат JPEG наоборот, хорошо передает плавные переходы цветов (градиент), но у него отсутствует прозрачный фон. Формат PNG-8 очень похож на GIF, только имеет лучший алгоритм сжатия. Формат PNG-24 имеет как поддержку градиентов, так и прозрачный фон (по другому называется &#8211; прозрачные пиксели). В нашем случае нам нужен как градиент, так и прозрачный фон, поэтому выбор однозначен &#8211; PNG-24.

Нижнее поле важно для контроля размера выходного файла. Photoshop автоматически подсчитывает размер, который получится, если сохранить файл в выбранном формате. В нашем случае это будет составлять 6Kb, что абсолютно приемлемо.

Все, сохраняем файл с выбранными настройками и задаем ему имя &#8211; logo.png.

На этом обзор примера нарезки макета в программе Photoshop заканчиваю. Думаю, он был достаточно полным и понятным.

Оцените статью:  
<span id="post-ratings-478" class="post-ratings" data-nonce="8a167b4df4"><img id="rating_478_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(478, 1, '1 Star');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_478_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(478, 2, '2 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_478_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(478, 3, '3 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_478_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(478, 4, '4 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_478_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(478, 5, '5 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>41</strong> votes, average: <strong>4,54</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_478_text"></span></span><span id="post-ratings-478-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/03/polo360.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/03/auto-select_photoshop.png
 [3]: http://localhost:7788/third/?p=316 "Photoshop - как объединить несколько слоев в один слой"
 [4]: http://localhost:7788/third/wp-content/uploads/2013/03/selected_layers1.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/03/ready_layers.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/03/merge_layers1.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/03/merged_layers.png
 [8]: http://localhost:7788/third/wp-content/uploads/2013/03/selected_logo.png
 [9]: http://localhost:7788/third/wp-content/uploads/2013/03/photoshop_new-document.png
 [10]: http://localhost:7788/third/wp-content/uploads/2013/03/photoshop_new-document_ready.png
 [11]: http://localhost:7788/third/wp-content/uploads/2013/03/ready_logo.png
 [12]: http://localhost:7788/third/wp-content/uploads/2013/03/deactivated_layer.png
 [13]: http://localhost:7788/third/wp-content/uploads/2013/03/save_for_web.png