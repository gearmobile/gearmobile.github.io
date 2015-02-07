---
title: Кратко о :first-of-type, :nth-of-type и :not
author: gearmobile
layout: post
permalink: /%d0%ba%d1%80%d0%b0%d1%82%d0%ba%d0%be-%d0%be-first-of-type-nth-of-type-%d0%b8-not/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Статьи по CSS
tags:
  - :first-of-type
  - :not
  - :nth-of-type
---
### Псевдоэлементы :first-of-type и :last-child

Псевдоэлемент `:first-of-type` служит для выборки дочернего элемента **определенного типа**. Можно сказать, что псевдоэлемент `:first-of-type` является частным случаем псевдоэлемента `:first-child`. Если псевдоэлемент `:first-child` выполняет выборку первого дочернего элемента вне зависимости от его типа, то псевдоэлемент `:first-of-type` осуществляет выборку первого дочернего элемента **только указанного типа** (если этот элемент отвечает заданному условию &#8211; типу элемента).

Аналогично работает псевдоэлемент `:last-of-type`, только применяется к последнему дочернему элементу определенного типа. Более общим случаем является псевдоэлемент `:last-child`.

Псевдоэлементы `:last-child`, `:nth-child()`, `:first-of-type` **НЕ ПОДДЕРЖИВАЮТСЯ IE8**.

Пример:

`.fofo p:first-of-type{}`

&#8230; в примере тег **p** является указанием типа дочернего элемента. То есть, будет выбран первый дочерний элемент типа **p**, родителем которого является элемент с классом `.fofo`.

`.wowo p:last-of-child{}`

Выбрать последний дочерний элемент типа **p**, родителем которого является элемент с классом `.wowo`.

Рабочий пример приведен ниже. Два одинаковых списка. К первому применен псевдоэлемент `:first-of-type`, ко второму &#8211; псевдоэлемент `:first-child`. В первом случае выбран первый параграф списка, так как в выражении указано выбрать именно первый дочерний элемент списка, являющийся параграфом **p**:

<pre>.fofo p:first-of-type{
  font-weight: bold;
  color: #222;
  font-variant: small-caps;
  text-shadow: 1px 1px 1px #999;
}
</pre>

Во втором случае к списку применен псевдоэлемент `:first-child` и в этом случае был отобран первый элемент указанного списка &#8211; ссылка **a**! А то, что этот элемент является ссылкой, а не параграфом **p**, роли не играет &#8211; тип элемента не был указан:

<pre>.wowo :first-child{
  font-size: 14px;
  font-style: italic;
  color: green;
  font-weight: bold;
}
</pre><figure id="attachment_937" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/first-of-type1-600x400.jpg" alt="Псевдоэлемент :first-of-type" width="600" height="400" class="size-medium wp-image-937" />][1]<figcaption class="wp-caption-text">Псевдоэлемент :first-of-type</figcaption></figure> 

Псевдоэлемент `:last-of-child` и его общий случай `:last-child` разбирать смысла нет, так как выборка элемента из HTML-документа осуществляется аналогично с тем лишь различием, что применяется не к первому, а последнему дочернему элементу.

### Псевдоэлемент :nth-of-type

Псевдоэлемент `:nth-of-type` является частным случаем псевдоэлемента `:nth-child`. В случае с `:nth-of-type` выборка элементов производится не только по порядковому номеру, **но и по типу элемента**.

Например, `p img:nth-of-type(odd){float: left}` и `p img:nth-of-type(even){float: right}` делает выборку четных и нечетных порядковых номеров только элементов **img**.

Отбираются все дочерние по отношению к `.nthOfType` элементы типа **img**, нечетные по порядковому номеру. И применяются к нему правила &#8211; смещение влево, `margin-right` и тень справа:

<pre>.nthOfType img:nth-of-type(odd){
  float: left;
  margin: 0 10px 0 0;
  box-shadow: 3px 3px 3px rgba(0,0,0,.65);
}
</pre>

Отбираются все дочерние по отношению к `.nthOfType` элементы типа **img**, четные по порядковому номеру. И применяются к нему правила &#8211; смещение право, `margin-left` и тень слева:

<pre>.nthOfType img:nth-of-type(even){
  float: right;
  margin: 0 0 0 10px;
  box-shadow: -3px 3px 3px rgba(0,0,0,.65);
}
</pre><figure id="attachment_933" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/nth-of-type-600x400.jpg" alt="Псевдоэлемент :nth-of-type" width="600" height="400" class="size-medium wp-image-933" />][2]<figcaption class="wp-caption-text">Псевдоэлемент :nth-of-type</figcaption></figure> 

### Псевдокласс :not

Псевдокласс `:not` (*псевдокласс отрицания*) &#8211; выбрать все элементы **p**, у которых **НЕТ** класса `.classy` и применить к ним следующие свойства: цвет и тень. Другими словами, выборка элементов с помощью псевдокласса `:not` производится **от обратного** &#8211; "выбрать все элементы, которые **НЕ ОТВЕЧАЮТ** следующему условию." Этот псевдокласс является антагонистом обычного условия &#8211; "если удовлетворяет условию, то примени такое-то свойство":

HTML-разметка:

<pre><p class="classy">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>


<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>


<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>


<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>
</pre>

CSS-стили:

<pre>.dodo p:not(.classy){
  color: blue;
  text-shadow: 1px 1px 1px rgba(0,0,255,.2);
}
</pre><figure id="attachment_934" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/not-600x400.jpg" alt="Псевдоэлемент :not" width="600" height="400" class="size-medium wp-image-934" />][3]<figcaption class="wp-caption-text">Псевдоэлемент :not</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-930" class="post-ratings" data-nonce="0312cef4a0"><img id="rating_930_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(930, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_930_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(930, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_930_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(930, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_930_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(930, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_930_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(930, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_930_text"></span></span><span id="post-ratings-930-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/02/first-of-type1.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2014/02/nth-of-type.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2014/02/not.jpg