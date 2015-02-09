---
title: О пользе анализа psd-макета
author: gearmobile
excerpt: Краткая статья о пользе предварительного анализа psd-макета, прежде чем приступать к верстке. Анализ ошибок дизайнера при создании psd-макета в Photoshop.
layout: post
permalink: /analize-psd-mockup/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 15
ratings_average:
  - 3.75
categories:
  - Photoshop для кодера
tags:
  - psd
  - ошибка дизайнера
---
Совсем короткий пост. Думал даже, нужно ли его публиковать вообще? Но потом решил, что раз уже &ldquo;накропал&rdquo; статью, то стоит ее разместить на своем бложике. Написал ее на &ldquo;едином дыхании&rdquo;, так как на том момент &ldquo;наболело&rdquo;. Смысл статьи заключается в том, что **нужно внимательно анализировать** psd-макет, прежде чем приступать к его верстке.

Так вот, мною был взят &ldquo;premium&rdquo;-макет из одного из видеокурсов по верстке (*не буду говорить, какой &#8211; это неважно*). Открыл его, посмотрел и впечатлился &#8211; красивый такой макет! Да и автор курса его нахваливал. Это потом стало ясно, что в данном случае psd-макет не мог быть реально хорошим, **по определению**.

Начал я верстать этот макет, с обязательным применением Susy (*кстати, я взялся сделать посильный русский перевод книги &#8211; [Learning Susy][1] автора Zell Liew*), ибо даже при первоначальном открытии макета на нем осталась сетка из guidelines, по которой дизайнер рисовал макет. *Капитан Очевидность* говорил о том, что данный макет нужно верстать по сетке.

Ну я и начал делать верстку на Susy, радостно потирая ручки от предвкушения, что вот сейчас сверстаю такой красивый шаблон! Но когда дошел до контентной части, то верстка у меня почему-то &ldquo;расползлась&rdquo;. Три колонки не вписывались по ширине в блок-родитель и последняя из них выпадала вниз. Сначала решил, что это я сделал что-то не так.

Немного поостыл и решил внимательно разобраться, в чем дело. И &hellip; е-мое! Вы только посмотрите на это &ldquo;чудо&rdquo; дизайнерской мысли!

Макет **вписан точно** в 960px! Не в 940px, как это можно было ожидать, а именно в 960px!<figure id="attachment_1820" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/full_width-600x436.png" alt="Ширина psd-макета на всю сетку" width="600" height="436" class="size-medium wp-image-1820" />][2]<figcaption class="wp-caption-text">Ширина psd-макета на всю сетку</figcaption></figure> <figure id="attachment_1822" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/left_side-600x448.png" alt="Левый край psd-макета" width="600" height="448" class="size-medium wp-image-1822" />][3]<figcaption class="wp-caption-text">Левый край psd-макета</figcaption></figure> <figure id="attachment_1823" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/right_side-600x565.png" alt="Правый край psd-макета" width="600" height="565" class="size-medium wp-image-1823" />][4]<figcaption class="wp-caption-text">Правый край psd-макета</figcaption></figure> 

Ну ладно, можно поправить ширину навигации и слайдера силами CSS, чтобы вписать ширину обоих в 940px. Но это было бы еще пол-беды! Ведь, если на главной странице сетка еще выдержана, то на остальных страницах &#8211; просто тихий ужас:<figure id="attachment_1824" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/width_of_columns-600x316.png" alt="Неравная ширина колонок psd-макета" width="600" height="316" class="size-medium wp-image-1824" />][5]<figcaption class="wp-caption-text">Неравная ширина колонок psd-макета</figcaption></figure> 

Более того, абсолютно непонятно, зачем этому &ldquo;дизайнеру&rdquo; сетка вообще понадобилась в данном случае:<figure id="attachment_1825" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/shift_content-600x272.png" alt="Смещение контента внутри psd-макета" width="600" height="272" class="size-medium wp-image-1825" />][6]<figcaption class="wp-caption-text">Смещение контента внутри psd-макета</figcaption></figure> 

Чтобы макет &ldquo;профессионально&rdquo; выглядел?

Становится ясно, что изначально этот макет делался (*и должен был делаться*) по сетке. Но дизайнер &ldquo;закосячил&rdquo; с самого начала. Или не знал о предназначении сетки вообще?

### Вывод

Такой макет нужно или отсылать на доработку; или верстать на &ldquo;ванильном&rdquo; CSS, без использования любой из grid system.

**Мораль сей басни такова**: нужно **внимательно анализировать макет** перед тем, как приступать к верстке. Чтобы не потерять время даром (*а время &#8211; деньги, как хорошо известно*).

Оцените статью:  
<span id="post-ratings-1818" class="post-ratings" data-nonce="e6ae508859"><img id="rating_1818_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1818, 1, '1 Star');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1818_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1818, 2, '2 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1818_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1818, 3, '3 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1818_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1818, 4, '4 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1818_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1818, 5, '5 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>3,75</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1818_text"></span></span><span id="post-ratings-1818-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://zell-weekeat.com/learnsusy/ "Learning Susy"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/09/full_width.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/09/left_side.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/09/right_side.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/09/width_of_columns.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/09/shift_content.png