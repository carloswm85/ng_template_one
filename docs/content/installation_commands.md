# Installation commands

## Table of contents

- [(1) Compatibility](#1-compatibility)
- [(2) Install the prerequisites](#2-install-the-prerequisites)
- [(3) Install and run the project](#3-install-and-run-the-project)
- [(4) Create another Angular 21 project](#4-create-another-angular-21-project)
- [(5) Add Angular Material](#5-add-angular-material)
- [(6) Upgrade an Angular 20 project](#6-upgrade-an-angular-20-project)

## (1) Compatibility

Angular 21.2 uses the following compatibility ranges:

| # | Angular | Node.js | TypeScript | RxJS |
|---:|---|---|---|---|
| 1 | `21.0.x` \|\| `21.1.x` \|\| `21.2.x` | `^20.19.0` \|\| `^22.12.0` \|\| `^24.0.0` | `>=5.9.0 <6.0.0` | `^6.5.3` \|\| `^7.4.0` |

This repository uses:

| # | Technology | Version |
|---:|---|---|
| 1 | Angular | `21.2.25` |
| 2 | Angular CLI | `21.2.27` |
| 3 | Angular Material and CDK | `21.2.14` |
| 4 | TypeScript | `5.9.3` |
| 5 | RxJS | `7.8.2` |
| 6 | Zone.js | `0.16.3` |
| 7 | pnpm | `11.17.0` |

Official compatibility matrix: <https://angular.dev/reference/versions>

## (2) Install the prerequisites

### (2.1) Install Node.js

Angular 21 supports Node.js `20.19.x`, `22.12.x` or later within Node 22, and Node
`24.x`. Download Node.js from <https://nodejs.org/>.

Verify the installation:

```bash
node --version
npm --version
```

### (2.2) Install NVM for Windows

NVM for Windows allows multiple Node.js versions to coexist:

- Repository: <https://github.com/coreybutler/nvm-windows>
- Releases: <https://github.com/coreybutler/nvm-windows/releases>

Example using Node.js 24:

```powershell
nvm install 24.0.0
nvm use 24.0.0
node --version
```

Common commands:

| # | Command | Description |
|---:|---|---|
| 1 | `nvm version` | Show the installed NVM version. |
| 2 | `nvm list` | List installed Node.js versions. |
| 3 | `nvm list available` | List downloadable Node.js versions. |
| 4 | `nvm install 24.0.0` | Install Node.js 24.0.0. |
| 5 | `nvm use 24.0.0` | Activate Node.js 24.0.0. |
| 6 | `nvm current` | Display the active Node.js version. |

### (2.3) Install pnpm

Install pnpm 11 globally:

```bash
npm install --global pnpm@11
pnpm --version
```

The `packageManager` property in `package.json` records the exact pnpm release used by
this repository.

## (3) Install and run the project

Run these commands from the repository root:

1. Install the locked dependencies.

   ```bash
   pnpm install
   ```

2. Start the development server.

   ```bash
   pnpm start
   ```

3. Open <http://localhost:4200/>.

Additional commands:

| # | Command | Description |
|---:|---|---|
| 1 | `pnpm build` | Create an optimized production build. |
| 2 | `pnpm watch` | Rebuild continuously using the development configuration. |
| 3 | `pnpm test` | Run the Jasmine and Karma tests. |
| 4 | `pnpm exec tsc --noEmit -p tsconfig.app.json` | Type-check the application without emitting files. |

## (4) Create another Angular 21 project

Create a project without installing Angular CLI globally:

```bash
pnpm create @angular@21 my-app
```

Alternatively, install the Angular 21 CLI globally:

```bash
pnpm add --global @angular/cli@21
ng new my-app
```

## (5) Add Angular Material

Use the Angular schematic when adding Material to another Angular 21 application:

```bash
ng add @angular/material@21
```

For a manual installation aligned with this repository:

```bash
pnpm add @angular/material@21.2.14 @angular/cdk@21.2.14
```

The legacy `@angular/animations` package is not required by this application. Angular
deprecated that package in v20.2 in favor of native CSS and `animate.enter` or
`animate.leave`.

## (6) Upgrade an Angular 20 project

Run official Angular migrations one major version at a time:

```bash
ng update @angular/core@21 @angular/cli@21
ng update @angular/material@21
```

Review the migration output, reinstall dependencies, and run type-checking, tests, and a
production build before merging the upgrade.
