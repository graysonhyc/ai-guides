[← Back to the guide directory](../README.md)

# AI Presentation Tools Tier List 2026: The Skills I Use for Decks

This is the full board from the video: six AI presentation tools, ranked by whether the deck they make can follow your own design system. After the board come the skills I use to make decks with Claude Code, plus a media-kit template so the deck follows your rules. The grades are my opinion as of September 2026, not a benchmark.

**Sources checked:** 28 September 2026, against each product’s own site. Plans and features change quickly. If this guide disagrees with the official page, the official page wins.

## The board

| Tier | Tool | One-line reason |
|---|---|---|
| S | [Claude Code](https://claude.com/product/claude-code) | The best flexibility: give it a skill and a media kit, and the deck follows your rules. |
| A | [Gamma](https://gamma.app/) | Polished, well-designed decks, but sometimes hard to match your exact design system. |
| A | [Canva](https://www.canva.com/presentations/) | Polished in the same way as Gamma, with lots of other tools to adjust your design. |
| B | [NotebookLM](https://notebooklm.google/) | You can easily add links and drop your research in, but the slide quality is still mediocre. |
| C | [Copilot in PowerPoint](https://www.microsoft.com/en-us/microsoft-365/powerpoint) | Clunky, and the output is too weak for a professional deck. |
| C | [Plus AI](https://plusai.com/) | The same clunky experience; you spend your time fighting the tool. |

## S tier

### Claude Code

[Claude Code](https://claude.com/product/claude-code) is Anthropic’s coding agent for the terminal, IDE and desktop.

Why S: it isn’t a slide app, which is why it wins. Give it a deck skill (how to build slides) and a media kit (your logo, colours, fonts and rules), and every deck it makes follows your system instead of a template’s. The setup is below.

## A tier

### Gamma

[Gamma](https://gamma.app/) generates presentations, documents and websites from a prompt.

Why A: the decks come out polished and well designed. Sometimes it is hard to get them to follow your exact design system.

### Canva

[Canva](https://www.canva.com/presentations/) is a design platform with AI presentation features.

Why A: it is polished in the same way as Gamma, and it comes with many other tools to adjust your design by hand.

## B tier

### NotebookLM

[NotebookLM](https://notebooklm.google/) is Google’s AI research notebook; its site now calls it Gemini Notebook.

Why B: you can easily add links and drop your research in, but the slides it generates are still mediocre.

## C tier

### Copilot in PowerPoint

[Copilot in PowerPoint](https://www.microsoft.com/en-us/microsoft-365/powerpoint) is Microsoft 365’s AI assistant inside PowerPoint.

Why C: the experience is clunky, and the output is too weak for a professional deck.

### Plus AI

[Plus AI](https://plusai.com/) is an AI add-in for PowerPoint and Google Slides.

Why C: it is the same clunky experience, and you end up fighting the tool.

## The skills I use to make decks with Claude Code

Two public skills cover both formats:

| Skill | What it makes | Source |
|---|---|---|
| `frontend-slides` | Animated HTML decks in one self-contained file; it can also convert an existing PowerPoint to web | [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides) (MIT) |
| `pptx` | Real PowerPoint files you can open, edit and send | [anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/pptx), in the `document-skills` plugin |

### 1. Install them

Run these inside Claude Code:

```text
/plugin marketplace add zarazhangrui/frontend-slides
/plugin install frontend-slides@frontend-slides

/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills
```

Then start a deck with `/frontend-slides`, or ask for a `.pptx`, and the `pptx` skill takes over.

### 2. Make a media kit

A skill knows how to build slides. A media kit tells it what yours look like. Put one folder in your project:

```text
media-kit/
├── BRAND.md          # the rules (template below)
├── logo.svg          # plus logo-dark.svg if you use dark slides
├── fonts/            # your heading + body font files, or their Google Fonts names in BRAND.md
└── examples/         # 2–3 screenshots of slides you like
```

Starter `BRAND.md`. Replace every value with your own:

```markdown
# Deck rules

## Colours
- Background: #0E0F11
- Text: #FFFFFF
- Accent (one per slide, for the key number or word): #FFD84D

## Type
- Headings: Inter Black, sentence case, max 8 words
- Body: Inter SemiBold, max 3 bullets per slide

## Layout
- 16:9, one idea per slide, generous margins
- Logo bottom-left on every slide except the title slide
- Charts use the accent for the highlighted series only

## Never
- No stock photos, no clip art, no gradients I didn't list
- No more than 25 words on a slide
```

### 3. Brief the deck

```text
Read media-kit/BRAND.md and follow it on every slide.
Use media-kit/logo.svg and the fonts in media-kit/fonts.
Make a 10-slide deck about [topic] for [audience].
Outline the slides first and wait for my OK, then build it.
Output: [an HTML deck with /frontend-slides | a .pptx file].
```

Because the rules live in a file rather than in each prompt, every deck you ask for afterwards follows them.

## Which one should you start with?

| If you want… | Start with |
|---|---|
| Decks that follow your own design system | Claude Code + a deck skill + a media kit |
| A polished deck fast, with no setup | Gamma or Canva |
| Slides built from your research and links | NotebookLM |
| To stay inside PowerPoint or Google Slides | Copilot or Plus AI, and expect to fix the output |

---

Created by [Grayson Ho](https://github.com/graysonhyc). More guides in the [directory](../README.md).
