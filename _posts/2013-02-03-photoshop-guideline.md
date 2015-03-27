---
title: "Photoshop - точное позиционирование направляющей"
layout: post
categories: photoshop
description: ""
excerpt: ""
tags: [guideline, photoshop]
---

> Иногда бывает необходимо задать точное расположение направляющей на макете в программе Photoshop.

Позиционировать ее с помощью мыши неблагодарное занятие. Это практически невозможно сделать. Да и зачем? В Photoshop есть для этого случая способ, предназначенный именно для этой цели.

## Задачу можно выполнить двумя способами.

**Первый способ** - с помощью меню. Для переходим в меню "View - New Guide Line". Появится небольшое плавающее окно, в котором можно выбрать расположение ("Orientation") создаваемой направляющей - горизонтальное или вертикальное.

И задать расстояние в пикселах ("Position"):

![Photoshop New Guideline]({{site.url}}/images/uploads/2013/02/photoshop-new_guideline.png)

Нажимаем ОК и видим результат:

![New Guideline Result]({{site.url}}/images/uploads/2013/02/newguideline_result.jpg)

**Второй способ** - не такой точный. В настройках Photoshop, относящихся к сетке, направляющим и слайсам ("Edit - Preferences - Guides, Grid & Slices") нужно установить шаг сетки в пикселах ("Gridline Every"):

![Guideline Preferencies]({{site.url}}/images/uploads/2013/02/guideline_pref.png)

Затем выполнить привязку направляющей к сетке ("View - Snap To"):

![Snap To Guideline]({{site.url}}/images/uploads/2013/02/snap_to_guideline.png)

И теперь можно с большей (*или меньшей*) точностью выставлять направляющие guidelines:

![Snap To Grid]({{site.url}}/images/uploads/2013/02/snap_to_grid.png)

На этом все.

---
