---
name: claude-animation-styles
description: Animate any scene in one of 10 hand-tuned visual styles (pixel art, paper cutout, blueprint, neon, flat vector, comic book, chalkboard, claymation, risograph, watercolor) as a single self-contained HTML file built with inline SVG and vanilla JavaScript. Use when the user asks for an animation, a looping scene, or "the same scene in another style".
---

# Claude Animation Styles

Ten animation styles that work with nothing but inline SVG, SVG filters and a little JavaScript. Each style is a recipe: palette, outline rule, filter, texture and frame rate.

## How to use

1. Ask the user for the scene (who, where, what happens) and the style. If they give no style, show the list of ten and let them pick; if they say "surprise me", pick the one that fits the mood.
2. Describe the scene as neutral shapes first: ellipses, rounded rectangles, paths, and thick round-capped lines for arms and legs. Give each shape a color NAME (sky, ground, hero, accent), not a color value.
3. Apply the style recipe below to those shapes: it decides the real colors, outlines, filters, background, overlay texture and frame rate.
4. Deliver ONE self-contained HTML file (inline SVG + vanilla JS, no libraries, no external images or fonts), 16:9, driven by a single time variable so it loops seamlessly (default loop: 6 seconds).
5. To show the same scene in several styles, keep step 2 untouched and only swap the recipe.

## Rules that apply to every style

- Stepped styles (12 fps or 8 fps) quantize the time variable: `t = Math.floor(t * fps) / fps`.
- Shapes that sit in front must hide what is behind them. In outline-only styles (blueprint, neon, chalkboard), fill shapes with the background color instead of `none`.
- Arms and legs are single thick lines with round caps; in outlined styles draw a wider dark line under the colored one.
- SVG filters that tile (the pixel-art mosaic) need `filterUnits="userSpaceOnUse"` with the frame size, otherwise nothing is drawn.
- Entrances overshoot slightly (back-out easing). Nothing pops in without a 0.2 to 0.3 s move.

## The ten recipes

| # | Style | Frame rate | Recipe |
|---|---|---|---|
| 1 | Pixel Art | 12 | Flat colors, no outlines. 8-px mosaic filter (feFlood 2×2 at 3,3 → feComposite 8×8 → feTile → feComposite in → feMorphology dilate 4), `crispEdges`. Retro console palette on deep navy. Whole-pixel moves. |
| 2 | Paper Cutout | 12 | Muted paper colors, no outlines, a soft drop shadow under every layer (dx 2.5, dy 5, blur 2.6, 50%). Paper grain multiplied on top. Layers slide and rotate, never morph. |
| 3 | Blueprint | 30 | #17479A paper with 40-px and 20-px white grids. Thin white outlines (2.3 px), shapes filled with the paper color, dashed construction lines, dimension lines, monospace title block with a live readout. |
| 4 | Neon | 30 | Night gradient #0A0720 → #1A0B2E. Colored outlines 3 px (magenta, cyan, lime, yellow, violet), near-black fills. Glow filter merging two blurs (5) with the sharp copy. Faint scanlines on top. |
| 5 | Flat Vector | 30 | Bold solid shapes, no outlines, gradients or textures. 6 to 8 colors on deep purple. Big geometric background shapes. Ease-in-out with back-out entrances. |
| 6 | Comic Book | 12 | Saturated flats with 5-px black outlines. Halftone dots over the frame (12-px grid, 30°, 13%), light rays behind, 10-px black panel border, an action word in bold italic inside a yellow starburst. |
| 7 | Chalkboard | 8 | Green board #2C5A4B with a wooden frame. Pastel chalk strokes 5 to 6 px, shapes filled with the board color. Filter: turbulence 0.055 + displacement 5, masked by fine noise 1.1. New turbulence seed every frame (the lines boil). |
| 8 | Claymation | 12 | Chunky rounded shapes in warm colors, lit as clay: blurred alpha → feDiffuseLighting (surfaceScale 7) multiplied → feSpecularLighting highlight → soft shadow. Dark purple studio backdrop, subtle grain, squash and stretch. |
| 9 | Risograph | 12 | Only cream #F3EAD7, blue #2742F5, pink #FF5C8A, yellow #FFD23F. Flat shapes, each drawn twice (dark-blue ghost shifted 5,4 at 45% under the real one). Heavy grain multiplied, cream margin around the frame. |
| 10 | Watercolor | 30 | Cream paper #F6F0E2. Translucent fills (80%) with a darker thin edge, edges wobbled (turbulence 0.035 + displacement 9) and blurred 0.9. Background wash of indigo and violet (displacement 60, blur 14). Paper grain on top; new seed every 6 frames. |

## What this skill does not do

It does not generate photos, 3D renders or video files. The result is a web page that plays the animation; recording it to MP4 needs a separate tool.
