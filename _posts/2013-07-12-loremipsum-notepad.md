---
title: "Плагин LoremIpsum в Notepad++"
layout: post
categories: notepad
tags: [loremipsum, notepad++]
share: true
---

> При версте сайта из макета одним из часто повторяющихся действий является наполнение содержимого так называемой "рыбой".

Что такое "рыба"? Это ничего незначащий текст, единственная роль которого состоит в качестве наполнителя текстом тех областей, в которых в последствии предполагается располагать осмысленный контент.

В процессе верстки такого текста у верстальщика естественно нет такого контента. Но он ему и не нужен. Для него главное создать полную копию макета и заполнить каким-либо текстом.

На практике каждый поступает при наполнении "рыбой", исходя из своих предпочтений. Кто-то пользуется статьями из Википедии, кто-то берет любые тексты из рефератов Яндекса.

Помимо двух указанных источников, существует так называемая классическая "рыба". Это текст на латинском языке, начинающийся со слов "Lorem ipsum dolor sit amet".

На самом деле этот текст, хоть и является латинским, также не несет в себе особого смысла, так как представляет их себя очень сильно искаженную выдержку из произведения какого-то древнеримского автора.

В Интернете имеется достаточное количество сайтов, являющихся генераторами подобного текста. К примеру, популярный сайт Lipsum.com.

Однако, для распространенного блокнота программистов Notepad++ имеется плагин, который также является генератором Lorem ipsum. Название плагина именно такое - "Lorem Ipsum". Устанавливается плагин через менеджер плагинов "Plugin Manager".

После установки плагин прописывается в меню "Плагины - InsertLoremIpsum - View Insert Dialog". При его активации открывается диалоговое окно в правой части:

![Плагин LoremIpsum в Notepad++]({{site.url}}/images/uploads/2013/11/plugin_lorem_ipsum.png)

Управление "LoremIpsum" минималистичное, но что называется - все по делу.

В верхнем окошке устанавливается число (по умолчанию оно равно 5), являющееся счетчиком слов, предложений или параграфов, которые будут вставлены в тело кода.

Следующие за ним три строки:

  * `words` (слова)
  * `sentences` (предложения)
  * `paragraphs` (параграфы)

... являются радиопереключателями, с помощью которых можно выбрать, что необходимо вставлять в код - слова, предложения или параграфы.

Флажок "Start with Lorem ipsum" задает условие, при котором каждый набор слов, предложения или параграфы начинаются с Lorem ipsum. И в самом низу расположена кнопка "Insert", предназначение которой очевидно - вставить выбранный набор слов, предложений или параграфов в код html-документа.

Перейдем от слов к делу и на практике вставим "рыбу".

Вставляем 4 слова. Устанавливаем в окне счетчика число 4, выбираем радиопереключатель в положение words. Чтобы вставляемые записи не повторялись, убираем галочку `checkbox` "Start with Lorem ipsum".

Устанавливаем курсор мыши в то место html-кода, куда необходимо поместить "рыбу" и нажимаем кнопку "Insert":

![Плагин LoremIpsum - вставка слов в Notepad++]({{site.url}}/images/uploads/2013/11/plugin_lorem_ipsum-4words.png)

Вставим 3 предложения. Устанавливаем счетчик в значение `3`. Переводим переключатель в положение `sentences` (предложения). Оставляем пустой строку "Start with Lorem ipsum".

Устанавливаем курсор мыши в то место html-кода, куда необходимо поместить "рыбу". Жмем на "Insert":

![Плагин LoremIpsum - вставка трех предложений в Notepad++]({{site.url}}/images/uploads/2013/11/plugin_lorem_ipsum-3sentences.png)

Вставляем 1 параграф. Устанавливаем счетчик в значение 1. Переводим радиокнопку в положение `paragraphs` (параграфы). Устанавливаем курсор мыши в то место html-кода, куда необходимо поместить "рыбу". Нажимаем кнопку "Insert":

![Плагин LoremIpsum - вставка одного параграфа в Notepad++]({{site.url}}/images/uploads/2013/11/plugin_lorem_ipsum-1paragraph.png)

## Заключение

Как мне кажется, использование плагина "LoremIpsum", встроенного в Notepad++, более удобно, чем сторонние источники, типа сайтов-генераторов. Удобство заключается в том, что все "под рукой". В любой момент можно открыть диалоговое окно вставки "рыбы" и произвести практически моментальное наполнение содержимым.

Особенно это удобно, если верстка производится автономно, без доступа в Интернет. Когда надобность в плагине отпадает, его можно сразу же закрыть, до следующего раза.

На этом все.

---