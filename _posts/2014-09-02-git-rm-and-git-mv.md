---
title: 'git rm и git mv &#8211; удаление и переименование в Git'
author: gearmobile
layout: post
---
Еще один важный практический вопрос при работе с Git &#8211; это операции с файлами. В частности, это операции удаления и переименования файлов. В системе [Git][1] имеются специальные команды, которые очень похожи на консольные команды `rm` и `mv` в Linux/Mac OS. Но для Git они выглядят несколько иначе: `git rm` &#8211; для удаления файлов и `git mv` &#8211; для переименования файлов. Ниже я рассмотрю обе эти комадны более подробно.

### Команда git rm

Для удаления файлов в системе Git, как уже упоминалось выше, имеется специальная команда `git rm`. Ее отличие от обычной консольной команды `rm` (в том же Linux) заключается в особенности самой системы Git.

Как хорошо известно, в системе Git файл может одновременно существовать в трех ипостасях: в области Working Directory, в области Staging Area, в области Repository. Удаление файла из области Working Directory не приведет к его удалению из областей Staging Area и Repository.

Поэтому, чтобы удалить файл, нужно (в идеале) выполнить три команды подряд для удаления файла из Рабочей области (Working Directory), затем из области индекса (Staging Area) и потом из области репозитория (Repository):

<pre>$ rm index.html
  $ git add .
  $ git commit -m 'Delete file index.html'
</pre>

Команда `git rm` является ни чем иным, как &#8220;вшитым&#8221; в Git сокращением двух первых команд:

<pre>$ rm index.html
  $ git add .
</pre>

Сделано это всего лишь для удобства пользования системой Git. Давайте на примере посмотрим работу команды `git rm`. Предположим, что имеется файл index.html, который проиндексирован и зафиксирован. Удалим его командой `git rm`:<figure id="attachment_1753" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-rm-600x304.png" alt="Команда git rm - удаление файлов в Git" width="600" height="304" class="size-medium wp-image-1753" />][2]<figcaption class="wp-caption-text">Команда git rm &#8211; удаление файлов в Git</figcaption></figure> 

Видим, что файл index.html был сразу удален из двух областей: рабочего каталога Working Directory и области индексации Staging Area. Но в репозитории файл все же остался, о чем говорит вывод команды `git status`. Любой последующий commit зафиксирует удаление этого файла:<figure id="attachment_1754" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_commit_deletion-600x304.png" alt="Фиксация удаления файла командой git rm" width="600" height="304" class="size-medium wp-image-1754" />][3]<figcaption class="wp-caption-text">Фиксация удаления файла командой git rm</figcaption></figure> 

#### Команда git rm &#8211;cached

У команды `git rm` имеется пара полезных ключей, одним из которых является ключ `--cached`. Задача этого ключа &#8211; позволить команде `git rm` удалить файл из области индексирования (Staging Area), но при этом оставить его в области рабочего проекта (Working Directory). Давайте рассмотрим пример, когда создан файл `second.html` и произведена его индексация (но не фиксация):<figure id="attachment_1755" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_second-html-600x304.png" alt="Созданный файл second.html" width="600" height="304" class="size-medium wp-image-1755" />][4]<figcaption class="wp-caption-text">Созданный файл second.html</figcaption></figure> 

Удалим его командой `git rm --cached`:<figure id="attachment_1756" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_cached-600x304.png" alt="Команда git rm --cached" width="600" height="304" class="size-medium wp-image-1756" />][5]<figcaption class="wp-caption-text">Команда git rm &#8211;cached</figcaption></figure> 

Отлично! Видим, что произошло удаление файла `second.html`. Кроме того, команда `git status` показывает, что в рабочей области Working Directory имеется неотслеживаемый (untracked) файл по имени `second.html`.

#### Команда git rm -f

В предыдущем разделе я рассмотрел вариант, когда созданный и проиндексированный файл удаляется из области индексирования (Staging Area), но остается в области Working Directory. Выполняется это с помощью команды `git rm --cached`.

Логическим продолжением этой команды является та же самая команда `git rm`, но с ключом `-f` &#8211; `git rm -f`. Такая команда удаляет проиндексированный (но еще не зафиксированный) файл как из области Staging Area, так и из области Working Directory.

Давайте рассмотрим на примере созданного и проиндексированного файла `third.html` его удаление с помощью команды `git rm -f`:<figure id="attachment_1757" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_third-html-600x304.png" alt="Созданный файл third.html" width="600" height="304" class="size-medium wp-image-1757" />][6]<figcaption class="wp-caption-text">Созданный файл third.html</figcaption></figure> <figure id="attachment_1758" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_f-600x304.png" alt="Команда git rm -f" width="600" height="304" class="size-medium wp-image-1758" />][7]<figcaption class="wp-caption-text">Команда git rm -f</figcaption></figure> 

Файл `third.html` удален как из области Staging Area, так и из области Working Directory. В итоге можно сказать, что между командой `git rm -f` и командой `git rm` практически нет никакой разницы.

### Команда git mv &#8211; перемещение или переименование файлов

В системе Git имеется &#8220;своя&#8221; команда для перемещения или переименования файлов. Слово &#8220;своя&#8221; здесь не даром взято в кавычки &#8211; аналогия с командой `git rm` полная. Команда `git mv` перемещает или переименовывает файлы, автоматически &#8220;уведомляя&#8221; об этих событиях область Staging Area:<figure id="attachment_1759" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-mv-600x304.png" alt="Команда git mv - перемещение файла в Git" width="600" height="304" class="size-medium wp-image-1759" />][8]<figcaption class="wp-caption-text">Команда git mv &#8211; перемещение файла в Git</figcaption></figure> 

Остается только зафиксировать эти изменения любым коммитом:

<pre>$ git commit -m 'Move index.html to papka'
  [master 868d428] Move index.html to papka
   1 file changed, 0 insertions(+), 0 deletions(-)
   rename index.html => papka/index.html (100%)
</pre>

Переименуем файл `index.html` с помощью команды `git mv`:<figure id="attachment_1760" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git-mv_index-600x304.png" alt="Команда git mv - переименование файла в Git" width="600" height="304" class="size-medium wp-image-1760" />][9]<figcaption class="wp-caption-text">Команда git mv &#8211; переименование файла в Git</figcaption></figure> 

Вот и все несложные операции по перемещению\переименованию или удалению файлов с помощью команд `git rm` и `git mv`, под всевидящим оком Git.

 [1]: http://git-scm.com/ "Git"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/09/git-rm.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_commit_deletion.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_second-html.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_cached.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_third-html.png
 [7]: http://localhost:7788/third/wp-content/uploads/2014/09/git-rm_f.png
 [8]: http://localhost:7788/third/wp-content/uploads/2014/09/git-mv.png
 [9]: http://localhost:7788/third/wp-content/uploads/2014/09/git-mv_index.png