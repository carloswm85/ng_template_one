- [ng-template-one v21.2.x](#ng-template-one-v212x)
  - [(1) Overview](#1-overview)
  - [(2) Compatibility](#2-compatibility)
  - [(3) Technology stack](#3-technology-stack)
  - [(4) Architecture](#4-architecture)
  - [(5) Implemented features](#5-implemented-features)
  - [(6) Current maturity](#6-current-maturity)
  - [(7) Development commands](#7-development-commands)
  - [(8) Angular 21 upgrade](#8-angular-21-upgrade)

---

# ng-template-one v21.2.x

---

![Under construction](./docs/img/under-construction.jpg)

- Main repository: <https://github.com/carloswm85/ng-template-one>
- Architecture reference in Spanish: <https://youtu.be/kLUdumt8lNY>

---

## (1) Overview

`ng-template-one` is an Angular 21.2 starter application demonstrating a modern,
feature-oriented architecture and an Angular Material 3 interface.

The application resembles a responsive content-management workspace with articles,
authentication screens, a dashboard, and a calendar. Most data and interactions remain
presentational rather than connected to application services or a backend.

---

## (2) Compatibility

|   # | Technology       | Supported range                           | Project version |
| --: | ---------------- | ----------------------------------------- | --------------- |
|   1 | Angular          | `21.0.x` \|\| `21.1.x` \|\| `21.2.x`      | `21.2.25`       |
|   2 | Angular CLI      | Angular 21                                | `21.2.27`       |
|   3 | Node.js          | `^20.19.0` \|\| `^22.12.0` \|\| `^24.0.0` | `24.0.0`        |
|   4 | TypeScript       | `>=5.9.0 <6.0.0`                          | `5.9.3`         |
|   5 | RxJS             | `^6.5.3` \|\| `^7.4.0`                    | `7.8.2`         |
|   6 | pnpm             | `>=10`                                    | `11.17.0`       |
|   7 | Angular Material | Angular 21                                | `21.2.14`       |
|   8 | Angular CDK      | Angular 21                                | `21.2.14`       |
|   9 | Zone.js          | `~0.15.0` \|\| `~0.16.0`                  | `0.16.3`        |

- Project setup: [Installation commands](./docs/content/installation_commands.md)
- Official compatibility matrix: <https://angular.dev/reference/versions>
- Angular release policy: <https://angular.dev/reference/releases>

Angular 21 is in long-term support through June 2027.

---

## (3) Technology stack

|   # | Area                | Technology                                               |
| --: | ------------------- | -------------------------------------------------------- |
|   1 | Framework           | Angular 21.2.25                                          |
|   2 | Language            | TypeScript 5.9.3                                         |
|   3 | UI components       | Angular Material 21.2.14                                 |
|   4 | Component utilities | Angular CDK 21.2.14                                      |
|   5 | Reactive library    | RxJS 7.8.2                                               |
|   6 | Package manager     | pnpm 11.17.0                                             |
|   7 | Testing             | Jasmine and Karma                                        |
|   8 | Architecture        | Standalone components with lazy-loaded routes            |
|   9 | Theme               | Material 3 Azure Blue with light, dark, and system modes |
|  10 | Icons               | Material Symbols                                         |

---

## (4) Architecture

The application uses a feature-oriented structure:

|   # | Directory            | Responsibility                                             |
| --: | -------------------- | ---------------------------------------------------------- |
|   1 | `core/`              | Global services, models, guards, and HTTP interceptors     |
|   2 | `features/auth/`     | Sign-in and registration screens                           |
|   3 | `features/articles/` | Article listing and article details                        |
|   4 | `features/admin/`    | Dashboard, calendar, and administrative layout             |
|   5 | `shared/components/` | Navigation bar and footer                                  |
|   6 | `docs/`              | Project documentation and versioned Angular learning notes |

Routes are separated by feature and lazy-loaded:

|   # | Route                 | Feature                 |
| --: | --------------------- | ----------------------- |
|   1 | `/login`              | Sign-in screen          |
|   2 | `/register`           | Account registration    |
|   3 | `/articles`           | Article list            |
|   4 | `/articles/:slug`     | Article details         |
|   5 | `/dashboard`          | Administrative overview |
|   6 | `/dashboard/calendar` | Administrative calendar |

The notes under `docs/v20.3.x/` are retained as version-specific Angular 20 reference
material. They do not describe the current runtime version.

---

## (5) Implemented features

- Responsive Angular Material application shell.
- Desktop navigation and mobile menu.
- Persistent light, dark, and system theme selection.
- Three sample article cards.
- Presentational article detail page.
- Presentational login and registration forms.
- Administrative side navigation.
- Dashboard metrics and recent activity.
- July 2026 calendar and upcoming events.
- Functional HTTP interceptor configuration.
- Route guard structure.
- Responsive layouts using Material system variables.

---

## (6) Current maturity

The project is a polished frontend prototype and architectural template, not yet a
production application.

|   # | Status | Area                | Current state                                         |
| --: | :----: | ------------------- | ----------------------------------------------------- |
|   1 |   🤔   | Authentication      | UI only; no login or registration behavior            |
|   2 |   ❌   | Route authorization | Guard exists but always returns `true`                |
|   3 |   ❌   | HTTP authentication | Interceptor forwards requests unchanged               |
|   4 |   🤔   | Articles            | Hard-coded presentation data                          |
|   5 |   🤔   | Article slug        | Route is dynamic, but the displayed article is static |
|   6 |   🤔   | Dashboard           | Hard-coded metrics and activity                       |
|   7 |   🤔   | Calendar            | Hard-coded July 2026 schedule                         |
|   8 |   ❌   | Services            | `ArticlesService` has no implementation               |
|   9 |   ❌   | Backend/API         | No backend is configured                              |
|  10 |   🤔   | Unit tests          | Only a basic root-component creation test exists      |
|  11 |   ❌   | End-to-end tests    | No runner is configured                               |
|  12 |   ❌   | Root route          | No default component or redirect is defined           |

See `TODO.md` for planned improvements.

---

## (7) Development commands

|   # | Task                 | Command                | Description                                                 |
| --: | -------------------- | ---------------------- | ----------------------------------------------------------- |
|   1 | Install dependencies | `pnpm install`         | Installs the locked dependency graph.                       |
|   2 | Development server   | `pnpm start`           | Starts the development server at `http://localhost:4200/`.  |
|   3 | Production build     | `pnpm build`           | Creates an optimized build under `dist/`.                   |
|   4 | Watch build          | `pnpm watch`           | Rebuilds automatically using the development configuration. |
|   5 | Unit tests           | `pnpm test`            | Runs the existing Jasmine and Karma test suite.             |
|   6 | Angular CLI          | `pnpm ng -- <command>` | Runs a command with the local Angular CLI.                  |

Angular CLI documentation: <https://angular.dev/cli>

---

## (8) Angular 21 upgrade

The project was migrated from Angular 20.3 to Angular 21.2 on October 17, 2026.

- Angular framework packages were upgraded to `21.2.25`.
- Angular CLI and build tooling were upgraded to `21.2.27`.
- Angular Material and CDK were upgraded to `21.2.14`.
- Zone.js was upgraded to `0.16.3`.
- TypeScript module resolution was migrated to `bundler`.
- Bootstrap configuration was migrated to explicit zone-based change detection.
- Deprecated, unused `@angular/animations` and `@angular/platform-browser-dynamic`
  dependencies were removed.
- The existing Jasmine and Karma test setup was retained to keep the upgrade focused.
