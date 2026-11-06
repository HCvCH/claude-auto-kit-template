---
name: video-pipeline
description: Router for video and 3D-animation projects. Picks the video format (explainer, 3D explainer, data/graph, map route, product breakdown, stick-figure or cartoon, illustrated story series, talking-head edit, shorts cut) and then the exact design, motion and render skills for it. Use at the start of any video, reel, short, explainer or animated-story project, before writing a storyboard.
---

# Video Pipeline

`project-pipeline` decides *that* a project is VIDEO. This skill decides *which kind* of video it is and which skills build it. It does not replace Phase 8 of `project-pipeline` (direction, storyboard, design rules 8a, still check 8b) — it runs right before it and hands over a filled-in plan.

## 1. Pick the format

Ask at most one question if the brief doesn't make the format obvious. Otherwise pick it and say which one.

| Format | Typical brief | Look | Build with | Render |
|---|---|---|---|---|
| Explainer (2D, full-visual) | "explain how X works", "how a battery wears out" | flat, dimensional shapes, one focal object per scene | a motion-graphics or video-direction skill for script, storyboard and timing, if installed | Remotion or HyperFrames, if installed |
| 3D explainer | "3D lazy river", "inside an engine", miniature or diorama look | soft-lit low-poly or clay diorama, slow orbiting camera, tilt-shift depth of field | React Three Fiber scene inside Remotion (`@remotion/three`); reference objects from a photo → an image-to-3D skill, if installed | Remotion |
| Data / graph | stats, rankings, bar races, "how X grew" | one chart per scene, numbers counted up, no dashboards | Remotion with data in JSON | Remotion |
| Map route | trips, journeys, "how far is X" | simplified flat map, animated path, pins that pop | SVG or GeoJSON map in Remotion; camera pans along the path | Remotion |
| Product / phone breakdown | exploded view, "what's inside a phone" | parts separate in layers, labels only as captions | 3D (React Three Fiber) if a model exists, otherwise layered flat illustration | Remotion |
| Stick figure / cartoon | sketches, jokes, short stories | thick-line characters, squash and stretch, limited palette | characters as reusable SVG rigs (head, body, limbs as separate groups) | Remotion or HyperFrames |
| Illustrated story series | episodic stories, "viewers vote on the next part" | one consistent illustration style per series, slow push-ins and parallax on stills | per-scene images from an image generator the user has, kept consistent with a written style sheet (palette, line, lighting, character sheet); parallax and Ken Burns motion in Remotion | Remotion |
| Talking-head edit | raw recording to cut | jump cuts, zooms on emphasis, captions | ffmpeg for cuts and audio; captions from word timestamps | ffmpeg + Remotion overlays |
| Shorts from long video | "cut this podcast into clips" | 9:16 reframe, hook in the first 2 s | transcript → pick self-contained segments → reframe | ffmpeg |
| Ranking / tier list | "top 5 …", tier rankings, versus clips | big numbered slots, items drop into tiers, one item per beat | Remotion template with items in JSON | Remotion |
| Faceless short from a topic | "make a short about X" with stock footage | stock clips + captions + voice-over | script → stock footage search → captions; ffmpeg for assembly | ffmpeg + Remotion captions |
| Depth UI reel | app or website showcase, "show my product" | screens float in 3D space with parallax and depth of field, cursor or tap highlights | React Three Fiber or CSS 3D in Remotion with screenshots as textures | Remotion |
| Coaching / talking clip | advice, tips, podcast snippet | speaker + big keyword captions + b-roll cut-ins every 3–5 s | ffmpeg for cuts, captions from Whisper timestamps, b-roll from free stock | ffmpeg + Remotion overlays |
| Photo tour / listing video | property, product or location photos → cinematic tour | slow push-ins, parallax from depth, smooth crossfades, music | photos as layers in Remotion (Ken Burns, 2.5D parallax) — no paid generator needed | Remotion |

Mechanical editing (cuts, reframes, captions, loudness) goes through ffmpeg (or an ffmpeg skill, if installed). Sound effects: use a local royalty-free SFX folder if the user has one (ask once for its path) before generating any.

If the format needs a tool that isn't installed (HyperFrames, an image generator, a TTS tool), say which one and use the fallback in the same row — never stall.

## 1b. Quick mode (one-prompt videos)

If the user gives only a short prompt ("make a full-visual explainer about how a touchscreen works") or says "quick": pick the format and ONE style direction yourself, write the style sheet, skip the questions, and still show the storyboard for a single OK before rendering. Every visual must be drawn in code or come from the image sources below — the result should look finished without any further input.

## 1c. Image and footage sources (free first)

1. **Code-drawn** (SVG, CSS, React Three Fiber) — default for explainers, data, maps, cartoons.
2. **Local image generation**, if the user has it set up (e.g. ComfyUI). Check the model's license before using images in monetized videos.
3. **Free stock** — Pexels and Pixabay (free API keys) for b-roll and photos.
4. **Paid generators** only if the user explicitly asks; then write the prompts with a video-prompt skill, if installed.

## 2. Pick the look

Offer three concrete style directions for the chosen format, as in Phase 1 of `project-pipeline` (named style, palette with hex values, type, motion feel). One of them must fit the format's "Look" column above. Wait for the pick.

Rules for every look:
- Apply the anti-slop rules of Phase 8a in `project-pipeline` to every frame.
- One visual style per series. Write it down as a short style sheet in `./video-style.md` (palette, line weight, lighting, camera, character sheet) and reuse it for every episode.
- No third-party characters, brands or logos (e.g. Pokémon, Disney, game characters) in anything meant to be posted or monetized — invent original ones.

## 3. Hand over to Phase 8

Write a short plan before the storyboard:

```text
Format: …
Look: … (style sheet: ./video-style.md)
Skills: …
Render: … (1080x1920, 9:16 unless told otherwise)
Audio: voice-over tool …, music/SFX source (generated or royalty-free only)
Length: … s, scenes: …
```

Then continue with Phase 8 of `project-pipeline`: storyboard with second-by-second timings, wait for OK, design rules 8a, still check 8b, final render to `./out/` as one finished file.

## 4. Series and repeat formats

For a format the user will repeat (story series, weekly explainer, ranking reels):
- Build the first video as a template: scenes as components, content in one JSON file.
- Keep the template and the style sheet in the project so the next episode only changes the JSON and the assets.
- Note in the plan which parts change per episode.

---
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit-template (see NOTICE.md)
