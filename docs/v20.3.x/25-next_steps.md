# 25 — Next steps

## Table of contents

- [(1) Signals](#1-signals)
- [(2) HTTP client](#2-http-client)
- [(3) Lazy-loaded routes](#3-lazy-loaded-routes)
- [(4) Further reading](#4-further-reading)

You've completed the Angular fundamentals. Here's what to explore next.

---

## (1) Signals

```ts
import { Component, signal, computed, effect } from '@angular/core';

@Component({ template: `<p>{{ doubled() }}</p> })
export class App {
  count   = signal(0);                        // writable reactive signal
  doubled = computed(() => this.count() * 2); // auto-updates when count changes

  constructor() {
    effect(() => console.log('count:', this.count())); // reactive side-effect
  }

  increment() {
    this.count.update(c => c + 1);            // update based on previous value
  }
}
```

---

## (2) HTTP client

```ts
// app.config.ts
import { provideHttpClient } from '@angular/common/http';
export const appConfig = { providers: [provideHttpClient()] };
```

```ts
// data.service.ts
import { inject, Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({ providedIn: 'root' })
export class DataService {
  private http = inject(HttpClient);

  getItems() {
    return this.http.get<Item[]>('/api/items');   // returns an Observable
  }
}
```

---

## (3) Lazy-loaded routes

```ts
// app.routes.ts
export const routes: Routes = [
  {
    path: 'dashboard',
    // component bundle only downloaded when user navigates to /dashboard
    loadComponent: () =>
      import('./dashboard/dashboard').then(m => m.Dashboard),
  },
];
```

---

## (4) Further reading

| # | Topic         | Link                                          |
| ---: | ------------- | --------------------------------------------- |
| 1 | Signals       | <https://angular.dev/guide/signals>           |
| 2 | HTTP Client   | <https://angular.dev/guide/http>              |
| 3 | Routing       | <https://angular.dev/guide/routing>           |
| 4 | Testing       | <https://angular.dev/guide/testing>           |
| 5 | Angular CLI   | <https://angular.dev/tools/cli>               |
| 6 | Full Tutorial | <https://angular.dev/tutorials/learn-angular> |
