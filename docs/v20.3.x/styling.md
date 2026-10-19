# Angular 20.3.x styling techniques

## Table of contents

- [(1) Component styling techniques](#1-component-styling-techniques)
  - [(1.1) Inline metadata styles](#11-inline-metadata-styles)
    - [(1.1.1) Advantages](#111-advantages)
    - [(1.1.2) Disadvantages](#112-disadvantages)
  - [(1.2) External stylesheets (`styleUrl` / `styleUrls`)](#12-external-stylesheets-styleurl--styleurls)
  - [(1.3) Style binding](#13-style-binding)
  - [(1.4) Class binding](#14-class-binding)
  - [(1.5) Attribute binding](#15-attribute-binding)
  - [(1.6) Host element binding](#16-host-element-binding)
  - [(1.7) Programmatic styling with `Renderer2`](#17-programmatic-styling-with-renderer2)
- [(2) Global styles](#2-global-styles)
- [(3) Styling frameworks](#3-styling-frameworks)
  - [(3.1) Angular Material (official Angular UI library)](#31-angular-material-official-angular-ui-library)
    - [(3.1.1) Install](#311-install)
  - [(3.2) Bootstrap](#32-bootstrap)
  - [(3.3) Tailwind CSS](#33-tailwind-css)
  - [(3.4) PrimeNG](#34-primeng)
  - [(3.5) NG-ZORRO](#35-ng-zorro)
  - [(3.6) Bulma](#36-bulma)
  - [(3.7) Foundation](#37-foundation)
  - [(3.8) DaisyUI](#38-daisyui)
- [(4) Summary table](#4-summary-table)

> Explanation generated with ChatGPT

---

## (1) Component styling techniques

Angular provides several ways to apply styles depending on the scope and use case.

| # | Technique                                       | Scope              | Best for                        |
| ---: | ----------------------------------------------- | ------------------ | ------------------------------- |
| 1 | Inline metadata styles                          | Component          | Small components, demos         |
| 2 | External stylesheets (`styleUrl` / `styleUrls`) | Component          | Most applications               |
| 3 | Style binding                                   | Individual element | Dynamic values                  |
| 4 | Class binding                                   | Individual element | Toggle CSS classes              |
| 5 | Attribute binding                               | Individual element | Styling through attributes      |
| 6 | Host element binding                            | Component host     | Styling the component itself    |
| 7 | Renderer2                                       | Runtime            | Dynamic DOM manipulation        |
| 8 | Global styles                                   | Entire application | Themes, resets, utility classes |

---

### (1.1) Inline metadata styles

Styles are declared directly inside the component.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-user-card',
  template: `
    <h2>User</h2>
  `,
  styles: [`
    h2 {
      color: royalblue;
      margin: 0;
    }
  `]
})
export class UserCardComponent {}
```

#### (1.1.1) Advantages

- Everything is in one file.
- Useful for examples and small components.

#### (1.1.2) Disadvantages

- Difficult to maintain for larger components.

---

### (1.2) External stylesheets (`styleUrl` / `styleUrls`)

The recommended approach for most applications.

```ts
@Component({
  selector: 'app-user-card',
  templateUrl: './user-card.component.html',
  styleUrl: './user-card.component.css'
})
export class UserCardComponent {}
```

Or multiple files:

```ts
@Component({
  selector: 'app-user-card',
  styleUrls: [
    './user-card.component.css',
    './user-card.component.theme.css'
  ]
})
export class UserCardComponent {}
```

Supported stylesheet formats include:

- CSS
- SCSS
- Sass
- Less

---

### (1.3) Style binding

Bind individual CSS properties dynamically.

```html
<div
  [style.color]="isAdmin ? 'red' : 'black'"
  [style.font-size.px]="fontSize"
>
  User
</div>
```

Component:

```ts
fontSize = 20;
isAdmin = true;
```

Useful for values that change frequently.

---

### (1.4) Class binding

Toggle one or more CSS classes.

```html
<div
  [class.active]="isActive"
  [class.disabled]="isDisabled">
  Button
</div>
```

Or multiple classes:

```html
<div [ngClass]="{
  active: isActive,
  warning: hasWarning,
  selected: isSelected
}">
  Item
</div>
```

---

### (1.5) Attribute binding

Some CSS relies on HTML attributes.

```html
<button
  [attr.aria-disabled]="disabled"
  [attr.data-theme]="theme">
  Save
</button>
```

CSS:

```css
button[data-theme="dark"] {
  background: black;
  color: white;
}
```

---

### (1.6) Host element binding

Apply styles to the component's host element.

Using the `host` metadata property (recommended):

```ts
@Component({
  selector: 'app-card',
  template: `<ng-content />`,
  host: {
    '[class.active]': 'isActive',
    '[style.border-color]': 'borderColor'
  }
})
export class CardComponent {
  isActive = true;
  borderColor = 'royalblue';
}
```

Or with `@HostBinding`:

```ts
import { Component, HostBinding } from '@angular/core';

@Component({
  selector: 'app-card',
  template: `Card`
})
export class CardComponent {

  @HostBinding('class.active')
  active = true;

  @HostBinding('style.background')
  background = 'lightblue';
}
```

Useful when the style belongs to the component itself rather than an internal element.

---

### (1.7) Programmatic styling with `Renderer2`

Used when manipulating the DOM safely.

```ts
import {
  Component,
  ElementRef,
  Renderer2,
  ViewChild
} from '@angular/core';

@Component({
  selector: 'app-demo',
  template: `
    <div #box>Hello</div>
  `
})
export class DemoComponent {

  @ViewChild('box')
  box!: ElementRef;

  constructor(private renderer: Renderer2) {}

  ngAfterViewInit() {
    this.renderer.setStyle(
      this.box.nativeElement,
      'background',
      'gold'
    );

    this.renderer.addClass(
      this.box.nativeElement,
      'highlight'
    );
  }
}
```

Common methods:

| # | Method           | Purpose               |
| ---: | ---------------- | --------------------- |
| 1 | `setStyle()`     | Add or update a style |
| 2 | `removeStyle()`  | Remove a style        |
| 3 | `addClass()`     | Add a CSS class       |
| 4 | `removeClass()`  | Remove a CSS class    |
| 5 | `setAttribute()` | Set an attribute      |

---

## (2) Global styles

Global styles affect the entire application.

Typical location:

```text
src/
    styles.css
```

Example:

```css
html,
body {
    margin: 0;
    font-family: Roboto, sans-serif;
}

* {
    box-sizing: border-box;
}
```

Additional global files can be configured in `angular.json`.

```json
"styles": [
  "src/styles.css",
  "src/themes/dark.css"
]
```

Typical uses:

- CSS reset
- Typography
- CSS variables
- Theme definitions
- Utility classes
- Third-party library styles

---

## (3) Styling frameworks

Angular works with virtually any CSS framework.

---

### (3.1) Angular Material (official Angular UI library)

Designed specifically for Angular and implements Material Design.

#### (3.1.1) Install

```bash
ng add @angular/material
```

The schematic can:

- Install packages
- Configure animations
- Configure theming
- Include Material Icons
- Update project configuration

Example:

```html
<button mat-raised-button color="primary">
  Save
</button>
```

Best for:

- Enterprise applications
- Admin dashboards
- Accessibility
- Responsive layouts

---

### (3.2) Bootstrap

Popular responsive CSS framework.

Install:

```bash
npm install bootstrap
```

Add to `angular.json`:

```json
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "src/styles.css"
]
```

Example:

```html
<button class="btn btn-primary">
    Save
</button>
```

---

### (3.3) Tailwind CSS

Utility-first CSS framework.

Install:

```bash
npm install tailwindcss @tailwindcss/postcss postcss
```

Configure according to the Angular 20 installation guide, then use utility classes:

```html
<button class="bg-blue-600 text-white px-4 py-2 rounded">
    Save
</button>
```

---

### (3.4) PrimeNG

Comprehensive Angular component library.

Install:

```bash
npm install primeng @primeuix/themes
```

Example:

```html
<p-button label="Save"></p-button>
```

Best for:

- Data-heavy business applications
- Rich UI components

---

### (3.5) NG-ZORRO

Angular implementation of Ant Design.

Install:

```bash
ng add ng-zorro-antd
```

Example:

```html
<button nz-button nzType="primary">
    Save
</button>
```

---

### (3.6) Bulma

Lightweight Flexbox-based framework.

Install:

```bash
npm install bulma
```

Add to `angular.json`:

```json
"styles": [
  "node_modules/bulma/css/bulma.min.css",
  "src/styles.css"
]
```

Example:

```html
<button class="button is-primary">
    Save
</button>
```

---

### (3.7) Foundation

Responsive front-end framework focused on flexibility.

Install:

```bash
npm install foundation-sites
```

Include its CSS in the global styles configuration or import it into your global stylesheet.

---

### (3.8) DaisyUI

Tailwind CSS component library.

Install:

```bash
npm install daisyui
```

Example:

```html
<button class="btn btn-primary">
    Save
</button>
```

---

## (4) Summary table

| # | Technique / Framework  | Dynamic                    | Scoped       | Typical use                 |
| ---: | ---------------------- | -------------------------- | ------------ | --------------------------- |
| 1 | Inline metadata styles | No                         | ✅           | Small components            |
| 2 | External stylesheet    | No                         | ✅           | Standard component styling  |
| 3 | Style binding          | ✅                         | Element      | Dynamic property values     |
| 4 | Class binding          | ✅                         | Element      | Toggle classes              |
| 5 | Attribute binding      | ✅                         | Element      | Attribute-driven styling    |
| 6 | Host element binding   | ✅                         | Host element | Style the component itself  |
| 7 | Renderer2              | ✅                         | Runtime      | Safe DOM manipulation       |
| 8 | Global styles          | No                         | Entire app   | Shared styles and themes    |
| 9 | Angular Material       | Component library          | App          | Material Design UI          |
| 10 | Bootstrap              | CSS framework              | App          | Responsive layouts          |
| 11 | Tailwind CSS           | Utility framework          | App          | Utility-first styling       |
| 12 | PrimeNG                | Angular component library  | App          | Enterprise components       |
| 13 | NG-ZORRO               | Angular component library  | App          | Ant Design UI               |
| 14 | Bulma                  | CSS framework              | App          | Lightweight responsive UI   |
| 15 | Foundation             | CSS framework              | App          | Responsive web applications |
| 16 | DaisyUI                | Tailwind component library | App          | Rapid UI development        |
