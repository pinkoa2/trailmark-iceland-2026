# Trailmark — Iceland Trip 2026

A static, single-page recap of a week-long trip around Iceland. Each day gets its own section with a Google Maps route, a short write-up, and a photo/video gallery.

**Live site:** [iceland.pinkoa2.lol](https://iceland.pinkoa2.lol)

## Stack

- [Svelte 5](https://svelte.dev) + [Vite](https://vite.dev) — plain Vite + Svelte, no SvelteKit
- No backend — everything is static files, deployed to GitHub Pages

## Running locally

```bash
npm install
npm run dev
```

## Project structure

```
public/photos/day-N/   Photos and videos for each day
src/lib/Banner.svelte  Hero banner with title
src/lib/Day.svelte     One day's section (map, description, gallery)
src/lib/Gallery.svelte Photo/video grid with lightbox
src/App.svelte         Wires up the banner + each day's content
```

Photos are compressed and resized before being committed (see `CLAUDE.md` for the exact process). Days load sequentially — a day's photos don't start fetching until the previous day has finished loading.

## About this project

This started as a one-off Iceland recap but is meant to be reused for future trips — see `CLAUDE.md` for the full build history and decisions.
