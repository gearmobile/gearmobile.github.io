---
title: "Nx monorepo Nestjs + Angular"
layout: post
categories: Development
tags: [nx, monorepo, angular, nest.js, prisma, sql]
share: true
---

На официальном сайте Nx я не смог найти готовых примеров конфигурации Nx для развертывания workspace - Angular + Nest.js. После некоторых поисков нашел такой пример на StackOverflow - [NX Monorepo (NestJS/Angular)](https://stackoverflow.com/questions/77347982/nx-monorepo-nestjs-angular).

Ниже привел *более подробный* вариант описания этого способа.

#### Первоначальное решение

Устанавливаем Nx глобально в системе - для более удобной последующей работы:

{% highlight bash %}
nx globally npm i -g nx
{% endhighlight %}

Переходим к процессу развертывания - инициализируем новый workspace командой [Installation](https://nx.dev/getting-started/installation):

{% highlight bash %}
npx create-nx-workspace

Need to install the following packages:
create-nx-workspace@19.2.3
Ok to proceed? (y)
{% endhighlight %}

... задаем имя для нового проекта:

{% highlight bash %}
Where would you like to create your workspace? ‣ awesome-project 
{% endhighlight %}

... на вопрос о выборе предпочтительного стека отвечаем - **None** - сами наполним workspace нужными стеками чуть позднее:

{% endhighlight bash %}
? Which stack do you want to use? …

None:          Configures a TypeScript/JavaScript project with minimal structure.
React:         Configures a React application with your framework of choice.
Vue:           Configures a Vue application with your framework of choice.
Angular:       Configures a Angular application with modern tooling.
Node:          Configures a Node API application with your framework of choice.
{% endhighlight %}

... на вопрос о выборе типа репозитория - выбираем - **Integrated Monorepo**:

{% highlight bash %}
? Package-based monorepo, integrated monorepo, or standalone project? …

Package-based Monorepo:     Nx makes it fast, but lets you run things your way.
Integrated Monorepo:        Nx creates a monorepo that contains multiple projects.
Standalone:                 Nx creates a single project and makes it fast.
{% endhighlight %}

... на предложение воспользоваться Nx Cloud отвечаем, что не хотим - **Skip for now**:

{% endhighlight bash %}
? Do you want Nx Cloud to make your CI fast? …

(it's free and can be disabled any time)
Yes, enable Nx Cloud
Yes, configure Nx Cloud for GitHub Actions
Yes, configure Nx Cloud for Circle CI
Skip for now
{% endhighlight %}

... процесс инициализации занимает некоторое время, после чего получаем готовый пустой workspace:

{% highlight bash %}
 NX   Creating your v19.2.3 workspace.

✔ Installing dependencies with npm
✔ Successfully created the workspace: awesome-project.
{% endhighlight %}

... переходим во вновь созданный проект:

{% highlight bash %}
cd awesome-project
{% endhighlight %}

... добавляем необходимые Nx-зависимости:

{% highlight bash %}
npm i -D @nx/angular @nx/nest @nx/js
{% endhighlight %}

... затем генерируем в workspace фронтенд на angular - [@nx/angular](https://nx.dev/nx-api/angular):

{% highlight bash %}
nx g @nx/angular:app frontend-part
{% endhighlight %}

... затем генерируем бекенд на nestjs - [@nx/nest](https://nx.dev/nx-api/nest):


{% highlight bash %}
nx g @nx/nest:app backend-part
{% endhighlight %}

... генерируем shared library [@nx/js:library](https://nx.dev/nx-api/js/generators/library):

{% highlight bash %}
nx g @nx/js:lib shared-lib
{% endhighlight %}

С этого момента у нас есть базовая настройка. Мы можете импортировать общую библиотеку следующим образом::

{% highlight typescript %}
import { sharedLib } from "@my-project/shared-lib";
{% endhighlight %}

Если в дальнейшем в проекте планируется использовать Prisma и PostgreSQL, то по дальнейшим шагам можно ознакомиться здесь - [Prisma - установка в Nest-проекте](https://gearmobile.github.io/prisma/prisma-connect/).

#### Дополнительные источники

В процессе общения по текущей теме в Discord (Nx-форум) c пользователем @rujorgensen последний любезно предложил свой вариант готового решения - [nx-workspace](https://github.com/rujorgensen/nx-workspace).

Можно сделать fork репозитория - и попробовать использовать его, как вариант.

#### Проверка первоначального решения

Как проверка работоспособности первоначального решения - привожу ссылку на учебный проект [Task Manager](https://github.com/My-Angular-Projects/task-manager).

На момент написания статьи - проект находится в стадии разработки.

---