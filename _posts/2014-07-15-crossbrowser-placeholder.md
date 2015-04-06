---
title: "Кросс-браузерный placeholder"
layout: post
categories: css
tags: [placeholder]
share: true
---

> Короткая статья, посвященная вопросу кросс-браузерности такого HTML5-атрибута для формы, как `placeholder`.

Недавно столкнулся в подобным вопросом, решение не смог найти. Однако, в книге "Недостающее руководство по HTML5" случайно столкнулся с подробным описанием решения этой маленькой проблемы. Проблема и вправду маленькая - вопрос поддержки или не поддержки браузерами данного атрибута на сегодняшний день - это мелочь. Ну правда, разве пострадает функциональность верстаемого сайта от того, что в поле поиска не будет отображаться подстановочный текст? Конечно, нет!

Еще один момент - говоря о кросс-браузерной поддержке атрибута `placeholder`, почти всегда подразумевается на самом деле поддержка этого атрибута только одним браузером. Конечно, это многострадальный Internet Explorer версии 7 или 8. О версии Internet Explorer 6 можно уже забыть. Остальные браузеры нормально справляются со своей задачей и понимают, что такое `placeholder`.

Автор статьи обладает некоторой долей перфекционизма - для него и такая мелочь является принципиальной мелочью, камнем преткновения. И вот, этот камень можно отодвинуть в сторону.

## Кросс-браузерные заплатки для HTML5

Начну с того, что решение вопроса кросс-браузерного `placeholder` было создано уже давно. Это для меня данный факт был открытием! Более того, существует большое количество способов, решающих данную проблему. Все они собраны воедино по одному адресу на GitHub - [HTML5 Cross Browser Polyfills ][1]. Вся эта коллекция называется "Кросс-браузерные заплатки для HTML5", но в нашем случае нужен только один раздел этой коллекции - [Web Forms : input placeholder][2].

Ого - там не одно решение, а целых одиннадцать! Причем, все они реализованы на JavaScript, поэтому и кросс-браузерные. Выбирать можно любой, какой понравиться - принцип работы и способ подключения к HTML-странице у них всех почти одинаков. Я возьму для себя способ [jquery.placeholder.js][3], просто потому, что название понравилось.

Плагин `jquery.placeholder.js` может реализовать поддержку атрибута `placeholder` как в Internet Explorer 7 или 8, так и в Internet Explorer 6. Ну, Internet Explorer 6 - это уже слишком! На момент написания статьи многие верстальщики (конечно, не все) имеют тенденцию "забывать" о существовании даже Internet Explorer 8.

## Подключение плагина jquery.placeholder.js

Подключение плагина `jquery.placeholder.js` абсолютно стандартное для такого рода скриптов. Ниже привожу пример такого подключения в HTML-коде:

{% highlight html %}
<!--  SCRIPTS  -->
<script src="js/jquery-1.10.2.min.js"></script>
<script src="js/jquery.placeholder.js"></script>
...
{% endhighlight %}

Затем идет скрипт инициализации для данного плагина. Общая картина будет выглядеть таким образом:

{% highlight html %}
<!--  SCRIPTS  -->
<script src="js/jquery-1.10.2.min.js"></script>
<script src="js/jquery.placeholder.js"></script>
<script>
  $('input, textarea').placeholder();
</script>
{% endhighlight %}

Плагин `jquery.placeholder.js` делает в HTML-документе выборку по двум HTML-элементам - `input` и `textarea`. А затем применяет к ним метод `placeholder()` - все просто.

## HTML-форма с placeholder

Ниже привожу пример HTML5-формы, в которой применен атрибут `placeholder` в полях ввода, реализованных через элемент `input`. А также в элементе `textarea`:

{% highlight html %}
<form action="#">
  <h1>zoo keeper application form</h1>
  <p>Please complete the form. Mandatory fields are marked as a <span>*</span></p>

  <!-- CONTACT DETAILS  -->
  <fieldset>
    <legend>contact details</legend>
    <label for="name">name <span>*</span></label>
    <input type="text" name="name" title="Your full name here" placeholder="John Resig" autofocus required><br>
    <label for="telephone">telephone <span>*</span></label>
    <input type="tel" name="telephone" title="Input your phone number here" placeholder="9(989)600-30-20" required><br>
    <label for="email">email <span>*</span></label>
    <input type="email" name="email" title="Your email required" placeholder="test@mail.ru" required>
  </fieldset>

  <!-- PERSONAL INFORMATION  -->
  <fieldset>
    <legend>personal information</legend>
    <label for="age">age <span>*</span></label>
    <input type="number" title="Your real age, please" name="age" min="10" max="90" value="29" step="1" required><br>
    <label for="gender">gender</label>
    <select name="gender" id="gender" size="1">
      <option value="female">female</option>
      <option value="female">male</option>
    </select><br>
    <label for="message">When did you first know you wanted to be a zoo-keeper?</label>
    <textarea name="message" id="message" cols="30" rows="10" placeholder="I have a dream ..."></textarea>
  </fieldset>

  <!-- FAVORITES ANIMALS  -->
  <fieldset>
    <legend>pick your favorite animals</legend>
    <label for="zebra"><input type="checkbox" value="zebra">zebra</label>
    <label for="elephant"><input type="checkbox" value="elephant">elephant</label>
    <label for="cat"><input type="checkbox" value="cat">cat</label>
    <label for="wildebeest"><input type="checkbox" value="wildebeest">wildebeest</label>
    <label for="anaconda"><input type="checkbox" value="anaconda">anaconda</label>
    <label for="pingeon"><input type="checkbox" value="pingeon">pingeon</label>
    <label for="human"><input type="checkbox" value="human" checked="checked">human</label>
    <label for="crab"><input type="checkbox" value="crab">crab</label>
  </fieldset>

  <input type="submit" value="send">
</form>
{% endhighlight %}

## Проверка поддержки placeholder в IE8

JS-скрипты подключены и создана HTML-разметка. Для тестирования работы плагина `jquery.placeholder.js` воспользуюсь браузером, в котором заведомо не реализована поддержка атрибута `placeholder` - это Internet Explorer 8. Открываю созданную HTML-страничку в этом браузере (связка Windows XP + IE8) и вижу результат:

![Placeholder в Internet Explorer 8]({{site.url}}/images/uploads/2014/07/placeholder.jpg)

Галочками отмечены поля, в которых сработал плагин `jquery.placeholder.js` - если бы не он, там было бы пусто. Отлично - плагин работает и его можно применять в деле, на готовом проекте!

---

 [1]: https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills "HTML5 Cross Browser Polyfills "
 [2]: https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills#web-forms--input-placeholder "Web Forms : input placeholder"
 [3]: https://github.com/serby/jquery.placeholder.js "jquery.placeholder.js"
