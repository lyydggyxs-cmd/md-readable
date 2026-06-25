# Contributing to md-readable

Thanks for wanting to help. This skill is young and contributions are welcome.

## Ways to Contribute

### Share Output Examples (Most Valuable)

Used this skill to make an agent's wall of text readable? **Share the output file** (or a screenshot). Real-world examples are the best documentation. Open an issue or PR with:

- What the original Markdown was (research report, decision memo, competitive analysis, etc.)
- A link to or screenshot of the HTML output
- What worked well and what didn't

### Report Bugs

If the skill produces broken HTML, loses content, misidentifies confidence, or generates a misleading signal card — open an issue. Include:

1. The approximate length and type of the input Markdown
2. What the output was (screenshot or description)
3. What you expected

### Improve the Design System

The design system (`references/design-system.md`) is the CSS and HTML skeleton that all output uses. Improvements to:

- Accessibility (WCAG compliance)
- Mobile responsiveness
- Print stylesheet
- Typography (especially CJK or RTL languages)
- Performance (reducing output file size)

are very welcome. Check the [10 design principles](README.md#design-system) first — any change must be traceable to a principle.

### Improve the Skill Instructions

`SKILL.md` is the instruction set Claude reads. The key constraint: **this skill's instructions are for Claude, not for humans.** Claude already knows HTML/CSS — the skill should tell it *what standard to meet*, not *how to write code*.

If you're proposing changes to SKILL.md, ask: "Does this tell Claude something it doesn't already know?"

### Add Language Support

Currently, the signal card and UI labels are in Chinese (source language detection with auto-translation is on the roadmap). If you can contribute translations for UI labels (signal card, premises, footer) to other languages, open a PR.

## Development

The repo is the skill directory itself. To test changes:

```bash
# The skill is installed at ~/.claude/skills/md-readable/
# Either symlink or copy your dev version:
ln -s $(pwd) ~/.claude/skills/md-readable

# Test in Claude Code:
/md-readable examples/ai-document-crisis.md
```

## Principles

- **Don't compress, reorganize.** Every word of the original must be preserved somewhere in the output. The skill doesn't summarize — it changes containers.
- **Semantics over syntax.** The value isn't in converting `## Heading` to `<h2>` — it's in knowing whether that heading is a conclusion, a premise, or a topic label.
- **Zero external dependencies.** The skill itself uses no pip/brew/npm. Claude is the engine.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
