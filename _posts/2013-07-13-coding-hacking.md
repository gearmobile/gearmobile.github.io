---
title: "Верстка - маленькая хитрость при выборе цвета на макете"
layout: post
categories: css
tags: [css]
share: true
---

> Маленькая заметка о хитрости верстки.

Не знаю, вряд-ли можно назвать ее серьезной и тянущей на более-менее основательную статью. При верстке psd-макета часто встречаются градиенты (gradient). В последнее время использование градиентов очень популярно, особенно это касается таких элементов страницы, как фон или различные кнопки.

С появлением стандарта CSS3 цветовые переходы можно передать в коде легко и быстро. Поэтому, закодировать градиент - это не вопрос. Главное - быть внимательным и не пропустить (заметить) его.

Ведь встречаются такие элементы страницы, где "на глаз" сложно определить, есть ли там цветовой переход или нет его. Особенно, если он сделан в еле заметных оттенках серого цвета. По-серьезному, это нужно выделять слой с элементом, который содержит в себе градиент.

И затем в палитре слоев "Layers" смотреть, какой цветовой переход дизайнер заложил в данном случае. Но вот, чтобы просто узнать, присутствует ли в элементе градиент или нет (*и стоит ли с ним "повозиться" впоследствии для передачи в коде*), можно поступить следующим образом.

Допустим, есть страница 404 от известной web-студии TemplateMonster.com с фоновой заливкой определенного цвета:

![Страница с фоном в Photoshop]({{site.url}}/images/uploads/2013/11/eyedropper_404.png)

Мне нужно по-быстрому узнать, есть ли на ней градиентный переход по-вертикали. Выбираю инструмент Photoshop под названием "Пипетка" (Eyedropper). Можно активировать его на панели инструментов, или же проще и быстрее воспользоваться "горячей клавишей" I (*заглавная буковка `I` в английской раскладке*). И "забираю" цвет в верхней четверти фона страницы:

![Цвет в верхней половине фона в Photoshop]({{site.url}}/images/uploads/2013/11/eyedropper_01.png)

Не закрываю окно "Пипетки". "Забираю" цвет во-второй четверти фоновой заливки и проверяю, не изменился ли цвет. И так далее - третья четверть, четвертая четверть. И каждый раз смотрю, поменялся цвет или нет:

![Цвет в нижней половине фона в Photoshop]({{site.url}}/images/uploads/2013/11/eyedropper_02.png)

Другими словами, я "пробежался" по-вертикали с помощью пипетки и выяснил, что в конкретном случае, который представлен здесь, цвет везде одинаков - `#140100`. Итог - фоновая заливка страницы 404 выполнена дизайнером с использованием одного цвета. Поэтому в CSS-правилах можно указать коротко:

{% highlight css %}
background: #140100
{% endhighlight %}

Все. Просто и со вкусом.

---