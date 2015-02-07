---
title: Macros в Sublime Text 3
author: gearmobile
excerpt: Создание макросов (macros) в редакторе Sublime Text. Сохранение макросов в редакторе Sublime Text. Назначение макросам сочетания клавиш для быстрого запуска.
layout: post
permalink: /sublime-macros/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 6
ratings_score:
  - 30
ratings_average:
  - 5
categories:
  - Web Tools
tags:
  - macro
  - sublime text
---
Отличная тема из разряда &#8220;как повысить эффективность своей работы&#8221;. Возможно, эта тема уже и избитая, но вот Google у меня выдает только англоязычные ресурсы со справкой по этим словам. Для меня это совсем не критично, но все же.

Захотел написать маленький обзор этой темы, когда пересматривал видео по верстке от Adi Purdila, записанное им для Tuts Plus. В этом видео он прямо-таки волшебным образом вставлял комментарии в HTML-файл. Конечно, делать комментарии в этаких файлах &#8211; дело нужное и полезное. Но вот добавлять их &#8211; это такая нудная задача!

Решил потратить немного своего времени, чтобы разобраться, как же он мог сделать? Немного подумал и пришел к мысли, что наверняка он делал это с помощью макросов (macros). Точнее &#8211; он создал макрос (macros), который вставляет комментарий в файл. А потом только применял этот макрос (macros) &#8211; просто и быстро!

Ну что же, давайте и мы разберемся, каким образом можно записать свой собственный макрос (macros) в Sublime Text. Чем мы хуже Adi Purdila? ))

## Что такое макрос (macros)?

Для начала неплохо было бы вспомнить, что такое макрос (macros)? В любой программе, будь то *MS Excel*, *Adobe Photoshop*, *Notepad++* или же *Sublime Text* макрос (macros) &#8211; это записанная этой программой **последовательность действий**, **выполненная пользователем**. Образно говоря, пользователь говорит программе &#8211; &#8220;смотри, запоминай и повторяй за мной&#8221;.

### Запись макроса (macros) в Sublime Text

Запись и воспроизведение макросов (macros) в Sublime Text можно выполнить **двумя способами**.

Первый &#8211; через панель инструментов по пути **&#8220;Tools&#8221; &#8211; &#8220;Record Macro&#8221;**, **&#8220;Tools&#8221; &#8211; &#8220;Playback Macro&#8221;**.

Или же более правильным способом (*ведь мы с вами настоящие кодеры?*) &#8211; через сочетание клавиш. Запуск записи макроса (macros) &#8211; через **Ctrl+Q**. Остановка записи макроса (macros) &#8211; тоже через **Ctrl+Q**. Воспроизведение записанного макроса (macros) &#8211; через **Shift+Ctrl+Q**.

Я создам макрос (macros) для вставки начального комментария для блока. Ниже приведено небольшое видео, какие последовательности действий выполнялись при включенной записи макроса (macros):



После остановки записи макроса (macros) он сохраняется в буфере обмена и при закрытии программы Sublime Text он пропадет. Поэтому его нужно сохранить через меню **&#8220;Tools&#8221; &#8211; &#8220;Save Macro &#8230;&#8221;**.

Все пользовательские макросы (macros) сохраняются в директорию **&#8220;Packages&#8221; &#8211; &#8220;User&#8221;**. Показанный на видео макрос я сохранил под именем `comment.sublime-macro` в этой директории.

В меню редактора Sublime Text сохраненный макрос (macro) можно найти по пути **&#8220;Tools&#8221; &#8211; &#8220;Macros&#8221;**. Там уже имеются дефолтные макросы (macros) самого редактора и плагинов, установленных в нем. В моем случае там есть макросы (macros) под плагин MarkdownEditing:<figure id="attachment_1861" style="width: 600px;" class="wp-caption aligncenter">

[<img class="size-medium wp-image-1861" src="http://localhost:7788/third/wp-content/uploads/2014/09/sublime_macros-600x314.png" alt="Sublime Text User Macros" width="600" height="314" />][1]<figcaption class="wp-caption-text">Sublime Text User Macros</figcaption></figure> 

Ради любопытства можно посмотреть на содержимое сохраненного мною макроса (macros) `comment.sublime-macro`. Ничего сложного в нем нет &#8211; это простая запись последовательности выполненных мною действий, в формате JSON.

Ниже привожу начальный отрывок этого файла &#8211; все мои действия легко читаются:

<pre>[
    {
      "args": null,
      "command": "find_under_expand"
    },
    {
      "args": null,
      "command": "upper_case"
    },
    {
      "args":
      {
        "extend": false,
        "to": "bol"
      },
      "command": "move_to"
    },
    {
      "args":
      {
        "characters": "&lt;!"
      },
      "command": "insert"
    },
    {
      "args":
      {
        "characters": "--"
      },
      "command": "insert"
    },
    ...
</pre>

### Создание key binding для макроса (macros)

Теперь неплохо было бы &#8220;повесить&#8221; на этот макрос (macros) сочетание горячих клавиш (&#8220;забиндить&#8221;), чтобы почти мгновенно вызывать его на исполнение. Для этого понадобятся вкладки **&#8220;Key Bindings &#8211; Default&#8221;** и **&#8220;Key Bindings &#8211; User&#8221;**. Обе они располагаются в меню **&#8220;Preferences&#8221;**.

Во вкладке **&#8220;Key Bindings &#8211; Default&#8221;** помещен список всех сочетаний клавиш по умолчанию, на которые повешены какие-либо действия в редакторе Sublime Text.

Во вкладке **&#8220;Key Bindings &#8211; User&#8221;** можно задать свои собственные сочетания клавиш и повесить на них нужное действие.

Мне захотелось повесить выполнение макроса `comment.sublime-macro` на сочетание клавиш **Shift+Ctrl+C**. Для этого я подстраховываю себя и проверяю, нет ли во вкладке **&#8220;Key Bindings &#8211; Default&#8221;** такого сочетания клавиш, чтобы не переопределить какое-либо действие.

Такого не оказалось, поэтому во вкладке **&#8220;Key Bindings &#8211; User&#8221;** добавляю такую строку:

<pre>[
    { "keys": ["alt+shift+c"], "command": "run_macro_file", "args": {"file": "Packages/User/comment.sublime-macro"} }
  ]
</pre>

Эта строка легко читается.

Здесь:

  * `"keys": ["alt+shift+c"]` &#8211; это записанное мною сочетание клавиш;
  * `"command": "run_macro_file"` &#8211; говорит Sublime, что необходимо запустить выполнение именно макроса, а не какого-либо другого действия;
  * `"args": {"file": "Packages/User/comment.sublime-macro"}` &#8211; указывает, какой именно макрос (macro) нужно выполнить.

Аналогично предыдущему макросу, создам еще один macros, который будет **вставлять конечный комментарий** для блока:



На него во вкладке &#8220;Key Bindings &#8211; User&#8221; я повешу сочетание клавиш **Shift+Ctrl+E**:

<pre>{ "keys": ["alt+shift+e"], "command": "run_macro_file", "args": {"file": "Packages/User/end_comment.sublime-macro"} }
</pre>

### Запуск макроса (macros) в Sublime Text

Теперь настало время проверить, как работают записанные мною макросы. Для этого в коде я воспользуюсь сочетаниями клавиш **Shift+Ctrl+C** и **Shift+Ctrl+E**:



Отлично! Быстрота и легкость вставки комментариев впечатляет. А сколько времени и сил при этом экономится! Конечно, одними комментариями для макросов (macros) можно не ограничиваться &#8211; тут уж насколько хватит фантазии.

Главное &#8211; что инструмент нужный и полезный, макросы (macros) в Sublime Text.

Оцените статью:  
<span id="post-ratings-1850" class="post-ratings" data-nonce="6619be1497"><img id="rating_1850_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1850, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1850_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1850, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1850_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1850, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1850_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1850, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1850_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1850, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>6</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1850_text"></span></span><span id="post-ratings-1850-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://localhost:7788/third/wp-content/uploads/2014/09/sublime_macros.png