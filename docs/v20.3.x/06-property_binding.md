# 06 — Property binding

Wrap an attribute name in `[ ]` to bind it dynamically to a class property.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- src is set from the imageURL property -->
    <img alt="photo" [src]="imageURL" />

    <!-- contentEditable toggled by the isEditable property -->
    <div [contentEditable]="isEditable"></div>
  `,
})
export class App {
  imageURL   = '/assets/photo.jpg';
  isEditable = true;
}
```

> `[attr]="value"` sets a **DOM property**. For HTML attributes use `[attr.aria-label]="value"`.
