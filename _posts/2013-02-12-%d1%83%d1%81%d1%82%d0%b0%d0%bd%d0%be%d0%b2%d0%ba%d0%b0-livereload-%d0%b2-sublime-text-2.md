---
title: Установка LiveReload в Sublime Text 2
author: gearmobile
layout: post
permalink: /%d1%83%d1%81%d1%82%d0%b0%d0%bd%d0%be%d0%b2%d0%ba%d0%b0-livereload-%d0%b2-sublime-text-2/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 4
ratings_score:
  - 15
ratings_average:
  - 3.75
categories:
  - Web Tools
---
В предыдущей статье, посвященной вопросу автообновления страниц в окне браузера, я упоминал об плагине для редактора Sublime Text 2 под названием LiveReload. Сегодня я вернусь к этому вопросу и выполню установку этого плагина. Она проста &#8211; там нет ничего сложного.

Итак, приступаем к установке и настройке LiveReload в Sublime Text 2.

Первое, что необходимо сделать, это установить менеджер пакетов в редакторе. Установка пакетов в Sublime Text может выполняться двумя способами &#8211; вручную или же автоматически. Последний способ более простой и удобный, поэтому воспользуюсь им.

### Установка менеджера пакетов

Открываем Sublime Text и переходим в меню по пути View &#8211; Show Console или же нажимаем сочетание клавиш Ctrl + \`, затем копируем и вставляем нижеприведенный код в окно консоли:

<textarea cols="80" rows="5">import urllib2,os; pf=&#8217;Package Control.sublime-package'; ipp=sublime.installed_packages_path(); os.makedirs(ipp) if not os.path.exists(ipp) else None; urllib2.install_opener(urllib2.build_opener(urllib2.ProxyHandler())); open(os.path.join(ipp,pf),&#8217;wb&#8217;).write(urllib2.urlopen(&#8216;http://sublime.wbond.net/&#8217;+pf.replace(&#8216; &#8216;,&#8217;%20&#8242;)).read()); print(&#8216;Please restart Sublime Text to finish installation&#8217;)</textarea>

Жмем Enter и затем закрываемснова открываем Sublime Text, чтобы изменения вступили в силу. Менеджер пакетов установлен.

### Установка LiveReload

Переходим к установке плагина LiveReload в Sublime Text 2.

Переходим в меню по пути &#8220;Preferences &#8211; Package Control&#8221;:<figure id="attachment_432" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-package_contol-600x446.png" alt="Sublime Package Control" width="600" height="446" class="size-medium wp-image-432" />][1]<figcaption class="wp-caption-text">Sublime Package Control</figcaption></figure> 

В менеджере пакетов выбираем из списка пункт Package Control: Install Package:<figure id="attachment_433" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-install_package-600x446.png" alt="Sublime Install Package" width="600" height="446" class="size-medium wp-image-433" />][2]<figcaption class="wp-caption-text">Sublime Install Package</figcaption></figure> 

Немного подождем, пока загрузится список пакетов. Затем в окне поиска введем имя пакета &#8211; LiveReload:<figure id="attachment_434" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-livereload-600x446.png" alt="Sublime LiveReload" width="600" height="446" class="size-medium wp-image-434" />][3]<figcaption class="wp-caption-text">Sublime LiveReload</figcaption></figure> 

Жмем Enter &#8211; пара секунд и плагин установлен. Снова перезагружаем редактор, чтобы изменения вступили в силу:<figure id="attachment_435" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-restart-600x446.png" alt="Sublime Restart" width="600" height="446" class="size-medium wp-image-435" />][4]<figcaption class="wp-caption-text">Sublime Restart</figcaption></figure> 

### Установка расширения LiveReload в Chrome

Плагин LiveReload работает совместно с одноименным расширением, которое устанавливается в браузер. В моем случае это будет Google Chrome. Приступаю к установке.

В настройках Chrome перехожу в раздел с расширениями и ввожу в строку поиска имя плагина &#8211; LiveReload:<figure id="attachment_436" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/livereload-chrome-600x375.jpg" alt="Установка LiveReload в Google Chrome" width="600" height="375" class="size-medium wp-image-436" />][5]<figcaption class="wp-caption-text">Установка LiveReload в Google Chrome</figcaption></figure> 

Соглашаюсь со всем и жму кнопочку &#8220;Установить&#8221;. Перезагрузки браузера не требуется &#8211; в панели инструментов сразу появляется значок расширения в виде двух круговых стрелочек.

Установка расширения произведена.

### Тестирование плагина LiveReload

Открываю в Sublime Text 2 редактируемый HTML-файл. И открываю его же в браузере Google Chrome. Нажимаю мышью на значок расширения LiveReload в панели инструментов и вижу в строке статуса следующее:<figure id="attachment_437" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-livereload-connected-600x446.jpg" alt="Sublime LiveReload Connected" width="600" height="446" class="size-medium wp-image-437" />][6]<figcaption class="wp-caption-text">Sublime LiveReload Connected</figcaption></figure> 

Это говорит о том, что плагин в редакторе Sublime Text 2 успешно подключился к плагину LiveReload в браузере. Можно приступать к работе. Изменяю код в файле, сохраняю изменения и вижу, как они автоматически применились в окне Chrome.

### Заключение

Применение плагина LiveReload мне кажется более удобным, нежели расширения, рассмотренные в предыдущей статье. Хотя бы тем, что изменения автоматически вступают в силу, не нужно ждать даже 1 секунды. Главное, не забыть нажать сочетание клавиш Ctrl + S. Вот если бы и этого не нужно было делать, было бы совсем замечательно! )).

Оцените статью:  
<span id="post-ratings-431" class="post-ratings" data-nonce="dedb31d57a"><img id="rating_431_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(431, 1, '1 Star');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_431_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(431, 2, '2 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_431_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(431, 3, '3 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_431_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(431, 4, '4 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_431_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(431, 5, '5 Stars');" onmouseout="ratings_off(3.8, 4, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>4</strong> votes, average: <strong>3,75</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_431_text"></span></span><span id="post-ratings-431-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2013/11/sublime-package_contol.png
 [2]: http://localhost:7788/third/wp-content/uploads/2013/11/sublime-install_package.png
 [3]: http://localhost:7788/third/wp-content/uploads/2013/11/sublime-livereload.png
 [4]: http://localhost:7788/third/wp-content/uploads/2013/11/sublime-restart.png
 [5]: http://localhost:7788/third/wp-content/uploads/2013/11/livereload-chrome.jpg
 [6]: http://localhost:7788/third/wp-content/uploads/2013/11/sublime-livereload-connected.jpg