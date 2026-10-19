# 18 — Validating forms

Pass `Validators` to `FormControl` to enforce rules. Use `FormGroup.valid` to gate submission.

```ts
import { Component } from '@angular/core';
import { ReactiveFormsModule, FormControl, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-root',
  template: `
    <form [formGroup]="profileForm" (ngSubmit)="handleSubmit()">

      <label>Name
        <input type="text" formControlName="name" />
      </label>

      <label>Email
        <input type="email" formControlName="email" />
      </label>

      <!-- button disabled while form is invalid -->
      <button type="submit" [disabled]="!profileForm.valid">Submit</button>

    </form>
  `,
  imports: [ReactiveFormsModule],
})
export class App {
  profileForm = new FormGroup({
    name:  new FormControl('', Validators.required),               // single validator
    email: new FormControl('', [Validators.required,
                                Validators.email]),                // multiple validators
  });

  handleSubmit() {
    if (this.profileForm.valid) {
      alert(this.profileForm.value.name + ' | ' + this.profileForm.value.email);
    }
  }
}
```

---

## (1) Built-in validators

| # | Validator                   | Description                  |
| ---: | --------------------------- | ---------------------------- |
| 1 | `Validators.required`       | Field must not be empty      |
| 2 | `Validators.email`          | Must be a valid email format |
| 3 | `Validators.minLength(n)`   | Minimum character count      |
| 4 | `Validators.maxLength(n)`   | Maximum character count      |
| 5 | `Validators.pattern(regex)` | Must match a regex           |
| 6 | `Validators.min(n)`         | Minimum numeric value        |
| 7 | `Validators.max(n)`         | Maximum numeric value        |
