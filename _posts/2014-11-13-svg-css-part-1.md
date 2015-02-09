---
title: 'Стилизация SVG с помощью CSS &#8211; Часть 1'
author: gearmobile
excerpt: 'Привожу вольный перевод великолепной статьи &#8220;Styling And Animating SVGs With CSS&#8221; от Sara Soueidan. Данная статья является одной из пяти в серии, посвященной формату SVG. Больше мне сказать нечего - читайте Сару :-) .'
layout: post
permalink: /svg-css-part-1/
ratings_users:
  - 1
ratings_score:
  - 5
ratings_average:
  - 5
cleanretina_sidebarlayout:
  - default
categories:
  - Web Development
tags:
  - svg
---
**От переводчика**. Привожу вольный перевод великолепной статьи &#8220;[Styling And Animating SVGs With CSS][1]&#8221; от [Sara Soueidan][2]. Данная статья является одной из пяти в серии, посвященной формату SVG. Больше мне сказать нечего &#8211; читайте Сару <img src="http://localhost:7788/third/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" /> .

CSS может использоваться для стилизации и анимации векторной графики точно также, как для стилизации и анимации HTML-элементов. В этой статье, которая является производной от [моего недавнего выступления][3] на конференциях [CSSconf EU][4] и [From the Front][5], где я рассказывала о перспективах и приемах работы с форматом векторной графики SVG и возможностях ее стилизации при помощи CSS.

Я покажу, каким образом можно экспотировать и оптимизировать SVG-файлы, способы вставки этих файлов в web-документ, способы стилизации и анимации SVG-файлов, на практике применим стили и анимацию к SVG-файлам-примерам.

### Введение

Масштабируемая векторная графика (SVG) представляет из себя векторные изображение для двухмерной графики (2D), в основе которой лежит формат XML. Подобная графика имеет поддержку интерактивности и анимации. Другими словами, SVG-файлы представляют из себя XML-теги, которые генерируют фигуры и изображения; к этим фигурам и изображениям могут быть применены стили и эффекты с помощью CSS точно также, как это делается с обычными HTML-элементами.

Анимация или интерактивность в SVG-файлах могут быть достигнута двумя способами &#8211; с помощью CSS или с помощью Javascript. В этой статье будет рассмотрен первый способ &#8211; как это сделать с помощью CSS.

Существует **много причин**, почему нужно делать выбор в пользу SVG и почему нужно использовать этот формат сегодня:

  * графика в формате SVG является **масштабируемой** и **не зависящей от разрешения**. Такая графика выглядит великолепно везде, будь то экраны с высоким разрешением Retina или же печатный вариант;
  * изображения имеют [отличную поддержку браузеров][6]. Создать fallbacks для браузеров, не имеющих поддержки, очень легко и в этой статье будет показано, как это сделать.
  * поскольку файлы в своей основе являются текстом, то они хорошо **поддаются архивации**, что позволяет сделать их значительно меньше по размеру, чем файлы форматов JPEG или PNG.
  * файлы стилизуются и анимируются с помощью CSS или Javascript
  * файлы формата SVG имеют встроенную поддержку clipping, masking, background blend modes и filters. Эти возможности эквиваленты возможностям обычного графического редактора, такого как Photoshop.
  * к файлам можно получить **доступ**. Другими словами, к ним можно получить легкий доступ через DOM API, что делает их прекрасным инструментом для инфографики и визуализации данных. Это дает ему преимущество перед HTML5 Canvas, поскольку контент последнего недоступен. С другой стороны, можно легко инспектировать каждый элемент файла с помощью инспектора элементов браузера точно также, как это делается с обычными HTML-элементами. Помимо этого, файлы доступны для экранных устройств чтения, если это необходимо. В последней части этой статье будет более подробно рассмотрен вопрос доступности файлов.
  * существует достаточно инструментов для создания, редактирования и оптимизации файлов. Помимо этого, существуют инструменты для облегчения и ускорения работы с SVG-файлами, что позволяет значительно ускорить рабочий процесс. Эти инструменты также будут рассмотрены позже.

#### Экспортирование SVG из графических редакторов и их оптимизация

Из всех редакторов векторной графики имеется **три самых популярных**:

1. [Adobe Illustrator][7]  
2. [Inkscape][8]  
3. [Sketch][9]

**Adobe Illustrator** &#8211; платное приложение от Adobe. Очень популярный редактор с прекрасным интерфейсом и множеством возможностей, что делает его любимым инструментом многих дизайнеров.

**Inkscape** является бесплатной альтернативой. Несмотря на более скромный интерфейс, этот редактор имеет все необходимые возможности для работы с векторной графикой.

**Sketch** &#8211; это приложение только под Mac OS X. Оно также не бесплатное, но уже успело стать достаточно популярным и собрать свою группу поклонников. Обладает множеством инструментов и возможностей, что делает работу в этом редакторе быстрее и удобнее.

Для создания векторной графики можно выбрать любой из этих трех редакторов. После создания SVG-файлов перед их вставкой на web-страницу нужно выполнить две операции: экспортирование из редактора и очистка этих файлов от лишних данных.

В этой статье я буду показывать экспортирование и оптимизацию SVG-файлов на примере редактора Adobe Illustrator. Этот процесс практически ничем не отличается от подобного в других редакторах. За исключением некоторых специфических настроек самого Illustrator, о чем будет упоминаться по ходу этой статьи.

Для экспортирования графики в SVG-формат в Illustrator нужно перейти в меню по пути “File” &#8211; “Save as”, а затем выбрать формат `.svg` из выпадающего списка форматов. Настройки в окне поменяются в соответствии с выбранным форматом `.svg`. Например, можно будет выбрать версию SVG; встраивать изображения в виде графики или же сохранить их отдельно, с созданием внешней ссылки на них; выбрать способ стилизации (с помощью презентационных аттрибутов или же при помощи CSS-стилей в элементе `style`).

Ниже показано изображение с окном экспорта SVG, в котором представлен наилучший набор настроек для сохранения файлов SVG для web:<figure id="attachment_1992" style="width: 477px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/ai-options-quick-preview-477x600.png" alt="Окно настроек экспорта SVG в Adobe Illustrator" width="477" height="600" class="size-medium wp-image-1992" />][10]<figcaption class="wp-caption-text">Окно настроек экспорта SVG в Adobe Illustrator</figcaption></figure> 

Почему представленный выбор настроек является наилучшим, рассказано Michaël Chaize в прекрасной статье [Export SVG for the Web With Illustrator CC][11].

Вне зависимости от того, какой графический редактор был выбран, в любом случае экспортируемый этим редактором SVG-файл не будет иметь чистого и оптимизированного кода. SVG-файлы, экспортированные из графических редакторов, как правило содержат много дополнительной информации, такой как метаданные самого редактора, комментарии, пустые группы, дефолтные значения, не оптимальные значения и другие подобные значения, которые можно безопасно удалить или конвертировать без оказания какого-либо эффекта на качество SVG-изображений. В случае, когда SVG-файлы созданы не вами, почти всегда они являются не оптимизированными; поэтому нужно в обязательном порядке использовать стороннее приложение для оптимизации SVG-графики.

Имеется несколько инструментов для оптимизации SVG-кода. Peter Collingridge создал online-инструмент [SVG Editor][12], в котором можно как вставлять напрямую, так и загружать свои собственные SVG-файлы. Инструмент обладает многими возможностями по оптимизации &#8211; удалением вспомогательного кода, комментариев, пустых групп и так далее. Одной из интересных настроек является управление числом знаков после запятой для координат точек:<figure id="attachment_1991" style="width: 500px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/svg-editor-quick-preview.png" alt="Окно настроек SVG Editor" width="500" height="362" class="size-full wp-image-1991" />][13]<figcaption class="wp-caption-text">Окно настроек SVG Editor</figcaption></figure> 

SVG Editor обладает возможностью автоматически перемещать SVG-изображение в самую верхнюю часть документа. Приятной особенностью данного инструмента является возможность предварительного просмотра, что позволяет сразу решить, какие изменения оставить, а какие &#8211; нет. Некоторые настройки могут привести к нарушению кода SVG-файла. Например, одного знака после запятой обычно хватает для оптимизации SVG-изображения. Но если вы работаете с SVG-файлом, который имеет много path, то при уменьшении числа знаков после запятой с четырех до одного может привести к нарушению SVG-изображения. Поэтому возможность предпросмотра является большим плюсом данного редактора.

Редактор SVG Editor является online-инструментом. Если вы предпочитаете offline инструмент, то попробуйте [SVGO][14] (O &#8211; сокращение от &#8220;оптимизатор&#8221;). Этот инструмент основан на Node.js, имеет простой и понятный [drag-and-drop интерфейс][15]. Если вам не нравиться использовать online-инструменты, то SVGO будет хорошей альтернативой.

Ниже представлено простое изображение формата &#8220;до и после&#8221;, иллюстрирующее процесс оптимизации SVG-файла в online-редакторе SVG Editor. Красным цветом выделены paths и наглядно показано, насколько эффективен процесс оптимизации в данном случае:<figure id="attachment_1990" style="width: 475px;" class="wp-caption aligncenter">

[<img src="http://localhost:7788/third/wp-content/uploads/2014/11/optimized-path-475x600.jpg" alt="Оптимизация SVG в SVG Editor" width="475" height="600" class="size-medium wp-image-1990" />][16]<figcaption class="wp-caption-text">Оптимизация SVG в SVG Editor</figcaption></figure> 

Обратите внимание на размер исходного SVG-файла и размер его оптимизированной версии. Вне всяких сомнений, оптимизированная версия более удобочитаемая.

После оптимизации SVG-файлов они готовы для встраивания их на web-страницу, для дальнейшей стилизации и анимации с помощью CSS.

#### P.S.

На практике воспользовался обоими инструментами оптимизации SVG &#8211; SVG Editor и SVGO. Могу сказать по личному опыту, что SVGO обладает **значительно лучшим коэффициентом оптимизации**. К слову сказать, это отечественная разработка команды Yandex.

Оцените статью:  
<span id="post-ratings-1989" class="post-ratings" data-nonce="6a674f84ff"><img id="rating_1989_1" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="1 Star" title="1 Star" onmouseover="current_rating(1989, 1, '1 Star');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1989_2" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="2 Stars" title="2 Stars" onmouseover="current_rating(1989, 2, '2 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1989_3" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="3 Stars" title="3 Stars" onmouseover="current_rating(1989, 3, '3 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1989_4" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="4 Stars" title="4 Stars" onmouseover="current_rating(1989, 4, '4 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /><img id="rating_1989_5" src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/stars_crystal/rating_on.gif" alt="5 Stars" title="5 Stars" onmouseover="current_rating(1989, 5, '5 Stars');" onmouseout="ratings_off(5, 0, 0);" onclick="rate_post();" onkeypress="rate_post();" style="cursor: pointer; border: 0px;" /> (<strong>1</strong> votes, average: <strong>5,00</strong> out of 5)<br /><span class="post-ratings-text" id="ratings_1989_text"></span></span><span id="post-ratings-1989-loading" class="post-ratings-loading"> <img src="http://localhost:7788/third/wp-content/plugins/wp-postratings/images/loading.gif" width="16" height="16" alt="Loading..." title="Loading..." class="post-ratings-image" />Loading...</span>

 [1]: http://www.smashingmagazine.com/2014/11/03/styling-and-animating-svgs-with-css/ "Styling And Animating SVGs With CSS"
 [2]: http://sarasoueidan.com/ "Sara Soueidan"
 [3]: https://www.youtube.com/watch?v=lf7L8X6ZBu8
 [4]: http://2014.cssconf.eu/ "CSSconf EU"
 [5]: http://2014.fromthefront.it/ "From the Front"
 [6]: http://caniuse.com/#feat=svg "Can I Use - SVG support"
 [7]: http://www.adobe.com/mena_en/products/illustrator.html "Adobe Illustrator"
 [8]: https://inkscape.org/en/ "Inkscape"
 [9]: http://bohemiancoding.com/sketch/ "Sketch"
 [10]: http://localhost:7788/third/wp-content/uploads/2014/11/ai-options-quick-preview.png
 [11]: http://creativedroplets.com/export-svg-for-the-web-with-illustrator-cc/ "Export SVG for the Web With Illustrator CC"
 [12]: http://petercollingridge.appspot.com/svg-editor "SVG Editor"
 [13]: http://localhost:7788/third/wp-content/uploads/2014/11/svg-editor-quick-preview.png
 [14]: https://github.com/svg/svgo "SVGO"
 [15]: https://github.com/svg/svgo-gui "SVGO"
 [16]: http://localhost:7788/third/wp-content/uploads/2014/11/optimized-path.jpg