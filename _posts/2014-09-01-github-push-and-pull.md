---
title: 'GitHub &#8211; команды push и pull'
author: gearmobile
excerpt: 'Работа с удаленным репозиторием на GitHub - возможность получения patch с помощью команды pull; возможность помещение patch на GitHub с помощью команды push. Также рассмотрено различие между командами pull и fetch.'
layout: post
permalink: /github-push-and-pull/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Кодинг
tags:
  - github
  - pull
  - push
---
Продолжаю открывать для себя возможности системы Git и сервиса GitHub. Уже сейчас, обладая минимальными базовыми знаниями Git и владея учетной записью на сервере GitHub, я не представляю, как я мог жить раньше без обоих этих вещей. Это действительно удобно и надежно! Благодаря им я знаю, что у меня никогда и ничто не потеряется; и все, что нужно &#8211; у меня всегда под рукой. На работе поработал над чем-либо &#8211; отправил на GitHub; домой пришел &#8211; &#8220;стянул&#8221; наработки с GitHub и продолжил работу с прерванного места.

Вот на последнем я хотел бы остановиться подробнее. Конечно, веб-разработчик, давно и хорошо знакомый с Git и GitHub, может только улыбнуться насчет того, чем я собираюсь поделиться. Настолько все это просто и понятно. Но это просто и понятно для него, опытного web-разработчика. А для начинающего веб-программиста &#8211; это новое и неизведанное. Впрочем, достаточно лирики &#8211; переходим к практике.

### GitHub &#8211; команда push

В предыдущей статье я познакомился с возможностью создания репозитория на сервисе GitHub. И возможностью клонирования этого репозитория на локальную машину &#8211; &#8220;[GitHub и Git &#8211; создание и работа с репозиторием][1]&#8220;.

Напомню, что в том примере было произведено **клонирование** репозитория с помощью команды:

<pre>$ git clone git@github.com:gearmobile/arbeit.git
</pre>

Другими словами, было произведено **копирование** существующего репозитория с удаленного сервера на локальную машину. Причем, копирование **как есть** &#8211; полностью весь репозиторий, со всеми его файлами, коммитами, индексами и тому подобным.

После внесений изменений в локальный репозиторий &#8211; индексации и фиксации &#8211; необходимо было отправить произведенные изменения на удаленный сервер, на GitHub.

Для этой цели существует (и я ею воспользовался) команда `push` (отправить). К примеру, давайте я внесу еще кое-какие изменения в локальном репозитории, затем проиндексирую и зафиксирую их, а затем отправлю на GitHub:

<pre>$ git add .

  $ git commit -m 'Continue write article about push and pull in GitHub'
  [master 5af3abc] Continue write article about push and pull in GitHub
   1 file changed, 18 insertions(+)

  $ git status
  On branch master
  Your branch is ahead of 'origin/master' by 1 commit.
    (use "git push" to publish your local commits)
  nothing to commit, working directory clean

  $ git push
  ...
  Counting objects: 7, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (4/4), done.
  Writing objects: 100% (4/4), 1.65 KiB | 0 bytes/s, done.
  Total 4 (delta 1), reused 0 (delta 0)
  To git@github.com:semenencko/articles
     022b756..5af3abc  master -> master
</pre>

Вот &#8211; все наработки, которые я сделал на домашнем компьютере, оказались с считанные секунды помещенными на сервере GitHub, под бдительным оком Git.

### GitHub &#8211; команда pull

Продолжим логическую картину моего рабочего процесса (workflow). На следующий день я прихожу на работу и у меня есть время и возможность поработать над своим проектом. Естественно, я хочу продолжить с того места, на котором остановился дома. Для этого я воспользуюсь командой `pull`, чтобы &#8220;стянуть&#8221; с GitHub **последние изменения**.

В данном случае команда `pull` будет выглядеть так:<figure id="attachment_1748" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github-pull-600x304.png" alt="GitHub - команда pull" width="600" height="304" class="size-medium wp-image-1748" />][2]<figcaption class="wp-caption-text">GitHub &#8211; команда pull</figcaption></figure> 

В выводе консоли (на картинке) видно, что было произведено добавление одного измененного файла по имени README.md, в котором были добавлены две строки.

Обратите внимание на **разницу** между командами `clone` и `pull` в данном случае. Команда `clone` **копирует весь репозиторий** целиком, как есть &#8211; со всеми его файлами. Команда `pull` **копирует разницу** между удаленным и локальным репозиторием. Эту разницу можно назвать **дельта** или **patch**.

В результате вышеприведенной команды в считанные секунды я получаю на рабочем компьютере точную копию того проекта, над которым работал дома. И могу продолжать с того места, на котором остановился.

### GitHub &#8211; команда fetch

Существует разновидность команды `pull` &#8211; это команда `fetch`. И одна, и вторая команда выполняют одинаковые задачи &#8211; получение patch удаленного репозитория. Но делают они это по разному.

Команда `pull` получает patch репозитория и автоматически производит слияние удаленной и локальной ветвей репозитория. Если произойдет конфликт слияния, то только в этом случае слияния не произойдет и решать конфликт придется вручную.

Команда `fetch` также производит получение patch удаленного репозитория. Но при этом автоматического слияния ветвей удаленного и локального репозиториев не происходит:<figure id="attachment_1749" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github-fetch-600x304.png" alt="GitHub - команда fetch" width="600" height="304" class="size-medium wp-image-1749" />][3]<figcaption class="wp-caption-text">GitHub &#8211; команда fetch</figcaption></figure> 

На картинке выше показано, что была выполнена команда `git fetch` после того, как на стороне сервиса GitHub было произведено редактирование файла README.md. Однако, последующая команда `git status` показала, что изменения есть, но они не слиты с локальной ветвью репозитория. И порекомендовала выполнить команду `git pull`, чтобы произвести такое слияние.

Помимо этого, имеются изменения в локальном репозитории, которые не проиндексированы и не зафиксированы. Что же, исправляю ситуацию &#8211; последовательно ввожу команды:

<pre>$ git pull
  $ git add .
  $ git commit -m 'Added fetch image'
  $ git push
</pre>

Производить слияние и разрешение конфликтов при слиянии я еще не умею, поэтому вопрос, как произвести слияние ветвей после команды `git fetch` я опущу в данной статье.

Вернувшись к вышесказанному, можно сделать вывод, что команда `pull` **более универсальная**, нежели команда `fetch`. Именно команду `pull` имеет смысл применять в практической работе.

Оцените статью:  
<span id="post-ratings-1746" class="post-ratings" data-nonce="cf9896af04"><img id="rating_1746_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1746, 1, '1 Star');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1746_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1746, 2, '2 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1746_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1746, 3, '3 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1746_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1746, 4, '4 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1746_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1746, 5, '5 Stars');" onmouseout="ratings_off(0, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (No Ratings Yet)<br /><span class="post-ratings-text" id="ratings_1746_text"></span></span><span id="post-ratings-1746-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/?p=1730 "GitHub и Git - создание и работа с репозиторием"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/08/github-pull.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/08/github-fetch.png