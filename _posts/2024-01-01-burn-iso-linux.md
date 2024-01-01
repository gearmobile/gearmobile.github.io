---
title: "Запись ISO на USB при помощи dd"
layout: post
categories: Linux
tags: [iso, usb, cli]
share: true
---

Команда dd для записи файла ISO на USB-накопитель

{% highlight bash %}
sudo dd if=ubuntu-20.04.1-live-server-amd64.iso of=/dev/sda bs=1M status=progress
{% endhighlight %}