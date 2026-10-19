# 05 — Control flow: `@for`

Use `@for` to repeat elements over an iterable. `track` is **required** and must uniquely identify each item.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    @for (user of users; track user.id) {
      <p>{{ user.name }}</p>             <!-- rendered once per user -->
    }
  `,
})
export class App {
  users = [
    { id: 0, name: 'Sarah' },
    { id: 1, name: 'Amy' },
    { id: 2, name: 'Rachel' },
    { id: 3, name: 'Jessica' },
    { id: 4, name: 'Poornima' },
  ];
}
```

> `@for` also exposes context variables: `$index`, `$first`, `$last`, `$even`, `$odd`.

```html
<!-- Angular @for context variables example -->

<ul>
  @for (user of users; track user.id; let i = $index) {

    <!-- $index -->
    <li>
      {{ i }}. {{ user.name }}
    </li>

    <!-- $first -->
    @if ($first) {
      <li><strong>👋 First user: {{ user.name }}</strong></li>
    }

    <!-- $last -->
    @if ($last) {
      <li><strong>🏁 Last user: {{ user.name }}</strong></li>
    }

    <!-- $even -->
    @if ($even) {
      <li>Even row: {{ user.name }}</li>
    }

    <!-- $odd -->
    @if ($odd) {
      <li>Odd row: {{ user.name }}</li>
    }

  }
</ul>
```

The rendered HTML (approximately) would look like:

```text
0. Alice
👋 First user: Alice
Even row: Alice

1. Bob
Odd row: Bob

2. Charlie
Even row: Charlie

3. David
🏁 Last user: David
Odd row: David
```
