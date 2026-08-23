[← Back to the guide directory](../README.md)

# 5 Claude Code Plugins for Better UI

Five tools that improve a different part of Claude Code's front-end workflow: visual direction, design-system consistency, reference-to-code implementation, interface review, and browser verification.

> **Last verified:** 23 August 2026
>
> **Works with:** Claude Code. Most of the agent skills also work with Codex, Cursor, and other tools that support the open `SKILL.md` format.

## First, a useful clarification

“Plugin” is convenient shorthand, but these five are not all Claude Code marketplace plugins:

| Tool | What it actually is | Job in the workflow |
|---|---|---|
| [Taste Skill](https://github.com/Leonxlnx/taste-skill) | Portable agent skill | Give the build stronger visual direction |
| [Awesome DESIGN.md](https://github.com/VoltAgent/awesome-design-md) | Design-system reference library | Lock colours, type, spacing, components, and visual rules |
| [Image to Code](https://github.com/Leonxlnx/taste-skill/tree/main/skills/image-to-code-skill) | Portable agent skill | Turn a visual reference into an implementation workflow |
| [Web Design Guidelines](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines) | Official Vercel agent skill | Audit interface code against published web-interface rules |
| [Playwright CLI](https://github.com/microsoft/playwright-cli) | Browser automation CLI with agent skills | Open, inspect, test, and screenshot the finished interface |

Think of them as one pipeline:

```text
Taste ──> DESIGN.md ──> Image to Code ──> Guidelines audit ──> Playwright check
direction    system       implementation       review             proof
```

Do not activate everything in every prompt. Give each tool one clear job, then move to the next stage.

---

## Before you install anything

You need:

- [Claude Code](https://code.claude.com/docs/en/overview);
- Node.js 18 or newer for the install commands and Playwright CLI;
- Git if you want to clone any repository; and
- an existing front-end project, or a clear brief for a new one.

These are third-party tools unless labelled otherwise. Read their current instructions, source, licence, dependencies, and requested permissions before using them in sensitive projects.

---

## 1. Taste Skill — set the visual direction

Taste Skill is an anti-generic front-end instruction set. It makes the agent read the brief, infer an appropriate design language, and make more deliberate decisions about layout, typography, spacing, motion, and density.

It is most useful at the beginning of a landing page, portfolio, or redesign. It does not replace a real product brief or user research.

### Install the main skill

Run this in your project terminal:

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
```

The current default is the project's experimental v2 skill. If you need the original behaviour, install the preserved v1 explicitly:

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend-v1"
```

You only need one of those versions.

### Give it a real brief

The skill works better when the agent has constraints instead of a vague request to “make it look good.”

```text
Use the design-taste-frontend skill.

Build a responsive landing page for an invoicing tool used by freelance designers.
The page should feel calm, editorial, and trustworthy rather than futuristic.
Primary goal: start a free trial.
Audience: UK freelancers who dislike accounting software.
Keep the existing React and Tailwind stack. Preserve accessibility and performance.
Before coding, state the visual direction you inferred and the design-system
family you will use.
```

### Tune the three design dials

Taste uses three ideas to control its output:

| Dial | Lower value | Higher value |
|---|---|---|
| Design variance | Symmetrical and conventional | Asymmetrical and experimental |
| Motion intensity | Mostly static | More cinematic and interactive |
| Visual density | Spacious and focused | Compact and information-heavy |

You do not need to edit the skill file. Describe the intended result in your prompt:

```text
Keep design variance around 6/10, motion around 3/10, and visual density around
4/10. The interface should feel considered, not theatrical.
```

**Best for:** choosing a strong art direction and avoiding the same generic SaaS layout.

**Watch for:** decorative motion, generated imagery, or unusual layouts that do not support the product goal. Treat the output as a direction to review, not an automatic design approval.

---

## 2. Awesome DESIGN.md — give Claude a consistent system

[Awesome DESIGN.md](https://github.com/VoltAgent/awesome-design-md) is a library of independent design-language analyses inspired by well-known websites. Each `DESIGN.md` describes visual tokens and practical rules that an agent can follow across multiple screens.

This is not a plugin and the files are not official brand guidelines. Use them as starting references, then adapt the chosen file to your own product and identity.

### Add one reference to your project

Browse the repository and choose one direction. For example, this safely downloads the Vercel-inspired file under a temporary reference name, without overwriting an existing `DESIGN.md`:

```bash
curl -L https://raw.githubusercontent.com/VoltAgent/awesome-design-md/main/design-md/vercel/DESIGN.md -o DESIGN.reference.md
```

Read the reference before using it. Create or update your project's `DESIGN.md`, remove irrelevant components, replace borrowed brand choices, and add your real tokens and constraints. Delete `DESIGN.reference.md` after you have transferred the decisions you want to keep.

Commit the adapted `DESIGN.md` with your code so future sessions share the same source of truth.

### Ask Claude to follow it

```text
Read DESIGN.md before changing the interface.

Use it as a design-language reference, not as permission to copy another brand.
Adapt the system to our product name, content, audience, and existing components.
Reuse our current tokens where they already satisfy the direction. If the brief
and DESIGN.md conflict, explain the conflict before coding.
```

### Turn the reference into your own system

After the first screen, ask Claude to record the decisions that are now specific to your product:

```text
Review the implemented screen against DESIGN.md. Update DESIGN.md with only the
decisions we actually adopted: semantic colours, type scale, spacing, radii,
button hierarchy, card treatment, responsive behaviour, and motion limits.
Do not claim another company's brand assets or proprietary rules as ours.
```

**Best for:** maintaining consistency across pages and across future agent sessions.

**Watch for:** copying a recognisable brand too literally. A design reference is not a substitute for original brand work, usability testing, or legal review.

---

## 3. Image to Code — implement from a visual source

The `image-to-code` skill in the Taste repository creates an image-first workflow: establish visual references, analyse them, extract the design decisions, implement the interface, and compare the result with the source.

Unlike a one-shot screenshot converter, the value is the sequence. Claude should not glance at an image, guess the style, and immediately produce loosely related code.

### Install the skill

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "image-to-code"
```

### Use a reference you have the right to use

Attach your own mock-up, a licensed reference, or a screenshot you are permitted to reproduce. Then prompt Claude:

```text
Use the image-to-code skill for the attached landing-page reference.

Follow this order:
1. Inspect the existing codebase and stack.
2. Analyse the reference: grid, hierarchy, type, colours, spacing, imagery,
   components, states, and responsive implications.
3. Map those decisions to our existing components and DESIGN.md.
4. Implement the page without copying logos, text, trademarks, or proprietary assets.
5. Run the project and compare the rendered page with the reference.
6. Report intentional differences, remaining mismatches, and verification results.
```

For a multi-section page, use clear full-size references. Tiny mood boards make precise analysis difficult.

### The similarly named screenshot-to-code app

You may also see [abi/screenshot-to-code](https://github.com/abi/screenshot-to-code) described as “Image to Code.” It is a separate open-source web application that converts screenshots, mock-ups, Figma designs, and short recordings into code. It offers a hosted product and a self-hosted React/FastAPI application.

Use that app when you want a dedicated conversion interface. Use the `image-to-code` skill when you want Claude Code to inspect your existing project, implement inside it, and complete the visual-review loop. Check model/API costs and avoid uploading confidential designs to services you have not approved.

**Best for:** translating an approved visual direction into a real project while keeping the reference visible throughout implementation.

**Watch for:** pixel matching at the expense of responsive behaviour, semantics, maintainability, or accessibility.

---

## 4. Web Design Guidelines — audit before you ship

Vercel's `web-design-guidelines` skill reviews UI code against the latest [Web Interface Guidelines](https://github.com/vercel-labs/web-interface-guidelines). It focuses on details such as accessibility, forms, interaction, typography, content, performance, and common interface mistakes.

This is a review tool. It does not prove that the product is easy to use, and it cannot replace testing with real users or assistive technologies.

### Install the skill

```bash
npx skills add https://github.com/vercel-labs/agent-skills --skill "web-design-guidelines"
```

### Audit the files you changed

```text
Use the web-design-guidelines skill to review the UI files changed in this branch.

Report findings as file:line references, grouped by severity. Check keyboard use,
focus visibility, labels, contrast, target size, responsive layout, reduced motion,
loading and error states, typography, and misleading interactions.

Do not modify files yet. After the report, propose the smallest safe fixes.
```

Review the findings before asking Claude to change the code. Some rules are contextual, and a terse automated recommendation may not understand your product constraint.

Then request the fix pass:

```text
Apply the confirmed audit fixes. Preserve the approved visual direction and avoid
unrelated refactors. Run the relevant lint, type, and test checks when finished.
```

**Best for:** a structured review after the interface is working and before final browser QA.

**Watch for:** treating a clean report as proof of full WCAG compliance. Test keyboard navigation, zoom, screen readers, contrast, motion preferences, and real content separately.

---

## 5. Playwright CLI — let Claude inspect the result

[Playwright CLI](https://github.com/microsoft/playwright-cli) gives coding agents a token-efficient browser interface. Claude can open the app, interact with controls, inspect page snapshots, and take screenshots instead of claiming the UI “looks correct” from source code alone.

### Install the CLI and its agent skill

```bash
npm install -g @playwright/cli@latest
playwright-cli install --skills
playwright-cli --help
```

The `--skills` flag is plural. By default, the skill is installed for the current workspace. Recent releases also support `-g` for a global skill installation:

```bash
playwright-cli install --skills -g
```

Use project-level installation when you want the browser workflow versioned and isolated with one codebase.

### Start your app first

Run the project's normal development command in one terminal. Then ask Claude to use Playwright CLI against the local URL:

```text
Use Playwright CLI to review http://localhost:3000 at desktop and mobile widths.

Test the primary user journey with keyboard and pointer input. Check navigation,
forms, validation, loading, empty, error, and success states. Capture screenshots
of the important states. Report console errors, failed requests, overflow, clipped
content, unreadable text, focus problems, and visual mismatches with DESIGN.md.

Do not change code until you have shown the evidence and identified the cause.
```

### A small manual smoke test

These commands open Microsoft's TodoMVC demo, add two items, and take a screenshot:

```bash
playwright-cli open https://demo.playwright.dev/todomvc/ --headed
playwright-cli type "Buy groceries"
playwright-cli press Enter
playwright-cli type "Review the mobile layout"
playwright-cli press Enter
playwright-cli screenshot
playwright-cli close
```

The CLI uses element references from its page snapshots for precise interaction. Do not reuse references blindly after navigation or large DOM changes; inspect the current snapshot.

**Best for:** proving that the rendered interface works, looks coherent at real viewports, and survives the main interaction path.

**Watch for:** running automation against production accounts or destructive actions. Use test data and local or staging environments wherever possible.

---

## Recommended order for a real project

### 1. Write the brief

Define the audience, product goal, primary action, required content, existing stack, accessibility needs, and visual constraints.

### 2. Choose the direction

Use **Taste Skill** to interpret the brief. Review and approve the direction before a large implementation.

### 3. Lock the system

Choose and adapt one **DESIGN.md**. Record your actual colours, typography, spacing, components, and motion limits.

### 4. Implement from references

Use **Image to Code** with rights-cleared mock-ups or screenshots. Keep the existing stack and components where they fit.

### 5. Audit the code

Run **Web Design Guidelines** on the changed files. Confirm each finding before applying fixes.

### 6. Verify the rendered UI

Use **Playwright CLI** at representative desktop and mobile viewports. Test the core path and keep screenshots as review evidence.

### 7. Get human approval

Review the result with the product owner or designer. Agents can accelerate implementation and QA, but they cannot decide whether the interface is right for your users.

---

## Copy-and-paste installation checklist

Run these in the front-end project's terminal:

```bash
# 1. Visual direction
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"

# 2. Reference-to-code workflow
npx skills add https://github.com/Leonxlnx/taste-skill --skill "image-to-code"

# 3. Interface audit
npx skills add https://github.com/vercel-labs/agent-skills --skill "web-design-guidelines"

# 4. Browser verification
npm install -g @playwright/cli@latest
playwright-cli install --skills
```

Add a chosen `DESIGN.md` separately because it is a project reference, not an installed skill:

```bash
curl -L https://raw.githubusercontent.com/VoltAgent/awesome-design-md/main/design-md/vercel/DESIGN.md -o DESIGN.reference.md
```

Review the reference, then create or update your own `DESIGN.md`. Do not keep the Vercel-inspired file unchanged unless that direction genuinely fits. Adapt it to your own product before treating it as the source of truth.

## One prompt for the full loop

Use this only after the skills are installed and your brief and references are ready:

```text
Improve this interface through five explicit passes.

1. Direction: use design-taste-frontend to interpret the product brief. State the
   chosen direction before coding.
2. System: read DESIGN.md and preserve our documented tokens and components.
3. Build: use image-to-code to analyse the attached approved references and
   implement them in the existing stack.
4. Audit: use web-design-guidelines on the changed UI files and fix confirmed
   high- and medium-impact findings.
5. Verify: run the app and use Playwright CLI at desktop and mobile widths. Test
   the primary journey and capture screenshots of key states.

Keep each pass separate. Do not introduce unrelated dependencies or refactors.
Finish with changed files, intentional visual decisions, checks run, screenshots,
remaining risks, and anything that still needs human approval.
```

## Keep the result honest

- A beautiful screenshot is not proof that the product is usable.
- A design reference is not permission to copy another company's identity or assets.
- A guidelines audit is not a complete accessibility certification.
- A Playwright pass only covers the journeys, viewports, browsers, and states you actually tested.
- Generated code still needs normal review for security, performance, maintainability, and correctness.

Used together with clear review gates, these tools give Claude Code a much stronger loop: decide deliberately, build from evidence, audit the details, and inspect the real result.

## Official project links

- [Taste Skill](https://github.com/Leonxlnx/taste-skill)
- [Awesome DESIGN.md](https://github.com/VoltAgent/awesome-design-md)
- [Image to Code skill](https://github.com/Leonxlnx/taste-skill/tree/main/skills/image-to-code-skill)
- [screenshot-to-code app](https://github.com/abi/screenshot-to-code)
- [Vercel Web Design Guidelines skill](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines)
- [Vercel Web Interface Guidelines](https://github.com/vercel-labs/web-interface-guidelines)
- [Microsoft Playwright CLI](https://github.com/microsoft/playwright-cli)

---

Created by [Grayson Ho](https://github.com/graysonhyc).
