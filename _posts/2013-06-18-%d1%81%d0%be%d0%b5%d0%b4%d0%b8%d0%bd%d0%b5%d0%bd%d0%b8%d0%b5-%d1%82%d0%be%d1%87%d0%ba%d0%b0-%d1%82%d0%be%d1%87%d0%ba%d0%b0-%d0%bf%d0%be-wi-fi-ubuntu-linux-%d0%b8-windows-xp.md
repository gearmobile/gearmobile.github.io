---
title: Соединение точка-точка (ad-hoc) по WiFi между Ubuntu Linux и Windows XP
author: gearmobile
layout: post
permalink: /%d1%81%d0%be%d0%b5%d0%b4%d0%b8%d0%bd%d0%b5%d0%bd%d0%b8%d0%b5-%d1%82%d0%be%d1%87%d0%ba%d0%b0-%d1%82%d0%be%d1%87%d0%ba%d0%b0-%d0%bf%d0%be-wi-fi-ubuntu-linux-%d0%b8-windows-xp/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
categories:
  - OS Linux
tags:
  - wifi
---
Рассмотрим случай, когда на одной машине (desktop) стоит все та же Ubuntu, а на другой машине (notebook) стоит Windows XP. Необходимо соединить оба компьютера по ad-hoc wifi. Требуется создать локальную домашнюю сеть, которая называется одноранговой. Другими словами, у нас нет в наличии таких сетевых устройств, как концентратор, коммутатор или маршрутизатор. Соединение между двумя (в нашем случае) компьютерами будет установлено напрямую, точка-точка. В первом шаге настроим сеть на десктопе в Ubuntu. Затем повторим настройку на ноутбуке в Windows XP. И в заключение, протестируем созданную нами сеть.

### Шаг Первый &#8211; настройка ad-hoc wifi в Ubuntu Karmic

1. Открываем NetworkManager правым щелчком мыши на значке в Панели Gnome и выбираем &#8220;Edit connections&#8230;&#8221;. Появляется окно &#8220;Network Connections&#8221;. Переходим на вкладку &#8220;Wireless&#8221; (Беспроводные):<figure id="attachment_579" style="width: 460px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Start-Network-Connections.png" alt="Start Network Connections" width="460" height="340" class="size-full wp-image-579" />][1]<figcaption class="wp-caption-text">Start Network Connections</figcaption></figure> 

2. Нажимаем Add (Добавить). Появляется окно из четырех вкладок (tabs) для создания нового соединения. В первой вкладке вводим общую информацию о создаваемой нами сети:

  * Connection name (имя сети) &#8211; это имя сети, которое будет отображаться на компьютере и в списке сетей NetworkManager;
  * SSID &#8211; реальное имя сети. Каждая сеть Wi-Fi имеет свое имя, по которому сетевые устройства распознают их и подключаются к ним;
  * Mode &#8211; режим сети. В выпадающем списке выбираем режим сети Ad-hoc;
  * остальные три поля &#8211; BSSID, MAC address и MTU оставляем пустыми.<figure id="attachment_580" style="width: 403px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Ubuntu-Editing-Windows_XP.png" alt="Ubuntu Editing Windows XP" width="403" height="517" class="size-full wp-image-580" />][2]<figcaption class="wp-caption-text">Ubuntu Editing Windows XP</figcaption></figure> 

3. Переходим на вкладку &#8220;Wireless Security&#8221;. Оставляем поле &#8220;Security&#8221; пустым (None):<figure id="attachment_581" style="width: 403px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Security-Editing-Windows_XP.png" alt="Security Editing Windows_XP" width="403" height="517" class="size-full wp-image-581" />][3]<figcaption class="wp-caption-text">Security Editing Windows_XP</figcaption></figure> 

4. Далее, переходим на вкладку &#8220;IPv4 Settings&#8221;. Здесь мы выбираем метод получения IP-адреса компьютером в сети. В нашем случае мы задаем его вручную. Для этого в выпадающем списке &#8220;Method&#8221; выбираем &#8220;Manual&#8221; (Ручной). Затем, в поле &#8220;Addresses&#8221; (Адреса) нажимаем кнопку Add (Добавить) и последовательно задаем IP-адрес (192.168.0.30), маску сети &#8220;Netmask&#8221; (255.255.255.0) и шлюз сети &#8220;Gateway&#8221; (1.1.1.1). Поля &#8220;DNS servers&#8221; и &#8220;Search domains&#8221; оставляем пустыми:<figure id="attachment_582" style="width: 419px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/IPv4-Settings-Editing-Windows_XP.png" alt="IPv4 Settings-Editing Windows_XP" width="419" height="517" class="size-full wp-image-582" />][4]<figcaption class="wp-caption-text">IPv4 Settings-Editing Windows_XP</figcaption></figure> 

5. Вкладку &#8220;IPv6 Settings&#8221; оставляем как есть, ничего не конфигурируя (Method &#8211; Ignore):<figure id="attachment_583" style="width: 419px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/IPv6-Settings-Editing-Windows_XP.png" alt="IPv6 Settings-Editing Windows_XP" width="419" height="517" class="size-full wp-image-583" />][5]<figcaption class="wp-caption-text">IPv6 Settings-Editing Windows_XP</figcaption></figure> 

6. Нажимаем кнопочку Apply (Применить) и видим конечный результат работы &#8211; список сетей в NetworkManager и нашу Windows_XP среди них:<figure id="attachment_584" style="width: 460px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Finish-Network-Connections.png" alt="Finish Network Connections" width="460" height="340" class="size-full wp-image-584" />][6]<figcaption class="wp-caption-text">Finish Network Connections</figcaption></figure> 

7. Закрываем окно. Вновь нажимаем, теперь уже левой кнопкой мыши, на значке NetworkManager в Панели Gnome. Выбираем в выпавшем списке &#8220;Connect to hidden wireless network&#8221; (Подключиться к скрытой беспроводной сети). В списке &#8220;Connection&#8221; выбираем нашу Windows XP и нажимаем Connect (Соединить):<figure id="attachment_627" style="width: 428px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Connect-to-Hidden-Wireless-Network1.png" alt="Connect to hidden wireless network" width="428" height="296" class="size-full wp-image-627" />][7]<figcaption class="wp-caption-text">Connect to hidden wireless network</figcaption></figure> 

8. В эмуляторе терминала набираем команду:

<pre>$ sudo ifconfig -a</pre>

и видим, что сетевой интерфейс поднят и сеть запущена:<figure id="attachment_586" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/ubuntu-desktop-600x419.png" alt="Ubuntu Desktop" width="600" height="419" class="size-medium wp-image-586" />][8]<figcaption class="wp-caption-text">Ubuntu Desktop</figcaption></figure> 

### Шаг Второй &#8211; Настройка ad-hoc wifi в Windows XP

1. Открываем в &#8220;Панели управления&#8221; &#8211; &#8220;Сетевые подключения&#8221;:<figure id="attachment_587" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Network-Connections-Windows-XP-600x564.png" alt="Network Connections Windows XP" width="600" height="564" class="size-medium wp-image-587" />][9]<figcaption class="wp-caption-text">Network Connections Windows XP</figcaption></figure> 

2. Кликаем правой кнопкой мыши на значке &#8220;Беспроводное сетевое соединение&#8221; и в контекстном меню &#8211; &#8220;Properties&#8221; (Свойства). В окне &#8220;Свойств&#8221; находим в самом низу строку &#8220;Протокол Интернета (TCP/IP)&#8221;:<figure id="attachment_588" style="width: 367px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/TCP_IP_Windows_XP.png" alt="TCP IP Windows XP" width="367" height="450" class="size-full wp-image-588" />][10]<figcaption class="wp-caption-text">TCP IP Windows XP</figcaption></figure> 

3. Нажимаем &#8220;Свойства&#8221;. Открывается окно настроек TCP/IP. Здесь мы задаем IP-адрес, маску сети и шлюз сети так же, как и в NetworkManager, за исключением того, что IP-адрес у нас будет несколько иной &#8211; 192.168.0.31:<figure id="attachment_589" style="width: 404px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Properties-TCP_IP-Windows-XP.png" alt="Properties TCP IP Windows XP" width="404" height="455" class="size-full wp-image-589" />][11]<figcaption class="wp-caption-text">Properties TCP IP Windows XP</figcaption></figure> 

4. Нажимаем OK. Далее кликаем левой кнопкой мыши на значке &#8220;Беспроводное сетевое соединение&#8221; в &#8220;Сетевые подключения&#8221; &#8220;Панели управления&#8221;. Открывается окно со списком беспроводных сетей, находящихся в зоне доступа компьютера:<figure id="attachment_590" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Start-Wireless-Networks-Windows-XP-600x457.png" alt="Start Wireless Networks Windows XP" width="600" height="457" class="size-medium wp-image-590" />][12]<figcaption class="wp-caption-text">Start Wireless Networks Windows XP</figcaption></figure> 

5. Выбираем &#8220;Установить беспроводную сеть&#8221; для создания сети ad-hoc. Запускается &#8220;Мастер беспроводной сети&#8221;, пошагово проведущий по несложной настройке новой сети windows:<figure id="attachment_624" style="width: 540px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step1.png" alt="Step1 Windows XP" width="540" height="482" class="size-full wp-image-624" />][13]<figcaption class="wp-caption-text">Step1 Windows XP</figcaption></figure> <figure id="attachment_623" style="width: 540px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step2.png" alt="Step2 Windows XP" width="540" height="482" class="size-full wp-image-623" />][14]<figcaption class="wp-caption-text">Step2 Windows XP</figcaption></figure> <figure id="attachment_622" style="width: 540px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step3.png" alt="Step3 Windows XP" width="540" height="482" class="size-full wp-image-622" />][15]<figcaption class="wp-caption-text">Step3 Windows XP</figcaption></figure> <figure id="attachment_621" style="width: 540px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step4.png" alt="Step4 Windows XP" width="540" height="482" class="size-full wp-image-621" />][16]<figcaption class="wp-caption-text">Step4 Windows XP</figcaption></figure> <figure id="attachment_620" style="width: 540px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step5.png" alt="Step5 Windows XP" width="540" height="482" class="size-full wp-image-620" />][17]<figcaption class="wp-caption-text">Step5 Windows XP</figcaption></figure> 

Нажимаем &#8220;Готово&#8221;. Вновь открывается окно со списков доступных беспроводных сетей. В этом списке появилась и наша windows:<figure id="attachment_619" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step6-Windows-XP-600x457.png" alt="Step6 Windows XP" width="600" height="457" class="size-medium wp-image-619" />][18]<figcaption class="wp-caption-text">Step6 Windows XP</figcaption></figure> 

Выбираем сеть windows и нажимаем &#8220;Подключить&#8221;:<figure id="attachment_618" style="width: 381px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step7-Windows-Xp.png" alt="Step7 Windows XP" width="381" height="190" class="size-full wp-image-618" />][19]<figcaption class="wp-caption-text">Step7 Windows XP</figcaption></figure> <figure id="attachment_617" style="width: 426px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step8-Windows-XP.png" alt="Step8 Windows XP" width="426" height="151" class="size-full wp-image-617" />][20]<figcaption class="wp-caption-text">Step8 Windows XP</figcaption></figure> 

В итоге получаем подключение к сети windows:<figure id="attachment_616" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Step9-Windows-XP-600x457.png" alt="Step9 Windows XP" width="600" height="457" class="size-medium wp-image-616" />][21]<figcaption class="wp-caption-text">Step9 Windows XP</figcaption></figure> 

### Шаг Третий &#8211; тестирование сети из Ubuntu

Ping самих себя:<figure id="attachment_615" style="width: 546px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Ping-Self-Network-Tools.png" alt="Ping Self - Network Tools" width="546" height="527" class="size-full wp-image-615" />][22]<figcaption class="wp-caption-text">Ping Self &#8211; Network Tools</figcaption></figure> 

Ping Windows XP:<figure id="attachment_614" style="width: 546px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Ping-Windows-Network-Tools.png" alt="Ping Windows - Network Tools" width="546" height="527" class="size-full wp-image-614" />][23]<figcaption class="wp-caption-text">Ping Windows &#8211; Network Tools</figcaption></figure> 

Трассировка Windows XP:<figure id="attachment_613" style="width: 546px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Traceroute-Windows-Network-Tools.png" alt="Traceroute Windows - Network Tools" width="546" height="527" class="size-full wp-image-613" />][24]<figcaption class="wp-caption-text">Traceroute Windows &#8211; Network Tools</figcaption></figure> 

Сканирование портов Windows XP:<figure id="attachment_612" style="width: 546px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/06/Port-Scan-Windows-Network-Tools.png" alt="Port Scan Windows - Network Tools" width="546" height="527" class="size-full wp-image-612" />][25]<figcaption class="wp-caption-text">Port Scan Windows &#8211; Network Tools</figcaption></figure> 

Оцените статью:  
<span id="post-ratings-577" class="post-ratings" data-nonce="165c6bf28d"><img id="rating_577_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(577, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_577_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(577, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_577_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(577, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_577_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(577, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_577_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(577, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_577_text"></span></span><span id="post-ratings-577-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/06/Start-Network-Connections.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/06/Ubuntu-Editing-Windows_XP.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/06/Security-Editing-Windows_XP.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/06/IPv4-Settings-Editing-Windows_XP.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/06/IPv6-Settings-Editing-Windows_XP.png
 [6]: http://localhost:7788/third/wp-content/uploads/2013/06/Finish-Network-Connections.png
 [7]: http://localhost:7788/third/wp-content/uploads/2013/06/Connect-to-Hidden-Wireless-Network1.png
 [8]: http://localhost:7788/third/wp-content/uploads/2013/06/ubuntu-desktop.png
 [9]: http://localhost:7788/third/wp-content/uploads/2013/06/Network-Connections-Windows-XP.png
 [10]: http://localhost:7788/third/wp-content/uploads/2013/06/TCP_IP_Windows_XP.png
 [11]: http://localhost:7788/third/wp-content/uploads/2013/06/Properties-TCP_IP-Windows-XP.png
 [12]: http://localhost:7788/third/wp-content/uploads/2013/06/Start-Wireless-Networks-Windows-XP.png
 [13]: http://localhost:7788/third/wp-content/uploads/2013/06/Step1.png
 [14]: http://localhost:7788/third/wp-content/uploads/2013/06/Step2.png
 [15]: http://localhost:7788/third/wp-content/uploads/2013/06/Step3.png
 [16]: http://localhost:7788/third/wp-content/uploads/2013/06/Step4.png
 [17]: http://localhost:7788/third/wp-content/uploads/2013/06/Step5.png
 [18]: http://localhost:7788/third/wp-content/uploads/2013/06/Step6-Windows-XP.png
 [19]: http://localhost:7788/third/wp-content/uploads/2013/06/Step7-Windows-Xp.png
 [20]: http://localhost:7788/third/wp-content/uploads/2013/06/Step8-Windows-XP.png
 [21]: http://localhost:7788/third/wp-content/uploads/2013/06/Step9-Windows-XP.png
 [22]: http://localhost:7788/third/wp-content/uploads/2013/06/Ping-Self-Network-Tools.png
 [23]: http://localhost:7788/third/wp-content/uploads/2013/06/Ping-Windows-Network-Tools.png
 [24]: http://localhost:7788/third/wp-content/uploads/2013/06/Traceroute-Windows-Network-Tools.png
 [25]: http://localhost:7788/third/wp-content/uploads/2013/06/Port-Scan-Windows-Network-Tools.png