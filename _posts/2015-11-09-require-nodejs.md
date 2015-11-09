---
title: "Что такое require и module.exports"
layout: post
categories: javascript
tags: [node.js, require, module.exports]
share: true
---

Данная статья является *прочтением* и *переосмыслением* перевода [Node.js, Require и Exports](http://habrahabr.ru/post/217901/) статьи-оригинала [Node.js, Require and Exports](http://openmymind.net/2012/2/3/Node-Require-and-Exports/).

Помимо этого, существует еще одна неплохая статья, посвященная данной тематике - [Understanding module.exports and exports in Node.js](http://www.sitepoint.com/understanding-module-exports-exports-node-js/).

Тематика данного поста посвящена двум командам Node.js - `require` и `module.exports`. Как оказалось, обе эти команды являются *служебными* и "принадлежат" Node.js. С помощью этих команд Node.js осуществляет взаимодействие своих модулей между друг другом.

Команда `require` **подключает** один модуль к другому. Команда `module.exports` делает модуль **доступным** для других модулей.

***

В Node.js все *штуки* видны друг другу только **в рамках одного и того же файла**. Под штуками я подразумеваю *переменные*, *функции*, *классы и их члены*.

Например, у нас есть файл `misc.js` следующего содержания:

{% highlight javascript %}
const x = 5;
let summ = function (value) {
	return value + x;
}
{% endhighlight %}

Привычный **доступ** к переменной `x` и функции `summ` из **другого файла невозможен**. Это никак не связано с использованием `var`. Дело в том, что Node.js состоит из **блоков**, называемых **модулями**; и каждый **отдельный файл** по своей сути — **отдельный блок**, чья **область видимости изолирована** от других таких же блоков (модулей).

Теперь перед тем как мы узнаем, как **сделать эти штуки видимыми вне модуля**, рассмотрим более подробно, как **загружаются модули** в Node.js.

Сейчас речь пойдет о том месте, где пишется - `require`. Служебное слово `require` используют для **загрузки модуля**, обычно **присваивая результат его работы какой-то переменной**:

{% highlight javascript %}
let someModule = require('./some_module');
{% endhighlight %}

> Другими словами можно сказать, что в Node.js служебное слово `require` служит для подключения одного независимого модуля (файла) к другому независимому модулю (файлу). Принцип подключения через `require` заключается в создании в целевом модуле **объекта** и помещении в этот объект подключаемого модуля.

Конечно же, до тех пор, пока наш модуль (`some_module`) ничего не **отдает**, все приведенные примеры бесполезны. А чтобы наш модуль (`some_module`) что-нибудь **отдал**, мы будем использовать служебное слово `module.exports`:

{% highlight javascript %}
const x = 5;
let summ = function (value) {
	return value + x;
};
module.exports.x = x; // сделали константу 5 доступной из других модулей
module.exports.summ = summ; // сделали переменную summ доступной из других модулей
{% endhighlight %}

Вот теперь наш модуль (`some_module`) стал гораздо **более полезным**:

{% highlight javascript %}
let someModule = require('./some_module');
{% endhighlight %}

В результате в целевом модуле будет создан объект `someModule` со свойством `x = 5` (`someModule.x`) и методом `summ` (`someModule.summ`).

Есть ещё такой способ отдать *штуки* из нашего модуля:

{% highlight javascript %}
let User = function (name, email) {
	this.name = name;
	this.email = email;
};
module.exports = User;
{% endhighlight %}

> То есть, в исходном модуле создается объект `User` со свойствами `User.name` и `User.email`. Затем с помощью служебного слова `module.exports` объект `User` делается доступным для других модулей Node.js.

**Разница** между этими подходами **не велика, но важна**. Как видно, в данном случае мы экспортируем **функцию напрямую**:

{% highlight javascript %}
module.exports.User = User;
// vs
module.exports = User;
{% endhighlight %}
Всё это к тому, что потом ее будет **легче использовать**:

{% highlight javascript %}
var user = require('./user');

var u = new user.User();
// vs
var u = new user();
{% endhighlight %}

Выгода от использования такого способа заключается в том, что в данном случае нам не важно, будет ли ваш модуль представлять контейнер c экспортируемыми значениями или нет.

Чтобы еще **более красочно** представить **процесс взаимодействия модулей**, давайте рассмотрим следующий пример:

{% highlight javascript %}
let powerLevel = function (level) {
	return level > 9000 ? "it's over 9000" : level;
};
module.exports = powerLevel;
{% endhighlight %}

Когда вы подключите данный модуль используя `require`, фактически им будет являться **функция**, что позволит вам сделать следующее:

{% highlight javascript %}
let someModule = require('./powerlevel')(9000);
{% endhighlight %}

Что, по сути, является **упрощенной записью** следующего кода:

{% highlight javascript %}
let someModule = require('./powerlevel');
someModule(9000);
{% endhighlight %}

Вот и все кратко о командах `require` и `module.exports`.
