---
title: "Git - создание ветвей (branch)"
layout: post
categories: git
tags: [git, branch]
share: true
---

> Продолжаю совместно с вами постепенно изучать магию Git\GitHub.

Слово магия здесь применено не случайно - не иначе, как магией возможности Git\GitHub не назовешь. По крайней мере, я впечатлен этими возможностями. Другое дело, что процесс изучения Git у меня лично идет как-то тяжеловато. Ну, это не страшно - главное, не останавливаться!

В этом разделе я попытаюсь осветить для себя (и возможно, для вас, уважаемый читатель) вопрос создания ветвей (branches) в Git, перемещение между ветвями (branches), слияние (merge) ветвей. Этот вопрос очень подробно и хорошо описан на странице официальной документации - "Git Branching - Basic Branching and Merging". Здесь я попробую самостоятельно описать данный вопрос.

## Инициализация Git-репозитория

Создаю тестовую директорию `git_branches`, в которой будут производиться эксперименты по созданию ветвей в Git. Внутри этой директории создаю два файла - индексный файл и файл таблиц стилей. А затем инициализирую Git-репозиторий, добавляю созданные файлы под версионный контроль Git:

{% highlight powershell %}
$ mkdir git_branches
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
{% endhighlight %}

Обратите на строку `On branch master` в выводе команды `git status`. Это не пустой набор служебной информации - здесь говориться о том, что в ветви `master` нечего фиксировать и рабочая директория чистая.

Итак, мы уже кое-что узнали. А именно - при инициализации Git-репозитория была автоматически создана ветвь (branch) по имени `master`. И на данный момент мы находимся в этой ветви.

Конечно, на самом деле это пока мало о чем говорит, так как не с чем сравнивать. Поэтому давайте я немного отредактирую оба файла `index.html` и `style.css`, проиндексирую\зафиксирую их.

В браузере примерный вид странички будет выглядеть таким образом:

![Git - ветвь (branch) master]({{site.url}}/images/uploads/2014/09/git_master_branch.png)

## Git - создание новой ветви (branch)

В системе Git (как уже упоминалось ранее) имеется механизм ветвления (branches). Попробую на словах объяснить, что он из себя представляет.

Допустим, в моем текущем проекте, у которого имеются два файла, нужно внести кардинальные изменения. Причем, изменения такого рода, что они могут нарушить работу уже существующего проекта. Чтобы обезопасить себя (подстраховать), создаю точную копию существующего проекта и перехожу в нее для дальнейшей работы.

Давайте я на практике осуществлю вышесказанные действия. Для этого создаю новую ветвь с произвольным именем `second`, которая на этом этапе будет точной копией ветви `master`:

{% highlight powershell %}
$ git checkout -b second
  Switched to a new branch 'second'
{% endhighlight %}

Строка `Switched to a new branch 'second'` услужливо информирует, что меня автоматически "перебросило" во вновь ветвь `second`. Можно проверить себя, набрав в консоли:

{% highlight powershell %}
$ git status
  On branch second
  nothing to commit, working directory clean
{% endhighlight %}

Строка `On branch second` говорит сама за себя.

Отлично! Теперь давайте я внесу некоторые изменения в файлы `index.html` и `style.css` и мы вместе посмотрим на результат в окне браузера. Изменения будут касаться добавления блока-обертки, еще нескольких параграфов и другой легкой стилизации.

Не забуду также проиндексировать и зафиксировать внесенные изменения. Обратите внимание на вид команды - `git commit -a`. Эта команда является сокращенным вариантом двух команд: `git add` и `git commit -m`. Применяется, когда нужно "проскочить" этап индексирования и сразу зафиксировать изменения.

{% highlight powershell %}
$ git commit -a -m 'Modify Brach Second'
  [second e4b5d5d] Modify Brach Second
  2 files changed, 24 insertions(+), 14 deletions(-)
  rewrite index.html (72%)
{% endhighlight %}

Смотрим, что у нас получилось в окне браузера - то, что и ожидалось:

![Git - ветвь (branch) second]({{site.url}}/images/uploads/2014/09/git_second_branch.png)

## Git - переключение между ветвями (branches)

А теперь настал самый интересный момент. Как вы помните, мы сейчас находимся в ветви `second`. Давайте я переключусь в ветвь `master` и мы снова посмотрим в окно браузера:

{% highlight powershell %}
$ git checkout master
  Switched to branch 'master'
{% endhighlight %}

![Git - ветвь (branch) master]({{site.url}}/images/uploads/2014/09/git_master_branch.png)

Оп! Мы видим старую картину - Git "запечатлел" тот момент, когда мы совершили переход из ветви `master` в ветвь `second`. Другими словами, мы вернулись в последнее зафиксированное состояние ветви `master`:

{% highlight powershell %}
$ git log --pretty=oneline
  b7105dab98d2f3798b5456c35695a4e906a80e92 Master Branch
  eeb12ca79f224af90cd31cf470143998a6312249 first launch
{% endhighlight %}

Если я снова вернусь в ветку `second` и запущу команду просмотра логов Git, то коммитов окажется больше:

{% highlight powershell %}
$ git checkout second
  Switched to branch 'second'

  $ git log --pretty=oneline
  e4b5d5df7a4b9a3ee56a7298726bdab4691a5a58 Modify Brach Second
  b7105dab98d2f3798b5456c35695a4e906a80e92 Master Branch
  eeb12ca79f224af90cd31cf470143998a6312249 first launch
{% endhighlight %}

Мне кажется, уже сейчас должно быть понятно, что такое ветви (branches) в Git и для чего они предназначены. На самом деле это действительно очень просто.

## Git - слияние ветвей (branches)

В предыдущем шаге я создал ветвь `second`, в которую внес "рискованные" изменения, чтобы проверить, "оправдают" ли они себя. Изменениями я доволен и хотел бы добавить их в первоначальную ветку `master`, чтобы потом продолжить развитие проекта уже с этого места.

Фактически, я хочу сделать слияние двух веток - `master` и `second`. Это сделать очень просто - для этого я перехожу в ветку `master`. То есть, я должен находиться в той ветке, **в которую** я вношу изменения из другой ветки. А затем произвожу само слияние:

{% highlight powershell %}
$ git checkout master
  Switched to branch 'master'

  $ git merge second
  Updating b7105da..e4b5d5d
  Fast-forward
   index.html | 8 ++++++--
   style.css  | 6 ++++++
   2 files changed, 12 insertions(+), 2 deletions(-)
{% endhighlight %}

Команда слияния проста - я просто указываю имя той ветки (branch), которую хочу слить (merge) с текущей, в которой я нахожусь на данный момент.

При слиянии ветвей зачастую может возникнуть ситуация, когда происходит **конфликт** между двумя ветвями. Рассмотрение вопроса решения конфликтов при слиянии не рассматривается мною, так как на данный момент еще не освоил этот вопрос до конца.

Давайте снова "заглянем" в окно браузера - что он нам интересного покажет?

![Git - результат слияния двух ветвей master и second]({{site.url}}/images/uploads/2014/09/git_second_branch.png)

Показал он то, что и следовало показать - результат объединения двух ветвей `master` и `second`.

## Git - графическое представление ветвей (branches)

Система Git имеет в своем составе возможность **графического представления ветвления** в репозитории. Причем, такое представление можно сделать даже в консоли, с помощью псевдографики.

Это можно сделать, набрав в консоли команду:

{% highlight powershell %}
$ git log --oneline --abbrev-commit --all --graph
{% endhighlight %}

На Stack Overflow я нашел примеры красивых изображений консоли с псевдографическим выводом команды `git log`:

![Красивая псевдографика команды git log]({{site.url}}/images/uploads/2014/09/git_branches.png)

![Красивая псевдографика команды git log]({{site.url}}/images/uploads/2014/09/git_branches_pretty.png)

На самом деле вариантов использования команды `git log` с ключом `--graph` бесчисленное множество. Поэтому нужно выбирать именно то, что нужно и нравиться именно вам.

Помимо псевдографики, ветви в Git можно визуализировать с помощью настоящего графического приложения. Под Mac OS X и Linux имеется достаточно большое количество таких приложений. Например, под Mac OS X это GitX, под Linux - Gitk или Gitg:

![Приложение Gitg под Linux]({{site.url}}/images/uploads/2014/09/git_branches-gitg.png)

## Git - удаление ветви (branch)

В разделе слияния ветвей в Git я научился процессу объединения двух ветвей в одну. Такой процесс в Git имеет название `merge` (слияние). Теперь ветвь `master` имеет в себе все, что есть и в ветви `second`. Поэтому ветвь `second` можно удалить.

Выполняется это командой:

{% highlight powershell %}
$ git branch -d second
  Deleted branch second (was 19a8328).
{% endhighlight %}

Посмотрим на вывод команды `git hist`:

{% highlight powershell %}
$ git hist
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
{% endhighlight %}

У меня осталась одна ветвь - `master`.

---

[1]: http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging "Git Branching - Basic Branching and Merging"
