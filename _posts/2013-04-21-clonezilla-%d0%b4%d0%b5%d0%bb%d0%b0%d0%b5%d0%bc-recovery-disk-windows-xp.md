---
title: Clonezilla – делаем recovery disk Windows XP
author: gearmobile
layout: post
permalink: /clonezilla-%d0%b4%d0%b5%d0%bb%d0%b0%d0%b5%d0%bc-recovery-disk-windows-xp/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 11
ratings_score:
  - 54
ratings_average:
  - 4.91
categories:
  - OS Linux
tags:
  - clonezilla
---
Дистрибутив Clonezilla предназначен для создания на резервном накопителе образа установленной операционной системы. При серьезных «поломках» операционную систему можно восстановить из этого образа до прежнего состояния. Clonezilla умеет работать с широким набором файловых систем (fat, ntfs, ext2, ext3, ext4, ufs, ufs2, reiserfs, jfs, xfs, vmfs) и операционных систем x86 и x86-64 (Windows, Linux, FreeBSD, OpenBSD, NetBSD, Mac OS (Intel)). Для клонирования не поддерживаемых файловых систем в Clonezilla используется утилита dd в режиме копирования sector-by-sector. Имеется возможность создания из образа операционной системы recovery disk для автоматического восстановления. Дистрибутив Clonezilla &#8211; из мира OpenSource, поэтому абсолютно бесплатен. Является аналогом своих более знаменитых собратьев из мира Windows – Norton Ghost и Acronis True Image Home. Два последних продукта – платные (Acronis True Image Home позиционируется производителем как программа для домашнего использования, поэтому имеет 15-дневный испытательный строк и цену где-то в 150 рублей).

Итак, у меня стоит задача – снять образ с установленной Windows XP и создать из него диск автоматической инсталляции хрупкого творения ООО «Microsoft».

На оф. сайте имеются подробные инструкции по использованию дистрибутива для разных задач, но все статьи на английском. Так как я научился пользоваться программой совсем недавно, то решил сделать небольшой мануальчик на русском.

Весь процесс создания recovery disk‘а будет разбит на три шага:

  1. скачивание дистрибутива, его запись на болванку и загрузка с Clonezilla LiveCD;
  2. создание образа установленной Windows XP;
  3. создание образа recovery disk‘а из заранее созданного образа.

> Стоит обратить внимание, что описываемый способ создания образа и затем восстановления из него подходит только в том случае, когда размер (расположение) диска\раздела остается неизменным. То есть, если создан образ раздела /dev/sda1 размером 19 Gb, то и восстанавливать образ нужно на раздел /dev/sda1 размером 19 Gb. В противном случае могут возникнуть некоторые несоответствия. А именно – Clonezilla не может клонировать (а именно это и делается в этой статье – через создание образа iso) больший диск\раздел на меньший. Но клонировать меньший диск\раздел на больший – да, это ей по силам. О создании такого образа iso можно почитать про настройки режима эксперта.

### Шаг первый

  1. Загружаем последнюю версию дистрибутива с официального сайта
  2. Записываем скачанный iso-образ на болванку (Brasero, K3B, wodim – по вкусу)

### Шаг второй

1. Загружаемся с Clonezilla LiveCD. При запуске появляется основное меню дистрибутива с вариантами запуска программы:<figure id="attachment_635" style="width: 576px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/ocs-01-bootmenu.jpg" alt="Загрузочное меню Clonezilla" width="576" height="432" class="size-full wp-image-635" />][1]<figcaption class="wp-caption-text">Загрузочное меню Clonezilla</figcaption></figure> 

Первые три варианта – запуск Clonezilla c поддержкой framebuffer‘а (ncurces). Варианты различаются только желаемым разрешением монитора.

Четвертый вариант – программа целиком загружается в оперативную память (RAM), освобождая CD/DVD-привод. Диск можно вытащить и использовать для других целей (например, запись на болванку из-под Clonezilla).

Идет загрузка и запуск Linux-системы, как обычно:<figure id="attachment_636" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/ocs-02-booting-600x450.jpg" alt="Загрузка Clonezilla" width="600" height="450" class="size-medium wp-image-636" />][2]<figcaption class="wp-caption-text">Загрузка Clonezilla</figcaption></figure> 

Затем окно выбора языка и кодировки консоли LiveCD:<figure id="attachment_637" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/ocs-03-lang-600x450.jpg" alt="Выбор языка Clonezilla" width="600" height="450" class="size-medium wp-image-637" />][3]<figcaption class="wp-caption-text">Выбор языка Clonezilla</figcaption></figure> 

И окно выбора раскладки клавиатуры. Я выбрал вариант по умолчанию – Don’t touch keymap (Не трогать раскладку). Проблем с «клавой» во время работы в LiveCD не заметил:<figure id="attachment_638" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/ocs-04-keymap-600x450.jpg" alt="Раскладка клавиатуры Clonezilla" width="600" height="450" class="size-medium wp-image-638" />][4]<figcaption class="wp-caption-text">Раскладка клавиатуры Clonezilla</figcaption></figure> 

2. Окно выбора варианта входа в систему. Здесь выдается запрос, что необходимо сделать – перейти в режим пошагового wisard‘а создания образа или перейти в bash-оболочку (командная строка) системы. Напомню, что Clonezilla построена на основе Debian Linux (Debian Sid – в частности). То есть, фактически – это урезанный Debian – без X-ов и части консольных программ. Выбираем первую строку и жмем Enter:<figure id="attachment_639" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_login-in-system-600x449.jpg" alt="Старт дистрибутива Clonezilla" width="600" height="449" class="size-medium wp-image-639" />][5]<figcaption class="wp-caption-text">Старт дистрибутива Clonezilla</figcaption></figure> 

3. Здесь мы выбираем задачи, которые хотим реализовать в Clonezilla.

Первая строка – &#8220;device-image&#8221; – работа с образами диска (раздела). То есть, создание образа диска (раздела диска), восстановление диска (раздела диска) из образа.

Вторая строка – &#8220;device-device&#8221; – работа напрямую с дисками (разделами дисков). То есть, копирование\перемещение дисков (разделов) с одного на другой.

Мы будем работать с образами дисков, поэтому выбираем первую строку – &#8220;device-image&#8221;:<figure id="attachment_640" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_device-image-600x449.jpg" alt="Clonezilla - работа с образами диска" width="600" height="449" class="size-medium wp-image-640" />][6]<figcaption class="wp-caption-text">Clonezilla &#8211; работа с образами диска</figcaption></figure> 

4. В этом окне выбираем режим работы:

  * local_dev – работа с локальными жесткими дисками (то есть, с винчестерами, что стоят внутри компа);
  * ssh\_server, samba\_server, nfs_server – варианты работы с удаленными жесткими дисками по сети (то есть, с винчестерами, которые находятся не внутри нашего компа, а где-то в другом месте);
  * enter_shell – войти в bash-оболочку и сделать все, что нужно, ручками&#8230;
  * skip – не пробовал, сказать ни чего не могу&#8230;

В этом окне выбираем опять первую строку – &#8220;local_dev&#8221; – работа с локальными жесткими дисками:<figure id="attachment_641" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_local_dev-600x449.jpg" alt="Clonezilla - работа с локальными жесткими дисками" width="600" height="449" class="size-medium wp-image-641" />][7]<figcaption class="wp-caption-text">Clonezilla &#8211; работа с локальными жесткими дисками</figcaption></figure> 

5. После нажатия Enter появится строка, выделенная желтым цветом. В ней говорится, что если мы хотим сохранить создаваемый образ на флешку, то сейчас самое время воткнуть ее, затем подождать 5 секунд и нажать Enter. Система попытается автоматически определить ее и примонтировать в `/home/partimag`. Флешки такого объема (примерно нужно более 4Gb) у меня нет, поэтому просто снова нажимаю Enter. Система начнет сканировать жесткий диск на наличие разделов на нем:<figure id="attachment_642" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_disk-scan-600x449.jpg" alt="Clonezilla - сканировать жесткий диск" width="600" height="449" class="size-medium wp-image-642" />][8]<figcaption class="wp-caption-text">Clonezilla &#8211; сканировать жесткий диск</figcaption></figure> 

6. После сканирования появится окно со списком всех разделов, которые нашла Clonezilla на жестком диске. Здесь система спрашивает, какой раздел мы бы хотели выбрать в качестве целевого, то есть, тот раздел, куда будем сохранять создаваемый образ. Clonezilla примонтирует его в `/home/partimag` для дальнейшей работы. В качестве «мусорки» у меня служит `/dev/sda8` с файловой системой reiserfs. Выбираю его (клавишами-стрелками) и нажимаю Enter:<figure id="attachment_643" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_select-partition-600x449.jpg" alt="Выбираем диск Clonezilla" width="600" height="449" class="size-medium wp-image-643" />][9]<figcaption class="wp-caption-text">Выбираем диск Clonezilla</figcaption></figure> 

7. Clonezilla «заглянет» в выбранный мною раздел и предложит выбрать папку (если таковые имеются на этом разделе), куда бы я хотел сохранять создаваемый ею образ. В строке вверху говорится об условии, по которым Clonezilla нашла\выбрала папки на этом разделе. Одно условие – папки должны быть только самого верхнего (top) уровня, то есть, корневые. Также она не предлагает (скрывает) папки, в именах которых имеются пробелы.

Я выбираю специально созданную для хранения образов папку &#8220;images&#8221; и нажимаю Enter:<figure id="attachment_644" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_store-images-600x449.jpg" alt="Директория хранения образов Clonezilla" width="600" height="449" class="size-medium wp-image-644" />][10]<figcaption class="wp-caption-text">Директория хранения образов Clonezilla</figcaption></figure> 

8. После просьбы программы нажать Enter появляется окно, где можно выбрать режим пошагового wizard‘а:

  * упрощенный (Beginner);
  * эксперт (Expert) – можно добавить дополнительные параметры для создаваемого образа.

Выбираю первый вариант – &#8220;Beginner&#8221; – (*для новичка*). Про опции режима &#8220;Эксперт&#8221; (Expert) можно почитать здесь. В принципе, ничего сложного там и нет:<figure id="attachment_645" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_beginner-600x449.jpg" alt="Режимы работы Clonezilla" width="600" height="449" class="size-medium wp-image-645" />][11]<figcaption class="wp-caption-text">Режимы работы Clonezilla</figcaption></figure> 

9. Следующее окно – что хотим делать с образом диска:

  * savedisk – сделать образ жесткого диска целиком;
  * saveparts – сделать образ отдельного раздела жесткого диска;
  * restoredisk – восстановить жесткий диск целиком из заранее созданного образа;
  * restoreparts – восстановить отдельный раздел жесткого диска из заранее созданного раздела;
  * recovery-iso-zip – создать загрузочный recovery disk (iso – для создания загрузочного диска, zip – для создания загрузочной флешки) из заранее созданного образа;
  * exit – выйти в bash-оболочку.

У меня еще не создан образ раздела, поэтому выбираю вторую строку – &#8220;saveparts&#8221; и нажимаю Enter:<figure id="attachment_646" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_saveparts-600x449.jpg" alt="Clonezilla - образ отдельного раздела диска" width="600" height="449" class="size-medium wp-image-646" />][12]<figcaption class="wp-caption-text">Clonezilla &#8211; образ отдельного раздела диска</figcaption></figure> 

10. Система запрашивает имя создаваемого образа и предлагает вариант по умолчанию. Подправляю его немного и нажимаю снова Enter:<figure id="attachment_647" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_image-name-600x449.jpg" alt="Clonezilla - имя создаваемого образа" width="600" height="449" class="size-medium wp-image-647" />][13]<figcaption class="wp-caption-text">Clonezilla &#8211; имя создаваемого образа</figcaption></figure> 

11. Clonezilla опять принимается за сканирование жесткого диска на наличие разделов. На этот раз она делает это для выбора раздела-источника, то есть, того раздела, образ которого мы будем создавать:<figure id="attachment_648" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_scan-hard-disk-600x449.jpg" alt="Clonezilla - сканирование жесткого диска" width="600" height="449" class="size-medium wp-image-648" />][14]<figcaption class="wp-caption-text">Clonezilla &#8211; сканирование жесткого диска</figcaption></figure> 

12. Снова «выкидывает» окно со списком найденных разделов. У меня Windows XP находится на первом разделе винчестера – /dev/sda1. Поэтому просто выделяю его (клавиша Пробел) и нажимаю Enter:<figure id="attachment_649" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_list-images-600x449.jpg" alt="Clonezilla - список найденных разделов" width="600" height="449" class="size-medium wp-image-649" />][15]<figcaption class="wp-caption-text">Clonezilla &#8211; список найденных разделов</figcaption></figure> 

13. Система выводит внизу экрана уведомление с показом полной команды, которую она собирается выполнить и просит подтвердить ее нажатием клавиши Enter:<figure id="attachment_650" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_confirm-command-600x449.jpg" alt="Clonezilla - подтвердить команду" width="600" height="449" class="size-medium wp-image-650" />][16]<figcaption class="wp-caption-text">Clonezilla &#8211; подтвердить команду</figcaption></figure> 

14. Следует еще одна строка с уведомлением (защита от дурака), куда и какой образ Clonezilla будет размещать\делать. Вводим буковку y и нажимаем Enter:<figure id="attachment_651" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_double-confirm-600x449.jpg" alt="Старт процесса Clonezilla" width="600" height="449" class="size-medium wp-image-651" />][17]<figcaption class="wp-caption-text">Старт процесса Clonezilla</figcaption></figure> 

15. Процесс пошел:<figure id="attachment_652" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_start-process-600x449.jpg" alt="Процесс создания образа Clonezilla" width="600" height="449" class="size-medium wp-image-652" />][18]<figcaption class="wp-caption-text">Процесс создания образа Clonezilla</figcaption></figure> 

17. По завершении выведет маленькое меню с вопросом – что ей делать дальше:<figure id="attachment_653" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_next-steps-600x449.jpg" alt="Выбор дальнейших действий Clonezilla" width="600" height="449" class="size-medium wp-image-653" />][19]<figcaption class="wp-caption-text">Выбор дальнейших действий Clonezilla</figcaption></figure> 

  * (0) Poweroff – выключить компьютер;
  * (1) Reboot – перезагрузить компьютер;
  * (2) Enter command line prompt – перейти в режим командной строки (bash-оболочка);
  * (3) Start over – вернуться в начало wizard‘а.

Так как я сделал только половину дела – создал образ раздела, то мне надо вернуться в начало, чтобы из полученного образа создать iso-образ загрузочного диска. Выбираю 3 и нажимаю Enter.

### Шаг третий

В последнем шаге создаем загрузочный iso-образ раздела. После возвращения в начало wizard‘а все этапы повторяются вновь в точности так, как они показаны в Шаге втором, вплоть до пункта 9. Напомню, что в этом пункте необходимо выбрать задачу, выполняемую над диском (разделом диска), то есть создание образа диска (раздела), восстановление диска (раздела) из образа или создание загрузочного образа диска (флешки).

1. Выбираю строку &#8220;recovery-iso-zip&#8221; – создать загрузочный &#8220;recovery disk&#8221; (iso – для создания загрузочного диска, zip – для создания загрузочной флешки):<figure id="attachment_654" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_make-recovery-disk-600x449.jpg" alt="Clonezilla - создание загрузочного диска" width="600" height="449" class="size-medium wp-image-654" />][20]<figcaption class="wp-caption-text">Clonezilla &#8211; создание загрузочного диска</figcaption></figure> 

2. Clonezilla найдет автоматически все уже созданные образы, имеющиеся на примонтированном в /home/partimag разделе. На скрине видно, что у меня их два – образ ArchLinux‘а и образ Windows XP. Выбираю последний и нажимаю Enter:<figure id="attachment_655" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_file-image-to-restore-600x450.jpg" alt="Clonezilla - найти созданные образы" width="600" height="450" class="size-medium wp-image-655" />][21]<figcaption class="wp-caption-text">Clonezilla &#8211; найти созданные образы</figcaption></figure> 

3. Здесь система спрашивает, какой раздел жесткого диска требуется восстановить:<figure id="attachment_656" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_select-image-to-restore-600x449.jpg" alt="Clonezilla - раздел жесткого диска для восстановления" width="600" height="449" class="size-medium wp-image-656" />][22]<figcaption class="wp-caption-text">Clonezilla &#8211; раздел жесткого диска для восстановления</figcaption></figure> 

4. Выбрать язык и кодировку консоли Clonezilla LiveCD:<figure id="attachment_657" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_console-600x449.jpg" alt="Clonezilla - язык и кодировка консоли" width="600" height="449" class="size-medium wp-image-657" />][23]<figcaption class="wp-caption-text">Clonezilla &#8211; язык и кодировка консоли</figcaption></figure> 

5. Выбрать раскладку клавиатуры. По умолчанию параметр None имеет значение американской раскладки «us«. Можно выбрать другую, по пути, подсказанному в шапке окна:<figure id="attachment_658" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_keymap-600x449.jpg" alt="Выбор раскладки клавиатуры Clonezilla" width="600" height="449" class="size-medium wp-image-658" />][24]<figcaption class="wp-caption-text">Выбор раскладки клавиатуры Clonezilla</figcaption></figure> 

6. Последнее окно – что мы хотим сделать из образа:

  * iso – создать загрузочный образ для прожига на CD/DVD-болванку;
  * zip – создать загрузочный образ для записи его на флешку;
  * both – создать сразу iso-образ и zip-образ.

Выбираю первую строку – iso – и нажимаю Enter:<figure id="attachment_659" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_iso-image-to-burn-600x449.jpg" alt="Clonezilla - загрузочный образ для прожига" width="600" height="449" class="size-medium wp-image-659" />][25]<figcaption class="wp-caption-text">Clonezilla &#8211; загрузочный образ для прожига</figcaption></figure> 

7. Система выводит на экран полную команду, которую она собирается выполнить и просит нашего подтверждения. Нажимаю Enter:<figure id="attachment_660" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_type-of-file-for-recovery-600x449.jpg" alt="Clonezilla - подтверждение выполнения команды" width="600" height="449" class="size-medium wp-image-660" />][26]<figcaption class="wp-caption-text">Clonezilla &#8211; подтверждение выполнения команды</figcaption></figure> 

8. Clonezilla копирует файлы образа в рабочую директорию и подсчитывает размер iso-образа, который должен получиться. Если iso-образ больше по объему, чем CD или DVD-болванка, программа заботливо сообщает об этом и просит подтвердить выбор, если мы знаем, что делаем:<figure id="attachment_661" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_confirm-of-size-image-600x449.jpg" alt="Подтверждение действий Clonezilla" width="600" height="449" class="size-medium wp-image-661" />][27]<figcaption class="wp-caption-text">Подтверждение действий Clonezilla</figcaption></figure> 

9. Я буду создавать образ размером с DVD-болванку (а программа предупреждает о слишком большом размере для CD-болванки), поэтому даю утвердительный ответ. Процесс пошел:<figure id="attachment_662" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_make-iso-image-process-600x449.jpg" alt="Процесс создания iso-образа в Clonezilla" width="600" height="449" class="size-medium wp-image-662" />][28]<figcaption class="wp-caption-text">Процесс создания iso-образа в Clonezilla</figcaption></figure> 

10. По окончании процесса Clonezilla опять выведет меню с выбором дальнейших действий. Выбираю 1 для перезагрузки. Дальше полученный образ можно записать на болванку в любой программе для записи. Диск аварийного восстановления Windows XP готов:<figure id="attachment_663" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_iso-recovery-finished-600x449.jpg" alt="Процесс Clonezilla завершен" width="600" height="449" class="size-medium wp-image-663" />][29]<figcaption class="wp-caption-text">Процесс Clonezilla завершен</figcaption></figure> 

P.S.

1. Clonezilla не умеет разделять полученный образ на несколько частей, если размер образа больше размера болванки CD или DVD.

2. При создании мануальчика столкнулся со следующей проблемой – снятие скриншотов в консоли Clonezilla. Консольных утилит для снятия скриншотов (fbgrab, fbshot, fbdump, fbcat или что-либо подобное) в дистрибутиве я не нашел. Решил задачу в скачивании deb-пакета fbgrab и его установки через dpkg (хоть это есть в Clonezilla). С вопросом по поводу данного неудобства обратился на форум Clonezilla:

> I have a question. How can I make screenshots, when I start Clonezilla? I need such screens for me. I can’t find such applications as fbgrab or fbshot in Clonezilla. And I never take screenshots in pure console (only X). Please, help me.

На что мною был получен ответ:

> Thanks for this idea. fbgrab was added to Clonezilla live 1.2.4-14, and it’s available in testing branch. Please give it a try. Steven

Оцените статью:  
<span id="post-ratings-633" class="post-ratings" data-nonce="f2585357bc"><img id="rating_633_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(633, 1, '1 Star');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_633_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(633, 2, '2 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_633_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(633, 3, '3 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_633_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(633, 4, '4 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_633_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(633, 5, '5 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>11</strong> votes, average: <strong>4,91</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_633_text"></span></span><span id="post-ratings-633-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/04/ocs-01-bootmenu.jpg
 [2]: http://localhost:7788/third/wp-content/uploads/2013/04/ocs-02-booting.jpg
 [3]: http://localhost:7788/third/wp-content/uploads/2013/04/ocs-03-lang.jpg
 [4]: http://localhost:7788/third/wp-content/uploads/2013/04/ocs-04-keymap.jpg
 [5]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_login-in-system.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_device-image.jpg
 [7]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_local_dev.jpg
 [8]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_disk-scan.jpg
 [9]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_select-partition.jpg
 [10]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_store-images.jpg
 [11]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_beginner.jpg
 [12]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_saveparts.jpg
 [13]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_image-name.jpg
 [14]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_scan-hard-disk.jpg
 [15]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_list-images.jpg
 [16]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_confirm-command.jpg
 [17]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_double-confirm.jpg
 [18]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_start-process.jpg
 [19]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_next-steps.jpg
 [20]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_make-recovery-disk.jpg
 [21]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_file-image-to-restore.jpg
 [22]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_select-image-to-restore.jpg
 [23]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_console.jpg
 [24]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_keymap.jpg
 [25]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_iso-image-to-burn.jpg
 [26]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_type-of-file-for-recovery.jpg
 [27]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_confirm-of-size-image.jpg
 [28]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_make-iso-image-process.jpg
 [29]: http://localhost:7788/third/wp-content/uploads/2013/04/clonezilla_iso-recovery-finished.jpg