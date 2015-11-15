---
title: "Различие между exports и module.exports"
layout: post
categories: javascript
tags: [node.js, exports, module.exports]
share: true
---

Попытка разобраться, в чем различие между `exports` и `module.exports`, основанная на статье [Understanding module.exports and exports in Node.js](http://www.sitepoint.com/understanding-module-exports-exports-node-js/).

## Что такое `module.exports` и `exports` в Node.js

Как web-разработчики, мы часто сталкиваемся с ситуацией, когда необходимо иметь дело с малознакомым кодом. И тогда сам собою возникает логичный вопрос - сколько времени мне потребуется для того, чтобы разобраться с чужим кодом и понять принцип его работы?

Типичный ответ на этот вопрос - ровно столько, чтобы начать самому писать код; а затем вернуться к изучению этой темы позже, когда позволит на это время. Ну что-же, как мне кажется, пришло время получше разобраться с такими понятиями, как `module.exports` и `exports` в Node.js. Спешу поделиться с вами тем, что я узнал по этому вопросу.

### Что такое модуль (module)

Основная концепция модуля заключается в том, что он инкапсулирует логически связанный между собой код в **единый блок**. Можно сказать иначе - создание модуля заключается в помещении всех взаимосвязанных между собой функций в **один единый файл**.

Для понимания вышесказанного лучше всего создать пример приложения под Node.js. Давайте создадим файл с именем `greetings.js`, внутри которого размещены **две функции**:

{% highlight javascript %}
sayHelloInEnglish = function () {
  return 'Hello';
}

sayHelloInSpanish = function () {
  return 'Hola';
}
{% endhighlight %}

### Экспорт модуля

Польза от файла (модуля) `greetings.js` (*и функций, которые находятся в этом файле*) появляется в том случае, когда файл `greetings.js` можно **использовать внутри других файлов (модулей)**.

Для достижения этого необходимо слегка изменить исходный код файла `greetings.js`. Чтобы понять, что происходит на самом деле, в данном случае будем выполнять **пошаговый процесс**:

* представьте себе, что эта строка существует в качестве первой линии кода в `greetings.js`:

{% highlight javascript %}
var exports = module.exports = {}
{% endhighlight %}

* видоизменим обе функции в файле `greetings.js` с помощью выражения `exports` таким образом, чтобы они были **доступны для внешних файлов (модулей)**:

{% highlight javascript %}
exports.sayHelloInEnglish = function () {
  return 'Hello';
}

exports.sayHelloInSpanish = function () {
  return 'Hola';
}
{% endhighlight %}

В приведенном выше коде можно было бы заменить выражение `exports` на `exports.module` и получить точно такой же результат.

Если этот момент кажется вам непонятным, то помните, что выражение `exports` и выражение `exports.module` ссылаются на один и тот же объект.

* это текущее значение выражения `module.exports`:

{% highlight javascript %}
module.exports = {

  sayHelloInEnglish = function () {
    return 'Hello';
  }

  sayHelloInSpanish = function () {
    return 'Hola';
  }
}
{% endhighlight %}

### Импортирование модуля

Давайте сделаем методы модуля `greetings.js` общедоступными для другого файла (модуля) с именем `main.js`. Этот процесс также разобьем пошагово для более лучшего понимания:

* в Node.js используется команда `require` для импортирования одного модуля в другой модуль:

{% highlight javascript %}
var require = function(path) {

  // ...

  return module.exports;
};
{% endhighlight %}

* давайте подключим модуль `greetings.js` в модуль `main.js`:

{% highlight javascript %}
// main.js
var greeting = require('./greetings.js');
{% endhighlight %}

Приведенная выше строка кода равнозначна нижеследующему коду:

{% highlight javascript %}
// main.js
var greeting = {

sayHelloInEnglish = function () {
  return 'Hello';
}

sayHelloInSpanish = function () {
  return 'Hola';
}

}
{% endhighlight %}

* теперь можно использовать функции модуля `greetings.js` внутри модуля `main.js` как методы объекта `greeting`:

{% highlight javascript %}
// main.js
var greeting = require('./greetings.js');

// Hello
greeting.sayHelloInEnglish('Hello');

// Hola
greeting.sayHelloInSpanish('Hola');
{% endhighlight %}

### Отличительные моменты

Команда `require` возвращает объект, свойства и методы которого доступны другим внешним модулям при помощи команды `module.exports`.

Нижеприведенный пример поможет разобраться в данном вопросе:

{% highlight javascript %}
// greetings.js

// var exports = module.exports = {};

exports.sayHelloInEnglish = function () {
  return 'Hello';
}
exports.sayHelloInSpanish = function () {
  return 'Hola';
}

// Эта строка кода выполняет повторное переопределение,

module.exports = 'Bonjour';
{% endhighlight %}

Теперь сделаем подключение модуля `greetings.js` в модуль `main.js`:

{% highlight javascript %}
// main.js
var greetings = require('./greetings.js')
{% endhighlight %}

На данный момент в нашем примере ничего не поменялось. В переменную `greetings` помещается код, доступный из модуля `greetings.js`. Не более того.

Однако, если мы попытаемся воспользоваться каким-либо из методов модуля `greetings.js` - `sayHelloInEnglish` или `sayHelloInSpanish`, то мы получим ошибку. Это произошло в следствие того, что было произведено переопределение экспортируемой структуры модуля при помощи команды `module.exports`.

Другими словами, последней командой `module.exports` экспортируется совсем другой модуль - `Bonjour`, у которого другие свойства и методы. Происходит **переопределение** экспортируемого модуля и вызов метода `sayHelloInEnglish` или `sayHelloInSpanish` вызовет ошибку:

{% highlight javascript %}
// main.js
// var greetings = require("./greetings.js");

/*
 * TypeError: object Bonjour has no
 * method 'sayHelloInEnglish'
 */
greetings.sayHelloInEnglish();

/*
 * TypeError: object Bonjour has no
 * method 'sayHelloInSpanish'
 */
greetings.sayHelloInSpanish();
{% endhighlight %}

Чтобы отследить ошибки при использовании модуля `greetings`, можно вывести их в консоль:

{% highlight javascript %}
// "Bonjour"
console.log(greetings);
{% endhighlight %}

### Заключение

Импорт и экспорт модулей в Node.js является ежедневной задачей. Я надеюсь, что благодаря этой статье стала ясна разница между командой `exports` и командой `module.exports`. Более того, если у вас когда-либо произойдет ошибка при доступе к общедоступным методам модуля в будущем, то я надеюсь, что у вас есть лучшее понимание того, почему может возникнуть эти ошибки.

### Заключение автора перевода

Если честно - прочитал статью и даже потрудился перевести ее, а вот разницы между `exports` и `module.exports` не заметил. Я хочу сказать, что автор этой статьи (как мне кажется) так и не показал разницы между ними. Могу ошибаться, конечно и буду рад комментариям.

**UPD**. Вопрос снят, так как решен. В принципе, существование этой и предыдущей статьи уже не надобно, так как есть отличный скринкаст от Ильи Кантора по Node.js, где раскрываются все вопросы - [Скринкаст NODE.JS](https://learn.javascript.ru/nodejs-screencast).

В свете этого скринкаста в обеих статьях обнаруживаются достаточно существенные ошибки. Прямо и не знаю - может убрать обе эти статьи о греха подальше? ))

***
