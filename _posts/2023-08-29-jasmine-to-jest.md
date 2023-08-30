---
title: "Jasmine vs Jest"
layout: post
categories: Test
tags: [jasmine, jest, test]
share: true
---

![Jest]({{site.url}}/images/uploads/2023/08/jest.webp)

### Соответствия matcher'ов в Jasmine и Jest

- and.callThrough() --> mockImplementation()
- and.callFake() --> mockImplementation()
- and.returnValue() --> mockReturnValue()
- and.spyOnProperty() --> spyOn()
- and.toHaveBeenCalledOnceWith() --> toHaveBeenCalledTimes(1)
- spyOn(...).and.callFake(() => {}) --> jest.spyOn(...).mockImplementation(() => {})
- jasmine.createSpy('name') --> jest.fn()
- toBeTrue --> toBe(true)
- toBeFalse --> toBe(false)

toHaveBeenCalled() - это алиас для toBeCalled()

### Jasmine createSpyObj в Jest

В Jasmine объект шпиона создается, используя функцию createSpyObj и передавая в него параметры имени класса и массива методов:

{% highlight typescript %}
const serviceMock = createSpyObj('service', ['method_1', 'method_2', 'method_3', 'method_4', 'method_5']);
{% endhighlight %}

В Jest просто создается объект с ожидаемыми свойствами, а функция jest.fn() создает методы-шпионы:

{% highlight typescript %}
const serviceMock = {
    method_1: jest.fn(),
    method_2: jest.fn(),
    method_3: jest.fn(),
    method_4: jest.fn(),
    method_5: jest.fn()
};
{% endhighlight %}

### Ссылки

- [https://ordina-jworks.github.io/testing/2018/08/03/testing-angular-with-jest.html](Testing Angular with Jest)
- [https://codewithhugo.com/run-skip-single-jest-test/](How to run, ignore or skip Jest tests, suites and files)
- [https://codewithhugo.com/jest-fn-spyon-stub-mock/](Jest .fn() and .spyOn() spy/stub/mock assertion reference)
- [https://jestjs.io/ru/docs/getting-started](Jest Documentation)
