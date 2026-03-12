# Token Changelog

## [2.0.0] — 2026-03-12 — Penpot Compliance Rewrite

### Summary

Full audit and rewrite of all token files to achieve 100% Penpot Tokens compatibility.
No color values, spacing values, or semantic intent have been changed — only naming and structure.

---

### Files Modified

#### `primitives/color/solid.json`
- **Before:** flat keys with `color-` prefix, e.g. `"color-black-100"`, `"color-steel-600"`
- **After:** nested structure, e.g. `black.100`, `steel.600`
- All 28 color palettes preserved (black, white, blue, steel, orange, red, tomato, magenta, pink, purple, blueberry, violet, ocean, indigo, turquoise, aquamarine, avocado, teal, green, lime, yellow, mango, brown, cacao, disabled, success, information, warning, error, pomegranate)

#### `primitives/color/opacity.json`
- **Before:** flat keys with `color-` prefix, e.g. `"color-white-10"`, `"$color-steel-10"`
- **After:** nested structure, e.g. `white.10`, `steel.10`
- Removed all `$` prefixes that caused Penpot parse failures
- 22 palettes × 9 opacity steps preserved

#### `primitives/spacing/spacing.json`
- **Before:** keys with `spacing-` prefix, e.g. `"spacing-m"`, `"spacing-5xs"`
- **After:** clean keys `m`, `5xs`, etc.
- All 15 spacing values preserved

#### `primitives/border/radius.json`
- **Before:** keys with `rounded-` prefix, e.g. `"rounded-s"`
- **After:** clean keys `xs`, `s`, `m`, `l`, `xl`
- All 5 radius values preserved

#### `primitives/border/width.json`
- **Before:** keys with `stroke-` prefix, e.g. `"stroke-s"`
- **After:** clean keys `s`, `m`, `l`, `xl`
- All 4 width values preserved

#### `primitives/elevation/shadow.json`
- **Before:** flat keys `box-shadow-0`, `box-shadow-0-left`, `box-shadow-0-right`, etc.
- **After:** nested structure `0.center`, `0.left`, `0.right`, `1.center`, etc.
- `x`, `y`, `blur`, `spread` were already numbers — confirmed valid
- Color reference updated: `{color-steel-10}` → `{steel.10}`
- All 15 shadow variants preserved (5 levels × 3 directions)

#### `primitives/typography/font-family.json`
- **Before:** single key `"font-audiense"` with value `Poppins`
- **After:** key renamed to `"primary"` to remove redundant prefix
- Value unchanged: `Poppins`

#### `primitives/typography/font-weight.json`
- **Before:** keys `"font-weight-400"`, `"font-weight-500"`, `"font-weight-600"`
- **After:** clean keys `"400"`, `"500"`, `"600"`
- All 3 weight values preserved

#### `primitives/typography/font-size.json`
- **Before:** keys `"font-size-s"`, `"font-size-m"`, etc.
- **After:** clean keys `"s"`, `"m"`, `"l"`, `"xl"`, `"2xl"`, `"3xl"`, `"4xl"`
- All 7 size values preserved

#### `primitives/typography/line-height.json`
- **Before:** keys `"font-leading-s"`, `"font-leading-m"`, etc.
- **After:** clean keys `"s"`, `"m"`, `"l"`, `"xl"`, `"2xl"`, `"3xl"`, `"4xl"`, `"5xl"`
- All 8 line-height values preserved

#### `primitives/typography/text-case.json`
- **Before:** keys `"font-case-upper"`, `"font-case-lower"`, `"font-case-title"`
- **After:** clean keys `"upper"`, `"lower"`, `"title"`

#### `primitives/typography/text-decoration.json`
- **Before:** keys `"font-decoration-underline"`, `"font-decoration-dashed"`
- **After:** clean keys `"underline"`, `"dashed"`

---

### Semantic Files Modified

#### `semantic/border/border.json`
- Updated all references: `{stroke-s}` → `{s}`, `{rounded-s}` → `{s}`, `{color-black-900}` → `{black.900}`
- Token keys unchanged: `dft`, `s`, `m`, `l`, `xl`

#### `semantic/elevation/elevation.json`
- Updated all references: `{box-shadow-0}` → `{0.center}`, `{box-shadow-0-left}` → `{0.left}`, etc.
- Token keys updated to nested: `elevation-0` → `0.center`, `elevation-0-left` → `0.left`, etc.

#### `semantic/typography/typography.json`
- Updated all references:
  - `{font-audiense}` → `{primary}`
  - `{font-weight-400}` → `{400}`, `{font-weight-500}` → `{500}`, `{font-weight-600}` → `{600}`
  - `{font-size-s}` → `{s}`, `{font-size-m}` → `{m}`, etc.
  - `{font-leading-s}` → `{s}`, `{font-leading-m}` → `{m}`, etc.
- Token keys restructured to nested hierarchy: `text.link`, `heading.2xl.600`, `body.m.400`, etc.
- `body-m-400-udl` preserved as `body.m.400udl` with description noting underline applied in code
- `body-s-500-ct` preserved as `body.s.500ct` with description

#### `semantic/color/color.json` (NEW)
- New file providing semantic color aliases for brand, neutral, feedback, and disabled states
- All references point to valid primitives in `solid.json`

---

### Trade-offs and Notes

| Topic | Decision |
|-------|----------|
| Typography `textDecoration` in composite tokens | Penpot does not reliably accept `textDecoration` inside `typography` type tokens. The `body-m-400-udl` variant is kept as a typography token without the decoration property; decoration must be applied manually in Penpot or in code. |
| `elevation` semantic tokens | Penpot `composition` type with `boxShadow` reference works when the shadow primitive is a `boxShadow` type. The nested `0.center` path keeps Penpot from treating `0` as an invalid token name. |
| Old flat `elevation-0`, `elevation-1` names | Renamed to `0.center`, `1.center` etc. to match the updated primitive structure. Any existing Penpot components using the old names will need re-linking. |
| `spacing-` and `stroke-` prefixes | Removed to comply with rule 3 (no prefix repetition). Any Style Dictionary / build pipeline referencing old keys must be updated. |
