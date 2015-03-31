---
title: "Псевдокласс `:target` - стили для элемента-якоря в HTML-документе"
layout: post
categories:
tags: [css, target]
share: true
---

> Настала очередь изучить, что такое псевдо-класс `:target`.

Вопрос достаточно интересный как с точки зрения теории, так еще больше - с точки зрения практики.

Начнем издалека и вспомним (*если кто читал*) одну из глав книги Энди Бадда "Мастерская CSS". Глава называется "Изменение стиля элемента при наведении указателя на отдаленный элемент" и речь в ней идет о том, как сделать так, чтобы управлять одним элементом с помощью другого.

Техника, описанная в данной главе, представляла из себя следующее. В ссылку вкладывались несколько элементов, которые позиционировались абсолютно на странице и размещались в любом ее месте.

Визуально создается впечатление, что они никак не связаны между собой. Но на самом деле они находятся внутри одного элемента - ссылки (ниже приведен кусок кода из этой главы в качестве примера):

{% highlight html %}
<a title="Richard Rutter" href="http://www.clagnut.com/">
  <span class="link">» Richard Rutter</span>
</a>
{% endhighlight %}

Способ достаточно хорош, за исключением того, что применяется дополнительная разметка и нарушается семантика HTML-документа. На момент написания этой книги это был единственный способ управления "отдаленными элементами на странице.

Но на сегодняшний день существует еще один способ, более аккуратный и универсальный - с помощью псевдо-класса `:target`. Другое дело, что поддержка в браузерах этого CSS-свойства не полностью реализована и здесь можно смело показать пальцем в сторону браузера IE, в нем оно поддерживается, начиная с 9-ой версии.

![Псевдо-класс target]({{site.url}}/images/uploads/2013/11/target.png)

С помощью этого псевдо-класса можно управлять абсолютно любым элементом в документе. При этом он не обязан располагаться в каком-то определенном месте, наоборот - он может находиться в нормальном потоке и не нарушать семантику.

Приведу в качестве примера кусок кода, демонстрирующий такой подход:

{% highlight html %}
  <p>Lorem ipsum dolor sit amet, sed do eiusmod tempor</p>
  <p>Lorem ipsum dolor <a href="#example">Example</a> et dolore magna aliqua.</p>
  <p id="example">Lorem ipsum dolor sit amet, ut enim ad minim veniam</p>
  <p>Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut</p>
  <p>Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut</p>
{% endhighlight %}

Видим ссылку, помещенную в середине документа, обрамленную элементами `p`. У ссылки атрибут `href` имеет значение `#example`, который очень похож на ссылку на якорь. На самом деле это и есть ссылка на якорь, который назначен для одного из параграфов с идентификатором `id="example"`.

Вид ссылки может быть не обязательно таким, но и более длинным - `http://localhost:7788/third/#example`. Все, что располагается в ней после знака диез `#`, называется `хэштег`.

Псевдо-класс `:target` как раз и служит для стилизации элемента с якорем, на который указывает такая ссылка. Давайте приступим к стилизации, чтобы воочию увидеть, как работает этот псевдо-элемент.

Для одного из параграфов мы уже назначили идентификатор, который является якорем. Пропишем для него немного правил:

{% highlight css %}
#example{
  font: 12px Georgia, serif;
  color: #778899;
  -webkit-transition: all .3s ease-in-out;
     -moz-transition: all .3s ease-in-out;
      -ms-transition: all .3s ease-in-out;
       -o-transition: all .3s ease-in-out;
          transition: all .3s ease-in-out;
}
{% endhighlight %}

Мы изменили семейство шрифтов, кегль и цвет. Эти правила устанавливаются "как обычно", то есть - как прописали, так они и отображаются в браузере. Теперь создадим немного стилей, которые первоначально себя никак не проявляют, а только по происшествии какого-то события.

В нашем случае это будет клик на ссылке. Для таких правил синтаксис следующий:

{% highlight css %}
#example:target{
  color: #bbddff;
  font-weight: bold;
  outline: 1px solid #ff0000;
  padding: 20px;
  text-shadow: 1px 1px 1px #667788;
}
{% endhighlight %}

Откроем созданную нами страницу в браузере - и почти ничего не увидим. Точнее - только те правила, которые явно прописаны в первом куске кода. Но если кликнуть мышью на ссылке с текстом `Example`, то увидим достаточно занимательную трансформацию параграфа. Это псевдо-класс `:target` в действии!

Он применил прописанные для него правила только при совершении некоего события. И применены они были к обособленному участку HTML-кода (помеченному идентификатором `#example`), который почти никак не связан со ссылкой.

Можно немного усложнить пример и связать несколько параграфов между собой, то есть таким образом:

{% highlight css %}
#example:target + p{
  font-variant: small-caps;
  font-weight: bold;
  color: #0000ff;
  text-indent: 3em;
}
{% endhighlight %}

Откроем вновь страницу в браузере и посмотрим результат. Все ОК.

Псевдо-класс `:target` может принимать любые CSS-свойства, в том числе скрытие\показ элементов с помощью правила `display`. Последнее довольно часто применяется при верстке различных блоков.

На странице сайта MDN приведен пример создания одного из таких блоков - [CSS LightBox][1]. Другим ярким примером использования этого элемента являются вкладки на чистом CSS, где необходима смена цвета вкладок и их содержимого при переключении.

Ниже привожу, как всегда, полный текст кода.

{% highlight html %}
  <p>Lorem ipsum dolor sit amet, sed do eiusmod tempor</p>
  <p>Lorem ipsum dolor <a href="#example">Example</a> et dolore magna aliqua.</p>
  <p id="example">Lorem ipsum dolor sit amet, ut enim ad minim veniam</p>
  <p>Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut</p>
  <p>Lorem ipsum dolor sit amet, sed do eiusmod tempor incididunt ut</p>
{% endhighlight %}

{% highlight css %}
#example{
  font: 12px Georgia, serif;
  color: #778899;
  -webkit-transition: all .3s ease-in-out;
     -moz-transition: all .3s ease-in-out;
      -ms-transition: all .3s ease-in-out;
       -o-transition: all .3s ease-in-out;
          transition: all .3s ease-in-out;
}

#example:target{
  color: #bbddff;
  font-weight: bold;
  outline: 1px solid #ff0000;
  padding: 20px;
  text-shadow: 1px 1px 1px #667788;
}

#example:target + p{
  font-variant: small-caps;
  font-weight: bold;
  color: #0000ff;
  text-indent: 3em;
}
{% endhighlight %}

В принципе, это и все, что можно сказать о псевдо-классе `:target`.

---

[1]: https://developer.mozilla.org/en-US/docs/Web/CSS/:target "MDN LightBox Target"