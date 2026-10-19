# 19 — Creating an injectable service

- Services encapsulate shared logic and data.
- Mark them with `@Injectable` so Angular's DI system can provide them.

```ts
// car.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',   // singleton — one instance shared across the whole app
})
export class CarService {
  private cars = ['Sunflower GT', 'Flexus Sport', 'Wraptor X'];

  getCars(): string[] {
    return this.cars;             // returns full list
  }

  getCar(id: number): string {
    return this.cars[id];         // returns a single car by index
  }
}
```

> `providedIn: 'root'` makes the service available application-wide without adding it to any `providers` array.
