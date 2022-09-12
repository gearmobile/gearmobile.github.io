---
title: "ESLint: TypeError: this.libOptions.parse is not a function"
layout: post
categories: Code
tags: [bug, eslint]
share: true
---

В новом учебном проекте под Nestjs столкнутся с такой ошибкой в WebStorm - **ESLint: TypeError: this.libOptions.parse is not a function**.

Ошибка связана с Eslint - точнее, в багом в версии 8.23.0 этого пакета. Команда Eslint вроде как работает над ее исправлением и есть надежда, что в скором времени она пропадет. Здесь и сейчас - баг лечится путем отката пакета eslint на версию 8.22.0.

### Шаги выполнения:

- удалить папку node_modules
- почистить кэш npm - npm cache clean --force
- удалить файл package-json.lock
- установить в package.json версию для пакета eslint - "eslint": "8.22.0",
- заново установить все зависимости проекта - npm install