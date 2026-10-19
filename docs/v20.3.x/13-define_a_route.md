# 13 — Define a route

Each route object maps a URL `path` to a `component`. Add `title` to set the browser tab title automatically.

```ts
// app.routes.ts
import { Routes } from '@angular/router';
import { Home } from './home/home';
import { User } from './user/user';

export const routes: Routes = [
  {
    path: '',           // matches "/" — default route
    title: 'App Home Page',
    component: Home,
  },
  {
    path: 'user',       // matches "/user"
    title: 'App User Page',
    component: User,
  },
];
```

---

## (1) Another example

```ts
// app.routes.ts — define application routes
import { Routes } from '@angular/router';
import { loggedGuard } from './core/guards/logged.guard';

export const routes: Routes = [
  {
    path: '',
    loadChildren: () =>
      import('./features/auth/auth.routes').then((m) => m.AUTH_ROUTES),
    canActivate: [loggedGuard],
  },
  {
    path: 'articles',
    loadChildren: () =>
      import('./features/articles/articles.routes').then(
        (m) => m.ARTICLES_ROUTES, // Routes
      ),
  },
  {
    path: 'dashboard',
    loadChildren: () =>
      import('./features/admin/admin.routes').then((m) => m.ADMIN_ROUTES),
  },
];
```

```ts
// articles.routes.ts
import { Routes } from '@angular/router';
import { ArticleListComponent } from './article-list/article-list.component';
import { ArticleDetailComponent } from './article-details/article-details.component';

export const ARTICLES_ROUTES: Routes = [
  { path: '', component: ArticleListComponent },
  { path: ':slug', component: ArticleDetailComponent },
];
```
