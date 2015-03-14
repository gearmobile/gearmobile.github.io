---
title: Теги шаблона WordPress
author: gearmobile
layout: post
---
> Наверное, это очередная бестолковая вещь, которую мои руки так и чешутся сделать. <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

И раз у меня есть на это время и нет сил на что-либо еще, то тогда уж точно &#8211; напишу! “О чем?” &#8211; может спросить уважаемый читатель. О тегах WordPress!

“О Боже!” &#8211; это в полном праве может сказать читатель &#8211; “&#8230; но ведь есть же <a href="http://codex.wordpress.org/" title="Codex WordPress" target="_blank">Кодекс WordPress</a>! Зачем еще?!”

Ну что же &#8211; очень и очень резонно! В качестве оправдания могу лишь привести две вещи.

**Первая причина** &#8211; из огромного количества тегов WordPress на практике используется лишь малая их часть. И вот здесь я хотел бы собрать воедино как раз те, которые используются.

Более того, могу сказать, что пользуясь лишь перечисленным ниже списком, я уже успел создать две вполне себе работающих темы под WordPress. Конечно, эти две темы простенькие, но факт остается фактом.

**Вторая причина** &#8211; я так быстрее запомню все эти теги WordPress <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

Итак &#8211; ниже представлен список “практичных” тегов WordPress с их кратким описанием. Все теги условно мною разбиты на области их применения в теме WordPress.

### Теги шаблона WordPress

Выводит название сайта:

{% highlight php %}<?php bloginfo('name'); ?>{% endhighlight %}

Выводит описание сайта:

{% highlight php %}<?php bloginfo('description'); ?>{% endhighlight %}

Возвращает ссылку на главную страницу сайта:

{% highlight php %}<?php bloginfo('url'); ?>{% endhighlight %}

Возвращает кодировку сайта (под WordPress это всегда utf–8):

{% highlight php %}<?php bloginfo('charset'); ?>{% endhighlight %}

Также возвращает ссылку на главную страницу сайта:

{% highlight php %}<?php echo get_home_url(); ?>{% endhighlight %}

Возвращает путь к файлу стилей style.css темы WordPress (*устарело и не рекомендуется использовать*):

{% highlight php %}<?php bloginfo('stylesheet_url'); ?>{% endhighlight %}

Возвращает путь к текущей теме WordPress:

{% highlight php %}<?php bloginfo('template_url'); ?>{% endhighlight %}

Также возвращает путь к текущей теме WordPress:

{% highlight php %}<?php echo get_directory_template_uri(); ?>{% endhighlight %}

Возвращает язык сайта (страницы):

{% highlight php %}<?php language_attributes(); ?>{% endhighlight %}

Возвращает e-mail администратора сайта:

{% highlight php %}<?php bloginfo('admin_email'); ?>{% endhighlight %}

Возвращает заголовок просматриваемой статьи или записи:

{% highlight php %}<?php wp_title(); ?>{% endhighlight %}

Подключить файл шаблона header.php:

{% highlight php %}<?php get_header(); ?>{% endhighlight %}

Подключить файл шаблона sidebar.php:

{% highlight php %}<?php get_sidebar(); ?>{% endhighlight %}

Подключить файл шаблона footer.php:

{% highlight php %}<?php get_footer(); ?>{% endhighlight %}

Запуск action в шапке и подвале страницы, обе функции необходимы для правильной работы некоторых плагинов и всей темы WordPress в целом:

{% highlight php %}<?php wp_head(); ?>{% endhighlight %}

&#8211; помещается перед тегом

{% highlight php %}<?php wp_footer(); ?>{% endhighlight %}

&#8211; помещается перед тегом

Подключить файл шаблона комментариев:

{% highlight php %}<?php comments_template(); ?>{% endhighlight %}

Вывод текущего года в шаблоне WordPress:

{% highlight php %}<?php echo date('Y'); ?>{% endhighlight %}

### Теги записи WordPress

Выводит *заголовок* текущей страницы или записи:

{% highlight php %}<?php the_title(); ?>{% endhighlight %}

Возвращает *ссылку* на текущую страницу или запись:

{% highlight php %}<?php the_permalink(); ?>{% endhighlight %}

Выводит *отрывок* (цитату) записи с помещением в конец этой цитаты символов \[…\] (может существовать только внутри цикла loop):

{% highlight php %}<?php the_excerpt(); ?>{% endhighlight %}

Выводит *полное содержимое* (весь текст) текущей записи (может существовать только внутри цикла loop):

{% highlight php %}<?php the_content(); ?>{% endhighlight %}

Выводит *имя автора* записи:

{% highlight php %}<?php the_author(); ?>{% endhighlight %}

Выводит *время* (дату) публикации текущей записи:

{% highlight php %}<?php the_time(); ?>{% endhighlight %}

*Стандартный цикл* loop для вывода записей в шаблоне WordPress:

{% highlight php %}<?php if(have_posts()) : while(have_posts()) : the_post(); ?>


<?php endwhile; ?>


<?php endif; ?>
{% endhighlight %}

Расширенный пример (*показанного выше*) стандартного цикла loop, который может послужить в качестве *миниатюрного шаблона*:

{% highlight php %}<?php if(have_posts()) : ?>


<?php while(have_posts()) : the_post(); ?>


<a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>


<?php the_content(); ?>


<?php endwhile; ?>


<?php endif; ?>
{% endhighlight %}

Возвращает ссылку на *предыдущую запись*:

{% highlight php %}<?php previous_post_link(); ?>{% endhighlight %}

Возвращает ссылку на *следующую запись*:

{% highlight php %}<?php next_post_link(); ?>{% endhighlight %}

Вывести *теги* записи (может существовать только внутри цикла loop):

{% highlight php %}<?php the_tags(); ?>{% endhighlight %}

Вывести ссылку на *комментарии* к записи (может существовать только внутри цикла loop):

{% highlight php %}<?php comments_popup_link(); ?>{% endhighlight %}

Вывести *миниатюру* записи внутри самой записи:

{% highlight php %}<?php the_post_thumbnail(); ?>{% endhighlight %}

Вывод *миниатюры по умолчанию*, если не задана другая миниатюра:

{% highlight php %}<?php if(has_post_thumbnail()): ?>


<?php the_post_thumbnail(); ?>


<?php else: ?>
  &lt;img src=“

<?php bloginfo('template_url'); ?>/images/image.jpg” alt=“Image”>


<?php endif; ?>
{% endhighlight %}

Вывести (создать) *постраничную навигацию* (пагинация):

{% highlight php %}<?php posts_nav_link(); ?>{% endhighlight %}

Подключить виджет в шаблоне WordPress:

{% highlight php %}<?php if(!dynamic_sidebar('идентификатор виджета')) : ?>


<?php endif; ?>
{% endhighlight %}

### Функции файла functions.php

Поставить на загрузку файл js-скриптов:

{% highlight php %}wp_enqueue_script();{% endhighlight %}

Поставить на загрузку файл CSS-стилей:

{% highlight php %}wp_enqueue_style();{% endhighlight %}

Пример функции для загрузки скриптов и стилей:

{% highlight php %}function load_scripts_and_styles(){
	wp_enqueue_script('jquery_custom',get_directory_template_uri().'/js/my-jquery.js');
	wp_enqueue_script('js_custom',get_directory_template_uri().'/js/my-js.js');
	wp_enqueue_style('style',get_directory_template_uri().'/style.css');
}

	add_action('wp_enqueue_scripts','load_scripts_and_styles');
{% endhighlight %}

Зарегистрировать новую панель под виджеты в шаблоне WordPress:

{% highlight php %}register_sidebar()
  'name' => 'имя новой панели',
  'id' => 'идентификатор новой панели',
  'description' => 'описание новой панели',
  'before_widget' => '',
  'after_widget' => '',
  'before_title' => '',
  'after_title' => ''
{% endhighlight %}

Включить возможность применения миниатюр в шаблоне WordPress:

{% highlight php %}add_theme_support('post-thumbnails');{% endhighlight %}

Установить размер миниатюр в шаблоне по умолчанию:

{% highlight php %}set_post_thumbnail_size($width,$height);{% endhighlight %}

Шаблон с метаданными темы WordPress:

{% highlight php %}/*
  Theme Name: Имя темы
  Theme URI: Домашняя страница темы
  Description: Краткое описание темы
  Author: Имя автора темы
  Author URI: Домашняя страница автора темы
  Version: Номер версии темы
*/
{% endhighlight %}

Будет дополняться (*возможно*) &#8230;
