---
title: "Парсинг interceptor response"
layout: post
categories: Development
tags: [angular, interceptor]
share: true
---

Пример парсинга responsa'а в интерсепторе Angular:

{% highlight typescript %}
intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    return next.handle(this.setHeader(request)).pipe(
        map((response: HttpEvent<unknown>) => {
            if (request.url === '/api/v1/sdi/page' && response instanceof HttpResponse) {
                const body = JSON.parse(JSON.stringify(response.body));
                body.layout.blocks[0].components[2].columns[2].type = 'phone';
                body.layout.blocks[0].components[2].filter.static[3].type = 'phone';
                response = response.clone({ body });
                console.log('response >>>', response);
        }
        return response;
    }));
}
{% endhighlight %}