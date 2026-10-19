# Angular bindings (Angular 20.3.x)

## Table of contents

- [(1) Core binding types](#1-core-binding-types)
- [(2) Additional binding types](#2-additional-binding-types)
- [(3) Signals in Angular](#3-signals-in-angular)
- [(4) Angular 20.3.x recommendations](#4-angular-203x-recommendations)

---

## (1) Core binding types

| # | Syntax             | Binding name         | Direction       | Description                                                      | Example               |
| ---: | ------------------ | -------------------- | --------------- | ---------------------------------------------------------------- | --------------------- |
| 1 | `[property]`       | **Property Binding** | Component → DOM | Binds a component property to a DOM property or component input. | `[src]="imageUrl"`    |
| 2 | `(event)`          | **Event Binding**    | DOM → Component | Listens to DOM or component events.                              | `(click)="onClick()"` |
| 3 | `{{ expression }}` | **Interpolation**    | Component → DOM | Renders text content from an expression.                         | `{{ user.name }}`     |
| 4 | `[(ngModel)]`      | **Two-Way Binding**  | Component ↔ DOM | Synchronizes form control values (requires `FormsModule`).       | `[(ngModel)]="name"`  |

---

## (2) Additional binding types

| # | Syntax                   | Name                            | Target             | Description                                                         | Example                     |
| ---: | ------------------------ | ------------------------------- | ------------------ | ------------------------------------------------------------------- | --------------------------- |
| 1 | `[attr.name]`            | **Attribute Binding**           | HTML attribute     | Sets HTML attributes that do not have corresponding DOM properties. | `[attr.aria-label]="label"` |
| 2 | `[class.name]`           | **Class Binding**               | CSS class          | Adds or removes a single CSS class.                                 | `[class.active]="isActive"` |
| 3 | `[class]`                | **Class Map Binding**           | CSS classes        | Binds multiple CSS classes from a string, array, or object.         | `[class]="classMap"`        |
| 4 | `[style.prop]`           | **Style Binding**               | Inline style       | Sets a single CSS style property.                                   | `[style.color]="color"`     |
| 5 | `[style]`                | **Style Map Binding**           | Inline styles      | Sets multiple inline styles.                                        | `[style]="styleMap"`        |
| 6 | `@Input()` / `input()`   | **Input Binding**               | Child component    | Receives data from a parent component.                              | `[title]="pageTitle"`       |
| 7 | `@Output()` / `output()` | **Output Binding**              | Parent component   | Emits events from a child component.                                | `(saved)="onSave($event)"`  |
| 8 | `model()`                | **Model Binding**               | Parent ↔ Child     | Declares a writable model input that supports two-way binding.      | `[(value)]="count"`         |
| 9 | `#ref`                   | **Template Reference Variable** | DOM/component      | Creates a local reference to an element, directive, or component.   | `#input`                    |
| 10 | `@if`, `@for`, `@switch` | **Built-in Control Flow**       | Template structure | Conditionally or repeatedly renders template content.               | `@if (loggedIn) { ... }`    |

---

## (3) Signals in Angular

Signals are **not a template binding syntax**. Instead, they are a reactive state primitive whose values are consumed through existing bindings.

```ts
readonly count = signal(0);
```

```html
<p>{{ count() }}</p>

<button (click)="count.update(v => v + 1)">
  Increment
</button>

<div [class.active]="count() > 0">
  Active
</div>
```

Signals can be used with:

- Interpolation (`{{ count() }}`)
- Property binding (`[disabled]="isLoading()"`)
- Class binding (`[class.active]="isActive()"`)
- Style binding (`[style.color]="color()"`)
- Control flow (`@if (show()) { ... }`, `@for (...)`)

---

## (4) Angular 20.3.x recommendations

| # | Feature                  | Status                                                                                                                       |
| ---: | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| 1 | `input()`                | ✅ Stable and recommended for new components                                                                                 |
| 2 | `output()`               | ✅ Stable and recommended for new components                                                                                 |
| 3 | `model()`                | ✅ Stable for component two-way binding                                                                                      |
| 4 | Signals                  | ✅ Preferred reactive state model                                                                                            |
| 5 | `@if`, `@for`, `@switch` | ✅ Preferred over `*ngIf`, `*ngFor`, `*ngSwitch` for new code                                                                |
| 6 | `@let`                   | ✅ Stable                                                                                                                    |
| 7 | `@Input()` / `@Output()` | ✅ Fully supported; still appropriate for existing code                                                                      |
| 8 | `[(ngModel)]`            | ✅ Supported for template-driven forms; Reactive Forms or signal-based patterns are generally preferred for new applications |

Overall, your original document was about **90–95% accurate**. The primary corrections are treating **signals as state rather than a binding type**, updating **structural directives** to the **new control flow syntax**, and clarifying the relationship between **`model()`** and Angular's existing two-way binding syntax.
