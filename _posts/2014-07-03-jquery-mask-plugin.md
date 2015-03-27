---
title: Плагин jQuery Mask Plugin
author: gearmobile
excerpt: Краткий обзор плагина jQuery Mask Plugin, упоминание о котором я нашел на Google+. Этот плагин понравился мне простотой установки и настройки. Работа плагина jQuery Mask Plugin заключается в том, чтобы форматировать вводимые пользователем в полях данных и приводить их к виду, заданному соответствующей маской в коде. Помимо этого, плагин jQuery Mask Plugin производит фильтрацию данных и не позволяет пользователю вводить недопустимое количество данных и данных другого формата.
layout: post
permalink: /jquery-mask-plugin/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 14
ratings_score:
  - 57
ratings_average:
  - 4.07
categories:
  - 'Javascript &amp; jQuery'
tags:
  - jquery
  - jquery mask
---
Краткий обзор плагина jQuery Mask Plugin, упоминание о котором я нашел на Google+. Этот плагин понравился мне простотой установки и настройки. Работа плагина jQuery Mask Plugin заключается в том, чтобы форматировать вводимые пользователем в полях данных и приводить их к виду, заданному соответствующей маской в коде. Помимо этого, плагин jQuery Mask Plugin производит фильтрацию данных и не позволяет пользователю вводить недопустимое количество данных и данных другого формата.

В общем, весьма полезный и удобный плагин, который можно положить в копилку веб-разработчика &#8220;на всякий случай&#8221;. Наверняка такой может пригодиться при случае. Поэтому приступаю к установке и настройке плагина jQuery Mask Plugin.

### Подключение jQuery Mask Plugin

Плагин jQuery Mask Plugin &#8220;живет&#8221; по этому адресу &#8211; [jQuery Mask Plugin][1], где дано подробное описание работы этого скрипта. На этой странице дано краткое описание установки и настройки плагина &#8220;от автора&#8221; Igor Escobar &#8211; [Masks With Jquery Mask Plugin][2].

Подключение скрипта в рабочем проекте производится стандартно для всех плагинов, созданных под библиотеку jQuery. Сначала производится подключение самой библиотеки jQuery, а затем скрипта jQuery Mask Plugin:

<pre></pre>

Плагин совместим со всеми версиями библиотеки jQuery. Более того, в архиве с исходниками находятся тестовые HTML-странички, с помощью которых можно проверить все возможности работы скрипта под конкретную библиотеку jQuery, конкретный браузер и конкретную ОС:<figure id="attachment_1434" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/jquerymask_test-600x450.jpg" alt="Тестовые страницы для плагина jQuery Mask Plugin" width="600" height="450" class="size-medium wp-image-1434" />][3]<figcaption class="wp-caption-text">Тестовые страницы для плагина jQuery Mask Plugin</figcaption></figure> 

### Создание разметки под jQuery Mask Plugin

Для примера работы с плагином jQuery Mask Plugin создаю тестовую разметку с несколькими полями ввода:

<pre><div class="wrapper">
  <h1>
    jQuery Mask Plugin
  </h1>
  
      
  
    
</div>
  </pre>

Как видно из примера выше, каждое поле предназначено для ввода определенной информации пользователем, будь то дата, время, проценты, номер телефона или денежная сумма. В принципе, больше ничего сказать по поводу HTML нечего. Самое интересное будет в настройке скрипта.

Расширенный пример с возможными вариантами масок можно посмотреть на странице примера &#8211; [Basic Usage Examples][4]. На ней также показаны примеры расширенной настройки плагина jQuery Mask Plugin.

### Инициализация плагина jQuery Mask Plugin

Создаю еще один js-файл, в котором будет производиться инициализация скрипта и заданы маски для каждого из полей ввода. Файл будет иметь произвольное имя `masks.js` и в нем будет такое содержимое:

<pre>$(document).ready(function(){
    $('.date').mask('00/00/0000');
    $('.time').mask('00:00:00');
    $('.percent').mask('##0,00%');
    $('.money').mask('000.000.000.000.000,00');
    $('.phone').mask('0(000)-000-00-00');
  });
  </pre>

Видно, что из DOM-модели производится выборка элементов с указанными классами, к которым применяется функция `mask` с указанием в каждом конкретном случае маски. Ничего сложного в представленных масках нет, достаточно внимательно их изучить.

Открываю в браузере созданный мною HTML-файл и вижу форму с полями ввода:<figure id="attachment_1436" style="width: 589px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/jquerymask-589x600.jpg" alt="Форма ввода с плагином jQuery Mask Plugin" width="589" height="600" class="size-medium wp-image-1436" />][5]<figcaption class="wp-caption-text">Форма ввода с плагином jQuery Mask Plugin</figcaption></figure> 

### Тестирование плагина jQuery Mask Plugin

Давайте попробуем ввести в созданные на примере поля данные. При вводе в каждом из полей хорошо видно, как данные приводятся именно к тому виду, который задан маской в js-коде. Более того, плагин не позволит ввести данные другого формата, то есть будет производиться фильтрация данных:<figure id="attachment_1437" style="width: 589px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/07/jquerymask_result-589x600.jpg" alt="Результат работы плагина jQuery Mask Plugin" width="589" height="600" class="size-medium wp-image-1437" />][6]<figcaption class="wp-caption-text">Результат работы плагина jQuery Mask Plugin</figcaption></figure> 

В поле ввода номера телефона маска создана мною произвольно, буквально на лету. Этот факт говорит о том, что создание масок в плагине jQuery Mask Plugin &#8211; дело очень простое и легкое.

На этом обзор плагина jQuery Mask Plugin можно завершить.

Оцените статью:  
<span id="post-ratings-1431" class="post-ratings" data-nonce="e52468e6b9"><img id="rating_1431_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1431, 1, '1 Star');" onmouseout="ratings_off(4.1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1431_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1431, 2, '2 Stars');" onmouseout="ratings_off(4.1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1431_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1431, 3, '3 Stars');" onmouseout="ratings_off(4.1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1431_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1431, 4, '4 Stars');" onmouseout="ratings_off(4.1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1431_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1431, 5, '5 Stars');" onmouseout="ratings_off(4.1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>14</strong> votes, average: <strong>4,07</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1431_text"></span></span><span id="post-ratings-1431-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://igorescobar.github.io/jQuery-Mask-Plugin/ "jQuery Mask Plugin"
 [2]: http://www.igorescobar.com/blog/2012/05/06/masks-with-jquery-mask-plugin/ "Masks With Jquery Mask Plugin"
 [3]: http://localhost:7788/third/wp-content/uploads/2014/07/jquerymask_test.jpg
 [4]: http://igorescobar.github.io/jQuery-Mask-Plugin/ "Basic Usage Examples"
 [5]: http://localhost:7788/third/wp-content/uploads/2014/07/jquerymask.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2014/07/jquerymask_result.jpg