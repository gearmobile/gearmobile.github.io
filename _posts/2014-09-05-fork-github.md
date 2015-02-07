---
title: 'Fork на GitHub &#8211; что это такое'
author: gearmobile
excerpt: 'Fork на GitHub - это тоже, что и branch в Git. Fork предназначен для создания копии репозитория на GitHub. Измененный fork можно отправить как pull request.'
layout: post
permalink: /fork-github/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 6
ratings_score:
  - 30
ratings_average:
  - 5
categories:
  - Кодинг
tags:
  - fork
  - github
---
Продолжаю увлекательное знакомство новичка с сервисом GitHub и с системой контроля версий Git. Так как имею учетную запись на GitHub, которую регулярно использую, то у меня возник вопрос, который не мог не возникнуть, рано или поздно. Касается он такой темы, как fork.

Не знаю даже, как правильно поступить дальше &#8211; попытаться самому описать вопрос, своими словами; или же попытаться сделать вольный перевод статьи на эту тему &#8211; [Fork A Repo][1]. Но лучше все же расскажу своими словами.

### Fork &#8211; это копия репозитория

Fork &#8211; это вcего навсего **копия репозитория**. Это тоже самое, что **branch** в Git. Только на GitHub такой **branch** называется fork &#8211; присутствует своя терминология. Само слово fork в переводе означает *ответвление*. Для того, чтобы воспользоваться fork, нужно иметь свою собственную учетную запись на GitHub; и нужно войти под ней на GitHub **в момент выполнения fork**.

Для чего нужен fork? Для тех же целей, что и **branch** в Git. С помощью него создается точная **копия оригинального репозитория**, только на сервисе GitHub. В копии репозитория можно вносить свои собственные изменения, редактировать файлы или удалять директории. Как только все изменения будут внесены, то можно поделиться ими &#8211; отправить авторам оригинального репозитория запрос на слияние вашего измененного репозитория с их оригинальным репозиторием. Такой запрос называется **pull request**. Если авторам оригинального репозитория ваши изменения понравятся, то они могут внести их в свой собственый оригинальный репозиторий &#8211; принять запрос и выполнить слияние.

Существование fork полностью отвечает идеологии OpenSource и GitHub, в частности. Идеология OpenSource заключается в свободном обмене исходным кодом программ и fork однозначно помогает в этом деле. С помощью fork можно одним движением получить копию любого исходного кода, выложенного на GitHub в свободном доступе.

### Fork &#8211; создание копии репозитория

Давайте от слов перейдем к делу и на практике выполним хотя бы один fork на GitHub. К слову сказать, в приведенной выше статье-оригинале [Fork A Repo][1] дается ссылка на репозиторий [Spoon-Knife][2], созданный авторами статьи **для учебных целей** &#8211; научиться работать с fork на GitHub. Вы, уважаемый читатель, также можете свободно воспользоваться им для себя, чтобы научиться пользоваться fork.

Я воспользуюсь другим репозиторием, который выложен в свободном доступе достаточно известным верстальщиком Юрием Артюхом (akella). Ниже привожу шаги по созданию Fork на GitHub.

  * захожу на GitHub под своей учетной записью
  * перехожу по ссылке [github/akella/sass][3], по которой расположен репозиторий **akella/sass**<figure id="attachment_1776" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/github-fork_start-600x414.png" alt="Репозиторий akella/sass на GitHub" width="600" height="414" class="size-medium wp-image-1776" />][4]<figcaption class="wp-caption-text">Репозиторий akella/sass на GitHub</figcaption></figure> 

Фактически, теперь я нахожусь в репозитории **akella/sass** пользователя akella (Юрий Артюх). Об этом красноречиво говорит надпись **akella/sass** в левом верхнем углу окна браузера. В правом верхнем углу окна браузера нахожу **кнопку Fork**.

И нажимаю на нее:<figure id="attachment_1777" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/09/github-fork_end-600x414.png" alt="Выполненный fork репозитория akella/sass" width="600" height="414" class="size-medium wp-image-1777" />][5]<figcaption class="wp-caption-text">Выполненный fork репозитория akella/sass</figcaption></figure> 

Может случиться, что вы, уважаемый читатель, ничего и не заметите. Но это не так на самом деле. Приглядитесь к &#8220;главной&#8221; надписи &#8211; она изменилась с **akella/sass** на **gearmobile/sass**; а ниже мелким шрифтом еще &#8211; *forked from akella/sass*. Думаю, тут и говорить больше нечего &#8211; все и так понятно. Теперь этот репозиторий мой &#8211; точнее, у меня теперь копия оригинального репозитория **akella/sass**. Я могу делать с ним все, что мне понадобиться &#8211; просто пользоваться или же вносить свои собственные изменения.

Если изменения мне покажутся существенными, то я могу отправить пользователю akella запрос на слияние (pull request) моего репозитория **gearmobile/sass** с его репозиторием **akella/sass**. Если пользователь akella посчитает эти изменения действительно существенными (с его точки зрения), то он может и принять мой запрос.

Я также могу удалить репозиторий **gearmobile/sass**, если в нем отпадет надобность. Надеюсь, вы хорошо помните, как удалять репозиторий на GitHub &#8211; [Как удалить репозиторий на GitHub][6].

Оцените статью:  
<span id="post-ratings-1767" class="post-ratings" data-nonce="4dcd968bbe"><img id="rating_1767_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1767, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1767_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1767, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1767_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1767, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1767_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1767, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1767_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1767, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>6</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1767_text"></span></span><span id="post-ratings-1767-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: https://help.github.com/articles/fork-a-repo "Fork A Repo"
 [2]: https://github.com/octocat/Spoon-Knife "Spoon-Knife"
 [3]: https://github.com/akella/sass "akella/sass"
 [4]: http://localhost:7788/third/wp-content/uploads/2014/09/github-fork_start.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/09/github-fork_end.png
 [6]: http://localhost:7788/third/?p=1738