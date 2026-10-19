# 08 — Component input properties

Use `input()` to pass data **into** a child component from its parent (similar to `props` in other frameworks).

```ts
// user.ts — child component
import { Component, input } from '@angular/core';

@Component({
  selector: 'app-user',
  template: `
    <p>The user's occupation is {{ occupation() }}</p>  <!-- call signal with () -->
    <p>The user's name is {{ name() }}</p>
  `,
})
export class User {
  occupation = input<string>();   // InputSignal — value comes from parent
  name       = input<string>();
}
```

```ts
// app.ts — parent component
import { Component } from '@angular/core';
import { User } from './user';

@Component({
  selector: 'app-root',
  template: `
    <!-- pass values using attribute syntax -->
    <app-user occupation="Angular Developer" name="Simran" />
  `,
  imports: [User],
})
export class App {}
```

> `input()` returns an `InputSignal` — always invoke it with `()` inside the template.
