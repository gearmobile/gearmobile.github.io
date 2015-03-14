---
layout: post
title: "В Photoshop шрифт в пунктах - как перевести в пикселы"
author: gearmobile
tags: [photoshop, pt, px]
---

Есть небольшая проблема. Столкнулся с тем, что при верстке макета необходимо получить размер шрифта, которым выполнена надпись. Однако, при выделении текста инструментом "Horizontal Type Tool" в панели Photoshop показывает мне размер шрифта в `points`. А мне необходимо в правилах CSS записать размер шрифта в пикселях.

Чтобы заставить Photoshop показывать размеры шрифтов в пикселях, нужно выполнить несложные настройки.

Переходим в меню Photoshop по пути "Edit - Preferences - Units & Rulers". Откроется окно, в котором неодходимо перейти в пункт "Units & Rulers".

В верхнем разделе правой части окна находим "Units" с двумя полями - "Rulers & Type":

<figure id="attachment_700" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/points_to_pixels1-600x233.png" alt="Окно настроек единиц измерения в Photoshop" width="600" height="233" class="size-medium wp-image-700" />][1]
	<figcaption class="wp-caption-text">Окно настроек единиц измерения в Photoshop</figcaption>
</figure> 

В выпадающем списке поля "Type" меняем значения с "Points" на "Pixels". Сохраняем изменения кнопкой ОК и и выходим из настроек. Проверим результат изменений. Снова выбираем инструмент "Horizontal Type Tool" и выделяем мышью текст в макете.

Смотрим на панель:

<figure id="attachment_701" style="width: 335px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/pixels1.png" alt="Размер шрифта в пикселях" width="335" height="46" class="size-full wp-image-701" />][2]
	<figcaption class="wp-caption-text">Размер шрифта в пикселях</figcaption>
</figure>

Что и требовалось. Теперь Photoshop автоматически показывает размер шрифта в пикселях, что удобно при написании правил в CSS.

Другой вопрос, что такой перевод из одних единиц измерения в другой весьма условный, так как многое зависит от разрешения, в котором был нарисован макет.

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/points_to_pixels1.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/pixels1.png