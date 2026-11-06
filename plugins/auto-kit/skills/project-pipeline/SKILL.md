---
name: project-pipeline
description: Step-by-step build pipeline for any new project. Use at the start of every new project, when the user says "new project", "start project", "/project-pipeline", or asks to build a website, landing page, dashboard, web app, game page, 3D scene, motion video, script, bot or tool from scratch. Classifies the project as WEB, 3D, VIDEO and/or CODE, always runs the quality, test and process skills for that type, and offers the look-defining design skills as distinct style directions for the user to pick, so no single skill makes every project look the same. Orchestrates every skill listed in its "Skill bundles" table.
---

# Project Pipeline

You run new projects through fixed phases. The project type decides which skills are relevant (see "Skill bundles" below). Skills from bundles that don't match are not used: a website gets web skills, but no 3D model and no video.

Inside a matching bundle there are three modes:

- **always** — quality, testing and process skills. They catch problems but don't decide what the result looks like, so they run on every matching project.
- **choose** — look-defining skills (layout catalogs, themes, brand systems, signature aesthetics). Used every time, they would make every project look alike. So they are never applied by default: you offer them inside distinct style directions in Phase 1 and the user picks. Only the picked direction shapes the design.
- **if** — only when the condition in the table is true.

## Phase 0 — Classify (always)

Read the user's request and any existing files. Classify the project as one or more of:

- **WEB** — website, landing page, dashboard, web app, browser game UI, any page with a UI
- **3D** — needs a 3D object or scene in the browser (always also WEB)
- **VIDEO** — motion graphic, TikTok/Reel, animated explainer, data video
- **CODE** — script, CLI, bot, backend/API without own UI, game logic outside the browser

A project can have several types (e.g. WEB + CODE for a web app with a separate API). The bundle is then the union.

For anything bigger than a single static page with a complete brief, ask a few targeted questions before posting the plan (not an interview). Then post the plan in this shape and wait for "ok" (or changes) before building:

```
Type: WEB
Phases: 1 Style → 2 DESIGN.md → 3 Build → 4 Motion → 5 Test → 6 Polish
Always: <every "always" skill from the table for these types>
If: <each "if" skill, with yes/no and why>
Choose in Phase 1: see the style directions below
Not in this project's bundles: <skills of other types>
Tell user: <manual-only skills worth running>

Style directions — pick one (or mix):
A) <named style> · layout · fonts · palette · motion: none/subtle/rich · look skills: <"choose" skills or none>
B) <clearly different style> · … · look skills: …
C) <clearly different again> · … · look skills: <none — own direction>
```

Build the "Always" and "If" lines by going through the "Skill bundles" table row by row.

If the user said not to ask, or is clearly away, pick the direction that fits the brief best, state it at the top, and continue.

## Phase 1 — Style (WEB, VIDEO)

Propose **three style directions** in the Phase 0 plan. They must differ in all of: named style (e.g. neo-brutalism, swiss, editorial, glassmorphism, bento grid, synthwave, claymorphism, wabi-sabi, Y2K), page structure, font pairing, palette and motion level. Rules for variety:

- Build the options fresh for each brief. Don't reach for the same favourite every time.
- Look at DESIGN.md files of sibling projects (`../*/DESIGN.md`) if they exist. No option may reuse the style, font pairing or palette of one of them unless the user asks for consistency.
- At most one option may be built around a single look-defining skill's signature aesthetic. At least one option is your own direction.
- Never default to purple gradients or centered-hero + three-card grids.
- VIDEO: each direction names a real reference family (e.g. Kurzgesagt-style flat illustration, Apple keynote, Swiss poster, risograph print). The "dark tech" default (dark navy + grid + mono labels + neon glow) is not allowed as an option unless the user asks for it.

Each option names which "choose" skills it would use. After the user picks, define for the chosen direction: one font pairing, background color, one accent color, corner radius, shadow style, motion level. The look skills of the unpicked options are not applied. They may still be used as reviewers for objective problems (spacing, contrast, hierarchy), never to push their own aesthetic.

## Phase 2 — DESIGN.md (WEB)

If the project root has no DESIGN.md:
- If the picked direction is a real brand look (Linear, Stripe, Vercel, Notion …), take its DESIGN.md from https://getdesign.md if available.
- Otherwise write a short DESIGN.md yourself from the Phase 1 decisions (colors, type scale, spacing scale, radius, shadows, motion level, component rules, do's and don'ts).

All later UI work must follow DESIGN.md. DESIGN.md wins over any skill's default style.

## Phase 3 — Build (WEB, CODE)

WEB: build inside the picked direction and DESIGN.md with the Phase 3 skills from the table. Use realistic copy, never lorem ipsum. Default stack: single index.html with vanilla JS for small things; Vite + React only when the project needs state across many views or the user asks for it.

WEB and CODE: for app logic (state, data handling, calculations, game rules — not pure layout), write tests first. On any bug, test failure or unexpected behavior, find the root cause before proposing a fix. If the project has more than one component (frontend + API, bot + database …), sketch the architecture before building and keep it in the README.

## Phase 4 — Motion (WEB)

Follow the motion level picked in Phase 1. "None" still covers basic feedback (hover, press, focus, loading, success/error). "Subtle" adds entrances and state changes. "Rich" adds scroll reveals and scroll-linked effects. Always respect `prefers-reduced-motion`. Use the Phase 4 skills from the table.

## Phase 5 — Test (WEB, 3D)

1. Open the page (local file or dev server) with a browser automation skill or tool if one is installed.
2. Full-page screenshots at 375, 768 and 1440 px into `./screenshots`.
3. Review them yourself: overflow, overlap, tiny text, tap targets under 44 px, broken line breaks, console errors.
4. Fix everything, re-screenshot, confirm.
5. Run the Phase 5 skills from the table (UI stress tests, guideline reviews, security checklists) and fix what they find.

## Phase 6 — Polish (WEB, CODE)

Run the Phase 6 skills from the table over the finished work and fix what they find, as long as the fix stays inside DESIGN.md. Then report a short before/after list.

## Phase 7 — 3D asset (3D)

Build the 3D object or scene with the Phase 7 skills from the table, embed it with orbit controls and soft lighting, then run Phase 5 on the page. Say so if a requested object (faces, characters) is a poor fit for procedural modelling.

## Phase 8 — Video (VIDEO)

Load `video-pipeline` first: it picks the format and the skills for it, then hands back here. Then use the Phase 8 skills from the table.

Always: 9:16 1080x1920 unless told otherwise. Offer the Phase 1 style directions for the video's look too. Show a storyboard with second-by-second timings first and wait for OK before rendering. Only generated or royalty-free audio. Render to `./out/`.

The final deliverable is ONE finished file (animation + burned-in captions + voice-over + SFX), not separate parts. If a voice-over exists, transcribe it for word timestamps and anchor every visual beat to a spoken phrase.

### 8a — Video design rules (always, before writing any scene code)

A video is watched, not paused and read like an infographic.

- **Captions are the text layer.** Besides captions, at most ONE other text element on screen at a time (a single keyword, max 3 words). No sub-lines under headlines, no step/progress bars, no "STEP 1 ·" chips, no label on every object.
- **One focal point per scene.** If two unrelated things compete for attention, cut one.
- **Banned default look:** dark navy + decorative grid, neon/outer glow and ripple rings, mono uppercase micro-labels, middle-dot (·) and arrow (→) chains, everything wrapped in a bordered rounded card, fake browser/app UI built from divs.
- **Objects are shapes, not cards.** Draw a laptop as a laptop, not an icon inside a rounded box.
- **Icons only from an icon library**, never hand-written SVG icon paths.
- **Motion carries the attention, not text:** camera moves, scale, morphs, color changes, objects reacting. Every animation must show something the voice-over says.

### 8b — Still check (always, before the full render)

Render 8–10 stills at key moments, contact-sheet them, and check each against 8a: count text elements per frame (max 2 incl. captions), look for every banned pattern, check safe areas (nothing important in the top/bottom ~200 px except captions). Fix, re-check, then render.

## Skill bundles

One row per skill. "Bundles" = project types the skill is relevant for. "Mode": **always** = run it on every matching project; **choose** = only via a style direction the user picked in Phase 1; **if** = only when the condition is true.

| Skill | Phase | Bundles | Mode |
|---|---|---|---|
| video-pipeline | 8 | VIDEO | always (format and skill router, runs before the storyboard) |
| *example:* a brainstorming or planning skill | 0 | WEB, 3D, VIDEO, CODE | always, except a single static page or small script with a complete brief |
| *example:* a theme or layout-catalog skill | 1 | WEB, 3D | choose |
| *example:* a browser test skill (e.g. Playwright) | 5 | WEB, 3D | always |

<!-- Maintained by the weekly automated task. Every new skill gets a row here (phase, bundles, mode) and a sentence in that phase's text. A skill that imposes its own look (themes, brand styles, signature aesthetics) gets mode "choose"; quality, test and process skills get "always" or "if". Replace or delete the example rows once real skills arrive. -->

## Rules

- Checkpoint after Phase 0 always (that's where the user picks the style direction); after Phase 3 show the result (screenshot) before Motion/Test unless the user said to run straight through.
- Before saying anything is done, fixed or working: check that every "always" skill and every true "if" skill was actually used.
- If a skill or tool from the table is missing, say which one and continue with the best fallback — never stall.
- Keep narration minimal. At the end: what was built, where the files are, which style direction and look skills were used, and which skills ran.

License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit-template (see NOTICE.md)
