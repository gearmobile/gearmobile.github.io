---
title: "Prisma - подключить в Nest-проекте"
layout: post
categories: Prisma
tags: [prisma, postgres, nest]
share: true
---

## Prisma - установка в Nest-проекте

Установка [Prisma][1] выполняется очень просто - при помощи двух команд. Первая - устанавливает клиентскую часть Prisma:

{% highlight bash %}
$ npm i @prisma/client
{% endhighlight %}

... вторая команда - устанавливает cli-часть Prisma:

{% highlight bash %}
$ npm i -D prisma
{% endhighlight %}

После этого - нужно запустить команду для инициализации Prisma в текущем проекте:

{% highlight bash %}
$ npx prisma init
{% endhighlight %}

В результате в корне проекта будет создана папка **prisma**, внутри которой будет находиться файл **schema.prisma** для настройки подключения Prisma к базе данных (и не только это).

Содержимое файла очень простое:

{% highlight typescript %}
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
{% endhighlight %}

Наиболее существенные здесь две вещи - это драйвер **postgresql** для подключения к базе данных Postgres (по умолчанию используется подключение именно к Postgres). Если база данных другая - MySQL и тп - то меняем на нужный драйвер.

Вторая - это строка **url**, которая используется как настроечный файл для подключения к базе данных. Эта строка (в виде переменной DATABASE_URL) хранится в файле **.env**, который также автоматически создается Prisma при инициализации.

Если посмотреть на содержимое файла **.env**, то он будет таким:

{% highlight typescript %}
# Environment variables declared in this file are automatically made available to Prisma.
# See the documentation for more detail: https://pris.ly/d/prisma-schema#accessing-environment-variables-from-the-schema

# Prisma supports the native connection string format for PostgreSQL, MySQL, SQLite, SQL Server, MongoDB (Preview) and CockroachDB (Preview).
# See the documentation for all the connection string options: https://pris.ly/d/connection-strings

DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"
{% endhighlight %}

То есть - в одной строке - выполняется полная настройка подключения к существующей базе данных. В моем учебном случае это выглядит таким образом:

{% highlight typescript %}
DATABASE_URL="postgresql://postgres:123@localhost:5432/udemy_medium_clone?schema=public"
{% endhighlight %}

То есть - **postgres** - имя пользователя базы данных; **123** - пароль пользователя базы данных; **udemy_medium_clone** - имя базы данных.

Откуда я взял\узнал эти данные? Просто я заранее создал учебную базу данных в Postgres, у себя локально (в моем случае):

{% highlight bash %}
postgres=# CREATE DATABASE udemy_medium_clone;
CREATE DATABASE
postgres=# \c udemy_medium_clone 
You are now connected to database "udemy_medium_clone" as user "postgres".
udemy_medium_clone=# \conninfo
You are connected to database "udemy_medium_clone" as user "postgres" via socket in "/var/run/postgresql" at port "5432".
{% endhighlight %}

**localhost:5432** - я оставил по умолчанию, так как - у меня Postgres также по умолчанию слушает этот порт.

Не забываем добавить файл **.env** в **.gitignore**, чтобы данные не засветились на удаленном репозитории - и все, основная настройка Prisma завершена.

## Prisma - миграция баз данных

В моем случае - база данных **udemy_medium_clone** - чистая, в ней пока нет никаких таблиц. Это можно исправить двумя способами.

Первый - создать таблицу в базе данных силами самого SQL и затем выполнить преобразование таблицы в модель данных (Prisma schema) в проекте - командой:

{% highlight bash %}
prisma db pull
{% endhighlight %}

Второй - наоборот, создать модель данных Prisma в проекте и затем мигрировать ее в Postgres, что автоматически приведет к созданию такой таблицы в базе данных.

Давайте поступим по второму варианту. Создадим в файле **schema.prisma** модель данных пользователя будущего приложения:

{% highlight typescript %}
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Users {
  id       Int     @id @default(autoincrement())
  email    String  @unique @db.VarChar(255)
  bio      String?
  image    String? @db.VarChar(500)
  password String  @unique @db.VarChar(255)
  username String  @unique @db.VarChar(255)

  @@map("users")
}
{% endhighlight %}

(кстати - под [VSC][3] и [WS][4] - есть специальные плагины для подсветки синтаксиса и форматирования файлов с расширением *.prisma; для VSC плагин работает отлично, для WS - так себе).

И все - можно выполнить миграцию в базу данных командой:

{% highlight bash %}
npx prisma migrate dev --name users
{% endhighlight %}

... где **--name users** - это имя конкретной миграции, чтобы можно было локально увидеть и отследить эту операцию. По выполнении Prisma выведет в консоль отчет об успешной операции:

{% highlight bash %}
Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma
Datasource "db": PostgreSQL database "udemy_medium_clone", schema "public" at "localhost:5432"

Applying migration `20220223160632_users`

The following migration(s) have been created and applied from new schema changes:

migrations/
  └─ 20220223160632_users/
    └─ migration.sql

Your database is now in sync with your schema.

✔ Generated Prisma Client (3.10.0 | library) to ./node_modules/@prisma/client in 75ms
{% endhighlight %}

Как видно из отчета, Prisma создала подпапку **migrations**, внутри которой будут находиться - папки с детальной информацией по каждой конкретной миграции.

В моем случае - это будет папка **20220223160632_users** (помним о ключе --name users) и внутри этой папки - любопытный файлик **migration.sql**. Если открыть этот файлик, то увидим не что иное, как набор обычных sql-команд по созданию таблицы базы данных:

{% highlight sql %}
-- CreateTable
CREATE TABLE "users" (
    "id" SERIAL NOT NULL,
    "email" VARCHAR(255) NOT NULL,
    "bio" TEXT,
    "image" VARCHAR(500),
    "password" VARCHAR(255) NOT NULL,
    "username" VARCHAR(255) NOT NULL,

    CONSTRAINT "users_pkey" PRIMARY KEY ("id")
);

-- CreateIndex
CREATE UNIQUE INDEX "users_email_key" ON "users"("email");

-- CreateIndex
CREATE UNIQUE INDEX "users_password_key" ON "users"("password");

-- CreateIndex
CREATE UNIQUE INDEX "users_username_key" ON "users"("username");
{% endhighlight %}

То есть, по факту - сперва была выполнена операция по преобразованию Prisma-модели в такой sql-запрос, а уже потом - этот запрос выполнился и была создана таблица в базе данных.

А давайте проверим, так ли это на самом деле? Легко!

{% highlight bash %}
udemy_medium_clone=# \d
                 List of relations
 Schema |        Name        |   Type   |  Owner   
--------+--------------------+----------+----------
 public | _prisma_migrations | table    | postgres
 public | users              | table    | postgres
 public | users_id_seq       | sequence | postgres
(3 rows)
{% endhighlight %}

... правда - таблица users была создана. А давайте посмотрим - что из себя представляет эта таблица users:

{% highlight bash %}
udemy_medium_clone=# \d users
                                     Table "public.users"
  Column  |          Type          | Collation | Nullable |              Default              
----------+------------------------+-----------+----------+-----------------------------------
 id       | integer                |           | not null | nextval('users_id_seq'::regclass)
 email    | character varying(255) |           | not null | 
 bio      | text                   |           |          | 
 image    | character varying(500) |           |          | 
 password | character varying(255) |           | not null | 
 username | character varying(255) |           | not null | 
Indexes:
    "users_pkey" PRIMARY KEY, btree (id)
    "users_email_key" UNIQUE, btree (email)
    "users_password_key" UNIQUE, btree (password)
    "users_username_key" UNIQUE, btree (username)
{% endhighlight %}

... хм, очень похоже на правду - это именно такая таблица, какую я спроектировал в качестве модели в Prisma.

## Заключение

Ну вот в принципе и все - Prisma установлена в проекте, успешно настроено ее подключение к конкретной базе данных; создана модель данных и выполнена успешная миграция ее в таблицу в базе данных. Prisma успешно подключена и готова к работе.

Конечно же, есть еще один инструмент для работы с базой данных в Next - это [TypeORM][2]. Но его настройка и подключение для меня настолько сложна, запутанна и трудоемка, что я не стыжусь признаться, что TypeORM я не знаю и особого желания знать пока не возникло.

***
[1]: https://www.prisma.io/ "Next-generation Node.js and TypeScript ORM"
[2]: https://typeorm.io/#/
[3]: https://marketplace.visualstudio.com/items?itemName=Prisma.prisma "Prisma VS Code Extension"
[4]: https://plugins.jetbrains.com/plugin/14240-prisma "Prisma"
