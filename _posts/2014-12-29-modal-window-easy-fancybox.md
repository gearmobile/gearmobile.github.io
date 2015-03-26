---
title: "Модальное окно на Easy FancyBox"
layout: post
categories: wordpress
description: ""
excerpt: ""
tags: [easy fancybox, wordpress]
share: true
---

> Три способа подключения всплывающего (модального) окна на WordPress, созданного с помощью плагинов Easy FancyBox и Contact Form 7.

Данная статья посвящена вопросу создания всплывающего (модального) окна на WordPress. Такие окна еще называются модальными и их также можно создавать на CSS.

<figure>
  <img src="images/uploads/2014/12/modal_window.jpg" alt="Easy Fancybox">
</figure>

Этой статьи очень легко могло бы не быть, если бы не **две причины**.

**Первая причина** - Сеть буквально завалена статьями и статейками на эту тему, но все они одна в одну повторяют друг друга. И только в одной я нашел грамотное, точное и краткое описание, как выполнять подключение модального окна в WordPress.

**Вторая причина** - у меня первоначально созданное модальное окно не заработало. И только на одном из форумов я нашел ответ на свой вопрос.

Ниже привожу описания решения обоих вопросов.

## Три способа подключения модального окна Easy FancyBox

Итак, как я уже говорил выше, статей по вопросу создания модального окна с помощью плагинов [Easy FancyBox][1] и [Contact Form 7][2] существует огромное количество. Поэтому здесь я его описывать не буду. А коснусь вопроса - как подключить уже созданную форму в WordPress.

### Код формы Easy FancyBox в шаблон

Если готовая форма **встраивается непосредственно в шаблон**, то код должен быть таким:

{% highlight html %}
<a class="fancybox" href="#contact_form_pop">Контактная форма</a>

<div class="fancybox-hidden" style="display:none">
<div id="contact_form_pop">
  <?php echo do_shortcode('[contact-form-7 id="" title=""]'); ?>
</div>
</div>
{% endhighlight %}

Обратите внимание на конструкцию `<?php echo do_shortcode(''); ?>`, в которую вставлен `shortcode`, созданный в плагине Contact Form 7.

### Код формы Easy FancyBox на страницу

Если готовая форма **встраивается в запись или на страницу**, то код должен быть таким:

{% highlight html %}
<a class="fancybox" href="#contact_form_pop">Контактная форма</a>

<div class="fancybox-hidden" style="display:none">
<div id="contact_form_pop">
  [contact-form-7 id="" title=""]
</div>
</div>
{% endhighlight %}

Здесь shortcode вставляется "как есть" - как его создал плагин Contact Form 7.

### Код формы Easy FancyBox в виджет

Готовую форму можно встраивать в виджет, но для этого сначала нужно **включить поддержку shortcode** в WordPress. Для этого в файле `functions.php` нужно добавить строку:

{% highlight php %}
add_filter('widget_text', 'do_shortcode');
{% endhighlight %}

Теперь виджет "Текст" имеет поддержку shortcode и **вставить готовую форму в виджет** "Текст" нужно таким образом:

{% highlight html %}
<a class="fancybox" href="#contact_form_pop">Контактная форма</a>

<div class="fancybox-hidden" style="display:none">
<div id="contact_form_pop">
  [contact-form-7 id="" title=""]
</div>
</div>
{% endhighlight %}

Здесь shortcode вставляется точно также - без изменений, как есть из плагина Contact Form 7.

Все три способа были "подсмотрены" мною здесь - "[Контактная форма (Contact Form 7) во всплывающем окне][3]".

## Модальное окно Easy FancyBox не работает

Перехожу ко второму вопросу - все настроено, но ничего не работает. Такое было у меня и было связано с тем, что мною была сверстана и создана тема под Worpdress с нуля.

Проблема заключалась в том, что я "забыл" добавить в созданную тему две функции, которые **обязательно должны присутствовать** в любой WordPress-теме - `wp_head();` и `wp_footer();`.

В файле шапки сайта `header.php` перед закрывающим тегом `</head>` необходимо вставить запись, которая будет выглядеть таким образом:

{% highlight php %}
...
<?php wp_head(); ?>
</head>
{% endhighlight %}

В файле подвала сайта `footer.php` перед закрывающим тегом `</body>` необходимо вставить запись, которая будет выглядеть таким образом:

{% highlight php %}
...
<?php wp_footer(); ?>
</body>
{% endhighlight %}

На этом все.


 [1]: https://wordpress.org/plugins/easy-fancybox/ "Easy FancyBox"
 [2]: http://contactform7.com/ "Contact Form 7"
 [3]: http://web.warwolf.org/kontaktnaya-forma-contact-form-7-vo-vsplyvayushhem-o/ "Контактная форма (Contact Form 7) во всплывающем окне"
