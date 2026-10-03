# Three hand-triggered effects with HyperFrames: finger trace, image carousel, spin halo

**Status:** companion guide for the "one prompt, three effects" short (MOTION), written 3 October 2026. The prompts are cleaned-up versions of the requests used to make that edit with Claude Code and HyperFrames. Results depend on your footage, so check every frame before you post.

All three effects are HyperFrames compositions driven by an AI coding agent. You film the gesture, and the agent puts the images on the timeline.

## Links

- [HyperFrames](https://hyperframes.heygen.com/): open-source (Apache-2.0) video framework from HeyGen
- [HyperFrames catalog](https://hyperframes.heygen.com/catalog): 380+ ready-made effects and animations
- Catalog carousels the effects are modelled on:
  - [carousel-path-1](https://hyperframes.heygen.com/catalog/blocks/carousel-path-1): finger trace
  - [carousel-vision-5](https://hyperframes.heygen.com/catalog/blocks/carousel-vision-5): image carousel
  - [carousel-circle-1](https://hyperframes.heygen.com/catalog/blocks/carousel-circle-1): spin halo

## Setup

```bash
npx hyperframes init my-video
cd my-video
npx hyperframes skills
```

Open the folder in Claude Code (or another coding agent) and put your clip in it.

## Film it so the effects work

- **Shoot vertical (9:16)**, with the camera 1.5–2 m away at eye level. Leave space above your head; the images need room.
- **Make each gesture slow and clear,** then hold it for half a second so the effect can land.
- **Keep your hands inside the frame.** Effects can't follow a finger the camera doesn't see.
- **Use a plain background and a top that contrasts with it.** This makes the cut-out cleaner.

## The prompts

### 1. Finger trace

```text
In this HyperFrames project, add a finger-trace effect to my clip from [start] to [end]. Track my index fingertip on every frame. Spawn [6] square image tiles: the first sits on my fingertip the moment my finger starts moving, and each new one stacks out from the previous one. Let them follow on soft springs so they trail behind my finger in an arc, settle when my finger stops, then shrink out. Use these images: [folder]. Keep the tiles out of the top 240 px and away from my face.
```

### 2. Image carousel

```text
Add an image carousel round my chest from [start] to [end], starting when I point. Ten image cards ride a tilted 3D ring and turn edge-on at the sides. Cut me out of the background with npx hyperframes remove-background so the back half of the ring passes behind my body. Use these images: [folder]. Keep the ring clear of the bottom 200 px and the right-hand icon column.
```

### 3. Spin halo

```text
Add a spin halo from [start] to [end], when I raise both index fingers. Eight small image cards spin in a flat ring around the top of my head. Cards at the back go behind my head using the cutout, and cards at the front pass over my hair. Pop them in one by one, then shrink them out at the end.
```

### 4. Label each effect

```text
Label each effect in the top-left as I say its name: a frosted-glass pill with a small matching icon. Each word should turn a lavender-to-pink gradient and pop slightly as I say it. Keep the labels below the top 240 px.
```

## Check before you post

- Watch frame 0 and every gesture at full size. Tiles should start on your finger, not before it moves.
- Look for leftover images after each effect ends.
- Check the cut-out edge around your hair and hands.
- Keep text, tiles and cards out of the phone's top bar, the bottom caption area and the right-hand like/comment column.
