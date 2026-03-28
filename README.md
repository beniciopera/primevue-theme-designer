# PrimeVue Theme Demo

A playground for designing and previewing custom PrimeVue 4 component themes.

## What it is

This project showcases PrimeVue 4 components (inputs, buttons, selects, dialogs, overlays, etc.) with a custom theme applied on top of the Aura preset. Use it to iterate on your theme visually before taking it to production.

## How to use

1. Edit `src/style.css` — this is your portable theme file. It contains global CSS overrides for PrimeVue components (underline inputs, backdrop blur on dialogs, etc.)
2. Edit the primary color palette and other semantic tokens in `src/main.ts` via `definePreset`
3. When happy with the result, copy `src/style.css` and the `definePreset` block from `src/main.ts` into any other PrimeVue 4 + Aura project

## Stack

- Vue 3 with `<script setup>` + TypeScript
- PrimeVue 4 (Aura preset)
- Vite

## Commands

```bash
pnpm dev       # start dev server
pnpm build     # type-check + build
pnpm preview   # preview production build
```
