---
title: "Соединение точка-точка (ad-hoc) по WiFi между Ubuntu Linux и Windows XP"
layout: post
categories: linux
tags: [wifi, linux]
share: true
---

> Рассмотрим случай, когда на одной машине (desktop) стоит все та же Ubuntu, а на другой машине (notebook) стоит Windows XP.

Необходимо соединить оба компьютера по `ad-hoc` wifi. Требуется создать локальную домашнюю сеть, которая называется одноранговой. Другими словами, у нас нет в наличии таких сетевых устройств, как концентратор, коммутатор или маршрутизатор. Соединение между двумя (в нашем случае) компьютерами будет установлено напрямую, `точка-точка`. В первом шаге настроим сеть на десктопе в Ubuntu. Затем повторим настройку на ноутбуке в Windows XP.

И в заключение, протестируем созданную нами сеть.

## Шаг Первый - настройка ad-hoc wifi в Ubuntu Karmic

Открываем NetworkManager правым щелчком мыши на значке в Панели Gnome и выбираем "Edit connections". Появляется окно "Network Connections".

Переходим на вкладку "Wireless" (Беспроводные):

![Start Network Connections]({{site.url}}/images/uploads/2013/06/Start-Network-Connections.png)

Нажимаем Add (Добавить). Появляется окно из четырех вкладок (tabs) для создания нового соединения. В первой вкладке вводим общую информацию о создаваемой нами сети:

  * `Connection name` (имя сети) - это имя сети, которое будет отображаться на компьютере и в списке сетей NetworkManager;
  * `SSID` - реальное имя сети. Каждая сеть Wi-Fi имеет свое имя, по которому сетевые устройства распознают их и подключаются к ним;
  * `Mode` - режим сети. В выпадающем списке выбираем режим сети Ad-hoc;
  * остальные три поля - `BSSID`, `MAC address` и `MTU` оставляем пустыми.

![Ubuntu Editing Windows XP]({{site.url}}/images/uploads/2013/06/Ubuntu-Editing-Windows_XP.png)

Переходим на вкладку "Wireless Security". Оставляем поле "Security" пустым (None):

![Security Editing Windows_XP]({{site.url}}/images/uploads/2013/06/Security-Editing-Windows_XP.png)

Далее, переходим на вкладку "IPv4 Settings". Здесь мы выбираем метод получения IP-адреса компьютером в сети. В нашем случае мы задаем его вручную.

Для этого в выпадающем списке "Method" выбираем "Manual" (Ручной). Затем, в поле "Addresses" (Адреса) нажимаем кнопку <kbd>Add</kbd> (Добавить) и последовательно задаем IP-адрес `192.168.0.30`, маску сети "Netmask" `255.255.255.0` и шлюз сети "Gateway" `1.1.1.1`. Поля "DNS servers" и "Search domains" оставляем пустыми:

![IPv4 Settings-Editing Windows_XP]({{site.url}}/images/uploads/2013/06/IPv4-Settings-Editing-Windows_XP.png)

Вкладку "IPv6 Settings" оставляем как есть, ничего не конфигурируя (Method - Ignore):

![IPv6 Settings-Editing Windows_XP]({{site.url}}/images/uploads/2013/06/IPv6-Settings-Editing-Windows_XP.png)

Нажимаем кнопочку <kbd>Apply</kbd> (Применить) и видим конечный результат работы - список сетей в "NetworkManager" и нашу Windows_XP среди них:

![Finish Network Connections]({{site.url}}/images/uploads/2013/06/Finish-Network-Connections.png)

Закрываем окно. Вновь нажимаем, теперь уже левой кнопкой мыши, на значке "NetworkManager" в Панели Gnome. Выбираем в выпавшем списке "Connect to hidden wireless network" (Подключиться к скрытой беспроводной сети).

В списке "Connection" выбираем нашу Windows XP и нажимаем <kbd>Connect</kbd> (Соединить):

![Connect to hidden wireless network]({{site.url}}/images/uploads/2013/06/Connect-to-Hidden-Wireless-Network1.png)

В эмуляторе терминала набираем команду:

<pre>
$ sudo ifconfig -a
</pre>

и видим, что сетевой интерфейс поднят и сеть запущена:

![Ubuntu Desktop]({{site.url}}/images/uploads/2013/06/ubuntu-desktop.png)

## Шаг Второй - Настройка `ad-hoc` wifi в Windows XP

Открываем в "Панели управления" - "Сетевые подключения":

![Network Connections Windows XP]({{site.url}}/uploads/2013/06/Network-Connections-Windows-XP.png)

Кликаем правой кнопкой мыши на значке "Беспроводное сетевое соединение" и в контекстном меню - "Properties" (Свойства). В окне "Свойств" находим в самом низу строку "Протокол Интернета (TCP/IP)":

![TCP IP Windows XP]({{site.url}}/images/uploads/2013/06/TCP_IP_Windows_XP.png)

Нажимаем "Свойства". Открывается окно настроек TCP/IP. Здесь мы задаем IP-адрес, маску сети и шлюз сети так же, как и в NetworkManager, за исключением того, что IP-адрес у нас будет несколько иной - `192.168.0.31`:

![Properties TCP IP Windows XP]({{site.url}}/images/uploads/2013/06/Properties-TCP_IP-Windows-XP.png)

Нажимаем <kbd>OK</kbd>. Далее кликаем левой кнопкой мыши на значке "Беспроводное сетевое соединение" в "Сетевые подключения" "Панели управления". Открывается окно со списком беспроводных сетей, находящихся в зоне доступа компьютера:

![Start Wireless Networks Windows XP]({{site.url}}/images/uploads/2013/06/Start-Wireless-Networks-Windows-XP.png)

Выбираем "Установить беспроводную сеть" для создания сети `ad-hoc`. Запускается "Мастер беспроводной сети", пошагово проведущий по несложной настройке новой сети windows:

![Step1 Windows XP]({{site.url}}/images/uploads/2013/06/Step1.png)

![Step2 Windows XP]({{site.url}}/images/uploads/2013/06/Step2.png)

![Step3 Windows XP]({{site.url}}/images/uploads/2013/06/Step3.png)

![Step4 Windows XP]({{site.url}}/images/uploads/2013/06/Step4.png)

![Step5 Windows XP]({{site.url}}/images/uploads/2013/06/Step5.png)

Нажимаем "Готово". Вновь открывается окно со списков доступных беспроводных сетей. В этом списке появилась и наша windows:

![Step6 Windows XP]({{site.url}}/images/uploads/2013/06/Step6-Windows-XP.png)

Выбираем сеть windows и нажимаем "Подключить":

![Step7 Windows XP]({{site.url}}/images/uploads/2013/06/Step7-Windows-Xp.png)

![Step8 Windows XP]({{site.url}}/images/uploads/2013/06/Step8-Windows-XP.png)

В итоге получаем подключение к сети windows:

![Step9 Windows XP]({{site.url}}/images/uploads/2013/06/Step9-Windows-XP.png)

## Шаг Третий - тестирование сети из Ubuntu

Ping самих себя:

![Ping Self - Network Tools]({{site.url}}/images/uploads/2013/06/Ping-Self-Network-Tools.png)

Ping Windows XP:

![Ping Windows - Network Tools]({{site.url}}/images/uploads/2013/06/Ping-Windows-Network-Tools.png)

Трассировка Windows XP:

![Traceroute Windows - Network Tools]({{site.url}}/images/uploads/2013/06/Traceroute-Windows-Network-Tools.png)

Сканирование портов Windows XP:

![Port Scan Windows - Network Tools]({{site.url}}/images/uploads/2013/06/Port-Scan-Windows-Network-Tools.png)

На этом все.

---