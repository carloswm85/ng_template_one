# 03 — Composing components

Use a component's `selector` as an HTML tag inside another component's template. Add it to `imports` to make it available.

```ts
// user.ts — child component
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',              // becomes <app-user /> in parent templates
  template: `<p>Username: youngTech</p>`,
})
export class User {}
```

```ts
// app.ts — parent component
import { Component } from '@angular/core';
import { User } from './user';

@Component({
  selector: 'app-root',
  template: `
    <section>
      <app-user />                   <!-- component rendered here -->
    </section>
  `,
  imports: [User],                   // must be listed in imports to use in template
})
export class App {}
```
