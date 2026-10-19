# 07 — Event handling

Wrap an event name in `( )` to bind it to a class method.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- (click) runs greet() on button click -->
    <button (click)="greet()">Say Hello</button>

    <!-- (mouseover) runs showSecretMessage() on hover -->
    <section (mouseover)="showSecretMessage()">
      {{ message }}
    </section>
  `,
})
export class App {
  message = '';

  greet() {
    console.log('Hello, there 👋');
  }

  showSecretMessage() {
    this.message = 'Way to go 🚀';    // updates the template on hover
  }
}
```

> Any native DOM event works: `(click)`, `(change)`, `(input)`, `(submit)`, `(keyup)`, `(mouseover)`, etc.
