---
title: "Кнопка внутри поля поиска - как создать с помощью CSS"
layout: post
categories: css
tags: [css, button]
share: true
---

> Интересный вопрос создания поля поиска с кнопкой внутри.

Сейчас такой прием очень популярен в дизайне и используется повсеместно на сайтах. Почему популярен - просто очень красив такой способ передачи поля ввода в веб-приложении. Чтобы было более понятно, о чем идет речь, давайте посмотрим пример макета с подобной формой поиска:

![Пример поля поиска с кнопкой внутри на макете]({{site.url}}/images/uploads/2013/11/search-form-example.jpg)

Дизайн нарисован таким образом, что видим следующее. Поле ввода текста с текстом-заглушкой `placeholder`, справа внутри поля находиться кнопка отправки запроса в виде текста "Send".

Все вроде так и в чем же проблема? Трудность заключается в том, что на сегодняшний день возможности CSS не позволяют поместить кнопку внутри элемента `input`. Поэтому в данном случае выход один - разместить рядом два элемента: `input` и кнопку (`button type="submit"` или `input type="submit"`).

Оба эти элемента обернуть в родительский элемент `form` (благо он является блочным) которому придать внешние свойства поля ввода - фоновую заливку, границу, внутренние отступы `padding`. А у настоящих элементов `input` или `button` убрать все визуальные признаки их присутствия внутри `form`.

На авторитетном для меня сайте htmlbook есть статья, посвященная подобному вопросу. Но в ней описывается способ, когда внутрь элемента форм вставляется дополнительный блок `div`. Которому назначаются все внешние атрибуты поля ввода.

Мне такой подход не совсем понятен - зачем плодить лишнюю разметку, когда с подобной задачей прекрасно справляется сам элемент `form`.

Мне более нравиться способ, представленный на сайте Speckyboy.com автором Catalin Rosu, в котором как раз и используются только три элемента: `form`, `input type="text"`, `button type="submit"`. В самом конце статьи я приведу код этого примера также, ибо он мне понравился.

Приступаем к первому примеру и начнем создавать поле поиска с кнопкой, как на картинке. Для начала придадим элементу `form` внешние признаки поля ввода: зададим границу с радиусом скругления, фоновую заливку и внутренние поля отступа `padding`.

Помимо этого, явно установим ширину и высоту нашего будущего "поля" ввода и немного приукрасим ее, анимировав цвет границы при наведении `hover`:

{% highlight css %}
form{
  border: 1px solid #ad9d80;
  padding: 4px 20px 4px 24px;
  width: 254px;
  margin: 0 0 25px 0;
  height: 30px;
  background-color: #e4d9c5;
  border-radius: 9px;
  
  &:hover{
    border-color: darken(#ad9d80, 10%);
  }
{% endhighlight %}

Теперь уберем все, что делает `input` таковым в нашем случае - обнулим границу, переопределим `padding` и установим в ноль `margin`.

Это основные свойства элемента `input`, назначаемые ему по умолчанию браузером. Затем немного поборемся с браузерами на WebKit (Chrome\Safari), которые создаются эффект свечения вокруг поля ввода при получении фокуса `outline` и рисуют тонкую линию-границу `-webkit-appearance: none` несмотря на то, что мы убрали ее, обнулив `border`.

Фоновый цвет сделаем одинаковым с элементом `form`, чтобы создавалась иллюзия однородности. Все остальные свойства можно не упоминать - они очевидны (кегль, цвет текста, высота `input` и так далее).

Практически также поступим для элемента `button`, за исключением характерных нюансов типа `text-transform: uppercase` или `color: #4f432e`.

Кстати, у Catalin Rosu я перенял "фишку", когда он применяет `button type="submit"` вместо `input type="submit"`. Это делается для дополнительной функциональности кнопки, так как `button` может перехватывать событие <kbd>Enter</kbd> (нажатие этой клавиши на клавиатуре) + событие мыши. А вот `input type="submit"` - только нажатие мыши на самом себе:

{% highlight css %}
input[type="text"]{
  border: none;
  margin: 0;
  outline: none;
  -webkit-appearance: none;
  height: 30px;
  vertical-align: top;
  background-color: #e4d9c5;
  color: #beb19a;
  font-size: 18px;
  font-style: italic;
  padding: 0 8px 0 0;
  width: 192px;
}
{% endhighlight %}

{% highlight css %}
button[type="submit"]{
  border: none;
  margin: 0;
  padding: 0;
  font-size: 18px;
  text-transform: uppercase;
  line-height: 30px;
  color: #4f432e;
  background-color: #e4d9c5;
  cursor: pointer;
  transition: color .2s;
  
  &:hover{
    color: lighten(#4f432e, 10%);
  }
{% endhighlight %}

Ну и в конце приукрасим текст-заглушку `placeholder`. Здесь придется использовать браузерные префиксы, так как данное свойство не поддерживается в полной мере браузерами на сегодня:

{% highlight css %}
input::-webkit-input-placeholder {
  color: #beb19a;
  font-size: 16px;
  font-weight: normal;
  font-style: italic;
}
input:-moz-input-placeholder {
  color: #beb19a;
  font-size: 16px;
  font-weight: normal;
  font-style: italic;
}
input:-ms-input-placeholder {
  color: #beb19a;
  font-size: 16px;
  font-weight: normal;
  font-style: italic;
}
{% endhighlight %}

Совсем забыл привести HTML-код, на основе которого создавались все вышеприведенные стили:

{% highlight html %}
<form action="#" method="#">
  <input type="text" name="email" id="email" placeholder="enter your email address...">
  <button type="submit">send</button>
</form>
{% endhighlight %}

Результат создания поля поиска показан ниже:

![Созданное в коде поле ввода с кнопкой внутри]({{site.url}}/images/uploads/2013/11/search-form-ready.jpg)

Все хорошо.

## Поле ввода и кнопка со стрелкой (псевдо-элемент) внутри.

На закуску привожу полный код (почти без объяснений - чего там объяснять) от Catalin Rosu, как и обещал.

Здесь есть интересный атрибут `required`, который делает значение в поле ввода обязательным. Если оно будет пустым и нажать кнопку отправки, то появиться сообщение о необходимости сначала ввести данные.

Также автором статьи намеренно используется элемент `input type="text"` вместо нового элемента `input type="search"`, который еще не до конца поддерживается всеми браузерами:

{% highlight html %}
<form class="catalin">
    <input type="text" placeholder="Search here ..." required>
    <button type="submit">Send</button>
  </form>
{% endhighlight %}

Довольно объемный, но это связано с теми эффектами, которые применены к данной форме:

{% highlight css %}
form.catalin{
  width: 390px;
  margin: 50px auto;
  overflow: hidden;
  padding: 10px;
  background-color: #ccc;
  border-radius: 8px;
  box-shadow: 0 0 8px rgba(0,0,0,.3) inset;
}
  form.catalin input{
    float: left;
    border: none;
    padding: 2px 10px 2px 4px;
    font: 16px Arial, Helvetica, sans-serif;
    height: 26px;
    width: 306px;
    margin: 0;
    -webkit-appearance: none;
    outline: none;
    box-shadow: 0 0 1px rgba(0,0,0,.5);
    border-radius: 3px 0 0 3px;
  }
  form.catalin button{
    float: left;
    border: none;
    background-color: #778899;
    padding: 0;
    margin: 0;
    width: 70px;
    height: 30px;
    font: bold 12px/30px Arial, Helvetica, sans-serif;
    position: relative;
    cursor: pointer;
    text-shadow: 1px 1px 1px rgba(255,255,255,.5);
    border-radius: 0 3px 3px 0;
    text-transform: uppercase;
    text-align: center;
  }
    form.catalin button:hover{
      background-color: #667788;
    }
  form.catalin button:before{
    content: '';
    position: absolute;
    top: 10px;
    left: -5px;
    border-top: 5px solid transparent;
    border-bottom: 5px solid transparent;
    border-right: 5px solid #778899;
  }
    form.catalin button:hover:before{
      border-right-color: #667788;
      text-shadow: 1px 1px 1px rgba(255,255,255,.6);
    }

/* Placeholder
-----------------------------------------------------*/
  form.catalin input::-webkit-input-placeholder {
     color: #999;
     font-weight: normal;
     font-style: italic;
  }
   
  form.catalin input:-moz-placeholder {
      color: #999;
      font-weight: normal;
      font-style: italic;
  }
   
  form.catalin input:-ms-input-placeholder {
      color: #999;
      font-weight: normal;
      font-style: italic;
  }
{% endhighlight %}

И результат этого кода - красивое поле ввода с не менее красивой кнопкой отправки данных на сервер:

![Поле ввода с кнопкой внутри]({{site.url}}/images/uploads/2013/11/search-form-catalin.jpg)

На этом все.

---