---
title: Установка Windows 7 на ноутбук ASUS K56CM
author: gearmobile
layout: post
permalink: /%d1%83%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%ba%d0%b0-windows-7-asus-k56cm/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 37
ratings_score:
  - 182
ratings_average:
  - 4.92
categories:
  - Разное
tags:
  - asus k56cm
  - bios
  - windows 7
---
Два дня назад на смену моему старенькому ноутбуку Acer Extensa 5620 пришел новый, молодой и современный &#8211; ноутбук **ASUS K56CM**. Компьютер понравился всем &#8211; алюминиевый корпус, матовый экран, технические возможности на уровне бюджетного ноутбука с хорошей производительностью. В тому же очень тихий в работе &#8211; его почти не слышно.<figure id="attachment_874" style="width: 500px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/02/asus-k56cm.jpg" alt="Ноутбук ASUS K56CM" width="500" height="500" class="size-full wp-image-874" />][1]<figcaption class="wp-caption-text">Ноутбук ASUS K56CM</figcaption></figure> 

Но, как всегда, не обошлось без ложки дегтя. На ASUS K56CM стояла предустановленная Windows 8. Сказать, что я имею какое-либо предубеждение против этой ОС я не могу. В принципе, она совсем неплохая и работать в ней можно абсолютно свободно. Что я попытался сделать в течение первых суток с момента появления нового ноутбука на моем рабочем столе.

Однако чувствовал я себя в этой системе неуютно. С моей личной точки зрения совершенно лишние для Desktop плитки. Зачем-то нужно было попадать курсором в правый нижний угол, чтобы добраться до кнопки выключения и всего лишь остановить машину. В общем и целом можно было сказать &#8211; не мое это!

После раздумий и взвешиваний за\против я решил для себя все-же &#8220;заморочиться&#8221;, но поставить на ASUS K56CM систему Windows 7 вместо Windows 8. Хотя и предвидел некоторые трудности на этом пути, две главные из которых &#8211; это BIOS и драйвера под Windows 7. Проблема с BIOS заключается в снятии блокировки на переустановку ОС на этом ноутбуке. Проблема с драйверами &#8211; почти не проблема, но также возникли некоторые сложности.

## Вход в BIOS ноутбука ASUS K56CM

Неожиданно для себя не смог сразу же войти в BIOS ноутбука, пришлось немного &#8220;поволноваться&#8221;. Но все оказалось просто.

Вход в BIOS ноутбука ASUS K56CM можно выполнить через клавиши (на выбор):

  * **Tab+F2**
  * **Delete** (который на NumPad)

Это два варианта, которые лично у меня сработали. Тут главное, чтобы нажать и держать нажатой клавишу **с самого момента запуска ноутбука**. Иначе момент &#8220;проскочит&#8221; и в BIOS не попадем.

### Снятие блокировки в BIOS ASUS K56CM

После того, как попали в BIOS, нужно выполнить два действия.

Первым шагом заходим во вкладку **Boot** и включаем (**Enabled**) опцию **Launch CSM**:

<pre>Boot - Launch CSM - Enabled</pre>

Вторым шагом переходим на вкладку **Security** и отключаем (**Disabled**) опцию **Secure Boot Control**:

<pre>Security - Secure Boot Control - Disabled</pre>

Сохраняем изменения в BIOS и выходим из него, нажав клавишу **F10**.

### Меню выбора загрузки ASUS K56CM

Когда нужные изменения внесены в BIOS, можно приступать к обычной процедуре установки Windows 7 с диска (я делал инсталляцию с него). Чтобы загрузиться с установочного диска, нужно открыть **меню выбора загрузки**. Для этого нужно нажать и держать нажатой **клавишу Esc**. Затем выбираем оптический дисковод и процесс запущен.

Но не стоит забывать одну вещь. Чтобы Windows 7 правильно встала и от Windows 8 не осталось и следа на ноутбуке ASUS K56CM, **перед инсталляций необходимо полностью удалить все существующие разделы** на жестком диске и создать новые, с соответствующим форматированием.

Делается это с помощью специальных программ для редактирования разделов жесткого диска. Такими программами являются Acronis Disk Director, Gparted и многие другие. Достаточно в поисковой строке Google ввести запрос: &#8220;*программы редактирования разделов жесткого диска*&#8220;. Есть платные и бесплатные &#8211; все дело вкуса и умения.

## Драйвера под Windows 7 на ASUS K56CM

После успешной инсталляции ОС Windows 7 на ноутбук ASUS K56CM насущной задачей стала установка драйверов. Для этого поступил привычным для себя способом &#8211; с помощью диска **DriverPack Solution 13 r399 Full Final**.

Автоматически поставились все драйвера, кроме чипсета под Intel. Перед этим система сделала предупреждение, что драйвера ненадежны! Однако я понадеялся на авось &#8211; и ноутбук вылетел с синим экраном смерти при попытке инсталляции этих драйверов.

Правда, я отделался легким испугом и все обошлось. Пришлось скачивать по отдельности все пять пакетов драйверов для чипсета с официального сайта ASUS.

Список этих пакетов (которые не захотели ставиться из-под DriverPack Solution) таков:

  * Chipset\_Intel\_Win7\_64\_Z9301020.zip
  * DPTF\_Intel\_Win7\_64\_Z6011067.zip
  * IRST\_Intel\_Win7\_64\_Z11101006.zip
  * MEI\_Intel\_Win7\_64\_Z8101252.zip
  * Rapid\_Start\_Technology\_NonUI\_Win7\_64\_Z1001024.zip

ASUS-ские утилиты-приблуды скачивать и устанавливать не стал. Только систему загромождают. Windows 7 на моем ноутбуке ASUS K56CM до сих пор работает нормально, проблем нет.

Оцените статью:  
<span id="post-ratings-866" class="post-ratings" data-nonce="132ebfefc2"><img id="rating_866_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(866, 1, '1 Star');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_866_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(866, 2, '2 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_866_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(866, 3, '3 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_866_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(866, 4, '4 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_866_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(866, 5, '5 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>37</strong> votes, average: <strong>4,92</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_866_text"></span></span><span id="post-ratings-866-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/02/asus-k56cm.jpg