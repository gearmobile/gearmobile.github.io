---
title: "Angular - именованные outlets"
layout: post
categories: angular
tags: [angular, outlet, routing]
share: true
---

Для меня немного запутанная картина с именованными областями отображения и главное - с правильной настройкой. Нужно немного прояснить для себя.

Первое - настройка маршрутов. В ключе _outlet_ указываем **имя** дополнительной области _outlet_ - _aux_:

{% highlight typescript %}
const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: 'home', component: FirstComponent },
  { path: 'chat', component: ChatComponent, outlet: 'aux' },
];
{% endhighlight %}

В шаблоне обозначаем разметку для дополнительной области отображения и указываем ее **имя** через атрибут _name_ - какое указали и в маршрутах:

{% highlight typescript %}
<div style="display: flex">
  <router-outlet></router-outlet>
  <router-outlet name="aux"></router-outlet>
</div>
{% endhighlight %}

В навигации в директиве _routerLink_ - добавляем конфигурационный объект с ключом _outlets_. Значение этого ключа - объект с ключами _primary_ и _aux_; эти ключи - имена областей отрисовки _outlets_;

имя _primary_ - это имя по умолчанию; имя _aux_ - это то имя дополнительной области отображения, которое указали в маршруте.

Самое неочевидное - это значения этих ключей. Значения - это path, указанный в настройках маршрута - _path: 'home'_, _path: 'chat'_.

{% highlight typescript %}
<nav>
  <a [routerLink]="['/']">first</a>
  <a [routerLink]="['/second']">second</a>
  <a [routerLink]="[{ outlets: { primary: 'home', aux: 'chat' } }]">open chat</a>
  <a [routerLink]="[{ outlets: { aux: null } }]">close chat</a>
</nav>
{% endhighlight %}

---
