---
title: 'ArchLinux &#8211; кратко о загрузчике SLiM'
author: gearmobile
layout: post
permalink: /archlinux-%d0%ba%d1%80%d0%b0%d1%82%d0%ba%d0%be-%d0%be-%d0%b7%d0%b0%d0%b3%d1%80%d1%83%d0%b7%d1%87%d0%b8%d0%ba%d0%b5-slim/
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
  - slim archlinux
---
Установка загрузчика SLiM в Archlinux. Краткий обзор конфигурационного файла. Команды включения, перезагрузки и выключения системы через SLim. Установка в Archlinux стандартная:

<pre>$ sudo pacman -S slim</pre>

После успешной установки нужно отредактировать файл /etc/rc.conf. Если до этого в системе стоял GDM, можно удалить его, а можно закомментировать gdm и добавить slim в строку:

<pre>DAEMONS=(@syslog-ng cpufreq laptop-mode @network @net-profiles hal ntpd fam !gdmslim !netfs gpm @crond alsa)</pre>

Поведение SLiM настраивается через конфигурационный файл /etc/slim.conf.

### Наиболее полезные параметры

  * default_user simone &#8211; Если строка раскомментирована и выставлено имя пользователя в качестве ее значения, то поле username заполняется автоматически при входе в SLiM.
  * focus\_password no &#8211; Параметр связан с параметром default\_user. Активируется, если задействован параметр default_user. В этом случае фокус автоматически устанавливается в поле password.
  * auto\_login no &#8211; Автоматический вход в систему пользователя по умолчанию, указанного в параметре default\_user. Для включения этой опции нужно выставить его значение на yes.
  * current_theme archlinux-simplyblack &#8211; Тема экрана приветствия SLiM. Все темы располагаются по адресу /usr/share/slim/themes/.
  * shutdown_msg The system is halting&#8230; &#8211; Сообщение, выводимое на экран при выключении компьютера.
  * reboot_msg The system is rebooting&#8230; &#8211; Сообщение, выводимое на экран при перезагрузке компьютера.
  * welcome_msg Welcome to %host &#8211; Сообщение-приветствие на экране.
  * screenshot_cmd import -window root /slim.png &#8211; Создание скриншота экрана SLiM. Действие команды привязано к клавише F11 клавиатуры.
  * sessions xfce4,icewm,wmaker,blackbox &#8211; Выбор сессии для запуска X-ов. То есть, если в системе стоят несколько WindowManager&#8217;ов или DE, как например &#8211; Xfce, KDE, GNOME, Openbox и т. д., все они указываются через запятую в качестве значения параметра sessions. Первый в списке является значением по-умолчанию. Для выбора нужного графического окружения при входе в SLiM нужно нажать клавишу F1. Параметр связан с командой login_cmd. Значение параметра sessions подставляется в качестве переменной %session.

После конфигурирования /etc/slim.conf нужно отредактировать файл ~/.xinit следующим образом:

<pre>DEFAULT_SESSION="gnome"
  case $1 in
  kde)
  exec startkde
  ;;
  xfce4)
  exec startxfce4
  ;;
  openbox)
  exec startopenbox
  ;;
  *)
  exec $DEFAULT_SESSION
  ;;
  esac</pre>

  * login_cmd exec /bin/bash -login ~/.xinitrc %session &#8211; Команда, выполняемая при успешном входе в систему (правильного ввода пары логинпароль). Стоит обратить внимание, что если в системе не установлен bash в качестве shell&#8217;а, то следует заменить значение /bin/bash на тот shell, который используется в системе. Например, в FreeBSD нужно выставить /bin/sh вместо /bin/bash. Также можно добавить в строку переменную %theme для задания определенной темы SLiM при его старте.
  * halt_cmd /sbin/shutdown -h now &#8211; Команда выключения компьютера из SLiM.
  * reboot_cmd /sbin/shutdown -r now &#8211; Команда перезагрузки компьютера из SLiM.
  * console_cmd /usr/bin/xterm -C -fg white -bg black +sb -T &#8220;Console login&#8221; -e /bin/sh -c &#8220;/bin/cat /etc/issue; exec /bin/login&#8221; &#8211; Запуск терминала консоли прямо из SLiM. Можно задать предпочитаемый эмулятор терминала, заменив xterm на свое, например, gnome-terminal, rxvt, aterm, mrxvt, materm, wterm, gnome-multi-terminal, eterm, rxvt-unicode (urxvt), mlterm, mliterm.
  * susliend_cmd /usr/sbin/susliend &#8211; Команда перевода компьютера в спящий режим из SLiM.
  * numlock on &#8211; Включениеотключение NumLock клавиатуры при запуске SLiM. Возможные значения параметра &#8211; on (включена), off (выключена).
  * hidecursor false &#8211; Скрытьпоказать курсор при вводе логинапароля. Возможные значения параметра &#8211; true|false.

### Полезные команды SLiM

Для остановки, перезагрузки, перевода в спящий режим компьютера или запуска эмулятора терминала из SLiM используются команды, представленные ниже. Правильный порядок ввода их следующий:

  * в поле username вводим команду (например, halt)
  * в поле password вводим пароль root&#8217;а.

Команды:</p> 

  1. Запуск эмулятора терминала &#8211; команда console;
  2. Выключение компьютера &#8211; команда halt;
  3. Перезагрузка компьютера &#8211; команда reboot;
  4. Перевод компьютера в спящий режим &#8211; команда susliend;
  5. Перейти в консоль &#8211; команда exit.

Оцените статью:  
<span id="post-ratings-543" class="post-ratings" data-nonce="2be405d121"><img id="rating_543_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(543, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_543_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(543, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_543_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(543, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_543_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(543, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_543_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(543, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_543_text"></span></span><span id="post-ratings-543-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>