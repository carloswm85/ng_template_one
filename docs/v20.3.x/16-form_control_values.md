# 16 — Getting form control values

Read form input values in the template via interpolation, or programmatically via `this.property`.

```ts
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-user',
  template: `
    <!-- display value directly in template via interpolation -->
    <p>Framework: {{ favoriteFramework }}</p>

    <label for="framework">
      Favorite Framework:
      <input id="framework" type="text" [(ngModel)]="favoriteFramework" />
    </label>

    <!-- read value programmatically on button click -->
    <button (click)="showFramework()">Show Framework</button>
  `,
  imports: [FormsModule],
})
export class User {
  favoriteFramework = '';

  showFramework() {
    alert(this.favoriteFramework);   // access value via this.property
  }
}
```
