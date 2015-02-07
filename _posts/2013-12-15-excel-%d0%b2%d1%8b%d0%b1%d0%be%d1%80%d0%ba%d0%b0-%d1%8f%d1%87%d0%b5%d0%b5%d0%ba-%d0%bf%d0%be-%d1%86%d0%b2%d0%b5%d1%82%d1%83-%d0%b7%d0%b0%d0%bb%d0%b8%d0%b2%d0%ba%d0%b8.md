---
title: 'Excel &#8211; выборка ячеек по цвету заливки'
author: gearmobile
layout: post
permalink: /excel-%d0%b2%d1%8b%d0%b1%d0%be%d1%80%d0%ba%d0%b0-%d1%8f%d1%87%d0%b5%d0%b5%d0%ba-%d0%bf%d0%be-%d1%86%d0%b2%d0%b5%d1%82%d1%83-%d0%b7%d0%b0%d0%bb%d0%b8%d0%b2%d0%ba%d0%b8/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 20
ratings_average:
  - 5
categories:
  - Разное
tags:
  - vba
---
На работе столкнулся с такой задачей &#8211; имеется таблица в Excel, в которой ведется табель выходов рабочих в цеху. В таблице подсчитывается количество часов, фактически отработанных; часов переработки и часов сверх нормы. Так вот, необходимо сделать так, чтобы производилась автоматическая выборка ячеек таблицы по цвету заливки последних. То есть, нужно отобрать все ячейки с заливкой определенного цвета, подсчитать их количество; а затем применить к полученному значению определенные формулы.

Чтобы было понятнее, приведу изображение подобной таблицы. В ней необходимо произвести подсчет ячеек с заливкой зеленого цвета:<figure id="attachment_848" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/12/tabel-600x399.jpg" alt="Табель выходов с зелеными ячейками" width="600" height="399" class="size-medium wp-image-848" />][1]<figcaption class="wp-caption-text">Табель выходов с зелеными ячейками</figcaption></figure> 

В Excel нет встроенных (*готовых*) инструментов для выборки подобного рода; можно отбирать ячейки только по одному условию &#8211; по значению, находящемуся в них. Поэтому решение задачи получалось только одно &#8211; через VBA (*пользовательские функции*).

Прекрасное и готовое решение моей задачи я нашел на сайте http://www.excel-vba.ru/. Даже не одно, а целых два решения, под разные условия. Ниже привожу последовательность шагов, которые привели меня к успеху )) Сразу скажу, что изображения были сделаны в Excel 2007. В Excel 2010 все несколько по другому, но запутаться невозможно, если что.

### Режим &#8220;Разработчик&#8221; в Excel

Первое, что нужно сделать &#8211; заставить Excel работать с пользовательскими функциями. Фактически, мы будем писать сценарий на языке VBA в Excel, но такая возможность по умолчанию отключена в этой программе. Включить ее можно следующим образом.

Переходим в "Пуск" &#8211; "Параметры Excel" и находим в левом списке пункт "Надстройки":<figure id="attachment_849" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/12/excel-надстройка-vba-600x464.jpg" alt="Excel - надстройка VBA" width="600" height="464" class="size-medium wp-image-849" />][2]<figcaption class="wp-caption-text">Excel &#8211; надстройка VBA</figcaption></figure> 

Выбираем в основном окне строчку "Пакет анализа &#8211; VBA" и жмем кнопочку "Перейти" в самом низу окна. Откроется еще одно окошко со списком доступных под Excel расширений (*надстроек*). Снова выбираем в этом списке "Пакет анализа &#8211; VBA" и соглашаемся, что хотим установить его, нажав кнопку "ОК":<figure id="attachment_850" style="width: 365px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/12/excel-пакет-анализа-vba.jpg" alt="Excel - Пакет анализа VBA" width="365" height="372" class="size-full wp-image-850" />][3]<figcaption class="wp-caption-text">Excel &#8211; Пакет анализа VBA</figcaption></figure> 

Потребуется установочный диск с Microsoft Office на нем (*или же подключение к Интернет*) чтобы программа получила необходимые пакеты для инсталляции. Если установка прошла успешно, то в "Ленте" появиться пункт "Разработчик" (Excel 2010). Можно перейти в него через эту панель или же с помощью сочетания клавиш Alt + F11.

Появиться окно, в котором выполняется написание кода на языке VBA, то есть фактически создаются пользовательские функции. Я писать их не буду, так как языка VBA не знаю и знать особого желания нет (*все знать невозможно*).

### Вставка готовых функций в Excel VBA

Но есть готовые решения, которые я вставлю в виде кода с помощью меню "Insert" &#8211; "Module". Просто берем отсюда код функций и вставляем в свой Excel. Затем сохраняем файл Excel с поддержкой VBA (*макросов*) и все готово для дальнейшей работы.

Вставленные функции появятся в списке формул таблицы:<figure id="attachment_851" style="width: 423px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/12/excel-пользовательские-функции.jpg" alt="Excel - пользовательские функции" width="423" height="369" class="size-full wp-image-851" />][4]<figcaption class="wp-caption-text">Excel &#8211; пользовательские функции</figcaption></figure> 

Ниже представлен готовый код двух функций на VBA, написанных их автором Дмитрием Щербаковым. Первая функция с именем **CountByInteriorColor** выполняет *подсчет количества ячеек по цвету заливки*. Вторая функция с именем **SumByInteriorColor** выполняет *выборку ячеек по цвету заливки и суммирует все значения в этих ячейках*.

Обе функции имеют одинаковый синтаксис и принимают **три входных аргумента**, первые два из которых **обязательные**, а третий &#8211; **необязательный**:

  * **rRange** &#8211; диапазон с ячейками для подсчета;
  * **rColorCell** &#8211; ячейка-образец с цветом заливки;
  * **bSumHide** &#8211; ИСТИНА или 1 учитывает скрытые ячейки; ЛОЖЬ, 0 или опущен(по умолчанию) &#8211; скрытые ячейки не подсчитываются.

#### Функция подсчета количества ячеек

<pre>'---------------------------------------------------------------------------------------
  ' Procedure : CountByInteriorColor
  ' Author    : The_Prist(Щербаков Дмитрий)
  '             http://www.excel-vba.ru
  ' Purpose   : Функция подсчета ячеек на основе цвета заливки.
  ' Аргументы:
  '             rRange     - диапазон с ячейками для подсчета.
  '             rColorCell - ячейка-образец с цветом заливки.
  '             bSumHide   - ИСТИНА или 1 учитывает скрытые ячейки.
  '                          ЛОЖЬ, 0 или опущен(по умолчанию) - скрытые ячейки не подсчитываются.
  '---------------------------------------------------------------------------------------
  Function CountByInteriorColor(rRange As Range, rColorCell As Range, Optional bSumHide As Boolean = False)
      Dim lColor As Long, rCell As Range, lCnt As Long, vVal
      lColor = rColorCell.Interior.Color
      For Each rCell In rRange
          If rCell.Interior.Color = lColor Then
              If rCell.EntireRow.Hidden Or rCell.EntireColumn.Hidden Then
                  If bSumHide Then lCnt = lCnt + 1
              Else
                  lCnt = lCnt + 1
              End If
          End If
      Next rCell
      CountByInteriorColor = lCnt
  End Function
</pre>

Синтаксис этой функции прост:

<pre>=CountByInteriorColor(D8:AG8;$E$65)
</pre>

#### Функция подсчета суммы ячеек

<pre>'---------------------------------------------------------------------------------------
  ' Procedure : SumByInteriorColor
  ' Author    : The_Prist(Щербаков Дмитрий)
  '             http://www.excel-vba.ru
  ' Purpose   : Функция суммирования ячеек на основе цвета заливки.
  ' Аргументы:
  '             rRange     - диапазон с ячейками для суммирования.
  '             rColorCell - ячейка-образец с цветом заливки.
  '             bSumHide   - ИСТИНА или 1 учитывает скрытые ячейки.
  '                          ЛОЖЬ, 0 или опущен(по умолчанию) - скрытые ячейки не суммируются.
  '---------------------------------------------------------------------------------------
  Function SumByInteriorColor(rRange As Range, rColorCell As Range, Optional bSumHide As Boolean = False)
      Dim lColor As Long, rCell As Range, dblSum As Double, vVal
      lColor = rColorCell.Interior.Color
      For Each rCell In rRange
          If rCell.Interior.Color = lColor Then
              vVal = rCell.Value
              If IsNumeric(vVal) Then
                  If rCell.EntireRow.Hidden Or rCell.EntireColumn.Hidden Then
                      If bSumHide Then dblSum = dblSum + vVal
                  Else
                      dblSum = dblSum + vVal
                  End If
              End If
          End If
      Next rCell
      SumByInteriorColor = dblSum
  End Function
</pre>

Синтаксис этой функции следующий:

<pre>=SumByInteriorColor(D8:AG37;E63)
</pre>

При вставке пользовательской функции **CountByInteriorColor** и **SumByInteriorColor** можно воспользоваться либо "Мастером функций", либо произвести указание диапазона ячеек и ячейку-критерий **вручную**.

### Описание рабочей формулы

Готовый пример работы функции **CountByInteriorColor** можно посмотреть на рисунке "Табель выходов с зелеными ячейками". В нем подсчет отработанного времени производится по следующей формуле:

<pre>=((Сумма фактически отработанных часов) - (Норма часов выхода за месяц)) + ((Кол-во дней с переработкой)*4)
</pre>

Фактически эта формула получается такой (*смотри строку №13 на рисунке*):

<pre>=(AH13-AI13) + (CountByInteriorColor(D13:AG13;$E$65)*4)  
</pre>

Думаю, что больше сказать по поводу создания (*точнее &#8211; вставки готового решения*) пользовательских функций и способа выборки ячеек в таблице по цвету их заливки мне нечего.

Оцените статью:  
<span id="post-ratings-846" class="post-ratings" data-nonce="98fa8dff70"><img id="rating_846_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(846, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_846_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(846, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_846_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(846, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_846_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(846, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_846_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(846, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_846_text"></span></span><span id="post-ratings-846-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/12/tabel.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/12/excel-надстройка-vba.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/12/excel-пакет-анализа-vba.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2013/12/excel-пользовательские-функции.jpg