---
title: 'Менеджер паролей KeepassX &#8211; установка в openSUSE 12.3 Linux'
author: gearmobile
layout: post
permalink: /%d0%bc%d0%b5%d0%bd%d0%b5%d0%b4%d0%b6%d0%b5%d1%80-%d0%bf%d0%b0%d1%80%d0%be%d0%bb%d0%b5%d0%b9-keepassx-%d1%83%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%ba%d0%b0-%d0%b2-opensuse-12-3-linux/
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
  - keepassx
---
Приложение KeepassX является менеджером паролей с графическим интерфейсом. Программа очень удобна в использовании. С помощью нее можно хранить большое количество паролей и логинов к множеству учетных записей в Интернете. Представьте, что у вас есть несколько почтовых ящиков, несколько учетных записей на сервисах торрентов, вы зарегистрированы в различных социальны сетях. Для каждой из учетных записей, по минимальным требованиям безопасности, необходим свой логин, который не должен повторяться; и пароль, также уникальный и имеющий определенную длину и уровень сложности.

Естественно, запомнить все учетные записи в таком случае просто не реально. Вот тут и приходит на помощь менеджер паролей KeepassX. Все создаваемые учетные записи хранятся в одном шифрованном файле, и нужно помнить один единственный пароль только к нему.

KeepassX имеет удобный и информативный интерфейс, с помощью которого можно хранить самые разнообразные данные. Проще говоря, эта программа очень существенно облегчает жизнь. Без нее нормальная работа в Интернет становится крайне не удобной. Поэтому приложение можно смело отнести к разряду must have.

В дистрибутивах, основанных на Debian (таких как Ubuntu, Mint и многих других) с установкой программы KeepassX не существует каких-либо проблем. Пакет входит в стандартные репозитории этих операционных систем. Но вот с openSUSE здесь несколько сложнее, так как в репозиториях этого дистрибутива по умолчанию такой программы нет.

### KeepassX в openSUSE 12.3 &#8211; последовательность действий

1. Открываем Центр управления YAST и в нем переходим &#8220;Программное обеспечение &#8211; Репозитории программного обеспечения&#8221;. Это необходимо для добавления стороннего репозитория, содержащего пакет KeepassX:<figure id="attachment_539" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/opensuse_yast-600x413.png" alt="Центр управления YAST" width="600" height="413" class="size-medium wp-image-539" />][1]<figcaption class="wp-caption-text">Центр управления YAST</figcaption></figure> 

2. В открывшемся окне добавляем URL-адрес репозитория &#8211; http://download.opensuse.org/repositories/security:/passwordmanagement/openSUSE\_12.1/. После несложной процедуры настройки получаем добавленный репозиторий в систему openSUSE12.3. В моем случае он имеет несколько нелогичное имя openSUSE\_12.1. Ну пусть будем таким, в принципе &#8211; какая разница. Хотя, для порядка, должно называться более информативно&#8230; Жмем ОК:<figure id="attachment_541" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/opensuse_add_repository_keepassx-600x479.png" alt="Добавленный репозиторий с пакетом KeepassX" width="600" height="479" class="size-medium wp-image-541" />][2]<figcaption class="wp-caption-text">Добавленный репозиторий с пакетом KeepassX</figcaption></figure> 

3. Все готово для установки программы KeepassX. Переходим в YAST в пункт &#8220;Управление программным обеспечением&#8221;. Откроется окно со множеством настроек. Но в нем потребуется только два элемента &#8211; поле для ввода имени пакета и кнопка &#8220;Поиск&#8221;. Вводим в поле имя нужного нам пакета keepassx и нажимаем кнопку &#8220;Поиск&#8221;. В правом окне почти моментально видим результат:<figure id="attachment_540" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/yast_keepassx-600x444.png" alt="Установка программы KeepassX" width="600" height="444" class="size-medium wp-image-540" />][3]<figcaption class="wp-caption-text">Установка программы KeepassX</figcaption></figure> 

Отмечаем галочкой пакет keepassx и жмем на кнопочку &#8220;Принять&#8221; в правом нижнем углу. YAST спросит подтверждения об установке дополнительных зависимостей и затем выполнит инсталляцию программы KeepassX.

4. Можно закрывать &#8220;Центр управления YAST&#8221;. Переходим в главное меню KDE и в строке поиска вводим KeepassX, чтобы долго не блуждать по различным пунктам меню типа Интернет, Офис и тому подобное.

5. Все, менеджер пакетов KeepassX установлен и готов к работе.

Оцените статью:  
<span id="post-ratings-538" class="post-ratings" data-nonce="590d767412"><img id="rating_538_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(538, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_538_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(538, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_538_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(538, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_538_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(538, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_538_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(538, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_538_text"></span></span><span id="post-ratings-538-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/opensuse_yast.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/opensuse_add_repository_keepassx.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/yast_keepassx.png