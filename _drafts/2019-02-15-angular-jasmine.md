---
title: "Angular Jasmine"
layout: post
categories: angular
tags: [javascript, angular, jasmine, test]
share: true
---

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

`beforeEach()` - глобальная функция Jasmine, которая вызывается на исполнение перед каждой спецификацией `it` в блоке `describe` (beforeEach is called once before every `it` block in a test).
`TestBed` - класс из Jasmine, который создает модуль тестирования, аналогичный реальному модулю `@NgModule`. У класса `TestBed` есть метод `configureTestingModule`, с помощью которого можно настроить этот модуль. Другими словами, с помощью класса `TestBed` можно создать и настроить любую тестовую среду.

При написании тестов не редка ситуация, когда надо иметь фиксированное воспроизводимое много раз состояние программы. Например, такая-то кнопочка нажата, такой-то класс содержит такие-то значения.

Чтобы не приходилось каждый раз вручную создавать подобное состояние программы используются fixture (фикстуры). Фикстуры позволяют сохранить состояние системы в файл, а потом его от туда загрузить.

`async()` - функция jasmine, припомощи которой выполняются все асинхронные операции в тестах. Даже не так - эта функция обеспечивает поддержку всех необходимых при тестировании асинхронных операций; она отслеживает все асинхронные задачи в тестах.

`compileComponents()` - ?

`inject()` - ?

`spyOn()` - функция Jasmine, которая перехватывает все вызовы реального метода.


***
[1]: http://speckyboy.com/2015/01/26/six-common-freelancing-myths/ "Six Common Freelancing Myths"
