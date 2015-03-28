---
title: "ArchLinux - кратко о загрузчике SLiM"
layout: post
categories: linux
share: true
tags: [archlinux, slim]
---

## Установка загрузчика SLiM в ArchLinux

> Краткий обзор конфигурационного файла. Команды включения, перезагрузки и выключения системы через SLim.

Установка в ArchLinux стандартная:

{% highlight powershell %}
$ sudo pacman -S slim
{% endhighlight %}

После успешной установки нужно отредактировать файл `/etc/rc.conf`. Если до этого в системе стоял GDM, можно удалить его, а можно закомментировать `gdm` и добавить `slim` в строку:

{% highlight powershell %}
DAEMONS=(@syslog-ng cpufreq laptop-mode @network @net-profiles hal ntpd fam !gdmslim !netfs gpm @crond alsa)
{% endhighlight %}

Поведение SLiM настраивается через конфигурационный файл `/etc/slim.conf`.

## Наиболее полезные параметры

  * `default_user simone` - Если строка раскомментирована и выставлено имя пользователя в качестве ее значения, то поле `username` заполняется автоматически при входе в SLiM.
  * `focus_password no` - Параметр связан с параметром default_user. Активируется, если задействован параметр `default_user`. В этом случае фокус автоматически устанавливается в поле `password`.
  * `auto_login no` - Автоматический вход в систему пользователя по умолчанию, указанного в параметре `default_user`. Для включения этой опции нужно выставить его значение на `yes`.
  * `current_theme ArchLinux-simplyblack` - Тема экрана приветствия SLiM. Все темы располагаются по адресу `/usr/share/slim/themes/`.
  * `shutdown_msg The system is halting` - Сообщение, выводимое на экран при выключении компьютера.
  * `reboot_msg The system is rebooting` - Сообщение, выводимое на экран при перезагрузке компьютера.
  * `welcome_msg Welcome to %host` - Сообщение-приветствие на экране.
  * `screenshot_cmd import -window root /slim.png` - Создание скриншота экрана SLiM. Действие команды привязано к клавише F11 клавиатуры.
  * `sessions xfce4,icewm,wmaker,blackbox` - Выбор сессии для запуска X-ов. То есть, если в системе стоят несколько WindowManager'ов или DE, как например - Xfce, KDE, GNOME, Openbox и т. д., все они указываются через запятую в качестве значения параметра `sessions`. Первый в списке является значением по-умолчанию. Для выбора нужного графического окружения при входе в SLiM нужно нажать клавишу F1. Параметр связан с командой `login_cmd`. Значение параметра sessions подставляется в качестве переменной %session.

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

  * `login_cmd exec /bin/bash -login ~/.xinitrc %session` - Команда, выполняемая при успешном входе в систему (правильного ввода пары логинпароль). Стоит обратить внимание, что если в системе не установлен `bash` в качестве `shell`'а, то следует заменить значение `/bin/bash` на тот `shell`, который используется в системе. Например, в FreeBSD нужно выставить `/bin/sh` вместо `/bin/bash`. Также можно добавить в строку переменную `%theme` для задания определенной темы SLiM при его старте.
  * `halt_cmd /sbin/shutdown -h now` - Команда выключения компьютера из SLiM.
  * `reboot_cmd /sbin/shutdown -r now` - Команда перезагрузки компьютера из SLiM.
  * `console_cmd /usr/bin/xterm -C -fg white -bg black +sb -T "Console login" -e /bin/sh -c "/bin/cat /etc/issue; exec /bin/login"` - Запуск терминала консоли прямо из SLiM. Можно задать предпочитаемый эмулятор терминала, заменив xterm на свое, например, gnome-terminal, rxvt, aterm, mrxvt, materm, wterm, gnome-multi-terminal, eterm, rxvt-unicode (urxvt), mlterm, mliterm.
  * `susliend_cmd /usr/sbin/susliend` - Команда перевода компьютера в спящий режим из SLiM.
  * `numlock on` - Включение-отключение NumLock клавиатуры при запуске SLiM. Возможные значения параметра - `on` (включена), `off` (выключена).
  * `hidecursor false` - Скрыть-показать курсор при вводе логинапароля. Возможные значения параметра - `true|false`.

## Полезные команды SLiM

Для остановки, перезагрузки, перевода в спящий режим компьютера или запуска эмулятора терминала из SLiM используются команды, представленные ниже.

Правильный порядок ввода их следующий:

  * в поле `username` вводим команду (например, `halt`)
  * в поле `password` вводим пароль `root`'а.

Команды:

  1. Запуск эмулятора терминала - команда `console`;
  2. Выключение компьютера - команда `halt`;
  3. Перезагрузка компьютера - команда `reboot`;
  4. Перевод компьютера в спящий режим - команда `susliend`;
  5. Перейти в консоль - команда `exit`.

---
