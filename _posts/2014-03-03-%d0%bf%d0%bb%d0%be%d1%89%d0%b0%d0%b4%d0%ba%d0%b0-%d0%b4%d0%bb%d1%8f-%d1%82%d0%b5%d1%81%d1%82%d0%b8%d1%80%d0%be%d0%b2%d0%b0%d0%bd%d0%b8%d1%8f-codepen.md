---
title: Площадка для тестирования CodePen
author: gearmobile
layout: post
permalink: /%d0%bf%d0%bb%d0%be%d1%89%d0%b0%d0%b4%d0%ba%d0%b0-%d0%b4%d0%bb%d1%8f-%d1%82%d0%b5%d1%81%d1%82%d0%b8%d1%80%d0%be%d0%b2%d0%b0%d0%bd%d0%b8%d1%8f-codepen/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
categories:
  - Статьи по CSS
tags:
  - codepen
---
Любому веб-мастеру необходима площадка для тестирования. На сегодняшний день таких проектов около десятка. Есть старые проекты, есть молодые; более "навороченные" или менее "навороченные". Каждый из мастеров выбирает себе тот, который ему больше всего нравиться.

Наиболее популярные сервисы такого рода это [CodePen][1] и [jsFiddle][2]. Лично мне больше нравиться jsFiddle, но у него есть один существенный для меня недостаток (*точнее &#8211; их два на самом деле*). В этом сервисе можно выполнить замену CSS на SCSS, но подключить библиотеку Compass &#8211; нельзя. И еще там нет автоматического обновления создаваемого проекта. 

Другой сервис &#8211; CodePen является идеальным инструментом для веб-мастера или верстальщика. В нем есть все, что нужно и ничего лишнего. Может быть, это потому, что проект был создан хорошо известным [Cris Coyier][3]?

Данная статья, возможно, никогда не была бы написана, если не одна причина &#8211; я не знал, как в этом сервисе подключить поддержку SCSS + Compass. Решение лежало на поверхности, достаточно было "остановиться на бегу" &#8211; выделить немного времени на изучение этого проекта.

Ниже привожу подробное и красочное описание работы с CodePen в картинках. Точнее &#8211; это будет описание основных, самых основных или ключевых моментов при написании кода в CodePen.

## Главная страница CodePen

Первое, что необходимо, это конечно же зайти на данный ресурс по адресу [http://codepen.io][4]. Тем, кто первый раз попал сюда, может зарябить в глазах, но это с непривычки:<figure id="attachment_954" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-main-600x337.jpg" alt="Главная страница CodePen" width="600" height="337" class="size-medium wp-image-954" />][5]<figcaption class="wp-caption-text">Главная страница CodePen</figcaption></figure> 

Самое основное на главной странице &#8211; это окна с готовыми работами других веб-мастеров. То есть, люди работали в этом сервисе, написали и протестировали какой-то код; и этот код в готовом виде демонстрируется в различных окошках проекта CodePen. Выборка работ производится в случайном порядке, насколько я понимаю.

Внизу каждого "окошка" с готовой работой показаны *метаданные* &#8211; информация об авторе. К примеру, рассмотрим код, созданный автором по имени Yaroslav. Видим, что веб-мастер экспериментировал с созданием на CSS различных продвинутых типов `background` (*насколько правильно я понял его работу чисто по внешнему виду, исходный код не смотрел*). Комментариев к его работе никто не пожелал оставить, хотя ознакомилось с ним уже 129 человек и семерым из них он даже понравился.

При щелчке мыши на любом из заинтересовавших проектов (*прямо в окошко*) открывается его исходный код, с которым можно детально ознакомиться при желании.

## Настройка CodePen &#8211; начало

В принципе, больше ничего нас в главном окне CodePen не интересует &#8211; ведь нам необходимо самим создавать "нетленные" работы! Для этого сначала нужно зарегистрироваться на CodePen, после чего получаем свой личный кабинет с настройками. Так как первоначально задача стояла в подключении SCSS + Compass в CodePen, то будет решать ее с первых шагов. В правом верхнем углу есть синий значок-аватар, по которому нужно щелкнуть мышью. Раскроется список, в котором необходимо выбрать строку **"Your Settings"**:<figure id="attachment_955" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-settings-600x331.jpg" alt="Доступ к личному профилю на CodePen" width="600" height="331" class="size-medium wp-image-955" />][6]<figcaption class="wp-caption-text">Доступ к личному профилю на CodePen</figcaption></figure> 

Все настройки CodePen уместились на одной странице и это замечательно! Окно разделено на четыре секции &#8211; **Syntax Hightlighting**, **Fonts**, **Key Bindings**, **Preprocessor & Library Defaults**. В принципе, здесь все интуитивно понятно:<figure id="attachment_956" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-profile-settings-600x337.jpg" alt="Настройки CodePen" width="600" height="337" class="size-medium wp-image-956" />][7]<figcaption class="wp-caption-text">Настройки CodePen</figcaption></figure> 

Секция **Syntax Hightlighting** служит для выбора цветовой схемы подсветки синтаксиса с предварительным просмотром. Можно выбрать одну из пяти, но первая (*по умолчанию*) самая лучшая.

Секция **Fonts** помогает выбрать шрифт и размер шрифта. Выбор шрифтов небольшой, но лучше оставить **Monaco** &#8211; он лучше всех смотрится. Размер шрифта можете выбрать, какой вам нравиться.

Секция **Key Bindings** совсем простенькая &#8211; здесь можно выбрать сочетание клавиш при работе в CodePen. **Normal** &#8211; это обычный набор сочетаний клавиш, а **Vim** для тех, кто привык и хорошо себя чувствует в линуксовом (*весьма своеобразном*) редакторе Vim.

Секция **Preprocessor & Library Defaults** самая большая и самая необходимая для нас, ведь ради нее мы и зашли в настройки. В этом разделе можно установить, какие препроцессоры для HTML, CSS и JavaScript будут использоваться в каждом новом проекте, создаваемом в CodePen. В строке **HTML Preprocessor** ничего не делаем, так как препроцессорами для HTML не пользуемся. В строке **CSS Preprocessor** выбираем из списка SCSS, а в следующей строке **CSS Preprocessor Add-on** выбираем библиотеку под SCSS &#8211; **Compass (for Sass)**. Строка **CSS Reset** служит для выбора "CSS-ластика": *CSS Reset* или *Normalize*. Можно также обратить внимание на строчку **Prefix Free?**, в которой есть возможность поставить галочку.<figure id="attachment_958" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-prefix_free-600x358.jpg" alt="JavaScript библиотека Prefix Free" width="600" height="358" class="size-medium wp-image-958" />][8]<figcaption class="wp-caption-text">JavaScript библиотека Prefix Free</figcaption></figure> 

**Prefix Free** &#8211; это JavaScript, созданный для того, чтобы работать с браузерными префиксами на самом современном уровне. Другими словами, этот скрипт фильтрует созданный CSS-код на предмет наличия в нем браузерных (вендорных) префиксов и проверяет, какие из них нужно использовать на сегодняшний день, а от каких уже можно отказаться. Польза **Prefix Free** в очистке CSS-кода от лишнего мусора и увеличение скорости загрузки в браузере.

Но продолжим разбор секции **Preprocessor & Library Defaults**. Три последние строчки относятся к поддержке JavaScript в CodePen. В строке **JS Preprocessor** выбирается препроцессор JavaScript, в строке **JS Library** &#8211; подключаем библиотеку JavaScript, а в строчке **Modernizr?** отмечаем, нужна ли нам встроенная поддержка JavaScript-библиотеки Modernizr.

Последняя строчка **Auto Run?** очень полезна и по умолчанию она включена. Ее задача автоматически обновлять создаваемый проект в окне предпросмотра. Очень удобная функция. К примеру, в jsFiddle этого нет, там нужно самому нажимать кнопку **Run** каждый раз, когда нужно обновить окно предпросмотра после внесения изменений в исходный код.

Вот и все, что можно или нужно сделать в настройках CodePen. Сохраняем изменения, нажав большую зеленую кнопку **Save All Settings** в нижнем правом углу окна.

### Быстрая настройка CSS-препроцессоров в CodePen

Стоит также сказать, чтобы настройки, рассмотренные выше, можно внести в создаваемый проект "на лету". Для этого нужно щелкнуть мышью на значке шестеренки в окне кода CSS. Появиться небольшое окошко с выбором одного из четырех CSS-препроцессоров: SASS, SCSS, LESS, Stylus. Также можно выбрать CSS-ластик: *Normalize*, *Reset* или вообще никакого (*Neither*). Включить библиотеку **Prefix-Free**; подключить внешнюю таблицу стилей CSS или же другой проект, указав в строке **External CSS File or Another Pen** абсолютный путь к этому файлу:<figure id="attachment_959" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-quick_settings-600x325.jpg" alt="Окно быстрых настроек CSS в CodePen" width="600" height="325" class="size-medium wp-image-959" />][9]<figcaption class="wp-caption-text">Окно быстрых настроек CSS в CodePen</figcaption></figure> 

Кнопка **Analyze CSS via CSS Lint** служит для проверки CSS-кода в CodePen на синтаксические ошибки с помощью известного проекта **CSS Lint** (*под редактор Sublime Text также есть подобный плагин*). На рисунке "Основное окно CodePen" внимательный читатель может заметить ошибки, на которые обязательно "заругается" **CSS Lint**. В частности, `font-size: 62,5%` ))<figure id="attachment_960" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-quick_select_preprocessor-600x321.jpg" alt="Выбираем CSS-препроцессор в CodePen" width="600" height="321" class="size-medium wp-image-960" />][10]<figcaption class="wp-caption-text">Выбираем CSS-препроцессор в CodePen</figcaption></figure> 

### Основное окно CodePen

С настройками CodePen разобрались, теперь давайте вкратце рассмотрим основное окно в этом редакторе. Оно разбито на три части для написания кода на HTML, CSS и JavaScript. Внизу расположено окно предварительного просмотра. Не стоит даже упоминать, что можно легко изменить расположение и вид этих окон:<figure id="attachment_961" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-pen-600x427.jpg" alt="Основное окно CodePen" width="600" height="427" class="size-medium wp-image-961" />][11]<figcaption class="wp-caption-text">Основное окно CodePen</figcaption></figure> 

Вверху находятся четыре большие кнопки: **Save**, **Fork**, **Info**, **Share**. Кнопка **Save** &#8211; конечно же для сохранения проекта (Pen). Если имеются несохраненные изменения, то вверху этой кнопки появляется оранжевая полоска, как напоминание о необходимости сохранить изменения. Кстати, забыл упомянуть, что в CodePen проект называется Pen (</em>вот так незатейливо</em>). Кнопка **Fork** &#8211; для создания ответвления (*fork*) проекта. Кнопка **Info** &#8211; внести информацию о создаваемом Pen: *его заголовок, описание и мета-теги*.<figure id="attachment_962" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-info-600x272.jpg" alt="Информация о проекте на CodePen" width="600" height="272" class="size-medium wp-image-962" />][12]<figcaption class="wp-caption-text">Информация о проекте на CodePen</figcaption></figure> 

Кнопка **Share** весьма и весьма полезна. С помощью нее можно поделиться созданным проектом (кодом) с другими людьми. *Собственно, именно для этой цели сервис CodePen и создавался.* Там же можно скачать проект в виде zip-архива или выложить его на GitHub. И даже отправить ссылку в виде SMS на указанный номер телефона!<figure id="attachment_963" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-share-600x272.jpg" alt="Публичная ссылка в CodePen" width="600" height="272" class="size-medium wp-image-963" />][13]<figcaption class="wp-caption-text">Публичная ссылка в CodePen</figcaption></figure> 

На CodePen можно встраивать один проект (Pen) в другой проект (Pen). Более того, созданный Pen можно встраивать в виде готового куска кода в другие проекты (*не обязательно созданные в CodePen*), в том числе и под CMS WordPress. Это уже совсем круто!<figure id="attachment_964" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-embed-600x337.jpg" alt="Встраивание CodePen в другой проект" width="600" height="337" class="size-medium wp-image-964" />][14]<figcaption class="wp-caption-text">Встраивание CodePen в другой проект</figcaption></figure> 

### Работаем с SCSS + Compass в CodePen

Настройку подключения SCSS + Compass в CodePen мы выполнили, осталось посмотреть, реально ли все работает. Да, действительно все нормально! Собственно, сам код SCSS внимательный читатель мог увидеть уже на рисунке "Основное окно CodePen", когда говорилось о трех основных окнах CodePen. Там же можно было заметить, что рядом с надписью CSS появилась еще одна &#8211; (SCSS), что говорит о включенной поддержке SCSS.

На рисунке хорошо видны **переменные SCSS** и **подключения mixin&#8217;ов из библиотеки Compass** для создания радиуса скругления (*border-radius*), линейного градиента (*linear gradient*) и тени блока (*box-shadow*):

<pre>@include border-radius(...)
@include single-box-shadow(...)
@include background-image(...)
</pre>

Двойной щелчок мыши на значке квадратика в правом верхнем углу окна CSS(SCSS) распахивает его на всю ширину окна браузера для большего удобства работы с кодом:<figure id="attachment_965" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-expand_pen-600x234.jpg" alt="Распахиваем окно кода в CodePen" width="600" height="234" class="size-medium wp-image-965" />][15]<figcaption class="wp-caption-text">Распахиваем окно кода в CodePen</figcaption></figure> 

А щелчок мыши на самой надписи CSS переводит окно в **режим компиляции**, то есть перевода SCSS в готовый CSS-код. <figure id="attachment_966" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-scss-600x431.jpg" alt="Создание SCSS-кода в CodePen" width="600" height="431" class="size-medium wp-image-966" />][16]<figcaption class="wp-caption-text">Создание SCSS-кода в CodePen</figcaption></figure> 

### Клавиатурные сокращения CodePen

В заключение можно упомянуть горячие клавиши для работы в CodePen. В принципе, ничего неожиданного в списке сочетания клавиш для CodePen нет, кроме, может быть, единственного &#8211; новый проект (Pen) создается с помощью **Ctrl+P** (а ожидался стандартный Ctrl+N). Также заметно, что сочетания клавиш обозначены под Mac OS X (*это естественно &#8211; у автора проекта рабочий компьютер Mac*). Но это не значит, эти горячие клавиши не будут работать и под Windows:<figure id="attachment_967" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/03/codepen-hotkeyes-600x321.jpg" alt="Список клавиатурных сокращений в CodePen" width="600" height="321" class="size-medium wp-image-967" />][17]<figcaption class="wp-caption-text">Список клавиатурных сокращений в CodePen</figcaption></figure> 

### Заключение

На этом статья о сервисе CodePen завершена. Конечно, можно было бы упомянуть о добавлении проектов Pen в **Коллекции**, о кнопке удаления Pen. Но я оставлю это в качестве "домашнего задания" для тех, кому это нужно. ))

Оцените статью:  
<span id="post-ratings-952" class="post-ratings" data-nonce="d7d215bb0f"><img id="rating_952_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(952, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_952_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(952, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_952_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(952, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_952_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(952, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_952_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(952, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_952_text"></span></span><span id="post-ratings-952-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://codepen.io "CodePen"
 [2]: http://jsfiddle.net/ "jsFiddle"
 [3]: http://css-tricks.com/ "Cris Coyier - CSS-TRICKS"
 [4]: http://codepen.io "Главная страница CodePen"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-main.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-settings.jpg
 [7]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-profile-settings.jpg
 [8]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-prefix_free.jpg
 [9]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-quick_settings.jpg
 [10]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-quick_select_preprocessor.jpg
 [11]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-pen.jpg
 [12]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-info.jpg
 [13]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-share.jpg
 [14]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-embed.jpg
 [15]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-expand_pen.jpg
 [16]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-scss.jpg
 [17]: http://localhost:7788/third/wp-content/uploads/2014/03/codepen-hotkeyes.jpg