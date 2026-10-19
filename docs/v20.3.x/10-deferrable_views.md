# 10 — Deferrable views

Use `@defer` to lazy-load heavy components, reducing the initial bundle and improving performance.

```ts
import { Component } from '@angular/core';
import { Comments } from './comments';

@Component({
  selector: 'app-root',
  template: `
    <article>
      <p>Blog post content...</p>
    </article>

    <!-- lazy-loads Comments when it scrolls into the viewport -->
    @defer (on viewport) {
      <comments />

    } @placeholder {
      <!-- shown before deferred loading starts; eagerly loaded -->
      <p>Future comments</p>

    } @loading (minimum 2s) {
      <!-- shown while fetching; minimum prevents flicker on fast loads -->
      <p>Loading comments...</p>
    }
  `,
  imports: [Comments],
})
export class App {}
```

---

## (1) Available triggers

| # | Trigger          | Loads when…                        |
| ---: | ---------------- | ---------------------------------- |
| 1 | `on idle`        | Browser is idle (default)          |
| 2 | `on viewport`    | Element enters the viewport        |
| 3 | `on interaction` | User clicks or focuses the element |
| 4 | `on hover`       | User hovers over the element       |
| 5 | `on timer(2s)`   | After a fixed delay                |
| 6 | `when condition` | Expression becomes truthy          |
