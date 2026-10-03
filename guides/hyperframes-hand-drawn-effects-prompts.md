# Three hand-drawn effects with HyperFrames: circle, arrow, underline

**Status:** companion guide for the "one prompt, three hand-drawn effects" short (MOTION), written 3 October 2026. The prompts are cleaned-up versions of the requests used to make that edit with Claude Code and HyperFrames. Check every frame on your own footage before you post.

The effects are marker-style strokes that draw themselves on, with a slight wobble so they look hand-drawn. You film the gesture, and the agent draws on the timeline.

## Links

- [HyperFrames](https://hyperframes.heygen.com/): open-source (Apache-2.0) video framework from HeyGen
- [HyperFrames catalog](https://hyperframes.heygen.com/catalog): 380+ ready-made effects and animations
- Catalog components the effects are modelled on:
  - [hw-callout-circle](https://hyperframes.heygen.com/catalog/components/hw-callout-circle): scribble callout circle
  - [hw-arrow](https://hyperframes.heygen.com/catalog/components/hw-arrow): hand-drawn arrow
  - [hw-underline](https://hyperframes.heygen.com/catalog/components/hw-underline): squiggle underline
  - [hw-boil](https://hyperframes.heygen.com/catalog/components/hw-boil): the hand-drawn wobble

## Setup

```bash
npx hyperframes init my-video
cd my-video
npx hyperframes skills
```

Open the folder in Claude Code (or another coding agent) and put your clip in it.

## Film it so the effects land

- **Shoot vertical (9:16)**, with the camera 1.5–2 m away at eye level, and leave space above your head.
- **Give each effect its own gesture:** point at yourself for the circle, thumbs out for the arrows, hands down for the underline. Hold each one for half a second.
- **Use a plain background and a top that contrasts with it.** The strokes and the cut-out both read better.

## The prompts

### 1. Hand-drawn circle

```text
In this HyperFrames project, while I point at myself from [start] to [end], draw a thick yellow marker circle around my face. It should look hand-drawn: slightly lopsided, overlapping where it closes. Draw it on in about half a second, add three small spark ticks at the top right when it closes, and give the strokes a subtle wobble every two frames. Keep it clear of my eyes and mouth.
```

### 2. Arrows

```text
From [start] to [end], when I do the thumbs-out, draw two thick pink hand-drawn arrows that swoop in from the top-left and top-right corners and point at my head. Draw the shafts first, then pop the arrowheads. Same wobble as the circle. Keep both arrows out of the top 240 px.
```

### 3. Underline

```text
When I say "underline" at [time], pop a big bold word above my head, then draw a yellow scribble underline beneath it from left to right, followed by a second, shorter underline just below. Fade everything out when the clip ends.
```

### 4. Label each effect

```text
Label each effect in the top-left as I say its name: a frosted-glass pill with a small icon, where each word turns a lavender-to-pink gradient and pops slightly as I say it. Keep the labels below the top 240 px.
```

## Check before you post

- Every stroke should start on your gesture, not before it.
- Check that nothing covers your eyes or mouth.
- Look for leftover strokes after each effect ends.
- Keep text and strokes out of the phone's top bar, the bottom caption area and the right-hand like/comment column.
