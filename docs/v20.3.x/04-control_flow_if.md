# 04 — Control flow: `@if`

Use `@if` / `@else` to conditionally render elements directly in the template.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    @if (isLoggedIn) {
      <p>Welcome back, Friend!</p>       <!-- shown when true -->
    }

    @if (isServerRunning) {
      <p>Yes, the server is running</p>  <!-- shown when true -->
    } @else {
      <p>No, the server is not running</p> <!-- shown when false -->
    }
  `,
})
export class App {
  isLoggedIn = true;
  isServerRunning = true;
}
```
