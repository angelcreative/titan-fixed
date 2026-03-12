# Titan Design Tokens

Penpot-compatible design token system for the Titan / Audiense design language.

## Structure

```
tokens/
  primitives/
    color/
      solid.json       # Base solid colors (nested: black.900, blue.600, etc.)
      opacity.json     # Alpha/opacity variants (nested: steel.10, white.50, etc.)
    spacing/
      spacing.json     # Spacing scale (5xs → 7xl)
    border/
      radius.json      # Border radius primitives (xs → xl)
      width.json       # Border width primitives (s → xl)
    elevation/
      shadow.json      # Box shadow definitions (0–4, with center/left/right variants)
    typography/
      font-family.json   # Font families (primary = Poppins)
      font-weight.json   # Font weights (400, 500, 600)
      font-size.json     # Font sizes (s → 4xl)
      line-height.json   # Line heights (s → 5xl)
      text-case.json     # Text case values (upper, lower, title)
      text-decoration.json  # Text decoration values (underline, dashed)
  semantic/
    color/
      color.json       # Semantic color aliases (brand, neutral, feedback, disabled)
    border/
      border.json      # Semantic border compositions (dft, s, m, l, xl)
    elevation/
      elevation.json   # Semantic elevation compositions (0–4, center/left/right)
    typography/
      typography.json  # Semantic typography compositions (text, heading, body)
```

## Penpot Compatibility Rules Applied

1. **Token names** use only letters and digits separated by `.` — no hyphens, no `$` prefix.
2. **No `$`-prefixed tokens** — all root-level special keys removed.
3. **No prefix repetition** — in `font-weight.json` the keys are `400`, `500`, `600` not `font-weight-400`.
4. **Nested structure** generates valid dot-path names: `black.900`, `steel.10`, `font-size.s`, etc.
5. **All references** use `{token.path}` format — e.g. `{black.900}`, `{primary}`, `{s}`.
6. **Shadow numbers** (`x`, `y`, `blur`, `spread`) are numbers, not strings.
7. **All JSON is valid** — no trailing commas, no comments.
8. **No `.DS_Store`** or other junk files.

## How to Import in Penpot

1. Open your Penpot file.
2. Go to **Assets panel > Libraries > Add local library**.
3. Select **Import tokens** (or use the Tokens plugin if available).
4. Load each JSON file from `tokens/primitives/` first, then `tokens/semantic/`.
5. Recommended import order:
   - `primitives/color/solid.json`
   - `primitives/color/opacity.json`
   - `primitives/spacing/spacing.json`
   - `primitives/border/radius.json`
   - `primitives/border/width.json`
   - `primitives/elevation/shadow.json`
   - `primitives/typography/font-family.json`
   - `primitives/typography/font-weight.json`
   - `primitives/typography/font-size.json`
   - `primitives/typography/line-height.json`
   - `primitives/typography/text-case.json`
   - `primitives/typography/text-decoration.json`
   - `semantic/color/color.json`
   - `semantic/border/border.json`
   - `semantic/elevation/elevation.json`
   - `semantic/typography/typography.json`

## Token Reference Examples

| Old key (broken)         | New path (Penpot-valid)   |
|--------------------------|---------------------------|
| `color-black-900`        | `black.900`               |
| `$color-steel-10`        | `steel.10`                |
| `font-weight-400`        | `400`                     |
| `font-size-m`            | `m`                       |
| `font-leading-s`         | `s`                       |
| `font-audiense`          | `primary`                 |
| `rounded-s`              | `s`                       |
| `stroke-s`               | `s`                       |
| `box-shadow-1`           | `1.center`                |
| `box-shadow-1-left`      | `1.left`                  |
| `spacing-m`              | `m`                       |
