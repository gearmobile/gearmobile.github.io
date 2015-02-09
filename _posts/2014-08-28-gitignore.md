---
title: 'gitignore &#8211; игнорирование файлов в Git'
author: gearmobile
excerpt: Cоздание файла .gitignore для игнорирования файлов и директорий в системе Git. Показаны примеры настройки файла .gitignore для игнорирования файлов и папок.
layout: post
permalink: /gitignore/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 3
ratings_score:
  - 15
ratings_average:
  - 5
categories:
  - Кодинг
tags:
  - git
  - gitignore
---
В системе Git можно настроить возможность автоматического **игнорирования файлов**. То есть, можно указать Git, что файлы определенного типа **не нужно отслеживать**. Выполняется такая настройка с помощью специального файла `.gitignore`. Подобная возможность отключения отслеживания файлов в системе Git может понадобиться в случае, когда автоматически генерируются **служебные файлы**.

К примеру, если развертывать в проекте Compass, то будет создан каталог `.sass`, в который данный фреймворк помещает свой кэш, генерируемый автоматически при каждом изменении любого из файлов проекта.

Давайте на практике разберемся, каким образом можно настроить **игнорирование файлов** в Git с помощью `.gitignore`.

### Создание нового проекта

Создаю новый проект с именем `git_ignore`, в котором помещаю несколько файлов разного типа:

<pre>$ mkdir git_ignore
    $ cd git_ignore/
    $ touch index.html style.css
  </pre>

Инициализирую репозиторий Git в директории `.git_ignore`, индексирую созданные файлы и фиксирую их:

<pre>$ git init
    Initialized empty Git repository in /home/aaron/Projects/git_ignore/.git/
    $ git add .
    $ git commit -m 'First Commit'
  </pre>

Вывод команды `git status` показывает, что все чисто:

<pre>$ git status
    On branch master
    nothing to commit, working directory clean
  </pre>

### Настройка игнорирования в .gitignore

Для настройки игнорирования определенных типов файлов в системе Git необходимо первоначально создать файл `.gitignore`:

<pre>$ touch .gitignore
  </pre>

Откроем созданный файл `.gitignore` в любом редакторе:

<pre>$ nano -w .gitignore
  </pre>

&#8230; и пропишем в нем следующие строки:

<pre>*.txt
    *.md
  </pre>

Тем самым мы говорим Git, что нужно игнорировать все файлы с расширением `.txt` и `.md` внутри директории `git_ignore`. То есть, система контроля не будет отслеживать изменения во всех файлах этих типов.

Проиндексируем и зафиксируем изменения (создание файла настроек `.gitignore`), а затем проверим данный факт. Для этого в рабочей директории `git_ignore` создаю еще несколько типов файлов:

<pre>$ touch main.css readme.txt humans.md
  </pre>

Затем выполняю индексацию всех файлов, которые были добавлены или изменены в рабочем каталоге:

<pre>$ git add .
  </pre>

И смотрю, что мне показывает команда `git status`:

<pre>$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD &lt;file>..." to unstage)

      new file:   main.css

  </pre>

Система Git увидела только новый файл `main.css`. Два других файла &#8211; `readme.txt` и `humans.md` &#8211; проигнорированы системой. Отлично! Зафиксирую изменения.

Можно создать еще пару файлов в разных директориях и посмотреть на вывод команды `git status` в консоли:<figure id="attachment_1720" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/gitignore-600x304.png" alt="Результат настройки файла .gitignore" width="600" height="304" class="size-medium wp-image-1720" />][1]<figcaption class="wp-caption-text">Результат настройки файла .gitignore</figcaption></figure> 

### Усложнить задачу игнорирования в .gitignore

Можно усложнить задачу игнорирования в Git, добавив в файл `.gitignore` директорию, содержимое которой также должно игнорироваться. Пускай это будет обычная директория `ignore` и скрытая директория `.ignore` (с точкой перед именем):

Добавлю в файл `.gitignore` пару строк таким образом:

<pre>$ cat .gitignore
    *.txt
    *.md
    ignore/
    .ignore/
  </pre>

Проиндексирую изменения, а затем выполню операции по созданию директорий и файлов внутри них:

<pre>$ mkdir ignore
    $ mkdir .ignore
    $ touch ignore/reset.css
    $ touch .ignore/normilize.css
  </pre>

Вновь ввожу команду просмотра состояния репозитория Git:

<pre>$ git status
    On branch master
    nothing to commit, working directory clean
  </pre>

Все сработало &#8211; Git не захотел видеть директории `ignore`, `.ignore`, а также их содержимое. Отлично!

### Шаблоны в файле .gitignore

Для файла `.gitignore` доступны шаблоны, с помощью которых можно задать маски для выборки необходимых типой файлов. Однако, обширная тема шаблонов выходит за рамки данной статьи. При желании можно почитать по теме шаблонов в книге &#8220;[Pro Git &#8211; профессиональный контроль версий][2]&#8220;.

Оцените статью:  
<span id="post-ratings-1716" class="post-ratings" data-nonce="c024202154"><img id="rating_1716_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1716, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1716_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1716, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1716_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1716, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1716_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1716, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1716_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1716, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>3</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1716_text"></span></span><span id="post-ratings-1716-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/08/gitignore.png
 [2]: http://git-scm.com/book/ru "Pro Git - профессиональный контроль версий"