---
title: "Repository - TypeORM"
layout: post
categories: typeorm
tags: [repository, typeorm]
share: true
---

**Repository** в [TypeORM][2] - это отдельный специальный класс, менеджер для управления таблицами в базе данных.

Для каждой таблицы в БД - создается свой собственный repository для управления записями в этой таблице.

Каждый репозиторий имеет набор методов для чтения, создания, обновления, удаления и тп - записей в таблице.

В нем ещё могут быть дата мапперы, которые маппят данные, пришедшие из БД в тот вид, который требует сервис.

Здесь представлены все [свойства и методы][1] класса Repository.

***
[1]: http://typeorm.delightful.studio/classes/_repository_repository_.repository.html "Class Repository<Entity>"
[2]: https://typeorm.io/ "TypeORM"