# 09 — Component output properties

Use `output()` to emit custom events **from** a child component **to** its parent.

```ts
// child.ts — child component
import { Component, output } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="addItem()">Add Item</button>`,
})
export class Child {
  addItemEvent = output<string>();     // declares an output of type string

  addItem() {
    this.addItemEvent.emit('🐢');      // emits a value up to the parent
  }
}
```

```ts
// app.ts — parent component
import { Component } from '@angular/core';
import { Child } from './child';

@Component({
  selector: 'app-root',
  template: `
    <!-- $event holds the emitted value -->
    <app-child (addItemEvent)="addItem($event)" />

    @for (item of items; track $index) {
      <p>{{ item }}</p>
    }
  `,
  imports: [Child],
})
export class App {
  items: string[] = [];

  addItem(value: string) {
    this.items.push(value);            // appends emitted turtle to the list
  }
}
```
