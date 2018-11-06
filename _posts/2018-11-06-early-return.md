---
title: "Return Early Pattern"
layout: post
categories: javascript
tags: [javascript, return, early, pattern]
share: true
---

Шаблон раннего возврата (return early pattern) в JavaScript - это простой способ уменьшить число else-операторов в теле функции до нуля. Есть много причин, чтобы предпочесть этот шаблон использованию else-операторов.

* Уменьшение общего количества кода на странице
* Уменьшение длины строк кода упрощением логической сложности
* Улучшение удобочитаемости кода

Суть шаблона раннего возврата (return early pattern) заключается в том, чтобы заменить необходимость дополнительных условий в функциях JavaScript, используя ключевое слово return в теле оператора if.

Создадим функцию, которая ведет себя по-разному при определенных условиях (примечание: это тривиальный и надуманный пример, просто чтобы получить представление о сути вопроса):

{% highlight javascript %}
function willItBlend (someObject) {
  var ItWillBlend;

  if (someObject.blendable === 'It will blend') {
    itWillBlend = true;
  } else {
    itWillBlend = false;
  }

  return itWillBlend;
}
{% endhighlight %}


Хотя данная функция кажется читаемой, добавим в нее еще одно условие для проверки того, что функция вызывается для работы с объектом вместо undefined:

{% highlight javascript %}
function willItBlend(someObject) {
  var itWillBlend;

  if (typeof someObject === 'object') {
    if (someObject.blendable === 'It will blend') {
      itWillBlend = true;
    } else {
      itWillBlend = false;
    }
  } else {
    itWillBlend = false;
  }

  return itWillBlend;
}
{% endhighlight %}

Эта функция понятной и ее имя является описательным, однако она представляется все-же излишне сложной. Можем ли мы использовать шаблон раннего возврата (return early pattern) для повышения удобочитаемости и уменьшения количества else-выражений?

Попробуем:

{% highlight javascript %}
function willItBlend(someObject) {
  if (typeof someObject !== 'object') {
    return false;
  }

  if (someObject.blendable !== 'It will blend') {
    return false;
  }

  return true;
}
{% endhighlight %}

Используя шаблон раннего возврата (return early pattern), мы смогли удалить все ненужные else-инструкции и сделать функцию намного яснее и более краткой.

## Бонус: одно условное выражение

Мы можем дополнительно переписать функцию для использования только одного оператора if.

Проверим:

{% highlight javascript %}
function willItBlend(someObject) {
  if (
    typeof someObject !== 'object' ||
    someObject.blendable !== 'It will blend'
    ) {
    return false;
  }

  return true;
}
{% endhighlight %}

***
