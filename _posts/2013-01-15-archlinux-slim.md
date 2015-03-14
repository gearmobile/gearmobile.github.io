---
layout: post
title: "ArchLinux &#8211; кратко о загрузчике SLiM"
author: gearmobile
---
Установка загрузчика SLiM в Archlinux. Краткий обзор конфигурационного файла. Команды включения, перезагрузки и выключения системы через SLim.

Установка в Archlinux стандартная:

{% highlight powershell %}
  $ sudo pacman -S slim
{% endhighlight %}

После успешной установки нужно отредактировать файл /etc/rc.conf. Если до этого в системе стоял GDM, можно удалить его, а можно закомментировать gdm и добавить slim в строку:

{% highlight powershell %}
  DAEMONS=(@syslog-ng cpufreq laptop-mode @network @net-profiles hal ntpd fam !gdmslim !netfs gpm @crond alsa)
{% endhighlight %}

Поведение SLiM настраивается через конфигурационный файл `/etc/slim.conf`.

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

После конфигурирования `/etc/slim.conf` нужно отредактировать файл `~/.xinit` следующим образом:

{% highlight powershell %}
DEFAULT_SESSION="gnome"
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
  esac
{% endhighlight %}

  * login_cmd exec /bin/bash -login ~/.xinitrc %session &#8211; Команда, выполняемая при успешном входе в систему (правильного ввода пары логинпароль). Стоит обратить внимание, что если в системе не установлен bash в качестве shell&#8217;а, то следует заменить значение /bin/bash на тот shell, который используется в системе. Например, в FreeBSD нужно выставить /bin/sh вместо /bin/bash. Также можно добавить в строку переменную %theme для задания определенной темы SLiM при его старте.
  * halt_cmd /sbin/shutdown -h now &#8211; Команда выключения компьютера из SLiM.
  * reboot_cmd /sbin/shutdown -r now &#8211; Команда перезагрузки компьютера из SLiM.
  * console_cmd /usr/bin/xterm -C -fg white -bg black +sb -T &#8220;Console login&#8221; -e /bin/sh -c &#8220;/bin/cat /etc/issue; exec /bin/login&#8221; &#8211; Запуск терминала консоли прямо из SLiM. Можно задать предпочитаемый эмулятор терминала, заменив xterm на свое, например, gnome-terminal, rxvt, aterm, mrxvt, materm, wterm, gnome-multi-terminal, eterm, rxvt-unicode (urxvt), mlterm, mliterm.
  * susliend_cmd /usr/sbin/susliend &#8211; Команда перевода компьютера в спящий режим из SLiM.
  * numlock on &#8211; Включениеотключение NumLock клавиатуры при запуске SLiM. Возможные значения параметра &#8211; on (включена), off (выключена).
  * hidecursor false &#8211; Скрытьпоказать курсор при вводе логинапароля. Возможные значения параметра &#8211; true|false.

### Полезные команды SLiM

Для остановки, перезагрузки, перевода в спящий режим компьютера или запуска эмулятора терминала из SLiM используются команды, представленные ниже.

Правильный порядок ввода их следующий:

  * в поле username вводим команду (например, halt)
  * в поле password вводим пароль root&#8217;а.

Команды:

  1. Запуск эмулятора терминала &#8211; команда console;
  2. Выключение компьютера &#8211; команда halt;
  3. Перезагрузка компьютера &#8211; команда reboot;
  4. Перевод компьютера в спящий режим &#8211; команда susliend;
  5. Перейти в консоль &#8211; команда exit.
