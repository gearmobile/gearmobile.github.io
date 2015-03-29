---
title: "Rankmirrors - выбор быстрых репозиториев в ArchLinux"
layout: post
categories: linux
tags: [rankmirrors, linux]
share: true
---

> В ArchLinux имеется скрипт для настройки конфигурационного файла `/etc/pacman.d/mirrorlist` – `rankmirrors`.

Что он делает? `rankmirrors` берет список IP-адресов зеркал репозиториев ArchLinuxlinux из заранее созданного файла и проверяет их на скорость доступа. А затем формирует список самых быстрых зеркал на основе этой проверки.

Что это дает? В результате работы `rankmirrors` в `/etc/pacman.d/mirrorlist` мы имеем сервера с самым быстрым (исходяя из местоположения нашей машины) доступом. При обновлении системы или установки какой-либо программы скорость инсталляции существенно возрастает (из чего складывается инсталляция? Из скачивания пакета с сервера и уже затем его установки). `rankmirrors` является python-скриптом. man-страницы не имеет, но есть опция `-help` с небольшим выбором команд.

Похожими утилитами являются `netselect` и особенно – `mirrorselect` (для Gentoo). Итак, приступим к настройке нашего списка зеркал с помощью `rankmirrors`.

1. Так как `rankmirrors` является python-скриптом, для его работы необходим установленный Python в системе. Устанавливаем, если его нет в системе:

{% highlight powershell %}
$ sudo pacman -Sy python
{% endhighlight %}

2. Переходим в директорию со списком зеркал pacman'а:

{% highlight powershell %}
$ cd /etc/pacman.d/
{% endhighlight %}

3. Делаем копию существующего списка зеркал `mirrorlist`:

{% highlight powershell %}
$ sudo cp mirrorlist mirrorlist.backup
{% endhighlight %}

4. Открываем копию списка зеркал в своем любимом редакторе и раскомментируем все строки с адресами серверов, географически наиболее близко расположенных к нам (по идее, это и будут сервера с самым быстрым доступом):

{% highlight powershell %}
$ sudo nano -w mirrorlist.backup
{% endhighlight %}

5. Сохраняем изменения в файле и выходим из него. Запускаем скрипт `rankmirrors` для выбора зеркал из указанного нами списка (для запуска `rankmirrors` потребуется войти в учетную запись `root`'а. Под `sudo` у меня скрипт отказался работать, ругаясь на отсутствие прав доступа к файлу `mirrorlist`).

Переходим в учетную запись `root`'а:

{% highlight powershell %}
$ su -
{% endhighlight %}

Запускаем `rankmirrors` под `root`'ом:

{% highlight powershell %}
# rankmirrors -n 6 mirrorlist.backup > mirrorlist
{% endhighlight %}

где:

  * `-n 6` – вывести (в нашем случае – записать) 6 сервером с самым маленьким временем отклика
  * `mirrorlist.backup` – список серверов для теста на время отклика
  * `mirrorlist` – файл, куда записываются адреса серверов скриптом `rankmirros`

В результате `rankmirrors` удалит все раскомментированные строки в `mirrorlist` и снесет адреса шести самых "быстрых" зеркал. Получится что-то вроде этого:

{% highlight powershell %}
# Result
  Server = ftp://ftp.nluug.nl/pub/metalab/distributions/ArchLinuxlinux/$repo/os/i686
  Server = ftp://ftp.free.fr/mirrors/ftp.ArchLinuxlinux.org/$repo/os/i686
  Server = ftp://ftp.mfa.kfki.hu/pub/mirrors/ftp.ArchLinuxlinux.org/$repo/os/i686
  Server = http://gd.tuwien.ac.at/opsys/linux/ArchLinuxlinux/$repo/os/i686
  Server = http://ftp.gigabit.nu/$repo/os/i686
  Server = http://mirror.svk.su/ArchLinuxlinux/$repo/os/i686
{% endhighlight %}

Здесь я раскомментировал все зеркала, географически расположенные в Европе и получил 6 из них.

6. Теперь осталось последнее – заставить `pacman` перечитать список зеркал и обновить список пакетов.

Делаем:

{% highlight powershell %}
# pacman -Syy
{% endhighlight %}

Результат:

{% highlight powershell %}
:: Синхронизируются базы данных пакетов…
  core 35,8K
  65,8K/s 00:00:01 [######################] 100%
  extra 443,7K 15,4K/s 00:00:29 [#########################] 100%
  community 367,8K
  18,1K/s 00:00:20 [###########################] 100%
  ArchLinuxlinuxfr 24,7K 5,7K/s 00:00:04 [############################] 100%
{% endhighlight %}

Данная статья является вольным переводом (опробованным для своих нужд) из Википедии ArchLinuxlinux.

На этом все.

---