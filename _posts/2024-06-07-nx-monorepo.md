---
title: "NX = Angular + Nest.js"
layout: post
categories: Development
tags: [nx, monorepo, angular, nest.js, prisma, sql]
share: true
---

Install nx globally:

```bash
$ nx globally npm i -g nx
```

Initiate a new workspace: https://nx.dev/getting-started/installation. Let's name it something like my-project. Use this options:

- Which stack do you want to use? · none
- Package-based monorepo, integrated monorepo, or standalone project? · integrated
- Enable distributed caching to make your CI faster · No

```bash
$ cd my-project
```

```bash
$ npm i -D @nx/angular @nx/nest @nx/js
```

Generate Angular app [@nx/angular](https://nx.dev/nx-api/angular):

```bash
$ nx g @nx/angular:app angular-app
```

Generate NestJS app [@nx/nest](https://nx.dev/nx-api/nest):

```bash
$ nx g @nx/nest:app nest-app
```

Generate shared library [@nx/js:library](https://nx.dev/nx-api/js/generators/library):

```bash
$ nx g @nx/js:lib shared-lib
```

From this point you have a basic setup. You can import your code form shared library like this:

```typescript
import { sharedLib } from "@my-project/shared-lib";
```
