---
title: 'ArchLinux - кратко о загрузчике SLiM'
layout: post
categories: linux
share: true
tags: [archlinux, slim]
---

## Установка загрузчика SLiM в ArchLinux

> Краткий обзор конфигурационного файла. Команды включения, перезагрузки и выключения системы через SLim.

Установка в ArchLinux стандартная:

{% highlight powershell %}
\$ sudo pacman -S slim
{% endhighlight %}

После успешной установки нужно отредактировать файл _/etc/rc.conf_. Если до этого в системе стоял GDM, можно удалить его, а можно закомментировать _gdm_ и добавить _slim_ в строку:

{% highlight powershell %}
DAEMONS=(@syslog-ng cpufreq laptop-mode @network @net-profiles hal ntpd fam !gdmslim !netfs gpm @crond alsa)
{% endhighlight %}

Поведение SLiM настраивается через конфигурационный файл _/etc/slim.conf_.

## Наиболее полезные параметры

- _default_user simone_ - Если строка раскомментирована и выставлено имя пользователя в качестве ее значения, то поле _username_ заполняется автоматически при входе в SLiM.
- _focus_password no_ - Параметр связан с параметром default*user. Активируется, если задействован параметр \_default_user*. В этом случае фокус автоматически устанавливается в поле _password_.
- _auto_login no_ - Автоматический вход в систему пользователя по умолчанию, указанного в параметре _default_user_. Для включения этой опции нужно выставить его значение на _yes_.
- _current_theme ArchLinux-simplyblack_ - Тема экрана приветствия SLiM. Все темы располагаются по адресу _/usr/share/slim/themes/_.
- _shutdown_msg The system is halting_ - Сообщение, выводимое на экран при выключении компьютера.
- _reboot_msg The system is rebooting_ - Сообщение, выводимое на экран при перезагрузке компьютера.
- _welcome_msg Welcome to %host_ - Сообщение-приветствие на экране.
- _screenshot_cmd import -window root /slim.png_ - Создание скриншота экрана SLiM. Действие команды привязано к клавише F11 клавиатуры.
- _sessions xfce4,icewm,wmaker,blackbox_ - Выбор сессии для запуска X-ов. То есть, если в системе стоят несколько WindowManager'ов или DE, как например - Xfce, KDE, GNOME, Openbox и т. д., все они указываются через запятую в качестве значения параметра _sessions_. Первый в списке является значением по-умолчанию. Для выбора нужного графического окружения при входе в SLiM нужно нажать клавишу F1. Параметр связан с командой _login_cmd_. Значение параметра sessions подставляется в качестве переменной %session.

После конфигурирования _/etc/slim.conf_ нужно отредактировать файл _~/.xinit_ следующим образом:

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

- _login_cmd exec /bin/bash -login ~/.xinitrc %session_ - Команда, выполняемая при успешном входе в систему (правильного ввода пары логинпароль). Стоит обратить внимание, что если в системе не установлен _bash_ в качестве _shell_'а, то следует заменить значение _/bin/bash_ на тот _shell_, который используется в системе. Например, в FreeBSD нужно выставить _/bin/sh_ вместо _/bin/bash_. Также можно добавить в строку переменную _%theme_ для задания определенной темы SLiM при его старте.
- _halt_cmd /sbin/shutdown -h now_ - Команда выключения компьютера из SLiM.
- _reboot_cmd /sbin/shutdown -r now_ - Команда перезагрузки компьютера из SLiM.
- _console_cmd /usr/bin/xterm -C -fg white -bg black +sb -T "Console login" -e /bin/sh -c "/bin/cat /etc/issue; exec /bin/login"_ - Запуск терминала консоли прямо из SLiM. Можно задать предпочитаемый эмулятор терминала, заменив xterm на свое, например, gnome-terminal, rxvt, aterm, mrxvt, materm, wterm, gnome-multi-terminal, eterm, rxvt-unicode (urxvt), mlterm, mliterm.
- _susliend_cmd /usr/sbin/susliend_ - Команда перевода компьютера в спящий режим из SLiM.
- _numlock on_ - Включение-отключение NumLock клавиатуры при запуске SLiM. Возможные значения параметра - _on_ (включена), _off_ (выключена).
- _hidecursor false_ - Скрыть-показать курсор при вводе логинапароля. Возможные значения параметра - _true|false_.

## Полезные команды SLiM

Для остановки, перезагрузки, перевода в спящий режим компьютера или запуска эмулятора терминала из SLiM используются команды, представленные ниже.

Правильный порядок ввода их следующий:

- в поле _username_ вводим команду (например, _halt_)
- в поле _password_ вводим пароль _root_'а.

Команды:

1. Запуск эмулятора терминала - команда _console_;
2. Выключение компьютера - команда _halt_;
3. Перезагрузка компьютера - команда _reboot_;
4. Перевод компьютера в спящий режим - команда _susliend_;
5. Перейти в консоль - команда _exit_.

---
