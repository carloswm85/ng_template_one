# 20 — Inject-based dependency injection

Use the `inject()` function to retrieve a service instance inside a component class property initializer.

```ts
// app.ts
import { Component, inject } from '@angular/core';
import { CarService } from './car.service';

@Component({
  selector: 'app-root',
  template: `<p>Car Listing: {{ display }}</p>`,
})
export class App {
  // inject() retrieves the singleton CarService from the DI system
  carService = inject(CarService);

  // initialized using the injected service immediately
  display = this.carService.getCars().join(' ⭐️ ');
}
```

> `inject()` must be called during class construction (field initializer or constructor body) — not inside lifecycle hooks or event handlers.
