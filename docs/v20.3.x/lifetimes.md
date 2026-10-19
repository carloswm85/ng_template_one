# Service lifetime (Angular 20.3.x)

## Table of contents

- [(1) Examples](#1-examples)
  - [(1.1) Application singleton (`root`)](#11-application-singleton-root)
  - [(1.2) Platform singleton (`platform`)](#12-platform-singleton-platform)
  - [(1.3) Per-injector (`any`)](#13-per-injector-any)
  - [(1.4) Component-scoped service](#14-component-scoped-service)
  - [(1.5) Route-scoped service](#15-route-scoped-service)
- [(2) Summary](#2-summary)
  - [(2.1) Recommendation](#21-recommendation)

| # | Provider location          | Instance lifetime                                                     | Typical use                                             |
| ---: | -------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------- |
| 1 | `providedIn: 'root'`       | **Singleton** (one instance for the entire application)               | Shared application state, APIs, authentication          |
| 2 | `providedIn: 'platform'`   | One instance per Angular platform                                     | Multiple Angular applications sharing the same platform |
| 3 | `providedIn: 'any'`        | One instance per injector (typically one per lazy-loaded environment) | Isolated instances for lazy-loaded features             |
| 4 | `providers` on a component | One instance per component instance (and its descendants)             | Component-local state                                   |
| 5 | `providers` on a route     | One instance per activated route injector                             | Route-scoped state and feature services                 |

---

## (1) Examples

### (1.1) Application singleton (`root`)

```ts
@Injectable({
  providedIn: 'root'
})
export class AuthService {}
```

- One instance for the entire application.
- The most common pattern.

---

### (1.2) Platform singleton (`platform`)

```ts
@Injectable({
  providedIn: 'platform'
})
export class SharedPlatformService {}
```

- Shared across multiple Angular applications running on the same page.
- Rarely used.

---

### (1.3) Per-injector (`any`)

```ts
@Injectable({
  providedIn: 'any'
})
export class FeatureCacheService {}
```

- Root injector gets one instance.
- Each lazy-loaded injector receives its own instance.
- Useful for feature-specific caches.

---

### (1.4) Component-scoped service

```ts
@Component({
  selector: 'app-editor',
  providers: [EditorStateService],
  template: `...`
})
export class EditorComponent {}
```

Each `EditorComponent` gets its **own** `EditorStateService`.

```text
Editor #1
 └── EditorStateService (A)

Editor #2
 └── EditorStateService (B)
```

---

### (1.5) Route-scoped service

```ts
export const routes: Routes = [
  {
    path: 'admin',
    providers: [AdminStateService],
    loadComponent: () =>
      import('./admin.component').then(m => m.AdminComponent)
  }
];
```

- A new instance is created when the route's injector is created.
- Destroyed when that route injector is destroyed.

---

## (2) Summary

| # | Scope                    | Singleton?            |
| ---: | ------------------------ | --------------------- |
| 1 | `providedIn: 'root'`     | ✅ Yes                |
| 2 | `providedIn: 'platform'` | ✅ Yes (per platform) |
| 3 | `providedIn: 'any'`      | ❌ No                 |
| 4 | Component `providers`    | ❌ No                 |
| 5 | Route `providers`        | ❌ No                 |

### (2.1) Recommendation

For most Angular **20.3.x** applications:

- ✅ Use `providedIn: 'root'` for shared application services.
- ✅ Use component providers for component-local state.
- ✅ Use route providers for feature- or route-specific state.
- ✅ Use `providedIn: 'any'` only when you specifically want separate instances across injector boundaries (such as lazy-loaded features).
