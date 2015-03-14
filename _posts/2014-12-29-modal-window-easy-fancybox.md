---
title: Модальное окно на Easy FancyBox
author: gearmobile
layout: post
---
> Три способа подключения всплывающего (модального) окна на WordPress, созданного с помощью плагинов Easy FancyBox и Contact Form 7.

Данная статья посвящена вопросу создания всплывающего (модального) окна на WordPress. Такие окна еще называются модальными и их также можно создавать на CSS.

[<img class="aligncenter wp-image-2152 size-medium" src="http://localhost:7788/third/wp-content/uploads/2014/12/modal_window-515x600.jpg" alt="easy fancybox" width="515" height="600" />][1]

Этой статьи очень легко могло бы не быть, если бы не **две причины**.

**Первая причина** &#8211; Сеть буквально завалена статьями и статейками на эту тему, но все они одна в одну повторяют друг друга. И только в одной я нашел грамотное, точное и краткое описание, как выполнять подключение модального окна в WordPress.

**Вторая причина** &#8211; у меня первоначально созданное модальное окно не заработало. И только на одном из форумов я нашел ответ на свой вопрос.

Ниже привожу описания решения обоих вопросов.

### Три способа подключения модального окна Easy FancyBox

Итак, как я уже говорил выше, статей по вопросу создания модального окна с помощью плагинов [Easy FancyBox][2] и [Contact Form 7][3] существует огромное количество. Поэтому здесь я его описывать не буду. А коснусь вопроса &#8211; как подключить уже созданную форму в WordPress.

#### Код формы Easy FancyBox в шаблон

Если готовая форма **встраивается непосредственно в шаблон**, то код должен быть таким:

{% highlight html %}
  <a class="fancybox" href="#contact_form_pop">Контактная форма</a>

  <div class="fancybox-hidden" style="display:none">
    <div id="contact_form_pop">
      <?php echo do_shortcode('[contact-form-7 id="" title=""]'); ?>
    </div>
  </div>
{% endhighlight %}

Обратите внимание на конструкцию `<?php echo do_shortcode(''); ?>`, в которую вставлен shortcode, созданный в плагине Contact Form 7.

#### Код формы Easy FancyBox на страницу

Если готовая форма **встраивается в запись или на страницу**, то код должен быть таким:

{% highlight html %}
  <a class="fancybox" href="#contact_form_pop">Контактная форма</a>

  <div class="fancybox-hidden" style="display:none">
    <div id="contact_form_pop">
      [contact-form-7 id="" title=""]
    </div>
  </div>
{% endhighlight %}

Здесь shortcode вставляется &#8220;как есть&#8221; &#8211; как его создал плагин Contact Form 7.

#### Код формы Easy FancyBox в виджет

Готовую форму можно встраивать в виджет, но для этого сначала нужно **включить поддержку shortcode** в WordPress. Для этого в файле `functions.php` нужно добавить строку:

{% highlight php %}
  add_filter('widget_text', 'do_shortcode');
{% endhighlight %}

Теперь виджет &#8220;Текст&#8221; имеет поддержку shortcode и **вставить готовую форму в виджет** &#8220;Текст&#8221; нужно таким образом:

{% highlight html %}
  <a class="fancybox" href="#contact_form_pop">Контактная форма</a>

  <div class="fancybox-hidden" style="display:none">
    <div id="contact_form_pop">
      [contact-form-7 id="" title=""]
    </div>
  </div>
{% endhighlight %}

Здесь shortcode вставляется точно также &#8211; без изменений, как есть из плагина Contact Form 7.

Все три способа были &#8220;подсмотрены&#8221; мною здесь &#8211; &#8220;[Контактная форма (Contact Form 7) во всплывающем окне][4]&#8220;.

### Модальное окно Easy FancyBox не работает

Перехожу ко второму вопросу &#8211; все настроено, но ничего не работает. Такое было у меня и было связано с тем, что мною была сверстана и создана тема под Worpdress с нуля.

Проблема заключалась в том, что я &#8220;забыл&#8221; добавить в созданную тему две функции, которые **обязательно должны присутствовать** в любой WordPress-теме &#8211; `wp_head();` и `wp_footer();`.

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

 [1]: http://localhost:7788/third/wp-content/uploads/2014/12/modal_window.jpg
 [2]: https://wordpress.org/plugins/easy-fancybox/ "Easy FancyBox"
 [3]: http://contactform7.com/ "Contact Form 7"
 [4]: http://web.warwolf.org/kontaktnaya-forma-contact-form-7-vo-vsplyvayushhem-o/ "Контактная форма (Contact Form 7) во всплывающем окне"