# 15 — Forms overview (template-driven)

Template-driven forms use `FormsModule` and `ngModel` for two-way data binding directly in the template.

```ts
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-user',
  template: `
    <label for="framework">
      Favorite Framework:
      <!-- [(ngModel)] two-way binds input value to favoriteFramework -->
      <input id="framework" type="text" [(ngModel)]="favoriteFramework" />
    </label>

    <p>{{ favoriteFramework }}</p>    <!-- updates in real time as user types -->
  `,
  imports: [FormsModule],            // required for ngModel to work
})
export class User {
  favoriteFramework = '';
}
```

> `[()]` is the "banana in a box" syntax — combines property binding `[]` and event binding `()` for two-way data flow.
