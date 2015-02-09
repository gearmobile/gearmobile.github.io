---
title: Использование SSL в административной панели WordPress
author: gearmobile
layout: post
permalink: /%d0%b8%d1%81%d0%bf%d0%be%d0%bb%d1%8c%d0%b7%d0%be%d0%b2%d0%b0%d0%bd%d0%b8%d0%b5-ssl-%d0%b2-wordpress/
ratings_users:
  - 2
ratings_score:
  - 2
ratings_average:
  - 1
cleanretina_sidebarlayout:
  - default
categories:
  - CMS WordPress
tags:
  - ssl
---
*Со времен, когда я увлекался изучением операционных систем семейства Linux, для меня небезразличной была тема цифровой безопасности. Благо, системы Linux имеют богатый набор инструментов в этой области.*

*С того времени ничего не изменилось и при любом удобном случае я всегда поступаю по принципу &#8211; &#8220;безопасности много не бывает&#8221;. Особенно, когда это касается сайтов, выложенных во всеобщем доступе и работающих на такой мега-популярной CMS, как WordPress (со всеми вытекающими отсюда последствиями).*

*Поэтому неудивительно, что рано или поздно у меня возник вопрос, а как так происходит, что я могу часами &#8220;висеть&#8221; подключенным к административной панели WordPress, передавая при этом на хостинг самую различную информацию: текст, изображения и пароли в том числе. И все это происходит по незащищенному, незашифрованному каналу.*

*То есть &#8211; я подключаюсь к панели, она у меня запрашивает пароль и я отсылаю его в открытом виде. Но ведь тогда любой желающий может подключиться и перехватить этот пароль в готовом виде, ему даже не потребуются всякие брутфорсы со словарями. Однако, так дело не пойдет!*

*Логичным для меня шагом было найти доступный мануальчик по созданию безопасного канала связи с административной панелью WordPress. Но вот незадача &#8211; на русском языке я такового не нашел. Пришлось перевести англоязычную статью, вольный перевод которой привожу ниже.*

Перед установкой WordPress у вас уже должен быть SSL-сертификат, который подключается к учетной записи хостинга, на котором будет располагаться ваш сайт. Если у вас нет сертификата SSL, вам необходимо приобрести его. Эта услуга платная и существуют различные службы для предоставления таких сертификатов. В том числе, вы можете воспользоваться регистратором доменных имен, так как многие из них также предоставляют подобные услуги.

Для того, чтобы активировать сертификат SSL в WordPress, необходимо отредактировать файл `wp-config.php`. Можете поступить двумя способами:

  1. скачать этот файл на локальную машину, используя файловый менеджер FTP
  2. воспользоваться встроенным редактором файлов в файловом менеджере FTP (например, FileZilla)

### Подключение SSL к административной панели WordPress

1. Открываем для редактирования файл `wp-config.php`

2. Находим в этом файле строку:

<pre>/* That's all, stop editing! Happy blogging. */</pre></p> 

3. Выше этой строки добавляем в файл две строки:

<pre>define('FORCE_SSL_ADMIN', true);
  define('FORCE_SSL_LOGIN', true);</pre></p> 

4. В результате файл `wp-onfig.php` должен выглядеть следующим образом:

<pre>define('FORCE_SSL_ADMIN', true);
  define('FORCE_SSL_LOGIN', true);
  /* That's all, stop editing! Happy blogging. */</pre></p> 

Теперь каждый раз, когда вы подключитесь к административной панели WordPress, в адресной строке браузера вы увидите, что url начинается с `https://` вместо `http://`.

### Заключение

Все хорошо, но теперь осталось выкроить &#8220;немного&#8221; маленьких зеленых бумажечек, чтобы приобрести SSL-сертификат ))

Оцените статью:  
<span id="post-ratings-732" class="post-ratings" data-nonce="06341c877b"><img id="rating_732_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(732, 1, '1 Star');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_732_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(732, 2, '2 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_732_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(732, 3, '3 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_732_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(732, 4, '4 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_732_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_off.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(732, 5, '5 Stars');" onmouseout="ratings_off(1, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>2</strong> votes, average: <strong>1,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_732_text"></span></span><span id="post-ratings-732-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>