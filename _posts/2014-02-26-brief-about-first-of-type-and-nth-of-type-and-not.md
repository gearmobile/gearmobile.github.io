---
title: "Кратко о :first-of-type, :nth-of-type и :not"
layout: post
categories: css
tags: [first-of-type, not, nth-of-type]
share: true
---

## Псевдоэлементы `:first-of-type` и `:last-child`

> Псевдоэлемент `:first-of-type` служит для выборки дочернего элемента определенного типа.

Можно сказать, что псевдоэлемент `:first-of-type` является частным случаем псевдоэлемента `:first-child`. Если псевдоэлемент `:first-child` выполняет выборку первого дочернего элемента вне зависимости от его типа, то псевдоэлемент `:first-of-type` осуществляет выборку первого дочернего элемента только указанного типа (если этот элемент отвечает заданному условию - типу элемента).

Аналогично работает псевдоэлемент `:last-of-type`, только применяется к последнему дочернему элементу определенного типа. Более общим случаем является псевдоэлемент `:last-child`.

Псевдоэлементы `:last-child`, `:nth-child()`, `:first-of-type` НЕ ПОДДЕРЖИВАЮТСЯ IE8.

Пример:

{% highlight css %}
.fofo p:first-of-type{}
{% endhighlight %}

... в примере тег `p` является указанием типа дочернего элемента. То есть, будет выбран первый дочерний элемент типа `p`, родителем которого является элемент с классом `.fofo`.

{% highlight css %}
.wowo p:last-of-child{}
{% endhighlight %}

Выбрать последний дочерний элемент типа `p`, родителем которого является элемент с классом `.wowo`.

Рабочий пример приведен ниже. Два одинаковых списка. К первому применен псевдоэлемент `:first-of-type`, ко второму - псевдоэлемент `:first-child`.

В первом случае выбран первый параграф списка, так как в выражении указано выбрать именно первый дочерний элемент списка, являющийся параграфом `p`:

{% highlight css %}
.fofo p:first-of-type{
  font-weight: bold;
  color: #222;
  font-variant: small-caps;
  text-shadow: 1px 1px 1px #999;
}
{% endhighlight %}

Во втором случае к списку применен псевдоэлемент `:first-child` и в этом случае был отобран первый элемент указанного списка - ссылка `a`! А то, что этот элемент является ссылкой, а не параграфом `p`, роли не играет - тип элемента не был указан:

{% highlight css %}
.wowo :first-child{
  font-size: 14px;
  font-style: italic;
  color: green;
  font-weight: bold;
}
{% endhighlight %}

![Псевдоэлемент :first-of-type]({{site.url}}/images/uploads/2014/02/first-of-type1.jpg){:.center-image}

Псевдоэлемент `:last-of-child` и его общий случай `:last-child` разбирать смысла нет, так как выборка элемента из HTML-документа осуществляется аналогично с тем лишь различием, что применяется не к первому, а последнему дочернему элементу.

## Псевдоэлемент `:nth-of-type`

Псевдоэлемент `:nth-of-type` является частным случаем псевдоэлемента `:nth-child`. В случае с `:nth-of-type` выборка элементов производится не только по порядковому номеру, но и по типу элемента.

Например, `p img:nth-of-type(odd){float: left}` и `p img:nth-of-type(even){float: right}` делает выборку четных и нечетных порядковых номеров только элементов `img`.

Отбираются все дочерние по отношению к `.nthOfType` элементы типа `img`, нечетные по порядковому номеру. И применяются к нему правила - смещение влево, `margin-right` и тень справа:

{% highlight css %}
.nthOfType img:nth-of-type(odd){
  float: left;
  margin: 0 10px 0 0;
  box-shadow: 3px 3px 3px rgba(0,0,0,.65);
}
{% endhighlight %}

Отбираются все дочерние по отношению к `.nthOfType` элементы типа `img`, четные по порядковому номеру. И применяются к нему правила - смещение право, `margin-left` и тень слева:

{% highlight css %}
.nthOfType img:nth-of-type(even){
  float: right;
  margin: 0 0 0 10px;
  box-shadow: -3px 3px 3px rgba(0,0,0,.65);
}
{% endhighlight %}

![Псевдоэлемент :nth-of-type]({{site.url}}/images/uploads/2014/02/nth-of-type.jpg){:.center-image}

## Псевдокласс :not

Псевдокласс `:not` (псевдокласс отрицания) - выбрать все элементы `p`, у которых НЕТ класса `.classy` и применить к ним следующие свойства: цвет и тень. Другими словами, выборка элементов с помощью псевдокласса `:not` производится от обратного - "выбрать все элементы, которые НЕ ОТВЕЧАЮТ следующему условию."

Этот псевдокласс является антагонистом обычного условия - "если удовлетворяет условию, то примени такое-то свойство":

{% highlight html %}
<p class="classy">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>
<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>
<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>
<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat.
</p>
{% endhighlight %}

{% highlight css %}
.dodo p:not(.classy){
  color: blue;
  text-shadow: 1px 1px 1px rgba(0,0,255,.2);
}
{% endhighlight %}

![Псевдоэлемент :not]({{site.url}}/images/uploads/2014/02/not.jpg){:.center-image}

На этом все.

---
