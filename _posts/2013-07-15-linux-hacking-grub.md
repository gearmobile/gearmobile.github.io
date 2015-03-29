---
title: "Взлом Linux через GRUB"
layout: post
categories: linux
tags: [grub, linux]
share: true
---

> Очень простой способ получить полный доступ (права `root`'а) к системе Linux, используя загрузчик GRUB (даже LiveCD не нужен).

Что для этого нужно? Просто грузим систему и ждем появления меню GRUB'а со списком установленных в системе операционных систем.

Список может быть примерно такой:

{% highlight powershell %}
Gentoo Linux 2.6.31-r6
ArchLinux 2.6.31
Ubuntu Karmic Koala 9.10
Sabayon Linux r5.1 KDE
{% endhighlight %}

Выбираем систему (стрелочками вверх-вниз), к которой хотим получить доступ. И нажимаем буковку `e` на клавиатуре (`e` – от `edit`). Например, нам нужно "попасть" в ArchLinux.

Выбираем пункт ArchLinux 2.6.31, нажимаем `e` и нам открывается для редактирования запись, соответствующая записи в конфигурационном файле GRUB `menu.lst` (для Debian-подобных систем, или `grub.cfg` – для Gentoo):

{% highlight powershell %}
title Archlinux 2.6.31
  root (hd0,5)
  kernel /boot/vmlinuz26 root=/dev/sda6 ro vga=0?318
  initrd /boot/kernel26.img
{% endhighlight %}

Удаляем в строке `kernel` (в данном случае – третья по счету) все, кроме пути к ядру `/boot/vmlinuz26` и пути к разделу `root` (`root=/dev/sda6`). То есть, у нас получится запись такого вида:

{% highlight powershell %}
kernel /boot/vmlinuz26 root=/dev/sda6
{% endhighlight %}

Дописываем в конец этой строки это: `rw init=/bin/bash`. В итоге запись будет выглядеть так:

{% highlight powershell %}
kernel /boot/vmlinuz26 root=/dev/sda6 rw init=/bin/bash
{% endhighlight %}

Сохраняем результаты нашего "непосильного" труда – нажимаем <kbd>Enter</kbd> и затем грузим ArchLinux с исправленными нами параметрами, нажав `b` (`b` – от `boot`).

В итоге у нас загружается консоль с правами `root`'а. Что и требовалось. Дальше – только дело фантазии и умения.

На этом все.

---