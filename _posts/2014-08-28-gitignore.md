---
title: "gitignore - игнорирование файлов в Git"
layout: post
categories: gulp
tags: [git, gitignore]
share: true
---

> В системе Git можно настроить возможность автоматического игнорирования файлов.

То есть, можно указать Git, что файлы определенного типа не нужно отслеживать. Выполняется такая настройка с помощью специального файла `.gitignore`. Подобная возможность отключения отслеживания файлов в системе Git может понадобиться в случае, когда автоматически генерируются служебные файлы.

К примеру, если развертывать в проекте Compass, то будет создан каталог `.sass`, в который данный фреймворк помещает свой кэш, генерируемый автоматически при каждом изменении любого из файлов проекта.

Давайте на практике разберемся, каким образом можно настроить игнорирование файлов в Git с помощью `.gitignore`.

## Создание нового проекта

Создаю новый проект с именем `git_ignore`, в котором помещаю несколько файлов разного типа:

{% highlight powershell %}
$ mkdir git_ignore
$ cd git_ignore/
$ touch index.html style.css
{% endhighlight %}

Инициализирую репозиторий Git в директории `.git_ignore`, индексирую созданные файлы и фиксирую их:

{% highlight powershell %}
$ git init
Initialized empty Git repository in /home/aaron/Projects/git_ignore/.git/
$ git add .
$ git commit -m 'First Commit'
{% endhighlight %}

Вывод команды `git status` показывает, что все чисто:

{% highlight powershell %}
$ git status
On branch master
nothing to commit, working directory clean
{% endhighlight %}

## Настройка игнорирования в .gitignore

Для настройки игнорирования определенных типов файлов в системе Git необходимо первоначально создать файл `.gitignore`:

{% highlight powershell %}
$ touch .gitignore
{% endhighlight %}

Откроем созданный файл `.gitignore` в любом редакторе:

{% highlight powershell %}
$ nano -w .gitignore
{% endhighlight %}

... и пропишем в нем следующие строки:

{% highlight json %}
*.txt
*.md
{% endhighlight %}

Тем самым мы говорим Git, что нужно игнорировать все файлы с расширением `.txt` и `.md` внутри директории `git_ignore`. То есть, система контроля не будет отслеживать изменения во всех файлах этих типов.

Проиндексируем и зафиксируем изменения (создание файла настроек `.gitignore`), а затем проверим данный факт. Для этого в рабочей директории `git_ignore` создаю еще несколько типов файлов:

{% highlight powershell %}
$ touch main.css readme.txt humans.md
{% endhighlight %}

Затем выполняю индексацию всех файлов, которые были добавлены или изменены в рабочем каталоге:

{% highlight powershell %}
$ git add .
{% endhighlight %}

И смотрю, что мне показывает команда `git status`:

{% highlight powershell %}
$ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

    new file:   main.css

{% endhighlight %}

Система Git увидела только новый файл `main.css`. Два других файла - `readme.txt` и `humans.md` - проигнорированы системой. Отлично! Зафиксирую изменения.

Можно создать еще пару файлов в разных директориях и посмотреть на вывод команды `git status` в консоли:

![Результат настройки файла .gitignore]({{site.url}}/images/uploads/2014/08/gitignore.png)

## Усложнить задачу игнорирования в .gitignore

Можно усложнить задачу игнорирования в Git, добавив в файл `.gitignore` директорию, содержимое которой также должно игнорироваться. Пускай это будет обычная директория `ignore` и скрытая директория `.ignore` (с точкой перед именем):

Добавлю в файл `.gitignore` пару строк таким образом:

{% highlight powershell %}
$ cat .gitignore
*.txt
*.md
ignore/
.ignore/
{% endhighlight %}

Проиндексирую изменения, а затем выполню операции по созданию директорий и файлов внутри них:

{% highlight powershell %}
$ mkdir ignore
$ mkdir .ignore
$ touch ignore/reset.css
$ touch .ignore/normilize.css
{% endhighlight %}

Вновь ввожу команду просмотра состояния репозитория Git:

{% highlight powershell %}
$ git status
  On branch master
  nothing to commit, working directory clean
{% endhighlight %}

Все сработало - Git не захотел видеть директории `ignore`, `.ignore`, а также их содержимое. Отлично!

## Шаблоны в файле .gitignore

Для файла `.gitignore` доступны шаблоны, с помощью которых можно задать маски для выборки необходимых типой файлов. Однако, обширная тема шаблонов выходит за рамки данной статьи. При желании можно почитать по теме шаблонов в книге "[Pro Git - профессиональный контроль версий][1]".

---

[1]: http://git-scm.com/book/ru "Pro Git - профессиональный контроль версий"
