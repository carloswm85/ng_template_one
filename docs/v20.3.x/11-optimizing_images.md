# 11 — Optimizing images

`NgOptimizedImage` improves Core Web Vitals by enforcing lazy loading, preventing layout shift, and prioritizing LCP images.

```ts
import { Component } from '@angular/core';
import { NgOptimizedImage } from '@angular/common';  // import the directive

@Component({
  selector: 'app-root',
  template: `
    <!-- replace src= with ngSrc= to activate the directive -->
    <img ngSrc="/assets/logo.svg" alt="Angular logo" width="32" height="32" />

    <!-- dynamic binding -->
    <img [ngSrc]="logoUrl" [alt]="logoAlt" width="32" height="32" />

    <!-- priority marks this as the LCP image — loads eagerly -->
    <img ngSrc="www.example.com/hero.png" width="800" height="600" priority />

    <!-- fill: image fills its container like a background image -->
    <div style="position: relative; width: 400px; height: 300px;">
      <img ngSrc="www.example.com/banner.png" fill />
    </div>
  `,
  imports: [NgOptimizedImage],                       // add to component imports
})
export class App {
  logoUrl = '/assets/logo.svg';
  logoAlt = 'Company Logo';
}
```

**Optional: CDN image loader** (`app.config.ts`)

```ts
import { provideImgixLoader } from '@angular/common';

export const appConfig = {
  providers: [
    provideImgixLoader('https://my.base.url/'),  // prefixed to all ngSrc paths
  ],
};
// <img ngSrc="image.png" />
// RESULT IS: https://my.base.url/image.png
```

> `width` and `height` are **required** on every image (unless using `fill`) to prevent layout shift (CLS).
>
> Cumulative Layout Shift (CLS) is a Google Core Web Vitals metric that measures how much webpage content unexpectedly jumps or shifts around while a website loads.
