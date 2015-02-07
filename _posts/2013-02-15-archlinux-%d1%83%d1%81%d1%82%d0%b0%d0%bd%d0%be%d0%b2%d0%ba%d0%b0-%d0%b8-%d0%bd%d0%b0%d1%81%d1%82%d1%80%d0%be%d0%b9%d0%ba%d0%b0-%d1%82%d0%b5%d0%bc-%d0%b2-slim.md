---
title: 'ArchLinux &#8211; установка и настройка тем в SLiM'
author: gearmobile
layout: post
permalink: /archlinux-%d1%83%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%ba%d0%b0-%d0%b8-%d0%bd%d0%b0%d1%81%d1%82%d1%80%d0%be%d0%b9%d0%ba%d0%b0-%d1%82%d0%b5%d0%bc-%d0%b2-slim/
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
cleanretina_sidebarlayout:
  - default
categories:
  - OS Linux
tags:
  - slim
---
Установка и настройка загрузчика SLiM операционной системы Archlinux. Почему именно этот загрузчик? Потому что он полностью отвечает философии этой системы &#8211; прост, легок, минимален в настройках. И к тому же красив. Это хорошая альтернатива стандартному gdm. Дефолтная тема имеет вид:<figure id="attachment_548" style="width: 500px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/default_slim.png" alt="Default SLiM Theme" width="500" height="312" class="size-full wp-image-548" />][1]<figcaption class="wp-caption-text">Default SLiM Theme</figcaption></figure> 

Тема состоит из трех файлов:</p> 

  * фоновая картинка (background image), может быть формата .png или .jpg;
  * картинка панели (panel image), также формата .png или .jpg;
  * строка ввода (input box) и приветствие (slim.theme).

Имеется возможность самому править готовые темы. Про тонкую настройку можно почитать здесь &#8211; SLiM Themes HowTo.

В репозиториях Archlinux имеются сборки тем.

Посмотрим их:

<pre>$ sudo pacman -Ss slim themes
  extra/archlinux-themes-slim 1.2-1
  Arch Linux themes for the SLiM login manager
  extra/slim-themes 1.2.3-3
  Themes Pack for Simple Login Manager</pre>

Установка этих тем стандартная для Arch:

<pre>$ sudo pacman -S archlinux-themes-slim slim-themes</pre>

Все темы автоматически распаковываются в директорию /usr/share/slim/themes/.

<pre>$ ls /usr/share/slim/themes/
  archlinux-darch-grey archlinux-simplyblack debian-moreblue flat lake parallel-dimensions rear-window wave
  archlinux-darch-white archlinux-soft-grey default flower2 lunar previous scotland-road zenwalk
  archlinux-retro capernoited fingerprint mindlock rainbow subway</pre>

SLiM поддерживает сторонние темы. Для установки таких тем сперва нужно скачать ее, а затем распаковать в директорию с темами. Все темы находятся по пути /usr/share/slim/themes/.

### Пример установки сторонней темы

1. Скачиваем понравившуюся по ссылке, указанной на домашней странице проекта &#8211; slim.berlios.de/themes. Пусть это будет тема 10th birthday of Gentoo (Blue).

2. Создаем для скачанной темы папку gentoo_blue по пути /usr/share/slim/themes/:

<pre>$ sudo mkdir /usr/share/slim/themes/gentoo_blue</pre>

3. Распаковываем туда архив темы:

<pre>$ sudo tar xjvf ~/Downloads/gentoo_10_blue.tar.bz2 -C /usr/share/slim/themes/gentoo_blue/
  background.jpg
  panel.png
  slim.theme</pre>

4. Проверяем, туда ли все распаковалось:

<pre>$ ls /usr/share/slim/themes/gentoo_blue/
  background.jpg panel.png slim.theme</pre>

5. Теперь открываем конфигурационный файл SLiM, находящийся по адресу /etc/slim.conf:

<pre>$ sudo nano -w /etc/slim.conf</pre>

6. Находим в конце файла строки:

<pre># current theme, use comma separated list to specify a set to
  # randomly choose from
  current_theme default</pre>

и меняем значение строки current\_theme с default на название папки со скачаной и распакованной темой, то есть, в нашем случае это папка gentoo\_blue:

<pre># current theme, use comma separated list to specify a set to
  # randomly choose from
  current_theme gentoo_blue</pre>

7. Сохраняем результат и выходим из редактора. Перезагружаемся и видим результат:<figure id="attachment_549" style="width: 500px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/gentoo_slim.png" alt="Gentoo SLiM Theme" width="500" height="312" class="size-full wp-image-549" />][2]<figcaption class="wp-caption-text">Gentoo SLiM Theme</figcaption></figure> 

Скриншот экрана приветствия\входа в систему можно сделать, нажав кнопочку F11. Скрин будет сохранен в формате .png с именем slim в корневой папке:

<pre>$ ls /slim.png
  /slim.png</pre>

Для создания скриншота необходимо наличие в системе пакета imagemagick.

P.S.

Можно настроить так, чтобы тема выбиралась случайно из набора. Для этого нужно в конфигурационном файле /etc/slim.conf в строке current_theme прописать через запятую список тех тем, которые мы хотим видеть. Например, так:

<pre># current theme, use comma separated list to specify a set to
  # randomly choose from
  current_theme archlinux-simplyblack,archlinux-soft-grey,archlinux-darch-grey,archlinux-darch-white,archlinux-retro</pre>

Оцените статью:  
<span id="post-ratings-547" class="post-ratings" data-nonce="e7746a730c"><img id="rating_547_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(547, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_547_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(547, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_547_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(547, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_547_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(547, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_547_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(547, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_547_text"></span></span><span id="post-ratings-547-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/default_slim.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/gentoo_slim.png