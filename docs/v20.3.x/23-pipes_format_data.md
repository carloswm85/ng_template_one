# 23 — Formatting data with pipes

Pass parameters to pipes using `:` after the pipe name.

```ts
import { Component } from '@angular/core';
import { DecimalPipe, DatePipe, CurrencyPipe } from '@angular/common';

@Component({
  selector: 'app-root',
  template: `
    <!-- DecimalPipe: format is {minInt}.{minFrac}-{maxFrac} -->
    <li>Number:   {{ num      | number:'3.2-2' }}</li>     <!-- 100.55 -->

    <!-- DatePipe: named formats or custom patterns -->
    <li>Date:     {{ birthday | date:'medium' }}</li>      <!-- Jun 15, 2015, 9:43:11 PM -->

    <!-- CurrencyPipe: defaults to USD $ -->
    <li>Currency: {{ cost     | currency }}</li>           <!-- $9.99 -->
  `,
  imports: [DecimalPipe, DatePipe, CurrencyPipe],
})
export class App {
  num      = 100.5468;
  birthday = new Date(2015, 5, 15, 21, 43, 11);
  cost     = 9.99;
}
```
