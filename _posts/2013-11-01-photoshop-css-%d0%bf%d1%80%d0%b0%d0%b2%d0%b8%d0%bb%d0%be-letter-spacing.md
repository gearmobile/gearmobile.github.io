---
title: 'Photoshop &#8211; CSS-правило letter-spacing'
author: gearmobile
layout: post
permalink: /photoshop-css-%d0%bf%d1%80%d0%b0%d0%b2%d0%b8%d0%bb%d0%be-letter-spacing/
ratings_users:
  - 13
ratings_score:
  - 59
ratings_average:
  - 4.54
cleanretina_sidebarlayout:
  - default
categories:
  - Photoshop для кодера
tags:
  - letter-spacing
---
Наконец-то у меня дошли руки и пришло время разобраться с палитрой &#8220;Символ&#8221; в Photoshop. До сегодняшнего дня о ней знал не полностью. Конечно, с такими полями, как &#8220;Шрифт&#8221;, &#8220;Размер шрифта&#8221;, &#8220;Цвет шрифта&#8221;, &#8220;Межстрочное расстояние&#8221; я был знаком. Но вот столкнулся в одном из psd-макетов с неизвестным мне полем. Предположительно, оно должно было означать расстояние между буквами строки. То самое, за которое в CSS отвечает правило letter-spacing.

Еще более загадочным для меня было значение этого поля: -25. То, что знак минуса означает &#8220;ужать&#8221; слова в строке, можно было догадаться. Но вот что за единицы измерения применяет Photoshop в данном случае? Как мне перевести это значение в CSS? В каких единицах &#8211; пикселях или em?

Ответы на эти вопросы в русскоязычной части Интернета я не нашел. Не спорю, может и плохо искал. Но обнаружил их в англоязычной части. Вольный пересказ одной замечательной статьи (http://www.justinmarsan.com/blog/researches/2012/01/07/css-letter-spacing/), посвященной этому вопросу, я привожу в данном небольшом обзоре.

Итак, есть psd-макет, на котором для шрифтов применено загадочное значение -25 в таком же, не менее загадочном, поле:<figure id="attachment_26" style="width: 236px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/letter-spacing_photoshop.png" alt="Letter-spacing в Photoshop" width="236" height="245" class="size-full wp-image-26" />][1]<figcaption class="wp-caption-text">Letter-spacing в Photoshop</figcaption></figure> 

Смотрим внимательно на панельку &#8220;Символ&#8221;. Здесь собраны воедино все свойства, отвечающие за прорисовку шрифта на макете.

Верхние два поля &#8211; &#8220;Georgia&#8221; и &#8220;Regular&#8221;. Здесь все просто и понятно &#8211; семейство шрифта и его начертание. В CSS данные значения оформляются через правила font-family и font-weight.

Второй ряд из двух полей, со значениями 22px и 24px. Думаю, здесь также не должно возникнуть вопросов. 22px &#8211; размер шрифта, 24px &#8211; интерлиньяж, межстрочное расстояние. За первое свойство в CSS отвечает правило font-size, за второе &#8211; line-height.

Перехожу к третьему ряду. Первое поле в нем &#8211; насколько я могу судить &#8211; предназначено для единиц измерения, в которых будет производиться изменение межбуквенного расстояния. Второе поле, как вы уже могли догадаться, это межбуквенное расстояние. В CSS имеется аналогичное правило, которое называется letter-spacing. Не стоит путать его с очень похожим правилом word-spacing. Разница между ними очевидна, хотя сфера применения одинакова &#8211; строка текста. Word-spacing задает расстояние между словами, а letter-spacing &#8211; расстояние между буквами.

Вернемся к нашим баранам. ) Видно, что в поле стоит значение -25. О том, как перевести его в CSS, расскажу немного позже. А пока кратко пробежимся по остальным строкам палитры &#8220;Символ&#8221;.

В четвертом ряду располагаются два поля, назначение которых в оригинале пишется так: &#8220;Vertical scalar tool&#8221; и &#8220;Horizontal scalar tool&#8221;. Можно догадаться, что с помощью этих настроек можно масштабировать (растягивать или сжимать) буквы как по-вертикали, так и по-горизонтали.

В последнем (пятом) ряду находится поле изменения расстояния для индексов, и поле цвета шрифта (букв).

Вот, в принципе, и все описание. Краткое &#8211; но к чему растягивать его? Полное описание с картинками, полезное для себя, нашел в этой статье (http://www.adobetutorialz.com/articles/705/1/Text-tools-in-Adobe-Photoshop).

Перейду к вопросу, который остался открыт &#8211; как преобразовать значение letter-spacing в Photoshop в аналогичное правило CSS?

Что за единицы измерения использует Photoshop в данном случае, честно сказать, не знаю. Какие-то загадочные, свои собственные, наверное. Но это и не интересно, если что. Нужно лишь перевести их в одну из двух наиболее популярных единиц измерения CSS &#8211; px или em.

Перевод осуществляется с помощью формул. Эти формулы были выведены опытным путем автором статьи &#8211; Justin Marsan. На своей собственной практике я пару раз проверил их и пришел к выводу, что они верны.

Формула перевода значения letter-spacing Photoshop в em:

<pre>X / 1000</pre>

где X &#8211; это значение letter-spacing в Photoshop. В конкретном случае оно будет равно: `-25 / 1000 = -0.025em`

Формула перевода значения letter-spacing Photoshop в пиксели (px):

<pre>X * Y / 1000</pre>

где X &#8211; это значение letter-spacing в Photoshop, Y &#8211; размер шрифта там же. То есть, сначала значение межбуквенного расстояния умножается на размер шрифта, а затем полученное значение делиться на 1000. В конкретном случае формула и результат будет следующим: `-25 * 22 / 1000 = -0.55px`.

На этом, думаю, что все сказано.

Оцените статью:  
<span id="post-ratings-23" class="post-ratings" data-nonce="804311a228"><img id="rating_23_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(23, 1, '1 Star');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_23_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(23, 2, '2 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_23_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(23, 3, '3 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_23_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(23, 4, '4 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_23_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(23, 5, '5 Stars');" onmouseout="ratings_off(4.5, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>13</strong> votes, average: <strong>4,54</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_23_text"></span></span><span id="post-ratings-23-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/letter-spacing_photoshop.png