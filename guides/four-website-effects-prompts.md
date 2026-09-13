[← Back to the guide directory](../README.md)

# 4 Website Effects: GitHub Links and Starter Prompts

Use GitHub as a starting point for better website visuals. Pick one effect, give Claude Code or Codex the repository link, and ask it to adapt the implementation to your page.

**Sources checked:** 13 September 2026. These are original starter prompts, not tested implementations or guaranteed results.

## The four repositories

| Effect | Repository | Start with |
|---|---|---|
| Glass panels | [Liquid Glass JS](https://github.com/dashersw/liquid-glass-js) | One readable navigation panel or button with a refractive glass treatment. |
| Interactive 3D | [React Three Fiber](https://github.com/pmndrs/react-three-fiber) | One small 3D object in an existing React page. It is a React renderer for Three.js. |
| Moving gradients | [ShaderGradient](https://github.com/ruucm/shadergradient) | A restrained animated background using your brand colours. |
| Metallic logos | [Liquid Logo](https://github.com/paper-design/liquid-logo) | A liquid-metal treatment for your own logo, using Paper Shaders. |

## Start with your actual page

1. Open a local copy or branch of your website in your coding agent.
2. Choose one effect and paste its repository link with the matching prompt below.
3. Have the agent inspect the current README, licence and your project's framework before installing anything. These projects have different integration requirements.
4. Review the result on a phone and desktop before deploying. Check readability, loading performance and the reduced-motion fallback.

You can direct the work in plain English. The agent still writes code, and the integration needs review.

## 1. Liquid Glass JS

```text
Use https://github.com/dashersw/liquid-glass-js as the reference.
Inspect its current README and my project's framework first. Add one glass
navigation panel to [page]. Preserve the content, typography and layout.
Keep labels readable on light and dark backgrounds. Provide a plain fallback
where the effect is unsupported. Show the result at phone and desktop widths,
and explain the files and dependencies you changed.
```

## 2. React Three Fiber

```text
Use https://github.com/pmndrs/react-three-fiber for one interactive [object]
in [page]. Confirm this React project and its dependency versions are compatible
before making changes. Use [lighting direction] and [background colour].
Keep the object secondary to the headline. Make interaction work without
blocking page scrolling. Provide a static fallback and report loading impact.
```

## 3. ShaderGradient

```text
Use https://github.com/ruucm/shadergradient to add a slow moving background
to [section], using these brand colours: [colours]. Read the current integration
instructions for my stack. Preserve the layout and keep the area behind text
calm and high-contrast. Respect reduced-motion preferences with a still fallback.
Show phone and desktop results and explain how to adjust colour and speed.
```

## 4. Liquid Logo

```text
Use https://github.com/paper-design/liquid-logo as the starting point for a
liquid-metal treatment of my supplied logo at [path]. Read the current project
instructions and check how it fits my website. Keep the silhouette, proportions
and wordmark intact. Use restrained motion on a calm background. Provide a
static fallback, explain dependencies, and show the result at its real page size.
```

## Before you keep the effect

- Can you still read the headline and use the page?
- Does it work with touch, keyboard navigation and reduced motion?
- Is the mobile loading cost acceptable?
- Does the actual logo remain recognisable?
- Have you checked the current licence and any asset-attribution requirements?

The four official repositories above are the source references. Choose the effect that helps the page rather than adding all four at once.

---

Created by [Grayson Ho](https://github.com/graysonhyc).
