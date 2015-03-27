---
title: Плагин LoremIpsum в Notepad++
author: gearmobile
layout: post
permalink: /%d0%bf%d0%bb%d0%b0%d0%b3%d0%b8%d0%bd-loremipsum-%d0%b2-notepad/
ratings_users:
  - 2
ratings_score:
  - 6
ratings_average:
  - 3
cleanretina_sidebarlayout:
  - default
categories:
  - Web Tools
tags:
  - loremipsum
---
При версте сайта из макета одним из часто повторяющихся действий является наполнение содержимого так называемой &#8220;рыбой&#8221;. Что такое &#8220;рыба&#8221;? Это ничего не значащий текст, единственная роль которого состоит в качестве наполнителя текстом тех областей, в которых в последствии предполагается располагать осмысленный контент. В процессе верстки такого текста у верстальщика естественно нет такого контента. Но он ему и не нужен. Для него главное создать полную копию макета и заполнить каким-либо текстом.

На практике каждый поступает при наполнении &#8220;рыбой&#8221;, исходя из своих предпочтений. Кто-то пользуется статьями из Википедии, кто-то берет любые тексты из рефератов Яндекса. Помимо двух указанных источников, существует так называемая классическая &#8220;рыба&#8221;. Это текст на латинском языке, начинающийся со слов &#8220;Lorem ipsum dolor sit amet&#8230;&#8221;.  
На самом деле этот текст, хоть и является латинским, также не несет в себе особого смысла, так как представляет их себя очень сильно искаженную выдержку из произведения какого-то древнеримского автора.

В Интернете имеется достаточное количество сайтов, являющихся генераторами подобного текста. К примеру, популярный сайт Lipsum.com.  
Однако, для распространенного блокнота программистов Notepad++ имеется плагин, который также является генератором Lorem ipsum. Название плагина именно такое &#8211; Lorem Ipsum. Устанавливается плагин через менеджер плагинов Plugin Manager. После установки плагин прописывается в меню &#8220;Плагины &#8211; InsertLoremIpsum &#8211; View Insert Dialog&#8221;. При его активации открывается диалоговое окно в правой части:<figure id="attachment_691" style="width: 486px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum.png" alt="Плагин LoremIpsum в Notepad++" width="486" height="540" class="size-full wp-image-691" />][1]<figcaption class="wp-caption-text">Плагин LoremIpsum в Notepad++</figcaption></figure> 

Управление LoremIpsum минималистичное, но что называется &#8211; все по делу.

В верхнем окошке устанавливается число (по умолчанию оно равно 5), являющееся счетчиком слов, предложений или параграфов, которые будут вставлены в тело кода.

Следующие за ним три строки:</p> 

  * words (слова)
  * sentences (предложения)
  * paragraphs (параграфы)

&#8230; являются радиопереключателями, с помощью которых можно выбрать, что необходимо вставлять в код &#8211; слова, предложения или параграфы.

Флажок &#8220;Start with &#8216;Lorem ipsum &#8230;'&#8221; задает условие, при котором каждый набор слов, предложения или параграфы начинаются с Lorem ipsum. И в самом низу расположена кнопка &#8220;Insert&#8221;, предназначение которой очевидно &#8211; вставить выбранный набор слов, предложений или параграфов в код html-документа.

Перейдем от слов к делу и на практике вставим &#8220;рыбу&#8221;.

Вставляем 4 слова. Устанавливаем в окне счетчика число 4, выбираем радиопереключатель в положение words. Чтобы вставляемые записи не повторялись, убираем галочку (checkbox) &#8220;Start with &#8216;Lorem ipsum &#8230;'&#8221;. Устанавливаем курсор мыши в то место html-кода, куда необходимо поместить &#8220;рыбу&#8221; и нажимаем кнопку &#8220;Insert&#8221;:<figure id="attachment_692" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum-4words-600x394.png" alt="Плагин LoremIpsum - вставка слов в Notepad++" width="600" height="394" class="size-medium wp-image-692" />][2]<figcaption class="wp-caption-text">Плагин LoremIpsum &#8211; вставка слов в Notepad++</figcaption></figure> 

Вставим 3 предложения. Устанавливаем счетчик в значение 3. Переводим переключатель в положение sentences (предложения). Оставляем пустой строку &#8220;Start with &#8216;Lorem ipsum &#8230;'&#8221;. Устанавливаем курсор мыши в то место html-кода, куда необходимо поместить &#8220;рыбу&#8221;. Жмем на &#8220;Insert&#8221;:<figure id="attachment_693" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum-3sentences-600x390.png" alt="Плагин LoremIpsum - вставка трех предложений в Notepad++" width="600" height="390" class="size-medium wp-image-693" />][3]<figcaption class="wp-caption-text">Плагин LoremIpsum &#8211; вставка трех предложений в Notepad++</figcaption></figure> 

Вставляем 1 параграф. Устанавливаем счетчик в значение 1. Переводим радиокнопку в положение paragraphs (параграфы). Устанавливаем курсор мыши в то место html-кода, куда необходимо поместить &#8220;рыбу&#8221;. Нажимаем кнопку &#8220;Insert&#8221;:<figure id="attachment_694" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum-1paragraph-600x390.png" alt="Плагин LoremIpsum - вставка одного параграфа в Notepad++" width="600" height="390" class="size-medium wp-image-694" />][4]<figcaption class="wp-caption-text">Плагин LoremIpsum &#8211; вставка одного параграфа в Notepad++</figcaption></figure> 

### Заключение

Как мне кажется, использование плагина LoremIpsum, встроенного в Notepad++, более удобно, чем сторонние источники, типа сайтов-генераторов. Удобство заключается в том, что все &#8220;под рукой&#8221;. В любой момент можно открыть диалоговое окно вставки &#8220;рыбы&#8221; и произвести практически моментальное наполнение содержимым. Особенно это удобно, если верстка производится автономно, без доступа в Интернет. Когда надобность в плагине отпадает, его можно сразу же закрыть, до следующего раза.

Оцените статью:  
<span id="post-ratings-690" class="post-ratings" data-nonce="417ee73fea"><img id="rating_690_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(690, 1, '1 Star');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_690_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(690, 2, '2 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_690_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(690, 3, '3 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_690_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(690, 4, '4 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_690_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(690, 5, '5 Stars');" onmouseout="ratings_off(3, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>3,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_690_text"></span></span><span id="post-ratings-690-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum-4words.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum-3sentences.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/plugin_lorem_ipsum-1paragraph.png