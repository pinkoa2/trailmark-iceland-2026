# Trailmark — Iceland Trip Recap Site

## Overview
A static, single-page site recapping a trip to Iceland. Built with Svelte.

## Working style
- User wants to go step by step and guide the build decisions directly, not have everything scaffolded at once.
- This file must be kept continuously up to date as new decisions/info come in during the project. Update it immediately whenever a new choice is made — don't wait to be asked.
- **Photo caption workflow**: when assigning captions to a day's photos, go one photo at a time — propose a suggested caption per photo, and let the user respond "keep" (use suggestion), "skip" (no caption for that photo), or give their own replacement text. Do not batch-propose captions for a whole day at once. Apply this same workflow for every day's photos going forward.

## Requirements (as of 2026-08-28)

### Structure
- Title
- Banner: a nice photo of Iceland at the top
- Per-day sections, each containing:
  - A Google Maps trajectory for that day
  - A short description
  - A photo gallery for that day

### Devices / responsiveness
- **Must work well on both desktop and phone.**
- Phone is expected to be the primary way this page gets viewed — design mobile-first.

### Maps
- Use Google Maps' native no-API-key iframe embed (Google Maps → plot route with multiple stops via "Add destination" → Share → "Embed a map" → copy the `src` URL).
- This shows an actual route/trajectory line per day, no billing or API key setup required.
- Each day component takes the embed URL as an input/prop.

### Photos
- Local photo files, dropped into the project by the user, organized per day into `public/photos/day-N/lowercase-hyphenated.jpg` (or `.mp4` for video).
- Workflow (used for all 7 days): user pastes raw photos into `public/photos/inbox/`; files get moved/renamed one day at a time, in-order captions assigned one-by-one, then files renamed again to match confirmed captions. `public/photos/inbox/` has since been deleted (was reference-only route screenshots, unused by the site) — recreate it if more days/photos are ever added.
- Videos are supported in the gallery (see decision log) — ffmpeg-generated poster JPGs for thumbnails, real `<video>` playback in the lightbox.
- Each photo in a day's array has `src`, `alt`, and optional `caption` (see photo caption workflow above) and `poster` (videos only).
- All photos are compressed with ImageMagick before being committed (see decision log for exact command) — no full-resolution originals are kept anywhere in or out of the repo anymore (user explicitly deleted the `originals/` backup after confirming compression quality).

### Hosting / deployment
- GitHub Pages, custom subdomain `iceland.pinkoa2.lol` (domain registered at Porkbun).
- Repo: `github.com/pinkoa2/trailmark-iceland-2026` (remote already configured, first commits pushed). Kept as `trailmark`-branded rather than renamed, per user's plan to later create a separate clean `trailmark` template repo for future trips.
- Still TODO: GitHub Actions build/deploy workflow, `CNAME` file in the repo, custom domain set in repo's Pages settings, and the CNAME DNS record at Porkbun (`iceland` → `pinkoa2.github.io`).

## Tech stack decisions
- Vite + Svelte (plain, not SvelteKit) — confirmed 2026-08-28. Project scaffolded via `npm create vite@latest`.
- Svelte 5, Vite 8, Node v24.11.1 (v18+ required for Vite).

## Deferred / future work
- Genericize `trailmark` into a clean, content-free template repo for future trips (e.g. Taiwan → `taiwan.pinkoa2.lol`), using GitHub's "template repository" feature. Deferred until the user actually starts the next trip — not needed for Iceland.

## Open questions / not yet decided
- GitHub Pages deployment isn't finished yet — see Hosting / deployment above for the exact remaining steps.

## Decision log
- 2026-08-28: Confirmed mobile is the primary viewing device — build mobile-first, verify on both phone and desktop.
- 2026-08-28: Confirmed use of Google Maps free iframe embed (no API key) instead of paid Google Maps JS API.
- 2026-08-28: Confirmed photos will be local files added by the user, not hosted externally.
- 2026-08-28: Confirmed hosting target is GitHub Pages.
- 2026-08-28: Confirmed plain Vite + Svelte (not SvelteKit) for build tooling; project scaffolded and `npm install` completed, dev server verified working.
- 2026-08-28: Built Banner, Day, and Gallery components. Gallery supports lightbox (tap photo to view full-screen with dimmed/blurred backdrop, keyboard + swipe-style prev/next nav) and optional per-photo captions.
- 2026-08-28: Day 1 fully completed: 6 photos organized into `public/photos/day-1/`, real Google Maps embed URL wired in (Keflavík Airport → Blue Lagoon → CityHub Reykjavik), photo order and captions finalized, description text written.
- 2026-08-28: Established the one-by-one photo caption workflow (see Working style) as the standing process for all remaining days.
- 2026-08-28: Added video support to Gallery (thumbnail + lightbox `<video>` playback). Video tiles span 2 grid columns at 16:9 (vs. 1:1 for photos) and use ffmpeg-generated poster frames (extracted at 1s) instead of relying on the browser to render a preview, which was unreliable.
- 2026-08-28: Day 2 fully completed: 11 media items (8 photos + 3 videos) organized into `public/photos/day-2/`, Golden Circle route embed wired in, order/captions finalized, description written.
- 2026-08-28: Deferred a per-day loading overlay idea (see Deferred / future work) rather than a whole-page preloader.
- 2026-08-28: Renamed Day 2 files post-caption for clarity (e.g. `suf.jpg`→`gullfoss.jpg`, `sitting.jpg`→`faxafoss.jpg`) — established pattern of renaming files to match confirmed captions after the fact, not just at intake.
- 2026-08-28: Gallery layout iterated significantly: tried CSS-column masonry (broke L-to-R/T-to-B order) → tried JS-computed CSS Grid masonry with row-span sizing (worked but had a caption-overlap bug, fixed by not letting `.thumb` stretch to 100% height) → settled on simplest approach per user request: fixed-size square boxes (2 columns, all breakpoints), `object-fit: contain` with transparent background so photos keep full aspect ratio letterboxed/pillarboxed and centered, no cropping. Images have 16px border-radius applied directly (not just the container) so rounding shows regardless of letterbox space. Captions are 0.7rem italic (grid) / 0.9rem italic (lightbox).
- 2026-08-28: Day 2 media files renamed to match confirmed captions (see above).
- 2026-08-28: Day 3 fully completed: 8 media items (7 photos + 1 video) organized into `public/photos/day-3/`, South Coast route embed wired in, order/captions finalized, description written. Note: `alex-rainbow.jpg` and `ting-rainbow.jpg` are both confirmed Skógafoss (not Seljalandsfoss as originally guessed for alex-rainbow) — file rename pending, user wants to do it as a batch later referencing these captions.
- 2026-08-28: Day 3 files renamed post-caption (`both-waterfall.jpg`→`seljalandsfoss.jpg`, etc.) — confirmed pattern of renaming after captions are locked in.
- 2026-08-28: Fixed gallery image/caption vertical gap: `.thumb` was centering images vertically within the fixed square box (`align-items: center`), leaving whitespace on both sides of letterboxed images and pushing captions visually away from the photo. Changed to `align-items: flex-end` so images sit flush at the bottom of their box and captions hug the image directly, with any letterbox space pushed to the top instead.
- 2026-08-28: Banner photo resolved — `Flag.JPG` (Icelandic flag) moved to `public/photos/banner.jpg` and wired into `<Banner src="/photos/banner.jpg">`. No longer a gradient placeholder.
- 2026-08-28: Fixed banner cropping the photo on wide desktop screens (`object-fit: cover` on a short/wide container cropped top/bottom of a 4:3 photo). Banner now layers a blurred/zoomed copy of the same photo as background (`object-fit: cover; filter: blur(24px)`) behind the full uncropped photo (`object-fit: contain`) on top — guarantees nothing gets cropped at any screen size.
- 2026-08-28: Shrunk banner title font (clamp 2rem-3.5rem → 1.5rem-2.5rem) and constrained width (`max-width: min(80%, 600px)` + `padding: 0 1.5rem`) so it no longer stretches edge-to-edge on the banner.
- 2026-08-28: Day 4 fully completed: 7 photos organized into `public/photos/day-4/` (glacier ice cave hike + Diamond Beach), route embed wired in, order/captions finalized, description written. Glacier identified as Breiðamerkurjökull.
- 2026-08-28: Day 5 fully completed: 7 photos organized into `public/photos/day-5/` (Reynisfjara Beach → Vík town → back to Reykjavík), route embed wired in, order/captions finalized, description written. `bus.jpg`/`bus-inside.jpg` are Skool Beans, a coffee shop in Vík converted from an actual bus. File renames for Day 5 not yet done — pending same as Day 3's pattern.
- 2026-08-28: Day 6 confirmed real (resolves the earlier day 6/7 gap question) — a relaxed last day in Reykjavík (shopping, bakeries), no route/map needed. Added a `noMap` prop to `Day.svelte` to distinguish "intentionally no map" (renders nothing) from "map not yet provided" (still shows the "Map coming soon" placeholder). Day 6 photos came in as generic `IMG_XXXX.JPG` filenames (no day/description baked in, unlike prior days) — identified by viewing the images directly: street cat, rainbow Skólavörðustígur street, restaurant meal. No captions requested. Day 6 fully completed: 3 photos organized into `public/photos/day-6/`.
- 2026-08-28: Day 7 resolved — a minimal entry, description only ("headed back to the airport"), `noMap`, no `photos` prop (Day.svelte/Gallery.svelte handle an absent/empty photos array fine, renders nothing). Trip recap is now complete Day 1 through Day 7.
- 2026-08-28: Added per-day loading state to Gallery.svelte — while a day's photos/video-posters are loading, shows a centered spinner + "Loading..." text (absolutely positioned over the gallery area, which already has a stable height thanks to the fixed-box layout) instead of the actual grid; fades in once every image has loaded (or errored, so a broken image can't hang it forever). Composes naturally with `loading="lazy"` — sections below the fold don't even start their spinner until they scroll near-into-view.
- 2026-08-28: Backed up all original full-resolution photos to `originals/photos/` (sibling to `public/`, NOT served/published — must be excluded when GitHub Pages deployment is set up) before compressing. Compressed all JPEGs in `public/photos/` in place with ImageMagick: `-auto-orient` (bakes EXIF rotation into pixels) → `-resize '2000x2000>'` (only shrinks if larger, preserves aspect ratio) → `-strip` (drops EXIF/GPS/metadata — also a privacy win for a public site) → `-quality 85`. Result: 81MB → 24MB for JPEGs (site total `public/photos/` 100MB → 42MB; videos untouched and are most of the remainder). `originals/` is the recovery path if a photo ever needs to be re-processed differently.
- 2026-08-28: Day 5 files renamed post-caption (`beach.jpg`→`reynisfjara-beach.jpg`, `bus.jpg`→`skool-beans.jpg`, etc.) — matches the established rename-after-captioning pattern. `yarn.jpg` kept as-is (no confirmed caption). All prior days' pending renames are now done.
- 2026-08-28: Added `title` prop usage — every Day now has both the "Day N" number (kept, per user preference) and a short descriptive title, e.g. "Day 2: The Golden Circle".
- 2026-08-28: Confirmed video compression is low-value here and skipped — videos aren't part of initial page load at all (only their poster JPGs are), the actual `.mp4` only fetches when a user opens that specific video in the lightbox, so compressing them wouldn't speed up the page, only that one on-demand click.
- 2026-08-28: Replaced independent per-day lazy-loading with true sequential cross-day loading: added `active`/`onloaded` props to `Gallery.svelte` (and passed through `Day.svelte`). A day's real `<img src>`s aren't rendered into the DOM until its `active` prop is true; native `loading="lazy"` was removed since it conflicted with forcing eager fetch order regardless of scroll position. `App.svelte` tracks `loadedThroughDay` and unlocks day N+1 only once day N reports fully loaded via `onloaded`. Tradeoff (explained to user): all days' photos eventually download in the background in order, even ones never scrolled to, in exchange for later days having a head start by the time the user reaches them.
- 2026-08-28: Deployment planning: user has a Porkbun domain `pinkoa2.lol` and wants `iceland.pinkoa2.lol` → this GitHub Pages site (subdomain approach chosen over path-based `/iceland`, since GitHub Pages can't natively split one domain across multiple repos/paths, and subdomains keep the door open for future unrelated projects on the same root domain). Plan: CNAME record at Porkbun (`iceland` → `<username>.github.io`) + GitHub Actions workflow to build/deploy + custom domain set in repo's Pages settings.
- 2026-08-28: User created the GitHub repo as `trailmark` (not `trailmark-iceland` or similar). Decision: keep it as `trailmark` for now holding the Iceland 2026 content; user will create a separate clean `trailmark` **template** repo later (GitHub's "template repository" feature) for future trips (e.g. Taiwan → `taiwan.pinkoa2.lol`) once they actually need it, rather than genericizing this repo preemptively. Branches were considered and ruled out for multi-trip hosting — GitHub Pages ties one custom domain to one deployed site per repo, so simultaneous live subdomains per trip need separate repos, not branches.
- 2026-08-28: Local git repo initialized (`git init`, not yet committed/pushed). `.gitignore` updated to exclude `originals/` (100MB full-res photo backups — not needed in the repo since compressed versions are already in `public/`).
- 2026-08-28: After confirming the compressed photos looked correct, permanently deleted (user-confirmed) `public/photos/inbox/` (unused route reference PNGs) and `originals/` (100MB full-res photo backups). No more full-resolution copies of the trip photos exist anywhere — only the compressed versions in `public/photos/`.
- 2026-08-28: User created the GitHub repo (`pinkoa2/trailmark-iceland-2026`, SSH remote) and added it as `origin` themselves. First commit ("Add Iceland 2026 trip recap site") pushed to `main` — 63 files, all of `public/photos/` included (~42MB). `.gitignore` excludes `node_modules`, build output, and `originals/`.
- 2026-08-28: Rewrote `README.md` — replaced the leftover default Vite/Svelte scaffold template README with actual project info (what it is, live URL, stack, how to run locally, project structure, the future-reuse plan). Committed and pushed.
