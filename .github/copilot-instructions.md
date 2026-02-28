# Project Overview

This is a **Nuxt 3 (Vue 3 + TypeScript)** starter application with a very small set of pages and components. It's mostly the minimal boilerplate created by `nuxi init` and has not been fleshed out yet.

## Structure & Architecture

- **`pages/`** folder defines routes automatically (`index.vue`, `policy.vue`, `support.vue`, `terms.vue`). Pages are Vue single-file components using `<script setup lang="ts">`.
- **`components/`** holds reusable UI pieces (`NavBar.vue`, `Welcome.vue`, etc.). Currently many are empty; new components should follow the `<script setup>` pattern and export nothing by default.
- **`public/`** is for static assets (`reset.css`, `robots.txt`, `logo.png` referenced in `useHead`). Files here are served at the project root.
- **`nuxt.config.ts`** contains the Nuxt configuration (compatibility date, devtools enabled). It is intentionally minimal.

Routing and data flow are purely via the Nuxt page/component system; there is no store or backend integration yet.

### Key Patterns

- **SEO / head manipulation:** Most pages use `@vueuse/head` helpers (`useSeoMeta`, `useHead`) to set title, meta and link tags. Example from `pages/index.vue`:
  ```ts
  import { useSeoMeta, useHead } from '@vueuse/head';
  useSeoMeta({ title: () => title, description: () => description });
  useHead({ link: [{rel:'icon',href:'/logo.png'}] });
  ```
- **Client‑only rendering:** `<client-only>` wrapper is used around components in `index.vue` indicating potential SSR incompatibility.
- **Styling:** A global CSS reset is loaded via a `<link>` in `useHead` pointing to `public/reset.css`.
- **TypeScript support:** Files declare `lang="ts"` and rely on Nuxt's generated tsconfig references.

## Developer Workflow

Steps are standard for a Nuxt project; see `README.md` for commands.

1. Install dependencies:
   ```bash
   npm install    # or pnpm/yarn/bun
   ```
2. Start development server:
   ```bash
   npm run dev
   ```
   Local host at `http://localhost:3000`.
3. Build for production:
   ```bash
   npm run build
   npm run preview   # optionally preview locally
   ```

There are **no tests**, linters, or additional build scripts in this repository.

> ⚠️ If adding tooling (ESLint, tests) follow Nuxt 3 conventions.

## Conventions & Notes

- All new components should use `<script setup lang="ts">` and be placed under `components/`.
- Pages are Vue components; use `definePageMeta` or `useSeoMeta` for metadata.
- Avoid manual route configuration; rely on file system routing.
- Static assets go in `public/`. Reference them with absolute paths (`/logo.png`).
- The project currently has no state management or external API integration; if added later, follow Nuxt composables or the new Pinia store pattern.

## Integration Points

- **Third-party dependencies:** Only `@vueuse/head` is imported explicitly. Add further packages via `npm`/`pnpm` as needed and update `nuxt.config.ts` if plugins are required.

## When Editing this File

Keep instructions concise. Only document patterns and workflows you can infer directly from existing files. When new architectural pieces appear (stores, modules, tests, CI), update this file accordingly.

---

*Ask the user for any missing context or unclear conventions.*
