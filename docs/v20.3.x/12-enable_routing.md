# 12 — Enable routing

Three steps to set up the Angular Router: define routes, register the provider, add the outlet.

```ts
// app.routes.ts — define application routes
import { Routes } from '@angular/router';

export const routes: Routes = [];   // add route objects here
```

```ts
// app.config.ts — register the router provider
import { ApplicationConfig } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [provideRouter(routes)],   // registers routes with the DI system
};
```

```ts
// app.ts — add <router-outlet> where routed components will render
import { Component } from '@angular/core';
import { RouterOutlet } from '@angular/router';

@Component({
  selector: 'app-root',
  template: `
    <nav>
      <a href="/">Home</a>  |
      <a href="/user">User</a>
    </nav>

    <!-- matched component renders here -->
    <router-outlet />
  `,
  imports: [RouterOutlet],
})
export class App {}
```
