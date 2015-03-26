---
title: "Установка LiveReload в Sublime Text 2"
layout: post
categories: sublime text
tags: [sublime text, livereload]
share: true
---

В предыдущей статье, посвященной вопросу автообновления страниц в окне браузера, я упоминал об плагине для редактора Sublime Text 2 под названием LiveReload. Сегодня я вернусь к этому вопросу и выполню установку этого плагина. Она проста - там нет ничего сложного.

Итак, приступаем к установке и настройке LiveReload в Sublime Text 2.

Первое, что необходимо сделать, это установить менеджер пакетов в редакторе. Установка пакетов в Sublime Text может выполняться двумя способами - *вручную* или же *автоматически*. Последний способ более простой и удобный, поэтому воспользуюсь им.

## Установка менеджера пакетов

Открываем Sublime Text и переходим в меню по пути "View - Show Console" или же нажимаем сочетание клавиш `Ctrl + \`, затем копируем и вставляем нижеприведенный код в окно консоли:

{% highlight powershell %}
import urllib2,os; pf=&#8217;Package Control.sublime-package'; ipp=sublime.installed_packages_path(); os.makedirs(ipp) if not os.path.exists(ipp) else None; urllib2.install_opener(urllib2.build_opener(urllib2.ProxyHandler())); open(os.path.join(ipp,pf),&#8217;wb&#8217;).write(urllib2.urlopen(&#8216;http://sublime.wbond.net/&#8217;+pf.replace(&#8216; &#8216;,&#8217;%20&#8242;)).read()); print(&#8216;Please restart Sublime Text to finish installation&#8217;)
{% endhighlight %}

Жмем "Enter" и затем закрываем и снова открываем Sublime Text, чтобы изменения вступили в силу. Менеджер пакетов установлен.

## Установка LiveReload

Переходим к установке плагина LiveReload в Sublime Text 2. Переходим в меню по пути "Preferences - Package Control":

<figure id="attachment_432" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-package_contol-600x446.png" alt="Sublime Package Control" width="600" height="446" class="size-medium wp-image-432" />][1]
	<figcaption class="wp-caption-text">Sublime Package Control</figcaption>
</figure>

В менеджере пакетов выбираем из списка пункт "Package Control: Install Package":

<figure id="attachment_433" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-install_package-600x446.png" alt="Sublime Install Package" width="600" height="446" class="size-medium wp-image-433" />][2]
	<figcaption class="wp-caption-text">Sublime Install Package</figcaption>
</figure>

Немного подождем, пока загрузится список пакетов. Затем в окне поиска введем имя пакета - "LiveReload":

<figure id="attachment_434" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-livereload-600x446.png" alt="Sublime LiveReload" width="600" height="446" class="size-medium wp-image-434" />][3]
	<figcaption class="wp-caption-text">Sublime LiveReload</figcaption>
</figure>

Жмем "Enter" - пара секунд и плагин установлен. Снова перезагружаем редактор, чтобы изменения вступили в силу:

<figure id="attachment_435" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-restart-600x446.png" alt="Sublime Restart" width="600" height="446" class="size-medium wp-image-435" />][4]
	<figcaption class="wp-caption-text">Sublime Restart</figcaption>
</figure>

## Установка расширения LiveReload в Chrome

Плагин LiveReload работает совместно с одноименным расширением, которое устанавливается в браузер. В моем случае это будет Google Chrome. Приступаю к установке.

В настройках Chrome перехожу в раздел с расширениями и ввожу в строку поиска имя плагина - "LiveReload":

<figure id="attachment_436" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/livereload-chrome-600x375.jpg" alt="Установка LiveReload в Google Chrome" width="600" height="375" class="size-medium wp-image-436" />][5]
	<figcaption class="wp-caption-text">Установка LiveReload в Google Chrome</figcaption>
</figure>

Соглашаюсь со всем и жму кнопочку "Установить". Перезагрузки браузера не требуется - в панели инструментов сразу появляется значок расширения в виде двух круговых стрелочек.

Установка расширения произведена.

## Тестирование плагина LiveReload

Открываю в Sublime Text 2 редактируемый HTML-файл. И открываю его же в браузере Google Chrome. Нажимаю мышью на значок расширения LiveReload в панели инструментов и вижу в строке статуса следующее:

<figure id="attachment_437" style="width: 600px;" class="wp-caption aligncenter">
	[<img src="http://localhost:7788/third/wp-content/uploads/2013/11/sublime-livereload-connected-600x446.jpg" alt="Sublime LiveReload Connected" width="600" height="446" class="size-medium wp-image-437" />][6]
	<figcaption class="wp-caption-text">Sublime LiveReload Connected</figcaption>
</figure>

Это говорит о том, что плагин в редакторе Sublime Text 2 успешно подключился к плагину LiveReload в браузере. Можно приступать к работе. Изменяю код в файле, сохраняю изменения и вижу, как они автоматически применились в окне Chrome.

## Заключение

Применение плагина LiveReload мне кажется более удобным, нежели расширения, рассмотренные в предыдущей статье. Хотя бы тем, что изменения автоматически вступают в силу, не нужно ждать даже 1 секунды. Главное, не забыть нажать сочетание клавиш <kbd>Ctrl + S</kbd>. Вот если бы и этого не нужно было делать, было бы совсем замечательно!.

На этом все.

---
