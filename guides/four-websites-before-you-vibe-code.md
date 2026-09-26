[← Back to the guide directory](../README.md)

# Four websites to check out before you vibe code

Collect four inputs before you ask an AI to build a website: a real component, a working page, a palette you have already seen on a layout, and a few references you are allowed to learn from. Each site below does one of those jobs.

**Sources checked:** 26 September 2026, against each product’s own site. Access, pricing and export options change. If this guide disagrees with the official page, the official page wins.

## The four websites

| Job | Site | Use it for |
|---|---|---|
| Component | [Watermelon UI](https://ui.watermelon.sh/) | An open-source React block you can paste into a landing page. |
| Working page | [Manus](https://www.manus.im/features/webapp) | A full-stack site from a plain-English brief, with analytics and SEO tools in the product. |
| Palette | [Realtime Colors](https://www.realtimecolors.com/) | Colours and fonts previewed on a real page, with a contrast check, before you build. |
| References | [Godly](https://godly.design/) | A curated gallery of published web, app and UI work. Save references. Do not clone them. |

A practical order is Watermelon, Realtime Colors, Godly, then Manus or your coding agent. The table follows the order in the video.

## 1. Watermelon UI

[Watermelon UI](https://ui.watermelon.sh/) is an open-source React catalog of components, landing-page blocks, dashboards and templates. The registry is MIT-licensed: [WatermelonCorp/watermellon-registry](https://github.com/WatermelonCorp/watermellon-registry). The public site source is [WatermelonCorp/watermelon-platform](https://github.com/WatermelonCorp/watermelon-platform), also MIT. You copy the blocks you need instead of installing a whole component library.

Pick one landing-page section. Read its current dependencies, then give this to your coding agent:

```text
Use this Watermelon UI block as a starting point: [block URL].
Read the current licence and the dependencies on that page before you add anything.
Adapt it to my page at [path]. Keep my copy, offer and brand. Reuse one spacing scale
and one corner radius. Preserve labels, buttons and keyboard focus.
Show the section at phone and desktop widths, and list every file you changed.
```

## 2. Manus

[Manus](https://www.manus.im/features/webapp) is a conversational builder for full-stack sites and apps. Its product page says you can describe the app in plain English, without writing the code yourself, and that the result can include a database, login, built-in analytics (page views, visitors, engagement) and SEO output such as meta tags and semantic HTML. It also describes deploying from the product and exporting the code.

Manus is a hosted product. Check the current plan before you start. Do not assume a free tier.

Paste a brief that already includes the other three inputs:

```text
Build a one-page site for [product].
Audience: [who]. Main action: [what they should do].
Use this palette and these fonts: [Realtime Colors export].
Use this section as the structural reference, not as a layout to copy: [Watermelon block].
Visual direction, in my own words: [three notes from the Godly references].
Include a headline, one proof section, and one clear call to action.
Set up analytics. Show me the live page and the SEO title and description before I publish.
```

Review the copy, the data you collect, and the live page on a phone before you send traffic to it.

## 3. Realtime Colors

[Realtime Colors](https://www.realtimecolors.com/) previews a palette and fonts on a sample website. The site says the tool is free. You set text, background, primary, secondary and accent colours, see a contrast reading, and export. Export formats listed on the site include CSS, SCSS, PNG, a zip and a QR code. Fonts can be a Google Fonts name or a font installed on your device.

1. Start with a text colour and a background colour that pass the on-page contrast check for body text.
2. Add one primary colour for the main action and one accent. Stop at six colours.
3. Type the font names and read a real paragraph, not just the heading.
4. Export CSS and keep the file with the brief.

The colours and fonts are yours to use. The site’s own licence covers its code, not the colours you pick.

## 4. Godly

[Godly](https://godly.design/) is a curated gallery of web, app, UI and visual design. Use it to decide what “good” means for this project. It is not a template library.

1. Open the gallery and save three sites that match the kind of product you are building.
2. For each one, write four notes in your own words: hierarchy, type, spacing, motion.
3. Give your agent those notes. Ask it to apply the constraints to your page.

```text
Here are three references I chose and what I want from them:
1. [URL] — [one note]
2. [URL] — [one note]
3. [URL] — [one note]
Apply only those constraints to my page. Do not copy layout, imagery, or wording.
Show a phone and desktop view, and tell me which note each change came from.
```

Check that you are allowed to use anything you screenshot. A public gallery is a place to look, not a licence to reproduce the work.

## Before you generate the page

- You have one component, one exported palette, and three written references.
- Body text passes the Realtime Colors contrast check.
- The Manus brief names the audience, the action, and what must not be copied.
- You have looked at the result on a phone before publishing.

---

Created by [Grayson Ho](https://github.com/graysonhyc).
