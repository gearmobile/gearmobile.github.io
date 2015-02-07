---
title: 'Gulp &#8211; знакомство и первый запуск'
author: gearmobile
excerpt: 'Эта статья является первой частью в серии статьей, посвященных знакомству с набирающим популярность менеджером задач Gulp. Произведем установку Gulp под Linux Mint и запустим свою первую задачу под Gulp. Также в кратце рассмотрим особенности менеджера Gulp - простоту файла настроек gulpfile.js, поточный метод работы, типы задач.'
layout: post
permalink: /gulp-introduction-and-first-launch/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 10
ratings_score:
  - 49
ratings_average:
  - 4.9
categories:
  - 'Javascript &amp; jQuery'
tags:
  - gulp
---
В этой статье будем знакомиться с новым менеджером задач (task manager) под названием [Gulp][1]. Постепенно вместе с вами я пройду весь процесс &#8211; от установки Gulp до установки плагинов, создания задач, отслеживания ошибок и еще многое другое.

Но для начала узнаем, что такое Gulp. Это точно такой менеджер задач, как и Grunt. Оба они являются модулями под Node.js и устанавливаются с помощью пакетного менеждера npm. Отличие от Grunt в том, что Gulp является переработкой Grunt. Как говорят его разработчики, цель создания была в том, чтобы выбросить из Grunt все лишнее. Кроме того, настройка Gulp значительно упростилась.<figure id="attachment_1597" style="width: 228px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/gulp.png" alt="Gulp" width="228" height="510" class="size-full wp-image-1597" />][2]<figcaption class="wp-caption-text">Gulp</figcaption></figure> 

На сегодня однозначным преимуществом Gulp перед Grunt является скорость обработки файлов &#8211; она в разы выше, чем у старенького Grunt.

## Установка Gulp

Установка будет производиться под операционной системой Linux Mint 17 Cinnamon. Поэтому, пользователи Mac OS найдут все нижеприведенные команды абсолютно идентичными для себя. Подразумевается, что в системе уже установлен Node.js и менеджер пакетов npm.

Процесс инсталляции выполняется в **два этапа**. Первоначально Gulp устанавливается **глобально**, с помощью ключа `-g`. Давайте так и поступим &#8211; произведем установку в системе:

<pre>$ sudo npm install -g gulp
</pre>

Затем создадим тестовую директорию с именем `gulp_test`, в которой будет производить наше знакомство:

<pre>$ mkdir gulp_test
  $ cd gulp_test/
</pre>

В этой директории создадим файл `package.json` и пропишем в нем **имя проекта** и его **версию**:

<pre>$ touch package.json
  $ cat package.json
  {
    "name": "first",
    "version": "0.0.1",
    "devDependencies": {}
  }
</pre>

Этого будет достаточно. Теперь установим Gulp внутри директории `gulp_test`. При этом воспользуемся ключом `--save-dev`, который будет &#8220;говорить&#8221; менеджеру пакетов npm вносить в файл `package.json` все устанавливаемые им пакеты в качестве зависимостей проекта:

<pre>$ npm install --save-dev gulp
</pre>

Теперь снова посмотрим на содержимое файла `package.json` и увидим, что npm добавил Gulp в качестве зависмости:

<pre>$ cat package.json
  {
    "name": "first",
    "version": "0.0.1",
    "devDependencies": {
      "gulp": "~3.8.7"
    }
  }
</pre>

Установка завершена и можно переходить к использованию этого менеждера задач.

## Первый запуск Gulp

Менеджер задач &#8211; само слово говорит за себя, это программа для управления задачами. В Gulp все задачи прописываются в одном единственном файле `gulpfile.js`. Первоначально этого файла не существует и его нужно создать самостоятельно, вручную:

<pre>$ touch gulpfile.js
</pre>

Затем в нем пропишем первую задачу. Все задачи деляться на **два неравнозначных типа**: **задача по умолчанию** (default task) и **именованные задачи** (named tasks). Разница между ними в том, что задача по умолчанию имеет имя `default`, которое можно и не указывать. Кроме того, задача по умолчанию запускается в консоли **всего одной командой**:

<pre>$ gulp
</pre>

В то время как **именованная задача** (named task) может иметь произвольное имя. Запуск такой задачи в консоли выполняется с указанием имени конкретной задачи:

<pre>$ gulp name_of_task
</pre>

Еще один важный момент заключается в том, что этот менеджер задач является **потоковым**. Что это значит? Не знаю, получиться ли у меня достаточно точно объяснить данный вопрос, но вот линуксоиды, хорошо знакомые с командной строкой, меня должны понять. В консоли Linux (Unix) есть такое понятие, как [pipe][3].

Например, простая команда:

<pre>$ ls -l | less
</pre>

&#8230; выполняет следующее: результат команды `ls -l` **перенаправляется** для обработки в программу `less`. Редактор `less` автоматически открывается в консоли с уже готовым для чтения текстом внутри себя.

Чисто схематично такой пример можно усложнить и представить в таком виде:

<pre>$ programm1 | programm2 | programm3 | programm4 | programm5
</pre>

Каждая из программ в этом списке будет производить обработку данных и передавать результат этой обработки другой программе, по цепочке.

Принцип работы Gulp точно такой же. Только вместо программ в нем используются плагины (я не забыл сказать, что он имеет модульную структуру?):

<pre>$ plugin1 | plugin2 | plugin3 | plugin4 | plugin5 | plugin6
</pre>

Отлично! С теорией закончили и можно снова возвращаться к практике, к нашему файлу настроек `gulpfile.js`. Откроем его и пропишем в нем такие строки:

<pre>var gulp = require('gulp');

  gulp.task('default', function(){
    console.log('Hello from Gulp!')
  });
</pre>

Первая строка `var gulp = require('gulp');` создает переменную `gulp`, в которую помещается сам Gulp. Это необходимо для Node.js, который будет читать файл `gulpfile.js` и работать с Gulp в виде переменной `gulp`.

Вторая строка, начинающаяся с `gulp.task` &#8211; это не что иное, как задача. Именно так создаются задачи в этом менеджере. Здесь `'default'` &#8211; это имя задачи (в данном случае это задача по умолчанию, как вы помните). Функция `function()` имеет в своем теле неограниченное количество инструкций. Так как мы еще не умеем работать с плагинами под Gulp, то в качестве инструкции пропишем вывод в консоль обычной текстовой строки &#8211; `console.log('Hello from Gulp!')`.

Давайте попробуем запустить наш менеджер задач, чтобы посмотреть, а работает ли он вообще? И как он работает? Для этого переходим в консоль и вводим в ней одну единственную команду `gulp`:

<pre>$ gulp
  [19:37:53] Using gulpfile ~/Projects/gulp_test/gulpfile.js
  [19:37:53] Starting 'default'...
  Hello from Gulp!
  [19:37:53] Finished 'default' after 169 μs
</pre>

Вот это да! А что означают все эти строки в консоли? Означают они только хорошее! Строка `Using gulpfile ~/Projects/gulp_test/gulpfile.js` говорит о том, что Gulp для своей работы воспользовался файлом настроек `gulpfile` по указанному пути. Затем было запущено выполнение задачи с именем `default` &#8211; `Starting 'default'...`. Результатом выполнения этой задачи был вывод в консоль строки &#8211; `Hello from Gulp!`. И задача с именем `default` благополучно завершилась &#8211; `Finished 'default' after 169 μs`, причем на ее выполнение ушло 169 миллисекунд.

Можно поздравить самих себя &#8211; мы только что создали и запустили на выполнение свою первую задачу под Gulp!

Оцените статью:  
<span id="post-ratings-1588" class="post-ratings" data-nonce="44300f3990"><img id="rating_1588_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1588, 1, '1 Star');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1588_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1588, 2, '2 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1588_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1588, 3, '3 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1588_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1588, 4, '4 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1588_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_half.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1588, 5, '5 Stars');" onmouseout="ratings_off(4.9, 5, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>10</strong> votes, average: <strong>4,90</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1588_text"></span></span><span id="post-ratings-1588-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://gulpjs.com/ "Gulp"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/08/gulp.png
 [3]: http://en.wikipedia.org/wiki/Pipeline_%28Unix%29 "Pipeline"