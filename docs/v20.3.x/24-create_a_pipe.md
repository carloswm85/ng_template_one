# 24 — Create a custom pipe

Implement `PipeTransform` and decorate with `@Pipe` to build a reusable data transformation.

```ts
// reverse.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'reverse',              // name used in templates with | operator
})
export class ReversePipe implements PipeTransform {
  transform(value: string): string {
    let reversed = '';
    for (let i = value.length - 1; i >= 0; i--) {
      reversed += value[i];     // build string character by character in reverse
    }
    return reversed;
  }
}
```

```ts
// app.ts
import { Component } from '@angular/core';
import { ReversePipe } from './reverse.pipe';

@Component({
  selector: 'app-root',
  template: `
    <!-- pipe name matches the name in @Pipe decorator -->
    <p>Reverse Machine: {{ word | reverse }}</p>   <!-- !ralugnA -->
  `,
  imports: [ReversePipe],       // add custom pipe to imports like any other pipe
})
export class App {
  word = 'Angular!';
}
```

---

## (1) Another example — `StarPipe`

```ts
@Pipe({ name: 'star' })
export class StarPipe implements PipeTransform {
  transform(value: string): string {
    return `⭐️ ${value} ⭐️`;  // wraps any string with stars
  }
}
// Usage: {{ 'Angular' | star }}  →  ⭐️ Angular ⭐️
```
