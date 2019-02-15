---
title: "Angular Jasmine"
layout: post
categories: angular
tags: [javascript, angular, jasmine, test]
share: true
---

## uniq()

Создает копию оригинального массива, состоящую только из уникальных элементов этого массива.


`TestBed` и `ComponentFixtures` - классы.
`async`, `fakeAsync`, `inject` - впсомогательные функции.
Все эти штуки являются частью пакета `@angular/core/testing` и служат интсрументами для написания тестов в Angular.

Тесты в Jasmine называются **спецификациями**, поэтому такие файлы имеют расширение `.spec.ts`. Важное условие - Karma по умолчанию автоматически ищет все файлы спецификации рекурсивно внутри директории `src/app`, поэтому все тестовые файлы должны располагаться в этой директории, чтобы быть протестированными.

`describe` - глобальная функция Jasmine.

Пример теста:

~~~ javascript
import { Pastebin } from './pastebin';

describe('Pastebin', () => {
    it('should create an instance of Pastebin',() => {
        expect(new Pastebin()).toBeTruthy();
    });
})
~~~

Что здесь происходит? Строкой `import { Pastebin } from './pastebin'` импортируется реальный, существующий класс `Pastebin`, который будет тестироваться. Создается глобальная функция `describe` с названием набора тестов и функцией - фактической реализацией данного теста, внутри которой создается функция `it` (спецификация) с описанием того, что будет тестироваться - будем проверять, что класс `Pastebin` может создавать свой экземпляр. Для этого испльзуем assertion-библиотеку Jasmine и его метод - `expect`:

~~~ javascript
expect(new Pastebin()).toBeTruthy()
~~~

мы ожидаем (expect), что вызов `new Pastebin()` создаст экземпляр класса `Pastebin` и вспомогательная функция `toBeTruthy()` подтвердит, что это правда.

Функция `toBeTruthy()` - вспомогательная функция. Другими примерами являются `toBedefined()`, `toBe()`, `toContaian()`.

~~~ js
it('should accept values', () => {
  let pastebin = new Pastebin();
  pastebin = {
    id: 123,
    title: 'Hello Jasmine',
    language: 'javascript',
    paste: 'print message'
  }
  expect(pastebin.id).toEqual(123);
  expect(pastebin.title).toEqual('Hello Jasmine');
  expect(pastebin.language).toEqual('javascript');
  expect(pastebin.paste).toEqual('print message');
})
~~~

`beforeEach()` - глобальная функция, которая вызывается на исполнение перед каждой спецификацией `it` в блоке `describe`.


***
[1]: http://speckyboy.com/2015/01/26/six-common-freelancing-myths/ "Six Common Freelancing Myths"
