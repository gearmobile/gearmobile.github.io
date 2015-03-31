---
title: "CSS - как сделать линию короче бокса"
layout: post
categories: css
tags: [css]
share: true
---

> При верстке макета сайта, кстати, совсем несложного, возник вопрос.

Заключается он в том, имеется информационная часть, разбитая на две колонки. Каждая из колонок также разделена на отдельные секции - посты. Для колонок и постов на макете задуманы дизайнером декоративные линии-разделители.

Проблемы с созданием таких линий, в принципе, нет никакой. Их можно легко создать с помощью стилевого правила `border-bottom` и `border-right`. Или же с помощью правил `border-right` и элемента `hr`.

Но вопрос заключается в том, что декоративные линии на макете короче, чем высота колонки или ширина поста. То есть, получается, что `border` должен быть короче, чем бокс:

![Декоративные линии короче, чем контент]({{site.url}}/images/uploads/2013/11/css-lines.png)

Как же поступить в данном случае? Скажем так, обычными способами CSS решить такой вопрос невозможно. Но решение было найдено с помощью форума htmlbook.

В данном случае можно выйти из положения с помощью псевдокласса `:after`. Для наглядности представим такой пример.

Создаем слой с контентом:

{% highlight html %}
text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text text
{% endhighlight %}

И пропишем для него стилевые правила:

{% highlight html %}
div {
  width: 300px;
  position: relative;
}
{% endhighlight %}

Как видим, их не так уж и много. Задаем ширину блока и устанавливаем для него относительное позициоирование. Затем для созданного нами бокса создаем псевдокласс `:after` и прописываем для него свойства:

{% highlight css %}
div:after {
  content: "";
  position: absolute;
  top: 30px;
  right: -10px;
  bottom: 30px;
  border-left: 1px solid #000;
}
{% endhighlight %}

Немного распишем, что да как в этом коде.

Внутри простого блока после его содержимого создается псевдоблок с абсолютным позиционированием, для которого устанавливаются координаты `top` и `bottom` (**благодаря двум последним он растягивается, так как создаются верхняя и нижняя координата для границы**) и для этого блока создается только левая граница `border-left` со свойствами: `1px сплошного черного цвета`.

На этом все.

---
