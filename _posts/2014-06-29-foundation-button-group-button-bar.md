---
title: "Foundation - button group и button bar"
layout: post
categories:
tags: [button, foundation]
share: true
---

> Продолжение темы Foundation, в которой рассмотрен вопрос создания группы кнопок (button group) и панели кнопок (button bar).

В предыдущем обзоре я с вами научился создавать кнопки на Foundation - "Foundation - создаем кнопки". В этом обзоре мы научимся создавать группы кнопок (button group) - несколько кнопок, объединенных в группу. Такие кнопки могут применяться на странице для самых различных целей.

## Группы кнопок (button group) на Foundation

С точки зрения HTML струкрута такой группы представляет из себя обычный маркированный список с вложенными ссылками. Все дело в CSS-классах фреймворка Foundation, которые применяются к этому списку. Ссылку мы создаем с помощью класса `.button`, как и в предыдущей статье. А для элемента `ul` мы присваиваем класс `.button-group`:

{% highlight html %}
<ul class="button-group">
  <li><a href="#" class="button">Link 1</a></li>
  <li><a href="#" class="button">Link 2</a></li>
  <li><a href="#" class="button">Link 3</a></li>
</ul>
{% endhighlight %}

В результате получаем группу с набором кнопок внутри:

![Button group на Foundation]({{site.url}}/images/uploads/2014/06/foundation_button_group.png)

## Видоизменение группы кнопок (button group) на Foundation

Созданную таким образом группу кнопок можно видоизменять с помощью дополнительных классов, как это делалось ранее. К примеру создадим две группы кнопок и применим к ним дополнительные классы. `.radius`, `.round`, `.alert`, `.secondary`, `.success` Кстати, дополнительные классы можно применять не только к элементам `a`, но и к элементу `ul`:

{% highlight html %}
<ul class="button-group radius">
  <li><a href="#" class="button alert">Link 1</a></li>
  <li><a href="#" class="button secondary">Link 2</a></li>
  <li><a href="#" class="button success">Link 3</a></li>
</ul>
<ul class="button-group round">
  <li><a href="#" class="button alert">Link 1</a></li>
  <li><a href="#" class="button secondary">Link 2</a></li>
  <li><a href="#" class="button success">Link 3</a></li>
</ul>
{% endhighlight %}

Результат будет что-то в виде цветов итальянского флага:

![Button group с дополнительными классами]({{site.url}}/images/uploads/2014/06/foundation_button_groups_additional.png)

## Панели кнопок (button bar) на Foundation

Группы кнопок, в свою очередь, можно объединять между собой, создавая панели кнопок (button bar). Для этой цели применяется элемент `div` в классом `.button-bar`:

{% highlight html %}
<div class="button-bar">
  <ul class="button-group">
    <li><a href="#" class="button success small round">Link 1</a></li>
    <li><a href="#" class="button success small round">Link 2</a></li>
    <li><a href="#" class="button success small round">Link 3</a></li>
  </ul>
  <ul class="button-group round">
    <li><a href="#" class="button alert small">Link 1</a></li>
    <li><a href="#" class="button alert small">Link 2</a></li>
    <li><a href="#" class="button alert small">Link 3</a></li>
  </ul>
</div>
{% endhighlight %}

Результат будет примерно таким:

![Button bar на Foundation]({{site.url}}/images/uploads/2014/06/foundation_button_bar.png)

## Видоизменение панели кнопок (button bar) на Foundation

Точно также, как и группу кнопок с классом `.button-group`, панель кнопок `.button-bar` можно видоизменять с помощью все тех же дополнительных классов, как показано на примере выше.

## Создание button group и button bar c помощью Sass

Ну и по становящейся уже традиции переходим к вопросу создания панели кнопок (button bar) на Foundation c помощью Sass. Для этой цели служат два миксина:

  * `button-group-container`
  * `button-group-style`

Создаю HTML-разметку с произвольным именем класса `.horizontal`:

{% highlight html %}
<ul class="horizontal">
  <li><a href="#">Link 1</a></li>
  <li><a href="#">Link 2</a></li>
  <li><a href="#">Link 3</a></li>
  <li><a href="#">Link 4</a></li>
  <li><a href="#">Link 5</a></li>
</ul>
{% endhighlight %}

В файле `app.scss` прописываю для него следующие правила:

{% highlight css %}
.horizontal{
  @include button-group-container;
  a{
    @include button;
  }
  &>li{
    @include button-group-style;
  }
} /* end horizontal */
{% endhighlight %}

Результат получается таким:

![Button bar с помощью Sass на Foundation]({{site.url}}/images/uploads/2014/06/foundation_button_bar_sass.png)

У миксинов `button-group-container` и `button-group-style` имеются дополнительные параметры для тонкой настройки. Пример использования данных параметров показан на странице официальной документации - [Button groups][1].

## Редактирование файла app.scss

До этого момента так и не удосужился рассмотреть вопрос редактирования файла `app.scss`. Точнее, я уже упоминал о нем в начале обзора Foundation как о пользовательской таблице стилей, куда можно и нужно писать свои собственные CSS-правила. Вот теперь решил, что как раз настало время исправить свой недочет.

В начале файла `app.scss` имеются две строки:

{% highlight css %}
@import "settings";
@import "foundation";
{% endhighlight %}

Назначение их должно быть понятно:

  * строка `@import "settings";` импортирует Sass-переменные и их значения в проект
  * строка `@import "foundation";` импортирует сам фреймворк Foundation в проект

Однако, по аналогии с библиотекой Compass под препроцесор Sass, фреймворк Foundation позволяет выборочно импортировать в проект те свои возможности, которые необходимы на данный момент. Все эти возможности оформлены в виде отдельных модулей и прописаны каждый в отдельной строке файла `app.scss` в виде длинного закоментированного списка:

{% highlight css %}
@import "settings";
@import "foundation";

// Or selectively include components
//   @import
//   "foundation/components/accordion",
//   "foundation/components/alert-boxes",
//   "foundation/components/block-grid",
//   "foundation/components/breadcrumbs",
...
{% endhighlight %}

Допустим, на данный момент нам необходим модуль фреймворка Foundation для создания групп (button group) и панелей (button bar) кнопок. Такой модуль располагается в строке (легко найти по названию!):

{% highlight css %}
// "foundation/components/button-groups";
{% endhighlight %}

И чтобы подключить только его, нужно выключить весь фреймворк Foundation целиком - закоментировать строку:

{% highlight css %}
// @import "foundation";
{% endhighlight %}

и раскомментировать нижележащие строки следующим образом (только не забыть заменить запятую на точку с запятой в конце):

{% highlight css %}
@import "settings";
// @import "foundation";

// Or selectively include components
@import
//   "foundation/components/accordion",
//   "foundation/components/alert-boxes",
//   "foundation/components/block-grid",
//   "foundation/components/breadcrumbs",
"foundation/components/button-groups";
// @import "foundation/components/buttons";
//   "foundation/components/clearing",
{% endhighlight %}

Вуаля! Все работает и не нужно "тащить" за собой целый воз плюшек, которые не нужны на данный момент.

---

 [1]: http://foundation.zurb.com/docs/components/button_groups.html "Button groups"
