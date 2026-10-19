# 02 — Updating the component class

Component logic lives in the TypeScript class. Use **interpolation** `{{ }}` to render class properties in the template.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    Hello {{ city }}         <!-- renders the value of the city property -->
    {{ 1 + 1 }}              <!-- expressions are evaluated -->
  `,
})
export class App {
  city = 'San Francisco';    // TypeScript infers string type automatically
}
```

> Interpolation evaluates any valid expression: math, ternary operators, method calls, etc.
