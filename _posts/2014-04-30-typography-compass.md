---
title: Типографика с помощью Compass
author: gearmobile
layout: post
permalink: /typography-compass/
cleanretina_sidebarlayout:
  - default
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
categories:
  - Статьи по CSS
tags:
  - compass
  - typography
---
Отличный момент познакомиться с еще одной безграничной возможностью библиотеки Compass &#8211; это поработать с типографикой. Для этого дела в Compass имеется достаточно большой набор готовых миксинов. И хотя принцип большинства из них прост, суть дела от этого не меняется.

### Убрать подчеркивание у ссылок в Compass

Начнем с простого и попробуем настроить вид и поведение ссылок с помощью Compass. Для этого необходимо подключить модуль в текущий проект в виде строки:

<pre>@import "compass/typography/links";</pre>

Затем создадим в HTML-файле пару параграфов с ссылками:

<pre><p>
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eius, eos, dolorum, eum blanditiis laudantium placeat aspernatur esse dolorem <a href="#">optio molestiae provident</a> nobis sint architecto dolores repudiandae magnam iste assumenda minima.
</p></p>


<p>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sequi, nobis, maiores, quasi molestias dignissimos repellendus quis nemo quibusdam <a href="#">accusamus culpa numquam</a> voluptas sunt dolor inventore pariatur cumque a unde ut.
  </p></pre>
  
  
  <p>
    &#8230; и применим к ссылкам миксин <code>hover-link</code>:
  </p>
  
  
  <pre>p{
    margin-bottom: 20px;
    a{
      @include hover-link;
    }
  }</pre>
  
  
  <p>
    Если теперь посмотрим на скомпилированный вывод в CSS-файле, то увидим две до удивления простые строчки:
  </p>
  
  
  <pre>p a {
  text-decoration: none;
}
p a:hover {
  text-decoration: underline;
}</pre>
  
  
  <p>
    То есть, суть миксина <code>hover-link</code> в убирании подчеркивания у ссылки в ее обычном состоянии; и добавлении подчеркивания при состоянии hover. Попробуйте ввести показанный выше код в своем HTML-редакторе и посмотреть результат.
  </p>
  
  
  <h3>
    Изменение цвета ссылок в Compass
  </h3>
  
  
  <p>
    В Compass имеется миксин <code>link-colors</code> для управления цветом ссылок. То есть, с помощью этого миксина можно изменять стандартные цвета ссылки при ее различных состояниях.
  </p>
  
  
  <p>
    Синтаксис миксина достаточно устрашающий, с первого взгляда:
  </p>
  
  
  <pre>link-colors($normal, $hover, $active, $visited, $focus)</pre>
  
  
  <p>
    Однако здесь нет ничего сложного. Пять переменных миксина принимают в качестве аргументов цвета для ссылки в пяти ее состояниях:
  </p>
  
  
  <ul>
    <li>
      $normal &#8211; цвет обычного состояния ссылки
    </li>
    
    
    <li>
      $hover &#8211; цвет ссылки при наведенном на нее курсоре мыши
    </li>
    
    
    <li>
      $active &#8211; цвет ссылки в момент нажатия на нее
    </li>
    
    
    <li>
      $visited &#8211; цвет посещенной ссылки
    </li>
    
    
    <li>
      $focus &#8211; цвет ссылки, получившей фокус с клавиатуры
    </li>
    
  </ul>
  
  
  <p>
    При этом только один из параметров миксина <code>link-colors</code> является обязательным &#8211; <code>$normal</code>. Остальные можно опустить и тогда будут использоваться цвета по умолчанию.
  </p>
  
  
  <p>
    Давайте поэскпериментируем и немного изменим цвета для ссылок в нашем примере. Перед этим не забудем подключить соответствующий модуль строкой:
  </p>
  
  
  <pre>@import "compass/typography/links/link-colors"</pre>
  
  
  <p>
    Откроем таблицу цветов, расположенную по адресу <a href="http://www.w3schools.com/html/html_colors.asp">w3schools &#8211; html_colors</a> и наугад возмем оттуда пять цветов в HEX-формате, которые передадим миксину в качестве аргументов:
  </p>
  
  
  <pre>a{
    @include link-colors(#CC0000,#CC3300,#CC6600,#CC9900,#CCCC00);
}</pre>
  
  
  <p>
    В скомпилированном CSS-файле появиться несколько строчек такого вида:
  </p>
  
  
  <pre>p a:visited {
  color: #cc9900;
}
p a:focus {
  color: #cccc00;
}
p a:hover {
  color: #cc3300;
}
p a:active {
  color: #cc6600;
}</pre>
  
  
  <p>
    Введите показанный здесь код у себя и посмотрите на результат.
  </p>
  
  
  <h3>
    Сброс всех стилей для ссылок в Compass
  </h3>
  
  
  <p>
    Последний миксин из данного раздела позволяет производить сброс всех стилей для ссылок и превращении их в обычный текст, внутри которого находятся данные ссылки. Например, имеется параграф с классом <code>.woo</code>, внутри которого расположена ссылка. Применим к ней миксин <code>unstyled-link</code> для сброса всех стилей, предварительно подключив модуль:
  </p>
  
  
  <pre>@import "compass/typography/links/unstyled-link";</pre>
  
  
  <pre>p.woo a{
    @include unstyled-link;
}</pre>
  
  
  <p>
    Посмотрим на результат компиляции кода в CSS и увидим такую картину:
  </p>
  
  
  <pre>p.woo a {
  color: inherit;
  text-decoration: inherit;
  cursor: inherit;
}
p.woo a:active, .wrap p.woo a:focus {
  outline: none;
}</pre>
  
  
  <p>
    Ссылка наследует от параграфа (<em>то есть &#8211; текста, входящего в этот параграф</em>) свойства цвета, подчеркивание и вид курсора; а также убирается рамка <code>outline</code> при получении ссылкой фокуса или щелчка мыши по ней. То есть, другими словами, ссылка становиться полностью похожей внешне и по поведению на <strong>весь остальной текст</strong>, который ее окружает.
  </p>
  
  
  <p>
    Попробуйте у себя вышеприведенный код, чтобы увидеть результат.
  </p>