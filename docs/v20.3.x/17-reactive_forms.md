# 17 — Reactive forms

- Reactive forms manage form state in the component class using `FormGroup` and `FormControl`.
- Logic stays in TypeScript, not the template.

```ts
import { Component } from '@angular/core';
import { ReactiveFormsModule, FormControl, FormGroup } from '@angular/forms';

@Component({
  selector: 'app-root',
  template: `
    <!-- [formGroup] binds the <form> to the FormGroup instance -->
    <form [formGroup]="profileForm" (ngSubmit)="handleSubmit()">

      <!-- formControlName binds each input to a named FormControl -->
      <label>Name
        <input type="text" formControlName="name" />
      </label>
      <label>Email
        <input type="email" formControlName="email" />
      </label>
      <button type="submit">Submit</button>
    </form>

    <!-- read values from the FormGroup directly -->
    <p>Name: {{ profileForm.value.name }}</p>
    <p>Email: {{ profileForm.value.email }}</p>
  `,
  imports: [ReactiveFormsModule],
})
export class App {
  profileForm = new FormGroup({
    name:  new FormControl(''),    // initial value is empty string
    email: new FormControl(''),
  });

  handleSubmit() {
    // access all values at once via .value
    alert(this.profileForm.value.name + ' | ' + this.profileForm.value.email);
  }
}
```
