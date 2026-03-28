# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

- **Dev server:** `pnpm dev`
- **Build:** `pnpm build` (runs `vue-tsc -b` then `vite build`)
- **Preview production build:** `pnpm preview`

## Tech Stack

Vue 3 with `<script setup>` SFCs, TypeScript (strict mode), and Vite. Package manager is pnpm. UI is built with **PrimeVue 4** using the Aura theme preset from `@primeuix/themes`.

## Architecture

Single-page app: `src/main.ts` mounts `App.vue`, which renders a global `<Toast>` and the `ComponentDemo` container component. Demo sub-components live in `src/components/demo/`. Global styles are in `src/style.css`.

TypeScript config uses a solution-style `tsconfig.json` with separate configs for app code (`tsconfig.app.json`) and Node/Vite tooling (`tsconfig.node.json`). Strict flags include `noUnusedLocals`, `noUnusedParameters`, and `erasableSyntaxOnly` (no const enums or namespace merging).

## PrimeVue Setup

Configured in `src/main.ts`:
- Theme: Aura preset with `darkModeSelector: '.app-dark'`
- Global services: `ToastService` (plugin) and `Tooltip` (directive `v-tooltip`)
- No auto-import — components must be explicitly imported from `primevue/<component>`

## Dark Mode

`ComponentDemo.vue` detects `prefers-color-scheme` on mount and provides a manual toggle. Dark mode activates by adding the `app-dark` class to `document.documentElement`. Body colors are driven by PrimeVue CSS variables (`--p-surface-ground`, `--p-text-color`).

## State Management Patterns

Components use `shallowRef` for primitive/simple values and `ref` only when deep reactivity is needed. No Pinia or Vuex — all state is local to components.
