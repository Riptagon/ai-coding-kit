# Design References

Drop your visual reference files here. Claude will read this folder automatically whenever UI components are created or modified.

## What to add

| File type | What it should show |
|-----------|---------------------|
| `.png` / `.jpg` / `.webp` | Screenshots of apps/sites you like, mockups, Figma exports |
| `.md` | Written style notes, color hex codes, font names, design tokens |

## Tips

- **Name files descriptively:** `dashboard-inspiration.png`, `button-style.png`, `color-palette.md`
- **Add multiple references** — Claude will synthesize a consistent style across all of them
- **Include a style notes file** if you have specific hex codes, font names, or design tokens you want enforced

## How it works

1. When you run `/design-inspiration`, Claude reads every file here and generates a `DESIGN_BRIEF.md`
2. During any frontend work (`/frontend` skill), Claude checks `DESIGN_BRIEF.md` and applies those patterns automatically
3. Run `/design-inspiration` again after adding new references to regenerate the brief
