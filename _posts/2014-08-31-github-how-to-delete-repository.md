---
title: Как удалить репозиторий на GitHub
author: gearmobile
layout: post
---
Как новичок в работе с системой [GitHub][1], столкнулся с вопросом &#8211; **как удалить созданный на GitHub репозиторий**? Оказалось, что ничего сложного в этом нет. Однако, задача эта и не такая простая, как может показаться. По крайней мере, чисто интуитивно у меня не получилось ее выполнить &#8211; пришлось искать ответ в Сети.

Итак, у меня есть учетная запись на GitHub, под которой создана пара репозиториев. Один из этих репозиториев был создан в учебных целях, поэтому для моей дальнейшей работы он мне не пригодиться и его можно удалить.

### Список репозиториев на GitHub

Для начала открою свою страничку на GitHub и посмотрю, какие репозитории у меня уже есть:<figure id="attachment_1739" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github-list_of_repos-600x464.png" alt="Список репозиториев на GitHub" width="600" height="464" class="size-medium wp-image-1739" />][2]<figcaption class="wp-caption-text">Список репозиториев на GitHub</figcaption></figure> 

Один из репозиторев &#8211; `arbeit` &#8211; можно удалить.

Для этой цели нужно просто зайти в него по ссылке:<figure id="attachment_1740" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github-repo_arbeit-600x464.png" alt="Репозиторий arbeit на GitHub" width="600" height="464" class="size-medium wp-image-1740" />][3]<figcaption class="wp-caption-text">Репозиторий arbeit на GitHub</figcaption></figure> 

В правом нижнем углу окна браузера, в списке, имеется строка `Settings`. Открываем ее, сразу же копируем имя репозитория в поле `Repository name` (оно нам понадобиться еще здесь) и **прокручиваем страницу вниз**, пока не находим **раздел с устрашающим названием** `Danger Zone`. В этой опасной зоне находим подраздел `Delete this repository` с одноименной кнопкой `Delete this repository`.

Жмем на эту кнопку и получаем в результате **окно с предупреждением об удаленни репозитория**. В окне запроса имени удаляемого репозитория вводим (или вставляем из буфера обмена) &#8211; `arbeit`:<figure id="attachment_1741" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github-delete_repo_arbeit-600x464.png" alt="Запрос имени удаляемого репозитория" width="600" height="464" class="size-medium wp-image-1741" />][4]<figcaption class="wp-caption-text">Запрос имени удаляемого репозитория</figcaption></figure> 

Снова жму на кнопку, на этот раз с еще более страшным напоминанием о последствиях совершаемого мною шага. И все! Репозиторий `arbeit` удален:<figure id="attachment_1742" style="width: 600px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/08/github-repo_arbeit_deleted-600x464.png" alt="Удаленный репозиторий на GitHub" width="600" height="464" class="size-medium wp-image-1742" />][5]<figcaption class="wp-caption-text">Удаленный репозиторий на GitHub</figcaption></figure> 

Ничего сложного, но так сразу и не догадаешься, что нужно делать. Разработчики GitHub постарались и обезопасили пользователей от случайного удаления репозиториев с данными.

 [1]: https://github.com/ "GitHub"
 [2]: http://localhost:7788/third/wp-content/uploads/2014/08/github-list_of_repos.png
 [3]: http://localhost:7788/third/wp-content/uploads/2014/08/github-repo_arbeit.png
 [4]: http://localhost:7788/third/wp-content/uploads/2014/08/github-delete_repo_arbeit.png
 [5]: http://localhost:7788/third/wp-content/uploads/2014/08/github-repo_arbeit_deleted.png