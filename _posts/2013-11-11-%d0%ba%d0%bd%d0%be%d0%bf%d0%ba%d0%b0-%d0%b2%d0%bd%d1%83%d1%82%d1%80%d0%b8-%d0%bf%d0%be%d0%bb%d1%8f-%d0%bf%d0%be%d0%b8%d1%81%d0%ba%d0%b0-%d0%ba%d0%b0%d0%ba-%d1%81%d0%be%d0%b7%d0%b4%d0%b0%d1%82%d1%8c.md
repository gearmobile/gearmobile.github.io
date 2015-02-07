---
title: 'Кнопка внутри поля поиска &#8211; как создать с помощью CSS'
author: gearmobile
layout: post
permalink: /%d0%ba%d0%bd%d0%be%d0%bf%d0%ba%d0%b0-%d0%b2%d0%bd%d1%83%d1%82%d1%80%d0%b8-%d0%bf%d0%be%d0%bb%d1%8f-%d0%bf%d0%be%d0%b8%d1%81%d0%ba%d0%b0-%d0%ba%d0%b0%d0%ba-%d1%81%d0%be%d0%b7%d0%b4%d0%b0%d1%82%d1%8c/
ratings_users:
  - 10
ratings_score:
  - 38
ratings_average:
  - 3.8
cleanretina_sidebarlayout:
  - default
categories:
  - Статьи по CSS
tags:
  - css
---
Интересный вопрос создания поля поиска с кнопкой внутри. Сейчас такой прием очень популярен в дизайне и используется повсеместно на сайтах. Почему популярен &#8211; просто очень красив такой способ передачи поля ввода в веб-приложении. Чтобы было более понятно, о чем идет речь, давайте посмотрим пример макета с подобной формой поиска:<figure id="attachment_405" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/search-form-example-600x465.jpg" alt="Пример поля поиска с кнопкой внутри на макете" width="600" height="465" class="size-medium wp-image-405" />][1]<figcaption class="wp-caption-text">Пример поля поиска с кнопкой внутри на макете</figcaption></figure> 

Дизайн нарисован таким образом, что видим следующее. Поле ввода текста с текстом-заглушкой (placeholder), справа внутри поля находиться кнопка отправки запроса в виде текста Send. Все вроде так и в чем же проблема? Трудность заключается в том, что на сегодняшний день возможности CSS не позволяют поместить кнопку внутри элемента input. Поэтому в данном случае выход один &#8211; разместить рядом два элемента: input и кнопку (button type=&#8221;submit&#8221; или input type=&#8221;submit&#8221;). Оба эти элемента обернуть в родительский элемент form (благо он является блочным) которому придать внешние свойства поля ввода &#8211; фоновую заливку, границу, внутренние отступы (padding). А у настоящих элементов (input или button) убрать все визуальные признаки их присутствия внутри form.

На авторитетном для меня сайте htmlbook есть статья, посвященная подобному вопросу. Но в ней описывается способ, когда внутрь элемента форм вставляется дополнительный блок div. Которому назначаются все внешние атрибуты поля ввода. Мне такой подход не совсем понятен &#8211; зачем плодить лишнюю разметку, когда с подобной задачей прекрасно справляется сам элемент form. Мне более нравиться способ, представленный на сайте Speckyboy.com автором Catalin Rosu, в котором как раз и используются только три элемента: form, input type=&#8221;text&#8221;, button type=&#8221;submit&#8221;. В самом конце статьи я приведу код этого примера также, ибо он мне понравился.

Приступаем к первому примеру и начнем создавать поле поиска с кнопкой, как на картинке. Для начала придадим элементу form внешние признаки поля ввода: зададим границу с радиусом скругления, фоновую заливку и внутренние поля отступа (padding). Помимо этого, явно установим ширину и высоту нашего будущего &#8220;поля&#8221; ввода и немного приукрасим ее, анимировав цвет границы при наведении hover:

<pre>form{
    border: 1px solid #ad9d80;
    padding: 4px 20px 4px 24px;
    width: 254px;
    margin: 0 0 25px 0;
    height: 30px;
    background-color: #e4d9c5;
    border-radius: 9px;
    &:hover{
      border-color: darken(#ad9d80, 10%);
    }
</pre>

Теперь уберем все, что делает input таковым в нашем случае &#8211; обнулим границу, переопределим padding и установим в ноль margin. Это основные свойства элемента input, назначаемые ему по умолчанию браузером. Затем немного поборемся с браузерами на WebKit (Chrome\Safari), которые создаются эффект свечения вокруг поля ввода при получении фокуса (outline) и рисуют тонкую линию-границу (-webkit-appearance: none) несмотря на то, что мы убрали ее, обнулив border. Фоновый цвет сделаем одинаковым с элементом form, чтобы создавалась иллюзия однородности. Все остальные свойства можно не упоминать &#8211; они очевидны (кегль, цвет текста, высота input и так далее).

Практически также поступим для элемента button, за исключением характерных нюансов типа text-transform: uppercase или color: #4f432e. Кстати, у Catalin Rosu я перенял &#8220;фишку&#8221;, когда он применяет button type=&#8221;submit&#8221; вместо input type=&#8221;submit&#8221;. Это делается для дополнительной функциональности кнопки, так как button может перехватывать событие Enter (нажатие этой клавиши на клавиатуре) + событие мыши. А вот input type=&#8221;submit&#8221; &#8211; только нажатие мыши на самом себе:

<pre>input[type="text"]{
    border: none;
    margin: 0;
    outline: none;
    -webkit-appearance: none;
    height: 30px;
    vertical-align: top;
    background-color: #e4d9c5;
    color: #beb19a;
    font-size: 18px;
    font-style: italic;
    padding: 0 8px 0 0;
    width: 192px;
  }
</pre>

<pre>button[type="submit"]{
    border: none;
    margin: 0;
    padding: 0;
    font-size: 18px;
    text-transform: uppercase;
    line-height: 30px;
    color: #4f432e;
    background-color: #e4d9c5;
    cursor: pointer;
    transition: color .2s;
    &:hover{
      color: lighten(#4f432e, 10%);
    }
</pre>

Ну и в конце приукрасим текст-заглушку (placeholder). Здесь придется использовать браузерные префиксы, так как данное свойство не поддерживается в полной мере браузерами на сегодня:

<pre>input::-webkit-input-placeholder {
    color: #beb19a;
    font-size: 16px;
    font-weight: normal;
    font-style: italic;
  }
  input:-moz-input-placeholder {
    color: #beb19a;
    font-size: 16px;
    font-weight: normal;
    font-style: italic;
  }
  input:-ms-input-placeholder {
    color: #beb19a;
    font-size: 16px;
    font-weight: normal;
    font-style: italic;
  }
</pre>

Совсем забыл привести HTML-код, на основе которого создавались все вышеприведенные стили:

<pre>&lt;form action="#" method="#"&gt;
    &lt;input type="text" name="email" id="email" placeholder="enter your email address..."&gt;
    &lt;button type="submit"&gt;send&lt;/button&gt;
  &lt;/form&gt;
</pre>

Результат создания поля поиска показан ниже:<figure id="attachment_406" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/search-form-ready-600x212.jpg" alt="Созданное в коде поле ввода с кнопкой внутри" width="600" height="212" class="size-medium wp-image-406" />][2]<figcaption class="wp-caption-text">Созданное в коде поле ввода с кнопкой внутри</figcaption></figure> 

Все хорошо.

#### Поле ввода и кнопка со стрелкой (псевдо-элемент) внутри.

На закуску привожу полный код (почти без объяснений &#8211; чего там объяснять) от Catalin Rosu, как и обещал.

HTML-код. Здесь есть интересный атрибут required, который делает значение в поле ввода обязательным. Если оно будет пустым и нажать кнопку отправки, то появиться сообщение о необходимости сначала ввести данные. Также автором статьи намеренно используется элемент input type=&#8221;text&#8221; вместо нового элемента input type=&#8221;search&#8221;, который еще не до конца поддерживается всеми браузерами:

<pre>&lt;form class="catalin"&gt;
    &lt;input type="text" placeholder="Search here ..." required&gt;
    &lt;button type="submit"&gt;Send&lt;/button&gt;
  &lt;/form&gt;
</pre>

CSS-код. Довольно объемный, но это связано с теми эффектами, которые применены к данной форме:

<pre>form.catalin{
    width: 390px;
    margin: 50px auto;
    overflow: hidden;
    padding: 10px;
    background-color: #ccc;
    border-radius: 8px;
    box-shadow: 0 0 8px rgba(0,0,0,.3) inset;
  }
    form.catalin input{
      float: left;
      border: none;
      padding: 2px 10px 2px 4px;
      font: 16px Arial, Helvetica, sans-serif;
      height: 26px;
      width: 306px;
      margin: 0;
      -webkit-appearance: none;
      outline: none;
      box-shadow: 0 0 1px rgba(0,0,0,.5);
      border-radius: 3px 0 0 3px;
    }
    form.catalin button{
      float: left;
      border: none;
      background-color: #778899;
      padding: 0;
      margin: 0;
      width: 70px;
      height: 30px;
      font: bold 12px/30px Arial, Helvetica, sans-serif;
      position: relative;
      cursor: pointer;
      text-shadow: 1px 1px 1px rgba(255,255,255,.5);
      border-radius: 0 3px 3px 0;
      text-transform: uppercase;
      text-align: center;
    }
      form.catalin button:hover{
        background-color: #667788;
      }
    form.catalin button:before{
      content: '';
      position: absolute;
      top: 10px;
      left: -5px;
      border-top: 5px solid transparent;
      border-bottom: 5px solid transparent;
      border-right: 5px solid #778899;
    }
      form.catalin button:hover:before{
        border-right-color: #667788;
        text-shadow: 1px 1px 1px rgba(255,255,255,.6);
      }

  /* Placeholder
  -----------------------------------------------------*/
    form.catalin input::-webkit-input-placeholder {
       color: #999;
       font-weight: normal;
       font-style: italic;
    }
     
    form.catalin input:-moz-placeholder {
        color: #999;
        font-weight: normal;
        font-style: italic;
    }
     
    form.catalin input:-ms-input-placeholder {
        color: #999;
        font-weight: normal;
        font-style: italic;
    }    
</pre>

И результат этого кода &#8211; красивое поле ввода с не менее красивой кнопкой отправки данных на сервер:<figure id="attachment_407" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/search-form-catalin-600x303.jpg" alt="Поле ввода с кнопкой внутри. Кнопка выполнена со стрелочкой." width="600" height="303" class="size-medium wp-image-407" />][3]<figcaption class="wp-caption-text">Поле ввода с кнопкой внутри. Кнопка выполнена со стрелочкой.</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-404" class="post-ratings" data-nonce="294778a933"><img id="rating_404_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(404, 1, '1 Star');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_404_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(404, 2, '2 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_404_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(404, 3, '3 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_404_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(404, 4, '4 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_404_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(404, 5, '5 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>10</strong> votes, average: <strong>3,80</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_404_text"></span></span><span id="post-ratings-404-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/search-form-example.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/search-form-ready.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/search-form-catalin.jpg