---
layout: post
title: "Excel - выборка ячеек по цвету заливки"
author: gearmobile
tags: [vba, excel, cell]
---

На работе столкнулся с такой задачей - имеется таблица в Excel, в которой ведется табель выходов рабочих в цеху. В таблице подсчитывается количество часов, фактически отработанных; часов переработки и часов сверх нормы. Так вот, необходимо сделать так, чтобы производилась автоматическая выборка ячеек таблицы по цвету заливки последних. То есть, нужно отобрать все ячейки с заливкой определенного цвета, подсчитать их количество; а затем применить к полученному значению определенные формулы.

Чтобы было понятнее, приведу изображение подобной таблицы. В ней необходимо произвести подсчет ячеек с заливкой зеленого цвета:

<figure id="attachment_848" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/12/tabel-600x399.jpg" alt="Табель выходов с зелеными ячейками" width="600" height="399" class="size-medium wp-image-848" />][1]
  <figcaption class="wp-caption-text">Табель выходов с зелеными ячейками</figcaption>
</figure>

В Excel нет встроенных (*готовых*) инструментов для выборки подобного рода; можно отбирать ячейки только по одному условию - по значению, находящемуся в них. Поэтому решение задачи получалось только одно - через VBA (*пользовательские функции*).

Прекрасное и готовое решение моей задачи я нашел на сайте http://www.excel-vba.ru/. Даже не одно, а целых два решения, под разные условия. Ниже привожу последовательность шагов, которые привели меня к успеху )) Сразу скажу, что изображения были сделаны в Excel 2007. В Excel 2010 все несколько по другому, но запутаться невозможно, если что.

### Режим "Разработчик" в Excel

Первое, что нужно сделать - заставить Excel работать с пользовательскими функциями. Фактически, мы будем писать сценарий на языке VBA в Excel, но такая возможность по умолчанию отключена в этой программе. Включить ее можно следующим образом.

Переходим в "Пуск" - "Параметры Excel" и находим в левом списке пункт "Надстройки":

<figure id="attachment_849" style="width: 600px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/12/excel-надстройка-vba-600x464.jpg" alt="Excel - надстройка VBA" width="600" height="464" class="size-medium wp-image-849" />][2]
  <figcaption class="wp-caption-text">Excel - надстройка VBA</figcaption>
</figure>

Выбираем в основном окне строчку "Пакет анализа - VBA" и жмем кнопочку "Перейти" в самом низу окна. Откроется еще одно окошко со списком доступных под Excel расширений (*надстроек*). Снова выбираем в этом списке "Пакет анализа - VBA" и соглашаемся, что хотим установить его, нажав кнопку "ОК":

<figure id="attachment_850" style="width: 365px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/12/excel-пакет-анализа-vba.jpg" alt="Excel - Пакет анализа VBA" width="365" height="372" class="size-full wp-image-850" />][3]
  <figcaption class="wp-caption-text">Excel - Пакет анализа VBA</figcaption>
</figure>

Потребуется установочный диск с Microsoft Office на нем (*или же подключение к Интернет*) чтобы программа получила необходимые пакеты для инсталляции. Если установка прошла успешно, то в "Ленте" появиться пункт "Разработчик" (Excel 2010). Можно перейти в него через эту панель или же с помощью сочетания клавиш <kbd>Alt + F11</kbd>.

Появиться окно, в котором выполняется написание кода на языке VBA, то есть фактически создаются пользовательские функции. Я писать их не буду, так как языка VBA не знаю и знать особого желания нет (*все знать невозможно*).

### Вставка готовых функций в Excel VBA

Но есть готовые решения, которые я вставлю в виде кода с помощью меню "Insert" - "Module". Просто берем отсюда код функций и вставляем в свой Excel. Затем сохраняем файл Excel с поддержкой VBA (*макросов*) и все готово для дальнейшей работы.

Вставленные функции появятся в списке формул таблицы:

<figure id="attachment_851" style="width: 423px;" class="wp-caption aligncenter">
  [<img src="http://localhost:7788/third/wp-content/uploads/2013/12/excel-пользовательские-функции.jpg" alt="Excel - пользовательские функции" width="423" height="369" class="size-full wp-image-851" />][4]
  <figcaption class="wp-caption-text">Excel - пользовательские функции</figcaption>
</figure>

Ниже представлен готовый код двух функций на VBA, написанных их автором Дмитрием Щербаковым. Первая функция с именем **CountByInteriorColor** выполняет *подсчет количества ячеек по цвету заливки*. Вторая функция с именем **SumByInteriorColor** выполняет *выборку ячеек по цвету заливки и суммирует все значения в этих ячейках*.

Обе функции имеют одинаковый синтаксис и принимают **три входных аргумента**, первые два из которых **обязательные**, а третий - **необязательный**:

  * **rRange** - диапазон с ячейками для подсчета;
  * **rColorCell** - ячейка-образец с цветом заливки;
  * **bSumHide** - ИСТИНА или 1 учитывает скрытые ячейки; ЛОЖЬ, 0 или опущен(по умолчанию) - скрытые ячейки не подсчитываются.

#### Функция подсчета количества ячеек

{% highlight vba %}
'---------------------------------------------------------------------------------------
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
{% endhighlight %}

Синтаксис этой функции прост:

{% highlight vba %}
=CountByInteriorColor(D8:AG8;$E$65)
{% endhighlight %}

#### Функция подсчета суммы ячеек

{% highlight vba %}
'---------------------------------------------------------------------------------------
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
{% endhighlight %}

Синтаксис этой функции следующий:

{% highlight vba %}
=SumByInteriorColor(D8:AG37;E63)
{% endhighlight %}

При вставке пользовательской функции **CountByInteriorColor** и **SumByInteriorColor** можно воспользоваться либо "Мастером функций", либо произвести указание диапазона ячеек и ячейку-критерий **вручную**.

### Описание рабочей формулы

Готовый пример работы функции **CountByInteriorColor** можно посмотреть на рисунке "Табель выходов с зелеными ячейками". В нем подсчет отработанного времени производится по следующей формуле:

{% highlight vba %}
=((Сумма фактически отработанных часов) - (Норма часов выхода за месяц)) + ((Кол-во дней с переработкой)*4)
{% endhighlight %}

Фактически эта формула получается такой (*смотри строку №13 на рисунке*):

{% highlight vba %}
=(AH13-AI13) + (CountByInteriorColor(D13:AG13;$E$65)*4)  
{% endhighlight %}

Думаю, что больше сказать по поводу создания (*точнее - вставки готового решения*) пользовательских функций и способа выборки ячеек в таблице по цвету их заливки мне нечего.

 [1]: http://localhost:7788/third/wp-content/uploads/2013/12/tabel.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/12/excel-надстройка-vba.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/12/excel-пакет-анализа-vba.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2013/12/excel-пользовательские-функции.jpg