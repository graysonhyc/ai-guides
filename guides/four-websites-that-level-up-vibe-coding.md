[← Back to the guide directory](../README.md)

# Four websites that level up your vibe coding

Use four sites for four layers of an AI-built page: motion, the working site, an SVG background, and a palette you have already tested. Add one layer at a time.

**Sources checked:** 26 September 2026, against each product’s own site. Access, pricing and framework requirements change. If this guide disagrees with the official page, the official page wins.

## The four websites

| Layer | Site | Use it for |
|---|---|---|
| Motion | [Motion Primitives](https://motion-primitives.com/) | Copy-paste React animation components. You adapt them. You do not write the animation from scratch. |
| Working page | [Manus](https://www.manus.im/features/webapp) | A full-stack site from a plain-English brief, with analytics and SEO tools in the product. |
| Background | [Haikei](https://haikei.app/) | Unique SVG and PNG backgrounds. The homepage says it is free, with no signup and no card. |
| Palette | [Realtime Colors](https://www.realtimecolors.com/) | Colours and fonts previewed on a real page, with a contrast check, before you build. |

A practical order is Realtime Colors, Haikei, Motion Primitives, then Manus or your coding agent. The table follows the order in the video.

## 1. Motion Primitives

[Motion Primitives](https://motion-primitives.com/) is an open-source set of animated React components built with Motion and Tailwind CSS. The code is MIT-licensed: [ibelick/motion-primitives](https://github.com/ibelick/motion-primitives). The project describes itself as beta, so read the current docs before you install.

Installation, from [the docs](https://motion-primitives.com/docs/installation): Tailwind CSS, `npm install motion`, a `cn` helper, and `lucide-react` where a component needs icons. You can copy a component by hand or add one with the CLI, for example `npx motion-primitives@latest add text-effect`.

Pick one component. One text effect or one reveal is enough.

```text
Add the Motion Primitives component at [component URL] to [section] of my React page.
Read the current install notes first. This project uses [Tailwind or not].
Keep my copy and layout. Use it once, for [the headline or the hero].
Respect prefers-reduced-motion with a still state. Show phone and desktop,
and list the dependencies you added.
```

## 2. Manus

[Manus](https://www.manus.im/features/webapp) is a conversational builder for full-stack sites and apps. Its product page says you can describe the app in plain English, without writing the code yourself, and that the result can include a database, login, built-in analytics (page views, visitors, engagement) and SEO output such as meta tags and semantic HTML. It also describes deploying from the product and exporting the code.

Manus is a hosted product. Check the current plan before you start. Do not assume a free tier.

Bring the other three outputs with you:

```text
Build a one-page site for [product].
Audience: [who]. Main action: [what they should do].
Palette and fonts: [Realtime Colors export].
Hero background: use the attached Haikei SVG. Keep the text on top readable.
Motion: one restrained entrance on the headline, with a still fallback.
Include a headline, one proof section, and one clear call to action.
Set up analytics. Show me the live page on a phone before I publish.
```

Review the copy, the data you collect, and the live page before you send traffic to it.

## 3. Haikei

[Haikei](https://haikei.app/) generates SVG design assets in the browser. The homepage says it is free, with no signup and no credit card. Generators include blobs, waves, steps, peaks, grids and gradients. Export is SVG or PNG, so you can drop the file into a page or a design tool.

1. Open one generator. Blob, layered waves, or a gradient is enough for a hero.
2. Set the canvas to the hero size and enter your own brand colours.
3. Export SVG. If the file is busy behind the headline, lower the contrast and export again.
4. Give the file to your coding agent and ask for a still fallback if the SVG is heavy.

```text
Place this Haikei SVG as the background of [section].
Do not stretch it. Keep the headline at a contrast that passes WCAG AA.
Pause or remove motion if the SVG is animated and the user prefers reduced motion.
Show phone and desktop.
```

## 4. Realtime Colors

[Realtime Colors](https://www.realtimecolors.com/) previews a palette and fonts on a sample website. The site says the tool is free. You set text, background, primary, secondary and accent colours, see a contrast reading, and export. Export formats listed on the site include CSS, SCSS, PNG, a zip and a QR code. Fonts can be a Google Fonts name or a font installed on your device.

1. Start with a text colour and a background colour that pass the on-page contrast check for body text.
2. Add one primary colour for the main action and one accent. Stop at six colours.
3. Type the font names and read a real paragraph, not just the heading.
4. Export CSS and use those values in Haikei and in the build brief.

The colours and fonts are yours to use. The site’s own licence covers its code, not the colours you pick.

## Before you add another layer

- Body text still passes the contrast check after the background is in place.
- The page has one motion component, not a different animation on every block.
- The Haikei file is yours, exported from the tool, not a screenshot of someone else’s site.
- You have looked at the result on a phone before publishing.

---

Created by [Grayson Ho](https://github.com/graysonhyc).
