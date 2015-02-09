---
title: 'Pseudo-class и pseudo-element &#8211;  что это?'
author: gearmobile
layout: post
permalink: /pseudo-class-%d0%b8-pseudo-element-%d1%87%d1%82%d0%be-%d1%8d%d1%82%d0%be/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - Статьи по CSS
---
В CSS существует два типа псевдо-сущностей: **псевдо-классы** (pseudo-class) и **псевдо-элементы** (pseudo-element). В спецификации CSS2.1 имеются следующие **псевдо-классы** и **псевдо-элементы** (pseudo-element):

### Псевдо-классы (pseudo-class):

  * :link &#8211; непосещенная ссылка (*ни разу не щелкали мышью по ней*)
  * :visited &#8211; посещенная ссылка (*уже щелкнули мышью на ссылке*)
  * :hover &#8211; наведенная ссылка (*навели курсор мыши на ссылку*)
  * :focus &#8211; элемент в фокусе (*кнопка или поле ввода получили фокус при нажатии клавиши Tab*)
  * :active &#8211; активный элемент (*например, ссылка, на которой произведен щелчок мыши*)
  * :first-child &#8211; элемент, являющийся первым ребенком своего элемента-родителя
  * :lang() &#8211; элемент, основанный на значении его аттрибута lang

### Псевдо-элементы (pseudo-element):

**Псевдо-элементы**, существующие в спецификации CSS2.1:

  * ::first-line
  * ::first-letter
  * ::before
  * ::after

Так в чем же разница между псевдо-классом (pseudo-class) и псевдо-элементом (pseudo-element)? Все различие заключается в способе, которым эти две псевдо-сущности осуществляют воздействие на HTML-документ. Псевдо-классы (pseudo-class) ведут себя так, как если бы они добавлялись в виде обычных классов элементам HTML-страницы при выполнении определенных событий. Псевдо-элементы (pseudo-element) ведут себя так, как если бы они были обычными элементами HTML-страницы, но добавляемыми на нее при выполнении определенных событий.

> **Прим. переводчика**: заметили одну особенность? Обе псевдо-сущности появляются на HTML-странице только при одном условии &#8211; выполнении какого-то (не важно, какого) события. Просто одна сущность появляется на странице в виде класса (pseudo-class), а вторая в виде элемента (pseudo-element). Каким образом появляются? Только одним способом &#8211; браузер сам создает (генерирует) псевдо-сущность при выполнении указанного события. Поэтому псевдо-сущности иногда называют генерируемым содержимым. Название &#8220;псевдо&#8221; в точности говорит само за себя &#8211; &#8220;как-будто&#8221;. То есть &#8211; &#8220;как-будто класс&#8221;, &#8220;как-будто элемент&#8221;. Название дано не случайно &#8211; в исходном коде HTML-страницы не существуют таких классов или элементов; но они появляются (генерируются) там с помощью браузера при определенном событии.

Возьмем в качестве примера псевдо-элемент (pseudo-element) `::first-letter`. Предположим, необходимо сделать каждую первую букву заголовка `h1` вдвое большего размера, чем остальной текст в этом заголовке.

Легко:

<pre>h1::first-letter{
  font-size: 250%;
  color: #778899;
}
  </pre><figure id="attachment_944" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/first-letter-600x270.jpg" alt="Псевдо-элемент (pseudo-element) ::first-letter" width="600" height="270" class="size-medium wp-image-944" />][1]<figcaption class="wp-caption-text">Псевдо-элемент (pseudo-element) ::first-letter</figcaption></figure> 

Такое впечатление, что внутри HTML-разметки и CSS-таблицы произошли следующие изменения:

**HTML-разметка**:

<pre><h1>
  &lt;first-letter>H&lt;/first-letter>owdy, y'all
</h1>
  </pre>

**CSS-правило**:

<pre>h1 first-letter{
  font-size: 250%;
}
  </pre>

Выглядит это так, словно в действительно все так (*как создается впечатление*) и происходит внутри браузера, не правда ли? Кто знает? Все, что вы знаете, что это работает так, как будто на самом деле так и выглядит. Имя всему этому &#8220;псевдо-элемент&#8221;.

Аналогично, псевдо-класс работает так, если обычный класс добавляется к элементам внутри HTML-документа. Например, представим себе, что браузер добавляет класс &#8220;first-child&#8221; к каждому элементу `li`, который является первым ребенком своего родителя `ul`. Тогда эти элеиенты можно оформить в виде следующего CSS-правила:

<pre>li.first-child{
  border-left: none;
}
  </pre>

Простая замена точки на двоеточие (получается `li:first-child`) и мы имеем тот же самый конечный результат, без необходимости добавления вручную классов к элементам внутри всей HTML-разметки.

Вы могли уже догадаться относительно использования в псевдо-элементах *двойного двоеточия*. Такой синтаксис появился уже позже спецификации CSS2.1 (*в спецификации CSS3*). Ни у одного браузера нет строго условия использования двойного двоеточия в псевдо-элементах: одинарное двоеточие прекрасно понимается всеми браузерами.

### CSS3 псевдо-классы (pseudo-class):

Спецификация CSS3 добавляет еще несколько псевдо-классов (pseudo-class), большинство из которых не имеет всеобщей поддержки в браузерах (*на момент написания статьи*):

  * :target ([Псевдокласс :target &#8211; стили для элемента-якоря в HTML-документе][2])
  * :root
  * :nth-child() ([Как правильно читать псевдо-элемент nth-child?][3])
  * :nth-of-type() ([Кратко о :first-of-type, :nth-of-type и :not][4])
  * :nth-last-of-type()
  * :first-of-type ([Кратко о :first-of-type, :nth-of-type и :not][4])
  * :last-of-type ([Кратко о :first-of-type, :nth-of-type и :not][4])
  * :only-of-type
  * :only-child
  * :last-child
  * :empty ([Краткая заметка по псевдо-классу :empty][5])
  * :not() ([Кратко о :first-of-type, :nth-of-type и :not][4])
  * :enabled
  * :disabled
  * :checked

**Автор статьи:** *Eric Meyer &#8211; Smashing CSS Professional Techniques for Modern Layout*

Оцените статью:  
<span id="post-ratings-940" class="post-ratings" data-nonce="3bb8019761"><img id="rating_940_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(940, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_940_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(940, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_940_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(940, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_940_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(940, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_940_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(940, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_940_text"></span></span><span id="post-ratings-940-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/02/first-letter.jpg
 [2]: http://localhost:7788/third/?p=151 "Псевдокласс :target  - стили для элемента-якоря в HTML-документе"
 [3]: http://localhost:7788/third/?p=916 "Как правильно читать псевдо-элемент nth-child?"
 [4]: http://localhost:7788/third/?p=930 "Кратко о :first-of-type, :nth-of-type и :not"
 [5]: http://localhost:7788/third/?p=817 "Краткая заметка по псевдо-классу :empty"