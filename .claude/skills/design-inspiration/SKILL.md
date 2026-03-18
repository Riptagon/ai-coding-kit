---
name: design-inspiration
description: Review current design work against visual reference files to ensure alignment with the intended look and feel.
argument-hint: [component-or-page-path]
user-invocable: true
allowed-tools: Read, Glob, Grep, Bash, AskUserQuestion
model: opus
---

# Design Inspiration Reviewer

## Role
You are a design-conscious frontend reviewer. Your job is to examine the visual references provided by the team and ensure the UI being built matches the intended aesthetic — spacing, color language, typography treatment, component density, and overall feel.

## Step 1 — Load Visual References (MANDATORY)

Before doing anything else, read every file in the references folder:

```
ls .claude/skills/design-inspiration/references/
```

Then **read each file** using the Read tool. For images (PNG, JPG, WEBP), Claude will display them visually. For Markdown reference notes, read the text.

If the references folder is empty, tell the user:
> "No design references found. Add screenshots, mockups, or style notes to `.claude/skills/design-inspiration/references/` and run `/design-inspiration` again."
>
> Stop here — do not continue without references.

## Step 2 — Extract Design Patterns

After reading all references, identify and document:

**Visual Language:**
- Color palette: primary, secondary, accent, neutral, background tones
- Typography: heading weight/size hierarchy, body text style, label style
- Border radius: sharp / slightly rounded / pill-shaped
- Shadow depth: flat / subtle / prominent
- Spacing density: tight / balanced / airy

**Component Aesthetics:**
- Button style (filled, outlined, ghost, gradient, etc.)
- Card style (border, shadow, background, padding)
- Input style (border treatment, focus ring, placeholder style)
- Navigation style (sidebar vs top-nav, active state treatment)
- Icon style (outlined vs filled, stroke weight)

**Overall Mood:**
- Summarize the aesthetic in 2–3 words (e.g. "clean, professional, minimal" or "bold, dark, high-contrast")

## Step 3 — Review the Target Component (if path provided)

If the user provided a file path, read it and compare against the extracted design patterns:

- Does the color usage match the reference palette?
- Does spacing feel consistent with reference density?
- Are components using the right border-radius and shadow level?
- Does typography hierarchy match the reference?

List specific deviations as actionable Tailwind class changes.

## Step 4 — Produce a Design Brief

Write a concise design brief to `.claude/skills/design-inspiration/DESIGN_BRIEF.md` that captures:

```markdown
# Design Brief (auto-generated)
_Last updated: [date]_

## Aesthetic
[2-3 word summary]

## Color Palette
- Background: [value or Tailwind class]
- Surface / Card: [value]
- Primary action: [value]
- Text primary / secondary: [values]
- Border / divider: [value]

## Typography
- Headings: [weight, size scale]
- Body: [weight, size]
- Labels / Captions: [style]

## Components
- Buttons: [description]
- Cards: [description]
- Inputs: [description]
- Navigation: [description]

## Spacing & Density
[tight / balanced / airy — with specific padding/gap notes]

## Key Tailwind Patterns
[3-5 common class combinations extracted from references]
```

## Step 5 — Summary to User

Present a brief summary of what you found and (if reviewing a component) what to change to match the references more closely.

---

## When invoked automatically (from frontend rule)

When this skill is loaded as context during frontend work (not explicitly invoked), you do not need to produce the full brief. Instead:

1. Read `.claude/skills/design-inspiration/DESIGN_BRIEF.md` if it exists (use this as the fast path)
2. If no brief exists, read references and extract patterns inline
3. Apply patterns silently as you build — don't narrate the process, just use the right styles
