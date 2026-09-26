[← Back to the guide directory](../README.md)

# Hover Reveal Effect: Two Images and One Prompt

A soft lens follows the cursor and reveals a second image underneath: the inside of a product, the finished version of a design, or the same view at night. You need two images and one prompt for your coding tool.

> **Last verified:** 26 September 2026. The build prompt below produced the working effect shown in the video: a single HTML file tested in desktop Chrome and a phone-sized viewport.

## 1. Prepare two images

The effect only works when the two images line up exactly.

- **Same size, same camera angle, same crop, same subject position.** Only the thing you want people to discover should change.
- **Strong contrast.** Outside ↔ inside, before ↔ after, wireframe ↔ finished page, day ↔ night. If the two images look similar, the reveal has nothing to show.
- Export both at the same pixel dimensions (for example 1500 × 1200).

### Making the second image with AI

Generate or pick the more detailed image first. Then upload it to ChatGPT, Gemini or your preferred image tool and ask for an edit, not a new image:

```text
Edit this image. Keep the exact framing, camera angle, crop, lighting direction and subject position.
Change only this: [open the case and show the movement inside / make it night with the windows lit / …].
Output the same size as the original.
```

Place the two results on top of each other and flick between them. If anything jumps, regenerate before you build.

## 2. Paste the build prompt

Open your coding tool (Claude Code, Codex, Cursor or similar), attach both images and paste:

```text
Build a hover reveal effect for the hero image on my website, using the two images I've attached.

Images
- `front` is shown by default. `back` is revealed under the cursor.
- Both images have the same size, camera angle and crop. Stack them exactly on top of each other in one container with a fixed aspect ratio that matches the images. Never stretch them.

Effect
- A soft circular lens follows the cursor and shows the `back` image inside it.
- The lens trails the cursor slightly (ease towards the pointer each frame, about 0.18 of the distance), so it feels smooth rather than stuck to the mouse.
- When the cursor leaves the image, shrink the lens to zero over about 300 ms.
- Draw it on a <canvas> with plain JavaScript: draw `front`, then draw `back` through a radial-gradient mask at the lens position. No libraries.

Controls
- Expose two settings at the top of the script:
  - SIZE — lens radius in CSS pixels (default 140).
  - STRENGTH — 0 to 1. At 1 the lens edge is crisp and the reveal is fully opaque; lower values give a softer, fainter edge (default 0.85).
- Add a small, removable tuning panel with a slider for each, so I can adjust them live and copy the values I like.

Quality
- Handle high-DPI screens (scale the canvas by devicePixelRatio, capped at 2) and resize with the container.
- Touch: dragging a finger moves the lens. Keyboard: when the image is focused, arrow keys move the lens.
- Respect prefers-reduced-motion: remove the trailing and move the lens directly.
- Only animate while the pointer is over the image or the lens is still shrinking.

Give me one self-contained HTML file I can open locally, then tell me where to swap in my own image paths.
```

## 3. Test and tweak

1. Open the HTML file and move the cursor slowly across the image.
2. Adjust **Size** until the lens shows enough to be interesting without covering the whole subject. 120–240 px suits most heroes.
3. Adjust **Strength**. Near 1 gives a crisp lens; around 0.4–0.6 gives a softer, more atmospheric reveal.
4. Copy the values into `SIZE` and `STRENGTH`, then delete the tuning panel.
5. Check it on a phone. Dragging should move the lens, and the images should stay sharp.

## Troubleshooting

| Problem | Fix |
|---|---|
| The subject jumps inside the lens | The images are not aligned. Fix the images, not the code. |
| The reveal looks blurry | Export larger images and confirm the canvas uses `devicePixelRatio`. |
| Nothing happens on touch | Ask your coding tool to set `touch-action: none` on the canvas and to listen for pointer events. |
| It feels laggy | Raise the easing value slightly (0.25–0.3) or reduce image size. |

---

Created by [Grayson Ho](https://github.com/graysonhyc).
