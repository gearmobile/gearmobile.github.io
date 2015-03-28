---
title: "ArchLinux - установка и настройка тем в SLiM"
layout: post
categories: linux
tags: [slim]
share: true
---

> Установка и настройка загрузчика SLiM операционной системы ArchLinux.

Почему именно этот загрузчик? Потому что он полностью отвечает философии этой системы - прост, легок, минимален в настройках. И к тому же красив. Это хорошая альтернатива стандартному `gdm`.

Дефолтная тема имеет вид:

![Default SLiM Theme]({{site.url}}/images/uploads/2013/11/default_slim.png)

Тема состоит из **трех файлов**:

  * фоновая картинка (background image), может быть формата .png или .jpg;
  * картинка панели (panel image), также формата .png или .jpg;
  * строка ввода (input box) и приветствие (slim.theme).

Имеется возможность самому править готовые темы. В репозиториях ArchLinux имеются сборки тем.

Посмотрим их:

{% highlight powershell %}
$ sudo pacman -Ss slim themes
  extra/archlinux-themes-slim 1.2-1
  Arch Linux themes for the SLiM login manager
  extra/slim-themes 1.2.3-3
  Themes Pack for Simple Login Manager
{% endhighlight %}

Установка этих тем стандартная для Arch:

{% highlight powershell %}
$ sudo pacman -S archlinux-themes-slim slim-themes
{% endhighlight %}

Все темы автоматически распаковываются в директорию `/usr/share/slim/themes/`.

{% highlight powershell %}
$ ls /usr/share/slim/themes/
  archlinux-darch-grey archlinux-simplyblack debian-moreblue flat lake parallel-dimensions rear-window wave
  archlinux-darch-white archlinux-soft-grey default flower2 lunar previous scotland-road zenwalk
  archlinux-retro capernoited fingerprint mindlock rainbow subway
{% endhighlight %}

SLiM поддерживает сторонние темы. Для установки таких тем сперва нужно скачать ее, а затем распаковать в директорию с темами. Все темы находятся по пути `/usr/share/slim/themes/`.

### Пример установки сторонней темы

1. Скачиваем понравившуюся по ссылке, указанной на домашней странице проекта - `slim.berlios.de/themes`. Пусть это будет тема `10th birthday of Gentoo (Blue)`.

2. Создаем для скачанной темы папку `gentoo_blue` по пути `/usr/share/slim/themes/`:

{% highlight powershell %}
$ sudo mkdir /usr/share/slim/themes/gentoo_blue
{% endhighlight %}

3. Распаковываем туда архив темы:

{% highlight powershell %}
$ sudo tar xjvf ~/Downloads/gentoo_10_blue.tar.bz2 -C /usr/share/slim/themes/gentoo_blue/
  background.jpg
  panel.png
  slim.theme
{% endhighlight %}

4. Проверяем, туда ли все распаковалось:

{% highlight powershell %}
$ ls /usr/share/slim/themes/gentoo_blue/
  background.jpg panel.png slim.theme
{% endhighlight %}

5. Теперь открываем конфигурационный файл SLiM, находящийся по адресу `/etc/slim.conf`:

{% highlight powershell %}
$ sudo nano -w /etc/slim.conf
{% endhighlight %}

6. Находим в конце файла строки:

{% highlight powershell %}
# current theme, use comma separated list to specify a set to
# randomly choose from
current_theme default
{% endhighlight %}

и меняем значение строки `current_theme` с `default` на название папки со скачаной и распакованной темой, то есть, в нашем случае это папка `gentoo_blue`:

{% highlight powershell %}
# current theme, use comma separated list to specify a set to
# randomly choose from
current_theme gentoo_blue
{% endhighlight %}

7. Сохраняем результат и выходим из редактора. Перезагружаемся и видим результат:

![Gentoo SLiM Theme]({{site.url}}/images/uploads/2013/11/gentoo_slim.png)

Скриншот экрана приветствия\входа в систему можно сделать, нажав кнопочку <kbd>F11</kbd>kbd>. Скрин будет сохранен в формате `.png` с именем `slim` в корневой папке:

{% highlight powershell %}
$ ls /slim.png
  /slim.png
{% endhighlight %}

Для создания скриншота необходимо наличие в системе пакета `imagemagick`.

## P.S.

Можно настроить так, чтобы тема выбиралась случайно из набора. Для этого нужно в конфигурационном файле `/etc/slim.conf` в строке `current_theme` прописать через запятую список тех тем, которые мы хотим видеть.

Например, так:

{% highlight powershell %}
  # current theme, use comma separated list to specify a set to
  # randomly choose from
  current_theme archlinux-simplyblack,archlinux-soft-grey,archlinux-darch-grey,archlinux-darch-white,archlinux-retro
{% endhighlight %}

---