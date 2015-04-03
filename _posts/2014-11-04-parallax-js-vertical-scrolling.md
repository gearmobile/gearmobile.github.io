---
title: "Parallax.js - создаем parallax со скроллингом"
layout: post
categories: javascript
tags: [javascript, parallax.js]
share: true
---

> В данном примере рассмотрим создание parallax с эффектом вертикального скроллинга. Это самый популярный вид parallax'а для страниц типа Landing Page.

Создавать эффект будет с помощью скрипта Parallax.js. По странному стечению обстоятельств данный скрипт имеет точно такое же имя, что и скрипт из предыдущего примера - "Parallax.js - создаем простой parallax". Однако, **это разные скрипты** и авторы у них разные; данный скрипт расположен на странице GitHub по адресу - [Parallax.js][1].

Домашняя страничка скрипта выполнена также с эффектом parallax - [Simple Parallax Scrolling][2].

## Parallax.js - создаем HTML-разметку

Разметка для скрипта Parallax.js проста. Это обычный блок, который может быть `div`, `section` или что-либо еще. Обязательным условием является подключение для блока класса `class="parallax-window"` и двух data-атрибутов: `data-parallax="scroll"` и `data-image-src="images/one.jpg"`.

Второй атрибут в качестве своего значения имеет относительный путь к файлу изображения, которое будет устанавливаться в виде фона. В дополнение можно задать еще несколько атрибутов для ускорения загрузки изображений браузером:

  * `data-natural-width` - реальная ширина изображения
  * `data-natural-height` - реальная высота изображения

Ниже приведу созданные мною четыре блока `section` с содержимым:

{% highlight html %}
<!-- begin one -->
<section data-parallax="scroll" data-image-src="images/one.jpg" class="parallax-window">
  <div class="wrap one">
    <h1>Welcome to Parallax!</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Temporibus consequatur, nulla neque voluptatum deserunt at voluptatibus eos. Magni sapiente rem, suscipit assumenda provident, quaerat doloribus libero? Eaque doloremque, quo sequi!</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sint nemo cum, dignissimos blanditiis iusto quasi, quis! Ducimus aperiam sunt libero deleniti numquam rerum esse architecto, officiis amet, officia recusandae aut.</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Itaque reiciendis vitae, amet! Quas saepe consequuntur, nisi quia, cupiditate dignissimos laborum incidunt soluta repellat, libero id quibusdam mollitia maiores omnis tempore.</p>
  </div>
</section>
<!-- end one -->

<!-- begin two -->
<section data-parallax="scroll" data-image-src="images/two.jpg" class="parallax-window">
  <div class="wrap two">
    <h2>Parallax is great!</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Modi accusamus deserunt ipsum nesciunt odit vero corporis eaque, quibusdam, enim, beatae, repellendus iusto. Amet corporis beatae, inventore officiis est aut. Ab!</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Maxime possimus sint a facere dignissimos! Labore at, beatae consequuntur corporis perspiciatis! Asperiores illum esse repellat veniam vero totam debitis! Quos, consectetur.</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nulla, totam maxime dolorum similique, ipsa a. Ea illo eligendi, ex, officia id eum sit sint nobis aperiam, error nihil ab dolorum.</p>
  </div>
</section>
<!-- end two -->

<!-- begin three -->
<section data-parallax="scroll" data-image-src="images/three.jpg" class="parallax-window">
  <div class="wrap three">
    <h3>Parallax is easy!</h3>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque quia ex doloremque et, eum soluta culpa ipsum placeat consectetur, error at, accusamus iure! Doloribus corporis, earum quo modi omnis hic.</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cum ab distinctio omnis repellendus exercitationem maiores ad sed, deleniti dolorem tempore praesentium nobis suscipit nihil quidem qui nostrum debitis ipsam culpa.</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Impedit, repellendus, qui. Aspernatur reiciendis eligendi, totam eaque iusto illo officia. Facere dicta harum, dolore sit perferendis in neque mollitia eligendi dignissimos?</p>
  </div>
</section>
<!-- end three -->

<!-- begin four -->
<section data-parallax="scroll" data-image-src="images/four.jpg" class="parallax-window">
  <div class="wrap">
    <h4>Let's start use it!</h4>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eius ab voluptates alias corporis, laborum provident corrupti assumenda dignissimos vel repellendus obcaecati, aspernatur earum ipsum rem. Voluptatum ipsum nostrum in! Rerum.</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reprehenderit alias illum minus asperiores culpa, modi veritatis quibusdam, aperiam accusantium repellendus at possimus qui cupiditate dolorem quod accusamus a. Mollitia, repudiandae.</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio quo nulla officia sapiente a tenetur maxime sunt mollitia accusantium aut, eius minus maiores fugit necessitatibus obcaecati ex eos quibusdam sequi.</p>
  </div>
</section>
<!-- end four -->
{% endhighlight %}

## Parallax.js - стилизация страницы

Стилизацию страницы буду выполнять на Sass/Compass с использованием вертикального ритма "Vertical Rhythm" - в данном случае он подойдет как раз к месту, как мне кажется:

{% highlight css %}
@import "compass";
@import "compass/reset";

$base-font-size: 24px;
$base-line-height: 36px;
$rhythm-unit: "rem";
$rem-with-px-fallback: true;

@include establish-baseline;

.parallax-window {
  min-height: 1080px;
  background: transparent;
  .wrap{
    margin-top: 100px;
    text-align: center;
    width: 1200px;
    margin: 0 auto;
    @include leader($lines: 7, $property: padding);
    p{
      @include rhythm-margins;
    }
    h1{
      @include adjust-font-size-to(2.074rem);
    }
    h2{
      @include adjust-font-size-to(1.728rem);
    }
    h3{
      @include adjust-font-size-to(1.44rem);
    }
    h4{
      @include adjust-font-size-to(1.2rem);
    }
    &.one{
      text-align: center;
      color: rgba(255,255,255,.8);
    }
    &.two{
      text-align: left;
      color: rgba(0, 0, 0, .8);
    }
    &.three{
      text-align: right;
      color: rgba(255, 255, 255, .8);
    }
  }
}
{% endhighlight %}

В этом коде наиболее важными строками являются две - без них скроллинга не получиться:

{% highlight css %}
.parallax-window {
  min-height: 1080px;
  background: transparent;
  ...
{% endhighlight %}

## Parallax.js - добавление Javascript

Разметка и стили готовы - осталось подключить скрипт Parallax.js и библиотеку jQuery:

<pre>
</pre>

jQuery "забираем" с Google, а скрипт Parallax.js - с GitHub-страницы проекта - [Parallax.js][2]. Все это "добро" пихаем в самый низ, подвал HTML-документа - перед закрывающим тегом `</body>`.

В дальнейшие украшательства вдаваться не буду - это дело техники. Мне важен сам принцип создания parallax с эффектом вертикального скроллинга.

В принципе, у меня все готово для того, чтобы полюбоваться результатом. Открываю страницу в браузере и любуюсь (не забывая скролить саму страницу):

![Страница на Parallax.js с вертикальным скроллингом]({{site.url}}/images/uploads/2014/11/ParallaxJX-_Scrolling.png)

Отлично! Получился прямо таки совсем неплохой parallax с вертикальным скроллингом. Готовый пример со всеми исходниками можно посмотреть на GitHub - [Parallax.js Scrolling][3].

---

 [1]: https://github.com/pixelcog/parallax.js/ "Parallax.js"
 [2]: http://pixelcog.com/parallax.js/ "Simple Parallax Scrolling"
 [3]: https://github.com/gearmobile/zencoder/tree/master/parallaxjs_scroll "Parallax.js Scrolling"
