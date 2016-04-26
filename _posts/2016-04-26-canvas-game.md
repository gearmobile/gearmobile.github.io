---
title: "Canvas - cоздание простой игры"
layout: post
categories: javascript
tags: [javascript, html5, canvas, game]
share: true
---

Данная статья планируется как пошаговый обзор создания простой JavaScript-игры класса "Ball and Paddle" на Canvas. Примерами такой игры могут послужить старые DOS-е игры наподобие таких - [Ball and Paddle](http://www.dosgamesonline.com/index/list/genre/Ball_and_Paddle.html "Ball and Paddle").

Пример кода из этой статьи взят из видео-курса достаточно известного Интернет-ресурса, посвященного фронтенд-разработке - [Udemy](https://www.udemy.com/ "Udemy").

Почему Canvas и почему игра? Лично для меня процесс познания JavaScript сильно облегчается благодаря Canvas - так интереснее. А создание игры на Canvas - это еще интереснее!

Итак, с чего начнем? Дальше в меру своих сил буду стараться детально пошагово рассказывать, что делает тот или иной кусок кода. И начнем с базового набора - создания Canvas.

## Базовый Canvas

HTML-разметка страницы будет предельно простой:

{% highlight html %}
<body>
  <canvas id="canvas"></canvas>
  <script src="script.js"></script>
</body>
{% endhighlight %}

В JavaScript'е создадим две глобальные переменные - одну для элемента Canvas, вторую - для 2d-контекста Canvas. Когда parser браузера построит DOM-дерево документа (событие `DOMContentLoaded`), инициализируем обе переменные, выполним проверку удачного получения 2d-контекста Canvas и если проверка будет пройдена успешно, то динамически зададим размеры Canvas:

{% highlight javascript %}
var canvas = null;
var ctx = null;

window.addEventListener('DOMContentLoaded', function () {
  canvas = document.querySelector('#canvas');
  ctx = canvas.getContext('2d');
  if ( ctx ) {
    canvas.width = 800;
    canvas.height = 500;
  }
}, false);
{% endhighlight %}

## Базовые элементы игры

Основа Canvas была создана в предыдущем шаге. В этом шаге создадим три фигуры, которые будут учавствовать в игре. Таковыми фигурами будут:

* фон игры
* мячик (ball)
* площадка (paddle)

Ниже я приведу JavaScript-код создания всех трех элементов, но сам код комментировать не буду, так как он очень простой и относится к основам Canvas:

{% highlight javascript %}
var canvas = null;
var ctx = null;

window.addEventListener('DOMContentLoaded', function () {

  canvas = document.querySelector('#canvas');
  ctx = canvas.getContext('2d');

  if ( ctx ) {

    canvas.width = 800;
    canvas.height = 500;

    ctx.fillStyle = '#000';
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.fillStyle = 'firebrick';
    ctx.beginPath();
    ctx.arc(50, 50, 10, 0, 360*Math.PI/180, true);
    ctx.fill();
    ctx.closePath();

    ctx.fillStyle = '#fff';
    ctx.fillRect(100, canvas.height-40, 100, 10);

  }
}, false);
{% endhighlight %}

Живой результат вышеприведенного кода можно посмотреть на этой странице - [Lesson1-1](http://codepen.io/gearmobile/pen/ONowpB "Lesson1-1"). Это то, что должно получиться и что послужит заготовкой для игры.

## Анимация мячика

В этом шаге предстоит сделать более интересные вещи. Во-первых, мы сделаем так, чтобы мячик начал двигаться как по-горизонтали, так и по-вертикали. А во-вторых, сделаем так, чтобы он вел себя как настоящий резиновый мячик - при ударе о стену отскакивал от нее и мчался в противоположном направлении.

Сделать это достаточно просто. Для этого нам понадобится одна из так называемых тайминговых функций JavaScript - `setInterval()`. А также немного воображения.

Анимация мячика будем делать по-простому принципу, по которому делается любой мультфильм или кино - мячик будет отрисовываться с заданной частотой (`1000/frames`), но каждый раз в новой позиции. В результате будет создаваться иллюзия его движения. Каждая новая позиция мячика - это его координата по оси X или Y с новым значением соответственно.

Чтобы мячик двигался достаточно быстро, изменять значения координат (`ballX += ballStepX` и `ballY += ballStepY`) мячика по оси X и Y будем с определенным шагом (`ballStepX` и `ballStepY`) - допустим, со значениями 5 или 6:

{% highlight javascript %}
var canvas = null;
var ctx = null;

var frames = 24;

var ballX = 50;
var ballY = 50;
var ballStepX = 5;
var ballStepY = 6;
var ballRadius = 10;

window.addEventListener('DOMContentLoaded', function () {

  canvas = document.querySelector('#canvas');
  ctx = canvas.getContext('2d');

  if ( ctx ) {

    canvas.width = 800;
    canvas.height = 400;

    setInterval( function () {

      ballX += ballStepX;
      ballY += ballStepY;

      if ( ballX < 0 || ballX > canvas.width) {
        ballStepX *= -1;
      }
      if ( ballY < 0 || ballY > canvas.height ) {
        ballStepY *= -1;
      }

      ctx.fillStyle = '#000';
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      ctx.fillStyle = 'firebrick';
      ctx.beginPath();
      ctx.arc(ballX, ballY, ballRadius, 0, 360*Math.PI/180,true);
      ctx.fill();
      ctx.closePath();

      ctx.fillStyle = '#fff';
      ctx.fillRect(100, canvas.height-40, 100, 10);

    }, 1000/frames);

  }
}, false);
{% endhighlight %}

Эффект отскакивания от стенок (как резиновый мячик) обеспечивает проверка условий в участке кода:

{% highlight javascript %}
...
if ( ballX < 0 || ballX > canvas.width) {
  ballStepX *= -1;
}
if ( ballY < 0 || ballY > canvas.height ) {
  ballStepY *= -1;
}
...
{% endhighlight %}

Здесь все просто - при выполнении условия знак переменной `ballStepX` или `ballStepY` будет меняться на противоположный. В результате значение переменной `ballX` или `ballY` будет возрастать или уменьшаться. Как следствие, мячик будет двигаться в одну или в другую сторону.

Живой пример приведенного выше кода можно посмотреть и изучить на этой странице - [Lesson1-2](http://codepen.io/gearmobile/pen/grdjdZ "Lesson1-2").

## Двигаем paddle

В этом шаге нужно заставить двигаться paddle при помощи мыши. Для этого по событию `mousemove` внутри элемента Canvas будем получать значение X-координаты курсора мыши. И передавать это значение элементу paddle, его X-координате левого верхнего угла. Тем самым мы заставим paddle двигаться. За все эти действия будет отвечать функция `mouseCoords()`:

{% highlight javascript %}
...
function mouseCoords (event) {
  var canvasOffset = canvas.getBoundingClientRect();
  var htmlElement = document.documentElement;
  mouseX = event.clientX - canvasOffset.left - htmlElement.scrollLeft;
  paddleX = mouseX - paddleWidth/2;
}
...
{% endhighlight %}

Обратите внимание на последнюю строку функции - `paddleX = mouseX - paddleWidth/2;`. Переменная `paddleX` необходима для того, чтобы при выходе за границы Canvas элемент paddle скрывался ровно на половину своей ширины.

Также не забудем создать переменные для paddle и передать их в код для отрисовки фигуры:

{% highlight javascript %}
...
var paddleX = null;
var paddleWidth = 100;
var paddleHeight = 10;
var paddleOffset = 40;
...
ctx.fillStyle = '#fff';
ctx.fillRect(paddleX, canvas.height - paddleOffset, paddleWidth, paddleHeight);
...
{% endhighlight %}

Живой пример приведенного выше кода можно посмотреть и изучить на этой странице - [Lesson1-3](http://codepen.io/gearmobile/pen/grdjVy "Lesson1-3"). Подвигайте курсором мыши право-влево, чтобы увидеть эффект.

## Мячик отскакивает от paddle

На этом этапе нужно сделать так, чтобы мячик отскакивал от paddle, когда последний оказывается на его пути. Выполнить эту задачу просто - ведь мячик уже отскакивает от "стен" Canvas. Следовательно, нужно научить мячик "видеть" еще и paddle.

Для этого сначала нужно опеределить внешние границы paddle - все его четыре стороны:

{% highlight javascript %}
...
var paddleLeftEdge = paddleX;
var paddleRightEdge = paddleLeftEdge + paddleWidth;
var paddleTopEdge = canvas.height - paddleOffset;
var paddleBottomEdge = paddleTopEdge + paddleHeight;
...
{% endhighlight %}

Когда значения всех сторон будут определены, то можно будет подставить эти значения в условие - и дело сделано:

{% highlight javascript %}
...
if ( ballX > paddleLeftEdge && ballX < paddleRightEdge && ballY > paddleTopEdge && ballY < paddleBottomEdge ) {
  ballStepY *= -1;
}
...
{% endhighlight %}

Живой пример приведенного выше кода можно посмотреть и изучить на этой странице - [Lesson1-4](http://codepen.io/gearmobile/pen/YqOOqd "Lesson1-4"). Подвигайте курсором мыши право-влево и постарайтесь поймать мячик с помощью paddle, чтобы увидеть эффект.

## Угол отскока мячика

В этом шаге сделаем так, чтобы наша игра смотрелась более правильной с точки зрения физики и обычной природы. То есть, при разном угле попадания на paddle мячик должен отскакивать от него с разной скоростью. Чем острее угол падения, тем с большей скоростью отскакивает от paddle мячик.

Решается эта задача несколькими строками кода:

{% highlight javascript %}
...
if ( ballX > paddleLeftEdge && ballX < paddleRightEdge && ballY > paddleTopEdge && ballY < paddleBottomEdge ) {
  ballStepY *= -1;
  var paddleCenter = paddleLeftEdge + paddleWidth/2;
  var ballDistance = ballX - paddleCenter;
  ballStepX = ballDistance * 0.35;
}
...
{% endhighlight %}

В первой строке `var paddleCenter = paddleLeftEdge + paddleWidth/2;` находится X-координата середины paddle. В строке `var ballDistance = ballX - paddleCenter;` определяется расстояние, на котором мячик соприкоснулся с paddle относительно его середины. В строке `ballStepX = ballDistance * 0.35;` полученная дистанция присваивается шагу приращения по оси Х мячика - `ballStepX`.

Логично предположить, что чем больше величина дистанции точки соприкосновения мячика относительно середины paddle, тем выше новая скорость движения мячика по-горизонтали. Чтобы эта скорость не была слишком высокой, ее необходимо уменьшить, умножив на 0.35, к примеру.

Живой пример приведенного выше кода можно посмотреть и изучить на этой странице - [Lesson1-5](http://codepen.io/gearmobile/pen/YqOOQg "Lesson1-5").

## Оптимизация кода

На данный момент наша задача по построению игры практически решена. Но остался один организационный момент.

Заключается он в том, что код необходимо реорганизовать в отдельные функции. Такой код будет читаться и поддерживаться значительно лучше.

Одна из таких функций уже была создана ранее - это функция `mouseCoords()`. Давайте преобразуемся и весь оставшийся код подобным образом:

{% highlight javascript %}
...
function drawRect (leftX, leftY, boxWidth, boxHeight, boxFillColor) {
  ctx.fillStyle = boxFillColor;
  ctx.fillRect(leftX, leftY, boxWidth, boxHeight);
}
...
function drawBall(centerX, centerY, radius, fillColor) {
  ctx.fillStyle = fillColor;
  ctx.beginPath();
  ctx.arc(centerX, centerY, radius, 0, 360*Math.PI/180, true);
  ctx.fill();
  ctx.closePath();
}
...
function drawAll() {
  drawRect(0, 0, canvas.width, canvas.height, '#000');
  drawBall(ballX, ballY, ballRadius, 'firebrick');
  drawRect(paddleX, canvas.height - paddleOffset, paddleWidth, paddleHeight, '#fff');
}
...
{% endhighlight %}

Готовый пример преобразованного в функции кода можно посмотреть на этой странице - [Lesson1-6](http://codepen.io/gearmobile/pen/EKeepp "Lesson1-6").

***
На этом все.
