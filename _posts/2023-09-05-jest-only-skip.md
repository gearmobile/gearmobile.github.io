---
title: "Jest - использование only"
layout: post
categories: Jest
tags: [jest, test]
share: true
---

В Karma\Jasmine есть варианы для запуска выборочных тестов - `fit`, `fdescribe`. В этом посте - разберусь, какие есть варианты для этого - в Jest.

## Использование .only для запуска только одного теста

В данном случае - запустится только один тест - первый:

{% highlight typescript %}
describe('my suite', () => {
  test.only('my only true test', () => {
    expect(1 + 1).toEqual(2);
  });
  // этот тест --> не запустится
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

В Jest для `test.only` есть алиас по аналогии с Jasmine - `fit`; то есть по идее - можно написать так:

{% highlight typescript %}
describe('my suite', () => {
  fit('my only true test', () => {
    expect(1 + 1).toEqual(2);
  });
  // этот тест --> не запустится
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

Ссылка из официальной документации - [Test.Only][2]

## Использование .only для запуска нескольких тестов

В данном случае - запустится несколько тестов - первый и второй; третий - будет пропущен:

{% highlight typescript %}
describe('my suite', () => {
  test.only('one of my .only test', () => {
    expect(1 + 1).toEqual(2);
  });
  test.only('other of my .only test', () => {
    expect(1 + 2).toEqual(3);
  });
  // этот тест --> не запустится
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

В Jest для `test.only` есть алиас по аналогии с Jasmine - `fit`; то есть по идее - можно написать так:

{% highlight typescript %}
describe('my suite', () => {
  fit('one of my .only test', () => {
    expect(1 + 1).toEqual(2);
  });
  fit('other of my .only test', () => {
    expect(1 + 2).toEqual(3);
  });
  // этот тест --> не запустится
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

Ссылка из официальной документации - [Test.Only][2]

## Использование .only для запуска набора тестов

Для выбора набора тестов для запуска - также можно использовать `.only`. В данном случае - запустятся тесты только из первого набора ('first suite'), для которого установлено `describe.only`; второй набор тестов ('second suite') - будет пропущен:

{% highlight typescript %}
describe.only('first suite', () => {
  test('one of my .only test', () => {
    expect(1 + 1).toEqual(2);
  });
});
// эти тесты --> не запустятся
describe('second suite', () => {
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

У `.only` есть - алиас `fdescribe`; то есть, в Jest можно (по идее) написать по аналогии с Jasmine:

{% highlight typescript %}
fdescribe('first suite', () => {
  test('one of my .only test', () => {
    expect(1 + 1).toEqual(2);
  });
});
// эти тесты --> не запустятся
describe('second suite', () => {
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

Ссылка из официальной документации - [Describe.Only][1]

## Использование .only для запуска нескольких наборов тестов

Аналогично предыдущему вварианту, можно указать `.only` для запуска нескольких наборов тестов; в данном случае - будут запущены только два первых набора тестов:

{% highlight typescript %}
describe.only('my suite', () => {
  test('one of my .only test', () => {
    expect(1 + 1).toEqual(2);
  });
});
describe.only('other suite', () => {
  test('other of my .only test', () => {
    expect(1 + 2).toEqual(3);
  });
});
// эти тесты --> не запустятся
describe('skipped other suite', () => {
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

У `.only` есть - алиас `fdescribe`; то есть, в Jest можно (по идее) написать по аналогии с Jasmine:

{% highlight typescript %}
fdescribe('my suite', () => {
  test('one of my .only test', () => {
    expect(1 + 1).toEqual(2);
  });
});
fdescribe('other suite', () => {
  test('other of my .only test', () => {
    expect(1 + 2).toEqual(3);
  });
});
// эти тесты --> не запустятся
describe('skipped other suite', () => {
  test('my only true test', () => {
    expect(1 + 1).toEqual(1);
  });
});
{% endhighlight %}

Ссылка из официальной документации - [Describe.Only][1]

***
[1]: https://jestjs.io/ru/docs/api#describeonlyname-fn "Describe.Only"
[2]: https://jestjs.io/ru/docs/api#testonlyname-fn-timeout "Test.Only"