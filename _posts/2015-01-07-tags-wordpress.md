---
title: Теги шаблона WordPress
author: gearmobile
layout: post
permalink: /tags-wordpress/
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
categories:
  - CMS WordPress
tags:
  - tag wordpress
---
> Наверное, это очередная бестолковая вещь, которую мои руки так и чешутся сделать. <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

И раз у меня есть на это время и нет сил на что-либо еще, то тогда уж точно &#8211; напишу! “О чем?” &#8211; может спросить уважаемый читатель. О тегах WordPress!

“О Боже!” &#8211; это в полном праве может сказать читатель &#8211; “&#8230; но ведь есть же <a href="http://codex.wordpress.org/" title="Codex WordPress" target="_blank">Кодекс WordPress</a>! Зачем еще?!”

Ну что же &#8211; очень и очень резонно! В качестве оправдания могу лишь привести две вещи.

**Первая причина** &#8211; из огромного количества тегов WordPress на практике используется лишь малая их часть. И вот здесь я хотел бы собрать воедино как раз те, которые используются.

Более того, могу сказать, что пользуясь лишь перечисленным ниже списком, я уже успел создать две вполне себе работающих темы под WordPress. Конечно, эти две темы простенькие, но факт остается фактом.

**Вторая причина** &#8211; я так быстрее запомню все эти теги WordPress <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

Итак &#8211; ниже представлен список “практичных” тегов WordPress с их кратким описанием. Все теги условно мною разбиты на области их применения в теме WordPress.

#### Теги шаблона WordPress

Выводит название сайта:

<pre><?php bloginfo(‘name’); ?></pre>

Выводит описание сайта:

<pre><?php bloginfo(‘description’); ?></pre>

Возвращает ссылку на главную страницу сайта:

<pre><?php bloginfo(‘url’); ?></pre>

Возвращает кодировку сайта (под WordPress это всегда utf–8):

<pre><?php bloginfo(‘charset’); ?></pre>

Также возвращает ссылку на главную страницу сайта:

<pre><?php echo get_home_url(); ?></pre>

Возвращает путь к файлу стилей style.css темы WordPress (*устарело и не рекомендуется использовать*):

<pre><?php bloginfo(’stylesheet_url’); ?></pre>

Возвращает путь к текущей теме WordPress:

<pre><?php bloginfo(‘template_url’); ?></pre>

Также возвращает путь к текущей теме WordPress:

<pre><?php echo get_directory_template_uri(); ?></pre>

Возвращает язык сайта (страницы):

<pre><?php language_attributes(); ?></pre>

Возвращает e-mail администратора сайта:

<pre><?php bloginfo(‘admin_email’); ?></pre>

Возвращает заголовок просматриваемой статьи или записи:

<pre><?php wp_title(); ?></pre>

Подключить файл шаблона header.php:

<pre><?php get_header(); ?></pre>

Подключить файл шаблона sidebar.php:

<pre><?php get_sidebar(); ?></pre>

Подключить файл шаблона footer.php:

<pre><?php get_footer(); ?></pre>

Запуск action в шапке и подвале страницы, обе функции необходимы для правильной работы некоторых плагинов и всей темы WordPress в целом:

<pre><?php wp_head(); ?></pre>

&#8211; помещается перед тегом 

<pre><?php wp_footer(); ?></pre>

&#8211; помещается перед тегом 

Подключить файл шаблона комментариев:

<pre><?php comments_template(); ?></pre>

Вывод текущего года в шаблоне WordPress:

<pre><?php echo date(‘Y’); ?></pre>

#### Теги записи WordPress

Выводит *заголовок* текущей страницы или записи:

<pre><?php the_title(); ?></pre>

Возвращает *ссылку* на текущую страницу или запись:

<pre><?php the_permalink(); ?></pre>

Выводит *отрывок* (цитату) записи с помещением в конец этой цитаты символов \[…\] (может существовать только внутри цикла loop):

<pre><?php the_excerpt(); ?></pre>

Выводит *полное содержимое* (весь текст) текущей записи (может существовать только внутри цикла loop):

<pre><?php the_content(); ?></pre>

Выводит *имя автора* записи:

<pre><?php the_author(); ?></pre>

Выводит *время* (дату) публикации текущей записи:

<pre><?php the_time(); ?></pre>

*Стандартный цикл* loop для вывода записей в шаблоне WordPress:

<pre><?php if(have_posts()) : while(have_posts()) : the_post(); ?>
		

<?php endwhile; ?>
	

<?php endif; ?>
</pre>

Расширенный пример (*показанного выше*) стандартного цикла loop, который может послужить в качестве *миниатюрного шаблона*:

<pre><?php if(have_posts()) : ?>
		

<?php while(have_posts()) : the_post(); ?>
			

<a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
			

<?php the_content(); ?>
		

<?php endwhile; ?>
	

<?php endif; ?>
</pre>

Возвращает ссылку на *предыдущую запись*:

<pre><?php previous_post_link(); ?></pre>

Возвращает ссылку на *следующую запись*:

<pre><?php next_post_link(); ?></pre>

Вывести *теги* записи (может существовать только внутри цикла loop):

<pre><?php the_tags(); ?></pre>

Вывести ссылку на *комментарии* к записи (может существовать только внутри цикла loop):

<pre><?php comments_popup_link(); ?></pre>

Вывести *миниатюру* записи внутри самой записи:

<pre><?php the_post_thumbnail(); ?></pre>

Вывод *миниатюры по умолчанию*, если не задана другая миниатюра:

<pre><?php if(has_post_thumbnail()): ?>
  

<?php the_post_thumbnail(); ?>


<?php else: ?>
  &lt;img src=“

<?php bloginfo(‘template_url’); ?>/images/image.jpg” alt=“Image”>


<?php endif; ?>
</pre>

Вывести (создать) *постраничную навигацию* (пагинация):

<pre><?php posts_nav_link(); ?></pre>

Подключить виджет в шаблоне WordPress:

<pre><?php if(!dynamic_sidebar(‘идентификатор виджета’)) : ?>


<?php endif; ?>
</pre>

#### Функции файла functions.php

Поставить на загрузку файл js-скриптов:

<pre>wp_enqueue_script();</pre>

Поставить на загрузку файл CSS-стилей:

<pre>wp_enqueue_style();</pre>

Пример функции для загрузки скриптов и стилей:

<pre>function load_scripts_and_styles(){
	wp_enqueue_script(‘jquery_custom’,get_directory_template_uri().’/js/my-jquery.js’);
	wp_enqueue_script(‘js_custom’,get_directory_template_uri().‘/js/my-js.js’);
	wp_enqueue_style(’style’,get_directory_template_uri().’/style.css’);
}

	add_action(‘wp_enqueue_scripts’,’load_scripts_and_styles’);
</pre>

Зарегистрировать новую панель под виджеты в шаблоне WordPress:

<pre>register_sidebar()
  ‘name’ => ’имя новой панели’,
  ‘id’ => ‘идентификатор новой панели’,
  ‘description’ => ‘описание новой панели’,
  ‘before_widget’ => ‘’,
  ‘after_widget’ => ‘’,
  ‘before_title’ => ‘’,
  ‘after_title’ => ‘’
</pre>

Включить возможность применения миниатюр в шаблоне WordPress:

<pre>add_theme_support(‘post-thumbnails’);</pre>

Установить размер миниатюр в шаблоне по умолчанию:

<pre>set_post_thumbnail_size($width,$height);</pre>

Шаблон с метаданными темы WordPress:

<pre>/*
  Theme Name: Имя темы
  Theme URI: Домашняя страница темы
  Description: Краткое описание темы
  Author: Имя автора темы
  Author URI: Домашняя страница автора темы
  Version: Номер версии темы
*/
</pre>

Будет дополняться (*возможно*) &#8230;

Оцените статью:  
<span id="post-ratings-2177" class="post-ratings" data-nonce="18deafd013"><img id="rating_2177_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(2177, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2177_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(2177, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2177_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(2177, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2177_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(2177, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_2177_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(2177, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_2177_text"></span></span><span id="post-ratings-2177-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>