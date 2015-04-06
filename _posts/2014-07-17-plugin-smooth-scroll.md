---
title: "Плагин Smooth Scroll"
layout: post
categories: javascript
tags: [smooth scroll, javascript]
---

> Обзор краткий такого же небольшого плагина Smooth Scroll, написанного под библиотеку jQuery.

Этот скрипт предназначен только для одной цели - плавного скроллинга (*прокрутки*) страницы. Благодаря этому улучшается юзабилити страницы и сайта в целом, так как нет резких скачков при переходе по ссылкам.

## Подключение плагина Smooth Scroll

Подключение Smooth Scroll к HTML-странице производится как обычно:

{% highlight html %}
<!--  SCRIPTS  -->
<script src="js/jquery-1.11.1.min.js"></script>
<script src="js/jquery.smooth-scroll.min.js"></script>
<script src="js/settings.js"></script>
...
{% endhighlight %}

... где первая строка - это библиотека jQuery, вторая строка - плагин Smooth Scroll, третья строка - файл инициализации плагина Smooth Scroll.

## Инициализация Smooth Scroll

Для того, чтобы заработал плагин Smooth Scroll и на странице появилась плавная прокрутка, нужно в js-файле скрипта прописать строки:

{% highlight javascript %}
$(document).ready(function(){
  $('a').smoothScroll();
});
{% endhighlight %}

... то есть - всем ссылкам страницы присвоить метод `smoothScroll()`, что дает плавный скроллинг. В принципе, этого достаточно - больше ничего и не надо.

## Варианты выборки в Smooth Scroll

Помимо показанной выше строчки, скрипт Smooth Scroll имеет несколько других вариантов режима работы. Другими словами, эти режимы работы - все навсего усложненный первый вариант, вариации на тему выборки HTML-элемента в библиотеке jQuery.

Примеры выборок взяты мною из файла `readme.md`, переводить их мне совсем не хочется; да и нет в этом необходимости - все понятно даже по коду:

  * Allows for easy implementation of smooth scrolling for same-page links.
  * Works like this: `$('a').smoothScroll();`
  * Specify a containing element if you want: `$('#container a').smoothScroll();`
  * Exclude links if they are within a containing element: `$('#container a').smoothScroll({excludeWithin: ['.container2']});`
  * Exclude links if they match certain conditions: `$('a').smoothScroll({exclude: ['.rough','#chunky']});`
  * Adjust where the scrolling stops: `$('.backtotop').smoothScroll({offset: -100});`
  * Add a callback function that is triggered before the scroll starts: `$(&#8216;a&#8217;).smoothScroll({beforeScroll: function() { alert(&#8216;ready to go!&#8217;); }});
  * Add a callback function that is triggered after the scroll is complete: `$('a').smoothScroll({afterScroll: function() { alert('we made it!'); }});`

## Пример работы Smooth Scroll

Ниже привожу пример HTML, SCSS и JS-кода, на котором проходил "испытание" плагин Smooth Scroll у меня, в моей "лаборатории".

{% highlight html %}
<head>
  <meta charset="utf-8">
  <title>Smooth Scroll Plugin</title>
  <link rel="stylesheet" href="css/style.css">
</head>

<body>

  <h1 class="head">smooth scroll plugin</h1>

  <ul class="scroll">
    <li><a href="#h1">header 1</a></li>
    <li><a href="#h2">header 2</a></li>
    <li><a href="#h3">header 3</a></li>
    <li><a href="#h4">header 4</a></li>
    <li><a href="#h5">header 5</a></li>
  </ul>

  <h1>header 1</h1>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h2>header 2</h2>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h3 id="h3">header 3</h3>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h4>header 4</h4>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5 id="h5">header 5</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 6</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 7</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h1>header 1</h1>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h2 id="h2">header 2</h2>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h3>header 3</h3>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h4>header 4</h4>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 5</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 6</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 7</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h1 id="h1">header 1</h1>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h2>header 2</h2>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h3>header 3</h3>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h4 id="h4">header 4</h4>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 5</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 6</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <h5>header 7</h5>

  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Laudantium odit sunt dicta, consequatur quis totam animi possimus. Dignissimos quod commodi enim accusamus obcaecati delectus, eaque similique quam hic perspiciatis fugiat.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis molestiae eos id provident veniam porro quas et optio vitae dignissimos delectus adipisci dolorum similique numquam necessitatibus sit magni, neque dolor.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non error dolorum, obcaecati, amet officia debitis nesciunt ullam quasi nobis aliquid quae voluptas mollitia ducimus accusantium veritatis quia esse autem inventore?</p>

  <!--  SCRIPTS  -->
  <script src="js/jquery-1.11.1.min.js"></script>
  <script src="js/jquery.smooth-scroll.min.js"></script>
  <script src="js/settings.js"></script>

</body>
{% endhighlight %}

{% highlight css %}
$color: #789;

h1,h2,h3,h4,h5{
  text-transform: uppercase;
  font-family: Georgia, sans-serif;
  text-align: center;
}

h1{
  font-size: 36px;
  color: $color;
}
h2{
  font-size: 32px;
  color: lighten($color,5%);
}
h3{
  font-size: 28px;
  color: lighten($color,10%);
}
h4{
  font-size: 24px;
  color: lighten($color,15%);
}
h5{
  font-size: 24px;
  color: lighten($color,20%);
}
h6{
  font-size: 20px;
  color: lighten($color,25%);
}
h7{
  font-size: 18px;
  color: lighten($color,30%);
}

.head{
  text-transform: capitalize;
  font-size: 48px;
  color: darken($color,5%);
}

.scroll{
  list-style-type: none;
  padding: 0 0 0 100px;
  li{
    margin-bottom: 10px;
    a{
      text-transform: capitalize;
      text-decoration: none;
      color: darken($color,10%);
      &:hover{
        color: darken($color,15%);
      }
    }
  }
}
{% endhighlight %}

{% highlight javascript %}
$(document).ready(function(){
  $('a').smoothScroll();
});
{% endhighlight %}

На этом все.

---

