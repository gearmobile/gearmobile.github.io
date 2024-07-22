---
title: "KDE и ssh-ключи"
layout: post
categories: Linux
tags: [linux, gnome-keyring, ssh-key, ssh-agent, ssh-add, eval]
share: true
---

В Ubuntu Gnome имеется утилита **gnome-keyring**, при помощи которой очень удобно работать с ключами ssh-key под GitHub или GitLab. Удобство работы с gnome-keyring заключается в том, что ssh-ключи подгружаются только один раз и потом в каждой сессии терминальной или в любом редакторе - VSC или WS - подтягиваются и используются под капотом.

В KDE, будь-то Manjaro или Kubuntu - нет пакета **gnome-keyring** и поэтому в каждой новой терминальной сессии или открытом редакторе при работе с Git - нужно будет авторизоваться и подгружать ssh-ключи при помощи команд:

{% endhighlight bash %}
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/awesome_ssh_key
{% endhighlight %}

Делать это каждый раз утомительно - отвлекает внимание и занимает лишнее время. Можно немного автоматизировать процесс при помощи конфигурационного файла **config**.

Делается это таким образом.

В папке **.ssh** создаем файл конфигурации **config**:

{% endhighlight bash %}
cd ~/.ssh
touch config
{% endhighlight %}

Открываем файл конфигурации **config**:

{% endhighlight bash %}
nano ~/.ssh/config
{% endhighlight %}

Добавляем в него такое содержимое:

{% endhighlight bash %}
IdentityFile ~/.ssh/github_key
IdentityFile ~/.ssh/gitlab_key
IdentityFile ~/.ssh/id_rsa_buhlServer
{% endhighlight %}

Как видим, первые две строки - это путь в ssh-ключам, в моем случае под GitHub и GitLab. Третья строка - если често, не знаю что делает. Но - благодаря этим трем строкам оба ssh-ключа теперь автоматически подгружаются и используются в любой терминальной сессии или редакторе кода.

Единственный момент - для подобного случая я генерировал ssh-ключи **без пароля**, чтобы система или редактор не спрашивали его каждый раз. В принципе, получилась почти полноценная замена **gnome-keyring**.

---
