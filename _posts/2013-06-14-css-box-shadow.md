---
layout: post
title: "CSS box shadow - создаем тени для блоков"
author: gearmobile
tags: [box-shadow, css]
---
Свойство box-shadow позволяет web-дизайнерам создавать очень интересные эффекты для элементов страницы. А именно - с помощью него можно задавать тень для блочных элементов, например таких, как div.

Создаваемая тень имеет несколько параметров, комбинация которых позволяет придать оригинальный и неповторимый вид элементу. Можно установить смещение тени по горизонтали, по вертикали, задать цвет, степень размытия краев, размер. В CSS3 имеется возможность создать для элемента сразу несколько теней, с разным цветом и размерами.

Можно также создать тень, которая будет размещена не снаружи элемента, а внутри него.

### Синтаксис свойства box-shadow:

{% highlight css %}
  box-shadow: h-shadow v-shadow blur spread color inset;
{% endhighlight %}

где:

  * h-shadow - смещение тени по горизонтали;
  * v-shadow - смещение тени по вертикали;
  * blur - размытие границ тени;
  * spread - размер тени;
  * color - цвет тени;
  * inset - создать тень внутри элемента.

Порядок следования значений свойства box-shadow необязательный, то есть, можно расположить их в любой последовательности.

Простой пример использования box-shadow:

Браузеры Firefox, Chrome, Opera и IE9 отобразят серую тень под этим блоком.

Код, выводящий данный результат:

{% highlight css %}
  box-shadow: 5px 5px 2px #888;
{% endhighlight %}

Однако, приведенный пример будет не совсем работоспособным. Для браузеров Firefox и Chrome более ранних версий может понадобиться добавление префиксов. Тогда полная версия кода будет выглядеть следующим образом:

{% highlight css %}
  box-shadow: 5px 5px 2px #888;
  -moz-box-shadow: 5px 5px 2px #888;
  -webkit-box-shadow: 5px 5px 2px #888;
{% endhighlight %}

Как говорилось выше, порядок следования значений свойства необязателен. Более того, из всех шести значений обязательными являются только два первых - смещение по горизонтали и по вертикали. Все остальные можно опустить, если в них нет необходимости.

### Примеры использования кода:

{% highlight css %}
  box-shadow: 5px 5px;
  box-shadow: 5px 5px 2px;
  box-shadow: 5px 5px 2px #888;
  box-shadow: 5px 5px 2px 3px #888;
  box-shadow: 5px 5px 2px 3px #888 inset;
  box-shadow: 5px 5px 2px #888, -5px -5px #f4f4f4, 1px 1px 2px #cc6600;
{% endhighlight %}

Последняя строка наиболее интересна, поэтому разберем ее подробнее.

Смещения по горизонтали и вертикали могут принимать как положительные, так и отрицательные значения. В последнем случае тень будет перемещаться не вправо, а влево. Размытие тени blur и размер тени spread могут иметь только положительные значения или 0. Несколько теней для одного элемента можно задавать последовательно, через запятую. В нашем примере было задано три тени с разными цветами и смещением.

### Теория box-shadow

По умолчанию, для элемента создается внешняя тень.

Тень создается как минимум с посощью двух обязательных параметров - горизонтального и вертикального смещения.

Горизонтальное смещение определяет смещение тени относительно элемента по горизонтали. Может принимать положительное или отрицательное значение. При положительном значении тень смещается вправо от элемента. При отрицательном - влево от элемента.

Вертикальное смещение задает смещение тени по вертикали относительно элемента. Может рпинимать положительное или отрицательное значение. При положительном значении тень смещается относительно элемента вниз по вертикали. При отрицательном значении смещение происходит вверх по вертикали.

Третье и необязательное значение свойства box-shadow, это размытие `blur`. По умолчанию оно равно 0 и граница тени четкая. Размытие может принимать только положительные значения. Чем больше число, тем сильнее происходит размытие. В спецификации не разъясняется точного алгоритма, по которому происходит усиления размытия при увеличении его значения.

Размер тени spread также явлется необязательным параметром и может принимать как положительные, так и отрицательные значения. При положительном значении тень увеличивается по всем направлениям. При отрицательном наоборот уменьшается.

### Несколько примеров теней

Ниже приведены несколько небольших примеров создания теней с разными смещениями, размытием и размером.

В примере A смещение тени происходит влево и вверх на 5 пикселей.

{% highlight css %}
  #Example_A {
  -moz-box-shadow: -5px -5px #888;
  -webkit-box-shadow: -5px -5px #888;
  box-shadow: -5px -5px #888;
}
{% endhighlight %}

В примере B точно также происходит смещение на пять пикселей вверх и влево, но при этом добавлено размытие тени величиной в 5 пикселей. Хорошо видно, что тень имеет нечеткие границы.

{% highlight css %}
  #Example_B {
  -moz-box-shadow: -5px -5px 5px #888;
  -webkit-box-shadow: -5px -5px 5px #888;
  box-shadow: -5px -5px 5px #888;
}
{% endhighlight %}

В примере С таже самая тень имеет размер в 5 пикселей.

{% highlight css %}
  #Example_C {
  -moz-box-shadow: -5px -5px 0 5px #888;
  -webkit-box-shadow: -5px -5px 0 5px#888;
  box-shadow: -5px -5px 0 5px #888;
}
{% endhighlight %}

Пример D показывает тень, имеющую размытие в 5 пикселей и размер в 5 пикселей.

{% highlight css %}
  #Example_D {
  -moz-box-shadow: -5px -5px 5px 5px #888;
  -webkit-box-shadow: -5px -5px 5px 5px#888;
  box-shadow: -5px -5px 5px 5px #888;
}
{% endhighlight %}

В примере E показана тень, которая не имеет смещения по горизонтали и вертикали, но у нее задано размытие в 5 пикселей.

{% highlight css %}
  #Example_E {
  -moz-box-shadow: 0 0 5px #888;
  -webkit-box-shadow: 0 0 5px#888;
  box-shadow: 0 0 5px #888;
}
{% endhighlight %}

В примере F тень также не имеет смещения, но имеет размытие и размер в 5 пикселей.

{% highlight css %}
  #Example_F {
  -moz-box-shadow: 0 0 5px 5px #888;
  -webkit-box-shadow: 0 0 5px 5px#888;
  box-shadow: 0 0 5px 5px #888;
}
{% endhighlight %}

На этом все.