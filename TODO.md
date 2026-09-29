# TODO List

- [x] Repasar video
- [x] Agregar archivos de configuración (base)
- [x] Estudiar notas para 20.3.x
- [ ] Agregar tema base: Angular Material
- [ ] ?
- [ ] ?
- [ ] ?
- [ ] ?

## Reapply Angular Material Redesign

```text
Work in this Angular repository and implement a Material 3 visual redesign.

Constraints:
- Preserve the existing routing files, paths, lazy-loading, guards, feature folders, and component structure.
- Do not upgrade or change existing Angular 20.3.x package versions.
- Add only Angular Material packages compatible with Angular 20.3.x:
  - @angular/material@20.2.14
  - @angular/cdk@20.2.14
- Use pnpm and update pnpm-lock.yaml.
- Do not add a new design system, external UI library, or unrelated functionality.
- Keep all existing components standalone.
- Use Angular Material components where appropriate.
- Add provideAnimationsAsync() in app.config.ts.

Theming:
- Apply Angular Material’s Material 3 Azure Blue prebuilt theme in src/styles.css:
  @import '@angular/material/prebuilt-themes/azure-blue.css';
- Replace the current centered body styling with a normal responsive application layout.
- Use Material system CSS variables for surface, typography, borders, and muted text.
- Ensure the layout is responsive for mobile screens.

Apply these UI changes:

1. App shell
- Update app.component.html to use:
  - app-nav-bar
  - a main.app-content containing router-outlet
  - app-footer
- Add a full-height flex application shell and centered responsive content width.

2. Navigation
- Convert shared/components/nav-bar to a MatToolbar.
- Add links for Articles, Dashboard, Calendar, Sign in, and Create account.
- Desktop: show inline navigation and account actions.
- Mobile: replace those actions with a Material menu button.
- Use RouterLink only; do not change route definitions.

3. Footer
- Use MatDivider and a minimal centered footer.
- Text: “Angular v20.3.x starter”.

4. Authentication screens
- Convert login and register screens to centered MatCard layouts.
- Use MatFormField, MatInput, and Material buttons.
- Login fields: email and password.
- Register fields: display name, email, password.
- Add reciprocal links between sign-in and registration.
- Keep forms presentational only; do not add authentication behavior.

5. Articles
- Convert the article list to a Material card grid with Material chips and “Read article” links.
- Include three presentational sample articles:
  - Designing for focus
  - A useful frontend baseline
  - Writing interfaces that explain themselves
- Convert article detail into a readable Material card with a back-to-articles button.
- Keep the existing dynamic `:slug` route unchanged.

6. Admin area
- Convert admin-layout to a MatSidenavContainer with a persistent side navigation.
- Side navigation links:
  - Overview: /dashboard
  - Calendar: /dashboard/calendar
- Keep the nested router-outlet.
- Convert dashboard to Material cards with three simple metrics and a recent activity card.
- Convert calendar to Material cards with a visual July 2026 schedule and a “Next up” event list.
- Keep all data presentational; do not add services or modify existing behavior.

Use these Material modules as needed:
- MatButtonModule
- MatCardModule
- MatChipsModule
- MatDividerModule
- MatFormFieldModule
- MatInputModule
- MatListModule
- MatMenuModule
- MatSidenavModule
- MatToolbarModule

Verification:
- Run `pnpm install`.
- Run `pnpm exec tsc --noEmit -p tsconfig.app.json`.
- Run `pnpm build`.
- Report every changed file, package versions added, and verification results.
- If the production build does not complete because of environment permissions or process issues, state that clearly and include the exact observed issue.
```
