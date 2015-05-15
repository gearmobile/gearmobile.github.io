---
title: "Функции .hide и .show библиотеки jQuery"
layout: post
categories: jquery
tags: [jquery, hide, show]
share: true
---

Две функции-близнеца, предназначенные для управления видимостью элементов на странице. Это осуществляется через CSS-свойство `display` (замечание: по внимательном перечтении оказалось не все так просто - в этой "магии" задействованы не только CSS-свойство `display`, но также `width`, `height`, `opacity`; и даже `margin` и `padding`!).

После скрытия элемента значение его CSS-свойство становится равным `dispaly: none`. Перед появлением элемента его CSS-свойство `display` изменяет свое значение на противоположное от `none`.

`duration` — продолжительность выполнения анимации (появления или скрытия). Может быть задана в миллисекундах или строковым значением 'fast' или 'slow' (200 и 600 миллисекунд). Если этот параметр не задан, анимация будет происходить мгновенно, элемент просто появится/исчезнет.

`callback` — функция, заданная в качестве обработчика завершения анимации (появления или скрытия).

## Примеры использования:

 - мгновенно скроет элемент с идентификатором `#leftFit`.

{% highlight javascript %}
$("#leftFit").hide();
{% endhighlight %}


 - мгновенно покажет элемент с идентификатором `#leftFit`:

{% highlight javascript %}
$("#leftFit").show();
{% endhighlight %}


 - в течении 1/3 секунды скроет элемент с идентификатором `#leftFit`:

{% highlight javascript %}
$("#leftFit").hide(300);
{% endhighlight %}

- в течении 600 миллисекунд вернет видимость элементу с идентификатором `#leftFit`:

{% highlight javascript %}
$("#leftFit").show("slow")
{% endhighlight %}

Можно скрывать и показывать элементы с помощью **сворачивания/разворачивания** (*за счет изменения высоты*). Это делают функции `slideUp()`, `slideDown()`.

Медленно скрывает и раскрывает все видимые параграфы, длительность анимационных эффектов — 600 миллисекунд:

{% highlight javascript %}
$('button').click(function () {
  $('p').hide('slow');
});

$('button').click(function() {
  $('p').show('slow');
});
{% endhighlight %}


Использование callback-функции:

{% highlight javascript %}
$('#clickme').click(function() {
  $('#book').hide('slow', function() {
    alert('Animation complete.');
  });
});

$('#clickme').click(function() {
  $('#book').show('slow', function() {
    alert('Animation complete.');
  });
});
{% endhighlight %}

Материал данной статьи основан на ресурсах:

* [http://jquery.page2page.ru][1]
* [http://jquery-docs.ru][2]
* [http://api.jquery.com][3]

... и не претендует на оригинальность.

***

[1]: http://jquery.page2page.ru "Hide and Show"
[2]: http://jquery-docs.ru "Hide and Show"
[3]: http://api.jquery.com "API jQuery"
