# 21 — Constructor-based dependency injection

An alternative to `inject()` is declaring dependencies as **constructor parameters**. Angular resolves and injects them automatically based on their type.

```ts
// car.service.ts
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class CarService {
  private cars = ['Sunflower GT', 'Flexus Sport', 'Wraptor X'];

  getCars(): string[] { return this.cars; }
}
```

```ts
// logger.service.ts
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class LoggerService {
  log(msg: string) { console.log(`[LOG]: ${msg}`); }
}
```

```ts
// app.ts
import { Component } from '@angular/core';
import { CarService } from './car.service';
import { LoggerService } from './logger.service';

@Component({
  selector: 'app-root',
  template: `<p>Car Listing: {{ display }}</p>`,
})
export class App {
  display: string;

  // Angular reads the parameter types and injects matching instances
  constructor(
    private carService: CarService,
    private loggerService: LoggerService,
  ) {
    this.display = this.carService.getCars().join(' ⭐️ ');
    this.loggerService.log('App initialized');
  }
}
```

---

## (1) Constructor DI vs `inject()` — when to use each

| # |                 | `inject()`                            | Constructor DI                    |
| ---: | --------------- | ------------------------------------- | --------------------------------- |
| 1 | Style           | Functional / modern                   | Class-based / traditional         |
| 2 | Works in        | Field initializers, factories, guards | Constructor body only             |
| 3 | Recommended for | Standalone components (Angular 14+)   | Libraries, pre-existing codebases |
| 4 | Testability     | Easy to mock                          | Easy to mock                      |

> Both approaches are fully supported in Angular 20. Prefer `inject()` for new standalone-component code.
