# Angular validators (Angular 20.3.x)

## Table of contents

- [(1) Built-in validators](#1-built-in-validators)
- [(2) Example](#2-example)
- [(3) Custom validators](#3-custom-validators)
- [(4) Simple custom validator](#4-simple-custom-validator)
- [(5) Validator with parameters](#5-validator-with-parameters)
- [(6) Cross-field validator (FormGroup)](#6-cross-field-validator-formgroup)
- [(7) Asynchronous validator](#7-asynchronous-validator)
- [(8) Validation errors](#8-validation-errors)
- [(9) Signals and forms](#9-signals-and-forms)
- [(10) Summary](#10-summary)

Angular Reactive Forms provide both **built-in validators** (via the `Validators` class) and **custom validators** that you can create yourself.

Validators can be:

- **Synchronous** (`ValidatorFn`)
- **Asynchronous** (`AsyncValidatorFn`)

---

## (1) Built-in validators

| # | Validator                        | Description                               | Applies to       |
| ---: | -------------------------------- | ----------------------------------------- | ---------------- |
| 1 | `Validators.required`            | Value must not be empty                   | Any control      |
| 2 | `Validators.requiredTrue`        | Value must be `true`                      | Checkbox, toggle |
| 3 | `Validators.email`               | Valid email address                       | Text             |
| 4 | `Validators.minLength(n)`        | Minimum number of characters              | String, array    |
| 5 | `Validators.maxLength(n)`        | Maximum number of characters              | String, array    |
| 6 | `Validators.pattern(regex)`      | Must match a regular expression           | String           |
| 7 | `Validators.min(n)`              | Minimum numeric value                     | Number           |
| 8 | `Validators.max(n)`              | Maximum numeric value                     | Number           |
| 9 | `Validators.nullValidator`       | Always returns `null` (always valid)      | Any control      |
| 10 | `Validators.compose([...])`      | Combines multiple synchronous validators  | Any control      |
| 11 | `Validators.composeAsync([...])` | Combines multiple asynchronous validators | Any control      |

> `compose()` and `composeAsync()` are utility methods for combining validators rather than validators that enforce validation rules themselves.

---

## (2) Example

```ts
import { FormControl, Validators } from '@angular/forms';

username = new FormControl<string>('', {
  nonNullable: true,
  validators: [
    Validators.required,
    Validators.minLength(3),
    Validators.maxLength(20),
    Validators.pattern(/^[a-zA-Z0-9_]+$/)
  ]
});
```

---

## (3) Custom validators

A custom validator is typically implemented as a `ValidatorFn`.

It receives an `AbstractControl` and returns either:

- `null` → valid ✅
- a `ValidationErrors` object → invalid ❌

---

## (4) Simple custom validator

```ts
import {
  AbstractControl,
  ValidationErrors,
  ValidatorFn
} from '@angular/forms';

export const noSpacesValidator: ValidatorFn =
  (control: AbstractControl): ValidationErrors | null => {

    return control.value?.includes(' ')
      ? { noSpaces: true }
      : null;
  };
```

Usage:

```ts
username = new FormControl<string>('', {
  nonNullable: true,
  validators: [
    Validators.required,
    noSpacesValidator
  ]
});
```

---

## (5) Validator with parameters

A validator can also be implemented as a factory function.

Example: forbid a specific word.

```ts
import {
  AbstractControl,
  ValidationErrors,
  ValidatorFn
} from '@angular/forms';

export function forbiddenWord(word: string): ValidatorFn {

  return (control: AbstractControl): ValidationErrors | null => {

    return control.value?.includes(word)
      ? { forbiddenWord: word }
      : null;
  };
}
```

Usage:

```ts
title = new FormControl<string>('', {
  nonNullable: true,
  validators: [
    forbiddenWord('admin')
  ]
});
```

---

## (6) Cross-field validator (FormGroup)

Sometimes validation depends on multiple controls.

Example: password confirmation.

```ts
import {
  FormGroup,
  ValidationErrors,
  ValidatorFn
} from '@angular/forms';

export const passwordMatchValidator: ValidatorFn =
  (group): ValidationErrors | null => {

    const password = group.get('password')?.value;
    const confirm = group.get('confirmPassword')?.value;

    return password === confirm
      ? null
      : { passwordMismatch: true };
  };
```

Usage:

```ts
form = new FormGroup(
  {
    password: new FormControl(''),
    confirmPassword: new FormControl('')
  },
  {
    validators: passwordMatchValidator
  }
);
```

---

## (7) Asynchronous validator

Asynchronous validators are useful when validation requires a server request.

```ts
import {
  AbstractControl,
  AsyncValidatorFn,
  ValidationErrors
} from '@angular/forms';

import { delay, map, of } from 'rxjs';

export function usernameTakenValidator(): AsyncValidatorFn {

  return (control: AbstractControl) => {

    return of(['admin', 'root']).pipe(
      delay(500),
      map(users =>
        users.includes(control.value)
          ? { usernameTaken: true }
          : null
      )
    );
  };
}
```

Usage:

```ts
username = new FormControl<string>('', {
  nonNullable: true,
  validators: [
    Validators.required
  ],
  asyncValidators: [
    usernameTakenValidator()
  ]
});
```

---

## (8) Validation errors

Every validator returns an error object with a key you can inspect.

| # | Validator       | Error object                                                  |
| ---: | --------------- | ------------------------------------------------------------- |
| 1 | `required`      | `{ required: true }`                                          |
| 2 | `requiredTrue`  | `{ required: true }`                                          |
| 3 | `email`         | `{ email: true }`                                             |
| 4 | `minLength(3)`  | `{ minlength: { requiredLength: 3, actualLength: 2 } }`       |
| 5 | `maxLength(10)` | `{ maxlength: { requiredLength: 10, actualLength: 15 } }`     |
| 6 | `min(18)`       | `{ min: { min: 18, actual: 15 } }`                            |
| 7 | `max(100)`      | `{ max: { max: 100, actual: 150 } }`                          |
| 8 | `pattern(...)`  | `{ pattern: { requiredPattern: "...", actualValue: "..." } }` |
| 9 | Custom          | Whatever object you return, e.g. `{ passwordMismatch: true }` |

You can access these through the control:

```ts
const errors = control.errors;

if (errors?.['required']) {
  // Required validation failed
}

if (errors?.['passwordMismatch']) {
  // Custom validator failed
}
```

---

## (9) Signals and forms

Angular Signals do not replace the Reactive Forms validation API.

Validators work exactly the same regardless of whether the component uses:

- Signals
- Standard class properties
- RxJS

Signals can be used to consume form state (for example, using `toSignal()`), but validators continue to use the Reactive Forms API.

---

## (10) Summary

| # | Validator type                              | Built into Angular | Reusable | Can access other controls | Async |
| ---: | ------------------------------------------- | ------------------ | -------- | ------------------------- | ----- |
| 1 | Built-in validators                         | ✅                 | ✅       | ❌                        | ❌    |
| 2 | Custom validator (`ValidatorFn`)            | ❌                 | ✅       | ❌                        | ❌    |
| 3 | Custom async validator (`AsyncValidatorFn`) | ❌                 | ✅       | ❌                        | ✅    |
| 4 | Custom `FormGroup` validator                | ❌                 | ✅       | ✅                        | ❌    |
| 5 | Custom async `FormGroup` validator          | ❌                 | ✅       | ✅                        | ✅    |

In practice, applications typically use the built-in validators for common field constraints (required, length, pattern, and numeric ranges), while custom validators implement business-specific rules such as password confirmation, unique usernames, valid date ranges, or domain-specific validation logic.
