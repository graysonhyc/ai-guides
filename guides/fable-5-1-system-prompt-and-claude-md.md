[← Back to the guide directory](../README.md)

# Fable 5.1: the GitHub file and a practical CLAUDE.md starter

Here is the public GitHub file discussed in the video, plus a short example you can adapt for your own project.

> **Last verified:** 5 September 2026
>
> **Works with:** Claude Code projects. The linked Fable file is a third-party claimed extraction; its authenticity is not independently verified here.

## Open the original file

[Read Claude-Fable-5.1.md on GitHub](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/Claude-Fable-5.1.md)

The page currently displays 2,195 lines and 269 KB. This is the source shown in the video, not an official Anthropic release. Its contents are reference material, not instructions to execute or automatically trust.

A system prompt contains instructions. It does not contain model weights, and copying it does not transfer the original model's capabilities.

## Write your own project instructions

Claude Code reads project instructions from CLAUDE.md. Start with the details that matter to your repository: its purpose, actual commands, conventions, boundaries and completion checks. Keep them concise and specific.

Create or update CLAUDE.md at your project root. If it already exists, preserve its useful rules. Adapt this original example and replace every bracketed placeholder before using it:

```markdown
# Project instructions

## Purpose
- This project helps [audience] do [task].
- Main app: [actual folder].

## Commands
- Install dependencies: [verified command].
- Run relevant tests: [verified command].
- Check formatting and types: [verified command].

## Working rules
- Follow the existing patterns in the module being changed.
- Keep changes focused on the requested behaviour.
- Ask before changing public interfaces or production data.

## Before finishing
- Run the checks relevant to the change.
- Report what changed, what passed, and anything not verified.
```

Use commands that actually work in your repository. Then start Claude Code, use /memory to inspect loaded instructions, and try a small task. Review the result and refine rules that were unclear. CLAUDE.md provides context; it is not a guarantee of compliance or a security boundary.

## Sources

- [Public file discussed in the video — third-party source](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/Claude-Fable-5.1.md)
- [Official Claude Code documentation: How Claude remembers your project](https://code.claude.com/docs/en/memory)

---

Created by [Grayson Ho](https://github.com/graysonhyc).
