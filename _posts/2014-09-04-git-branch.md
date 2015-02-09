---
title: 'Git &#8211; создание ветвей (branch)'
author: gearmobile
excerpt: Рассмотрен вопрос создания ветвей (branch) в Git. Перемещение (checkout) между ветвями, слияние (merge) ветвей. А также удаление (-d) ветвей в системе Git.
layout: post
permalink: /git-branch/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 2
ratings_score:
  - 10
ratings_average:
  - 5
categories:
  - Кодинг
tags:
  - git
  - git branch
---
Продолжаю совместно с вами постепенно изучать магию Git\GitHub. Слово магия здесь применено не случайно &#8211; не иначе, как магией возможности Git\GitHub не назовешь. По крайней мере, я впечатлен этими возможностями. Другое дело, что процесс изучения Git у меня лично идет как-то тяжеловато. Ну, это не страшно &#8211; главное, не останавливаться!

В этом разделе я попытаюсь осветить для себя (и возможно, для вас, уважаемый читатель) вопрос создания ветвей (branches) в Git, перемещение между ветвями (branches), слияние (merge) ветвей. Этот вопрос очень подробно и хорошо описан на странице официальной документации &#8211; [Git Branching &#8211; Basic Branching and Merging][1]. Здесь я попробую самостоятельно описать данный вопрос.

### Инициализация Git-репозитория

Создаю тестовую директорию `git_branches`, в которой будут производиться эксперименты по созданию ветвей в Git. Внутри этой директории создаю два файла &#8211; индексный файл и файл таблиц стилей. А затем инициализирую Git-репозиторий, добавляю созданные файлы под версионный контроль Git:

<pre>$ mkdir git_branches
    $ cd git_branches
    $ touch index.html
    $ touch style.css

    $ git init
    Initialized empty Git repository in /home/username/Desktop/projects/git_branches/.git/

    $ git add .
    $ git commit -m 'first launch'
    [master (root-commit) eeb12ca] first launch
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 index.html
     create mode 100644 style.css

    $ git status
    On branch master
    nothing to commit, working directory clean
  </pre>

Обратите на строку `On branch master` в выводе команды `git status`. Это не пустой набор служебной информации &#8211; здесь говориться о том, что в ветви `master` нечего фиксировать и рабочая директория чистая.

Итак, мы уже кое-что узнали. А именно &#8211; при инициализации Git-репозитория была автоматически создана ветвь (branch) по имени `master`. И на данный момент мы находимся в этой ветви.

Конечно, на самом деле это пока мало о чем говорит, так как не с чем сравнивать. Поэтому давайте я немного отредактирую оба файла `index.html` и `style.css`, проиндексирую\зафиксирую их.

В браузере примерный вид странички будет выглядеть таким образом:<figure id="attachment_1769" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git_master_branch-600x501.png" alt="Git - ветвь (branch) master" width="600" height="501" class="size-medium wp-image-1769" />][2]<figcaption class="wp-caption-text">Git &#8211; ветвь (branch) master</figcaption></figure> 

### Git &#8211; создание новой ветви (branch)

В системе Git (как уже упоминалось ранее) имеется механизм ветвления (branches). Попробую на словах объяснить, что он из себя представляет.

Допустим, в моем текущем проекте, у которого имеются два файла, нужно внести кардинальные изменения. Причем, изменения такого рода, что они могут нарушить работу уже существующего проекта. Чтобы обезопасить себя (подстраховать), создаю точную копию существующего проекта и перехожу в нее для дальнейшей работы.

Давайте я на практике осуществлю вышесказанные действия. Для этого создаю новую ветвь с произвольным именем `second`, которая на этом этапе будет точной копией ветви `master`:

<pre>$ git checkout -b second
    Switched to a new branch 'second'
  </pre>

Строка `Switched to a new branch 'second'` услужливо информирует, что меня автоматически &#8220;перебросило&#8221; во вновь ветвь `second`. Можно проверить себя, набрав в консоли:

<pre>$ git status
    On branch second
    nothing to commit, working directory clean
  </pre>

Строка `On branch second` говорит сама за себя.

Отлично! Теперь давайте я внесу некоторые изменения в файлы `index.html` и `style.css` и мы вместе посмотрим на результат в окне браузера. Изменения будут касаться добавления блока-обертки, еще нескольких параграфов и другой легкой стилизации.

Не забуду также проиндексировать и зафиксировать внесенные изменения. Обратите внимание на вид команды &#8211; `git commit -a`. Эта команда является сокращенным вариантом двух команд: `git add` и `git commit -m`. Применяется, когда нужно &#8220;проскочить&#8221; этап индексирования и сразу зафиксировать изменения.

<pre>$ git commit -a -m 'Modify Brach Second'
    [second e4b5d5d] Modify Brach Second
     2 files changed, 24 insertions(+), 14 deletions(-)
     rewrite index.html (72%)
  </pre>

Смотрим, что у нас получилось в окне браузера &#8211; то, что и ожидалось:<figure id="attachment_1770" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git_second_branch-600x501.png" alt="Git - ветвь (branch) second" width="600" height="501" class="size-medium wp-image-1770" />][3]<figcaption class="wp-caption-text">Git &#8211; ветвь (branch) second</figcaption></figure> 

### Git &#8211; переключение между ветвями (branches)

А теперь настал самый интересный момент. Как вы помните, мы сейчас находимся в ветви `second`. Давайте я переключусь в ветвь `master` и мы снова посмотрим в окно браузера:

<pre>$ git checkout master
  Switched to branch 'master'
  </pre><figure id="attachment_1769" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git_master_branch-600x501.png" alt="Git - ветвь (branch) master" width="600" height="501" class="size-medium wp-image-1769" />][2]<figcaption class="wp-caption-text">Git &#8211; ветвь (branch) master</figcaption></figure> 

Оп! Мы видим старую картину &#8211; Git &#8220;запечатлел&#8221; тот момент, когда мы совершили переход из ветви `master` в ветвь `second`. Другими словами, мы вернулись в последнее зафиксированное состояние ветви `master`:

<pre>$ git log --pretty=oneline
    b7105dab98d2f3798b5456c35695a4e906a80e92 Master Branch
    eeb12ca79f224af90cd31cf470143998a6312249 first launch
  </pre>

Если я снова вернусь в ветку `second` и запущу команду просмотра логов Git, то коммитов окажется больше:

<pre>$ git checkout second
    Switched to branch 'second'

    $ git log --pretty=oneline
    e4b5d5df7a4b9a3ee56a7298726bdab4691a5a58 Modify Brach Second
    b7105dab98d2f3798b5456c35695a4e906a80e92 Master Branch
    eeb12ca79f224af90cd31cf470143998a6312249 first launch
  </pre>

Мне кажется, уже сейчас должно быть понятно, что такое ветви (branches) в Git и для чего они предназначены. На самом деле это действительно очень просто.

### Git &#8211; слияние ветвей (branches)

В предыдущем шаге я создал ветвь `second`, в которую внес &#8220;рискованные&#8221; изменения, чтобы проверить, &#8220;оправдают&#8221; ли они себя. Изменениями я доволен и хотел бы добавить их в первоначальную ветку `master`, чтобы потом продолжить развитие проекта уже с этого места.

Фактически, я хочу сделать слияние двух веток &#8211; `master` и `second`. Это сделать очень просто &#8211; для этого я перехожу в ветку `master`. То есть, я должен находиться в той ветке, **в которую** я вношу изменения из другой ветки. А затем произвожу само слияние:

<pre>$ git checkout master
    Switched to branch 'master'

    $ git merge second
    Updating b7105da..e4b5d5d
    Fast-forward
     index.html | 8 ++++++--
     style.css  | 6 ++++++
     2 files changed, 12 insertions(+), 2 deletions(-)
  </pre>

Команда слияния проста &#8211; я просто указываю имя той ветки (branch), которую хочу слить (merge) с текущей, в которой я нахожусь на данный момент.

При слиянии ветвей зачастую может возникнуть ситуация, когда происходит **конфликт** между двумя ветвями. Рассмотрение вопроса решения конфликтов при слиянии не рассматривается мною, так как на данный момент еще не освоил этот вопрос до конца.

Давайте снова &#8220;заглянем&#8221; в окно браузера &#8211; что он нам интересного покажет?<figure id="attachment_1770" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git_second_branch-600x501.png" alt="Git - результат слияния двух ветвей master и second" width="600" height="501" class="size-medium wp-image-1770" />][3]<figcaption class="wp-caption-text">Git &#8211; результат слияния двух ветвей master и second</figcaption></figure> 

Показал он то, что и следовало показать &#8211; результат объединения двух ветвей `master` и `second`.

### Git &#8211; графическое представление ветвей (branches)

Система Git имеет в своем составе возможность **графического представления ветвления** в репозитории. Причем, такое представление можно сделать даже в консоли, с помощью псевдографики.

Это можно сделать, набрав в консоли команду:

<pre>$ git log --oneline --abbrev-commit --all --graph
  </pre>

На Stack Overflow я нашел примеры красивых изображений консоли с псевдографическим выводом команды `git log`:<figure id="attachment_1771" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git_branches.png" alt="Красивая псевдографика команды git log" width="600" height="500" class="size-full wp-image-1771" />][4]<figcaption class="wp-caption-text">Красивая псевдографика команды git log</figcaption></figure> <figure id="attachment_1772" style="width: 600px;" class="wp-caption aligncenter">[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git_branches_pretty.png" alt="Красивая псевдографика команды git log" width="600" height="500" class="size-full wp-image-1772" />][5]<figcaption class="wp-caption-text">Красивая псевдографика команды git log</figcaption></figure> 

На самом деле вариантов использования команды `git log` с ключом `--graph` бесчисленное множество. Поэтому нужно выбирать именно то, что нужно и нравиться именно вам.

Помимо псевдографики, ветви в Git можно визуализировать с помощью настоящего графического приложения. Под Mac OS X и Linux имеется достаточно большое количество таких приложений. Например, под Mac OS X это GitX, под Linux &#8211; Gitk или Gitg:<figure id="attachment_1773" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/git_branches-gitg-600x582.png" alt="Приложение Gitg под Linux" width="600" height="582" class="size-medium wp-image-1773" />][6]<figcaption class="wp-caption-text">Приложение Gitg под Linux</figcaption></figure> 

### Git &#8211; удаление ветви (branch)

В разделе слияния ветвей в Git я научился процессу объединения двух ветвей в одну. Такой процесс в Git имеет название `merge` (слияние). Теперь ветвь `master` имеет в себе все, что есть и в ветви `second`. Поэтому ветвь `second` можно удалить. Выполняется это командой:

<pre>$ git branch -d second
    Deleted branch second (was 19a8328).
  </pre>

Посмотрим на вывод команды `git hist`:

<pre>$ git hist
    * fa8b252 2014-09-03 | Last Commit in Master Branch (HEAD, master)
    *   22a9487 2014-09-03 | Merge Second Branch in Master Branch (origin/master, origin/HEAD)
    |\
    | * 19a8328 2014-09-03 | Six Commit in Second Branch
    | * e273e6c 2014-09-03 | Fifth Commit in Second Branch
    | * 8e2fe40 2014-09-03 | Fourth Commit in Second Branch
    | * 3290a23 2014-09-03 | Third Commit in Second Branch
    | * 0584a1c 2014-09-03 | Second Commit in Second Branch
    | * 38fab33 2014-09-03 | First Commit in Second Branch
    * | 8543256 2014-09-03 | Seventh Commit in Master Branch
    * | e852688 2014-09-03 | Six Commit in Master Branch
    * | d6ccde3 2014-09-03 | Fifth Commit in Master Branch
    * | c0d8e2f 2014-09-03 | Fourth Commit in Master Branch
    * | 7d2377a 2014-09-03 | Third Commit in Master Branch
    |/
    * b3e0f1f 2014-09-03 | Second Commit in Master Branch
    * be4e1f0 2014-09-03 | First Commit in Master Branch
    * ac2961a 2014-09-03 | Added git_branches
    * db9e01b 2014-09-03 | Initial commit
  </pre>

У меня осталась одна ветвь &#8211; `master`.

Оцените статью:  
<span id="post-ratings-1765" class="post-ratings" data-nonce="a525700f2a"><img id="rating_1765_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1765, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1765_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1765, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1765_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1765, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1765_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1765, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1765_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1765, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1765_text"></span></span><span id="post-ratings-1765-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging "Git Branching - Basic Branching and Merging"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/09/git_master_branch.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/09/git_second_branch.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/09/git_branches.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/09/git_branches_pretty.png
 [6]: http://localhost:7788/third/wp-content/uploads/2014/09/git_branches-gitg.png