---
title: "Ubuntu - проблема с KVM Switch"
layout: post
categories: Linux
tags: [ubuntu]
share: true
---

Суть вопроса - имеется личный ноутбук с Ubuntu Gnome 22.04 и есть рабочий ноутбук с Windows 10. Ради удобства работы - был приобретен KVM Switch - для подключения обоих ноутбуков - к одному монитору, клавиатуре и мыше; и удобного и быстрого переключения между ноутами.

Подключение было выполнено успешно. Однако, возникла небольшая проблема - если переключиться с работающего ноутбука Ubuntu на ноутбук с Windows, а затем - выполнить переход обратно - с ноутбука Windows на ноутбук Ubuntu, то в этом случае возникала следующая ситуация.

Ноутбук Ubuntu - к моменту переключения на него обратно - успевал "заснуть"; и заставить его проснуться можно было - только открыв крышку ноута. Весьма неудобно и теряется смысл существования kvm switch'а.

После некоторого изыскания и помощи на стороне reddit - решение было найдено. Оригинал помощи находится здесь - [How to Change Lid Close Behavior in Ubuntu 20.04](https://ubuntuhandbook.org/index.php/2020/05/lid-close-behavior-ubuntu-20-04/)

Шаги исправления просты.

















// CODE SNIPPET
{% highlight typescript %}
// ...
{% endhighlight %}

// INLINE LINK
[link]( "link title")

// ANNOUNCEED LINK
[text][1]

// INLINE IMAGE
![image title]({{site.url}}/images/uploads/2015/08/image.jpg "image alt")

***
[1]: http://speckyboy.com/2015/01/26/six-common-freelancing-myths/ "Six Common Freelancing Myths"
