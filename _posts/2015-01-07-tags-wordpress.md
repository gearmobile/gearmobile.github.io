---
title: "Теги шаблона WordPress"
layout: post
share: true
tags: [wordpress, tag]
---
> Наверное, это очередная бестолковая вещь, которую мои руки так и чешутся сделать.

И раз у меня есть на это время и нет сил на что-либо еще, то тогда уж точно - напишу! “О чем?" - может спросить уважаемый читатель. О тегах WordPress!

"О Боже!" - это в полном праве может сказать читатель - но ведь есть же [Кодекс WordPress][1]! Зачем еще?!"

Ну что же - очень и очень резонно! В качестве оправдания могу лишь привести две вещи.

**Первая причина** - из огромного количества тегов WordPress на практике используется лишь малая их часть. И вот здесь я хотел бы собрать воедино как раз те, которые используются.

Более того, могу сказать, что пользуясь лишь перечисленным ниже списком, я уже успел создать две вполне себе работающих темы под WordPress. Конечно, эти две темы простенькие, но факт остается фактом.

**Вторая причина** - я так быстрее запомню все эти теги WordPress.

Итак - ниже представлен список "практичных" тегов WordPress с их кратким описанием. Все теги условно мною разбиты на области их применения в теме WordPress.

### Теги шаблона WordPress

Выводит название сайта:

~~~ php
<?php bloginfo('name'); ?>
~~~

Выводит описание сайта:

~~~ php
<?php bloginfo('description'); ?>
~~~

Возвращает ссылку на главную страницу сайта:

~~~ php
<?php bloginfo('url'); ?>
~~~

Возвращает кодировку сайта (под WordPress это всегда utf–8):

~~~ php
<?php bloginfo('charset'); ?>
~~~

Также возвращает ссылку на главную страницу сайта:

~~~ php
<?php echo get_home_url(); ?>
~~~

Возвращает путь к файлу стилей style.css темы WordPress (*устарело и не рекомендуется использовать*):

~~~ php
<?php bloginfo('stylesheet_url'); ?>
~~~

Возвращает путь к текущей теме WordPress:

~~~ php
<?php bloginfo('template_url'); ?>
~~~

Также возвращает путь к текущей теме WordPress:

~~~ php
<?php echo get_directory_template_uri(); ?>
~~~

Возвращает язык сайта (страницы):

~~~ php
<?php language_attributes(); ?>
~~~

Возвращает e-mail администратора сайта:

~~~ php
<?php bloginfo('admin_email'); ?>
~~~

Возвращает заголовок просматриваемой статьи или записи:

~~~ php
<?php wp_title(); ?>
~~~

Подключить файл шаблона header.php:

~~~ php
<?php get_header(); ?>
~~~

Подключить файл шаблона sidebar.php:

~~~ php
<?php get_sidebar(); ?>
~~~

Подключить файл шаблона footer.php:

~~~ php
<?php get_footer(); ?>
~~~

Запуск action в шапке и подвале страницы, обе функции необходимы для правильной работы некоторых плагинов и всей темы WordPress в целом:

~~~ php
<?php wp_head(); ?>
~~~

- помещается перед тегом

~~~ php
<?php wp_footer(); ?>
~~~

- помещается перед тегом

Подключить файл шаблона комментариев:

~~~ php
<?php comments_template(); ?>
~~~

Вывод текущего года в шаблоне WordPress:

~~~ php
<?php echo date('Y'); ?>
~~~

### Теги записи WordPress

Выводит *заголовок* текущей страницы или записи:

~~~ php
<?php the_title(); ?>
~~~

Возвращает *ссылку* на текущую страницу или запись:

~~~ php
<?php the_permalink(); ?>
~~~

Выводит *отрывок* (цитату) записи с помещением в конец этой цитаты символов \[…\] (может существовать только внутри цикла loop):

~~~ php
<?php the_excerpt(); ?>
~~~

Выводит *полное содержимое* (весь текст) текущей записи (может существовать только внутри цикла loop):

~~~ php
<?php the_content(); ?>
~~~

Выводит *имя автора* записи:

~~~ php
<?php the_author(); ?>
~~~

Выводит *время* (дату) публикации текущей записи:

~~~ php
<?php the_time(); ?>
~~~

*Стандартный цикл* loop для вывода записей в шаблоне WordPress:

~~~ php
<?php if(have_posts()) : while(have_posts()) : the_post(); ?>
  <?php endwhile; ?>
<?php endif; ?>
~~~

Расширенный пример (*показанного выше*) стандартного цикла loop, который может послужить в качестве *миниатюрного шаблона*:

~~~ php
<?php if(have_posts()) : ?>
  <?php while(have_posts()) : the_post(); ?>
    <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
    <?php the_content(); ?>
  <?php endwhile; ?>
<?php endif; ?>
~~~

Возвращает ссылку на *предыдущую запись*:

~~~ php
<?php previous_post_link(); ?>
~~~

Возвращает ссылку на *следующую запись*:

~~~ php
<?php next_post_link(); ?>
~~~

Вывести *теги* записи (может существовать только внутри цикла loop):

~~~ php
<?php the_tags(); ?>
~~~

Вывести ссылку на *комментарии* к записи (может существовать только внутри цикла loop):

~~~ php
<?php comments_popup_link(); ?>
~~~

Вывести *миниатюру* записи внутри самой записи:

~~~ php
<?php the_post_thumbnail(); ?>
~~~

Вывод *миниатюры по умолчанию*, если не задана другая миниатюра:

~~~ php
<?php if(has_post_thumbnail()): ?>
  <?php the_post_thumbnail(); ?>
  <?php else: ?>
    <img src="<?php bloginfo('template_url'); ?>/images/image.jpg" alt="Image">
<?php endif; ?>
~~~

Вывести (создать) *постраничную навигацию* (пагинация):

~~~ php
<?php posts_nav_link(); ?>
~~~

Подключить виджет в шаблоне WordPress:

~~~ php
<?php if(!dynamic_sidebar('идентификатор виджета')) : ?>
<?php endif; ?>
~~~

### Функции файла functions.php

Поставить на загрузку файл js-скриптов:

~~~ php
wp_enqueue_script();
~~~

Поставить на загрузку файл CSS-стилей:

~~~ php
wp_enqueue_style();
~~~

Пример функции для загрузки скриптов и стилей:

~~~ php
function load_scripts_and_styles(){
	wp_enqueue_script('jquery_custom',get_directory_template_uri().'/js/my-jquery.js');
	wp_enqueue_script('js_custom',get_directory_template_uri().'/js/my-js.js');
	wp_enqueue_style('style',get_directory_template_uri().'/style.css');
}
add_action('wp_enqueue_scripts','load_scripts_and_styles');
~~~

Зарегистрировать новую панель под виджеты в шаблоне WordPress:

~~~ php
register_sidebar()
  'name' => 'имя новой панели',
  'id' => 'идентификатор новой панели',
  'description' => 'описание новой панели',
  'before_widget' => '',
  'after_widget' => '',
  'before_title' => '',
  'after_title' => ''
~~~

Включить возможность применения миниатюр в шаблоне WordPress:

~~~ php
add_theme_support('post-thumbnails');
~~~

Установить размер миниатюр в шаблоне по умолчанию:

~~~ php
set_post_thumbnail_size($width,$height);
~~~

Шаблон с метаданными темы WordPress:

~~~ php
/*
  Theme Name: Имя темы
  Theme URI: Домашняя страница темы
  Description: Краткое описание темы
  Author: Имя автора темы
  Author URI: Домашняя страница автора темы
  Version: Номер версии темы
*/
~~~

Будет дополняться (*возможно*).

[1]: http://codex.wordpress.org/ "Codex WordPress"

----