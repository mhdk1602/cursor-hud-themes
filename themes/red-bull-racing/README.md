# Oracle Red Bull Racing — Cursor IDE Theme (RB21 livery)

> *Lights out — and away we go.*
> Aurora-Axis architecture rebranded in full RB21 livery: Marine-blue navy, Honda HRC red, Red Bull yellow, champagne gold.

A premium dark theme for Cursor / VS Code, built with the same strict zero-RAM-overhead discipline as Aurora Axis, but reskinned end-to-end in Oracle Red Bull Racing's RB21 livery. The architecture (calm at rest, fireworks on touch) is preserved; the identity (palette + decorations) is swapped to evoke an F1 paddock pit-wall console.

---

## Design Doctrine

> **Calm at rest. Fireworks on touch.**

Identical philosophy to Aurora Axis (see [`../aurora-dusk/README.md`](../aurora-dusk/README.md) for the full essay), with the visual identity swapped:

- **Idle chrome**: Marine-blue panels with whisper-soft **speed-line scanlines at 150°** (race-car body-line angle), and **RB livery-stripe sidebar columns** (red ⇄ yellow ⇄ red).
- **Editor pane**: ambient **podium-champagne** gradient at the bottom (red → yellow → gold), and **RB stage lighting** in the corners (yellow top-left = acceleration zone, red top-right = DRS zone, champagne bottom-right = finish line).
- **Widgets/popups**: visionOS 8-layer spatial shadows + Raycast light-catcher borders + Glassmorphism 2.0 lensing — inherited unchanged.
- **Active state**: brake-disc cursor (red core + yellow halo), tricolor active tab (blue → red → yellow), DRS-zone status bar (yellow hairline + red glow underneath).
- **Boot prompt**: `▶ ORACLE RED BULL RACING · RB21 ONLINE · LIGHTS OUT — AND AWAY WE GO` in red text with yellow halo, fades in once on every window mount.

## Palette — RB21 Livery

The base is a deep marine-blue navy (RB's primary livery color), with chrome dropped to near-black navy for maximum editor contrast. Accents are the Honda HRC red + Red Bull yellow tricolor, with champagne gold for "victory" emphasis (types, built-ins).

| Token | Hex | Role | Used for |
|---|---|---|---|
| **RB Red** | `#E10600` | Active state, you-are-here | Cursor caret core, active tab middle stop, focus ring, active activity-bar item, active panel border, list highlight match, active line gutter, badge background, progress bar |
| **RB Red Deep** | `#D40404` | Important / mutable | Errors, debug toolbar, breakpoints, `self`/`this`/`super`, HTML tags, deleted git lines, conflict markers, invalid syntax |
| **RB Yellow** | `#FFC906` | Caution / warn / dirty | Tab dirty indicator (caution flag), warning diagnostics, cursor halo, status-bar top hairline (DRS zone), CSS class selectors |
| **RB Blue** | `#3671C8` | Default UI / structure | Inactive activity-bar icons, file tree folder icons, modified-git markers, breadcrumb separators, function calls, level-1 brackets, hyperlinks |
| **RB Cyan** | `#5DD3FF` | Info / interpolation / telemetry | Info diagnostics, hint diagnostics, JSDoc/docstrings, escape sequences in strings, object property keys, CSS tag selectors, h3 markdown |
| **RB Gold (Champagne)** | `#F7D060` | Built-in / namespace / accents | Built-in functions, primitives, regex literals, import/export keywords, namespaces, h4-h6 markdown, finish-line stage light |
| **RB Green** | `#79E589` | Positive / additive | Strings, added git lines, success terminal decorations, untracked files |
| **RB Orange** | `#FF8E1A` | Numeric / literals / brake glow | Numbers, booleans, null/undefined, constants, enum members, `await`/`async` |
| **Neon Red** | `#FF2A2A` | Decoration tier (cursor, glow, hover) | Cursor primary, button hover halo, neon ambient glow on widgets, boot prompt text |
| **Neon Yellow** | `#FFD933` | Decoration tier | Cursor halo secondary, hover halos on yellow elements, DRS hairline glow |
| **Background (RB Navy)** | `#0F1B3C` | Editor surface | Main editor background, gutter, peek view, breadcrumb bar, active tab |
| **Surface (Deep Midnight)** | `#050912` | Side surfaces | Sidebar, panel, status bar, title bar, activity bar (kept darker for contrast) |
| **Foreground** | `#E8EAF4` | Default text | Editor text, sidebar text, terminal text |
| **Foreground bright** | `#F2F5FF` | Emphasized text | Active tab text, list item text, focused row |
| **Muted** | `#7B82A6` | De-emphasized | Comments, line numbers, inactive descriptions |

## Architecture

Identical two-layer architecture as Aurora Dusk / Aurora Axis:

### Layer 1+ — `settings.json` (zero RAM cost)

All workbench color overrides + token color rules + editor experience flags. Fira Code with ligatures, semantic highlighting, sticky scroll, breadcrumbs, custom title bar, refined minimap, padded editor (16px top/bottom), inlay hints. Same key set as Aurora — only the hex values are swapped to RB21 livery.

### Layer 2 — `red-bull-racing.css` (≤6 MB cost)

A 1,756-line static stylesheet. The first ~1,555 lines are the inherited Aurora-Axis architecture (chrome restraint, editor stage lighting, visionOS spatial shadows, Glassmorphism 2.0 lensing, light-catcher borders, 3D hover tilt, single-fire keyframes, mask fades, refined corner radii) with every color value swapped through the RB palette. The final ~200 lines are the **RB OVERRIDES** block — 12 race-flavored moves layered on top.

### RB OVERRIDES — The race-flavored decoration layer

| # | Move | Trick |
|---|---|---|
| RB-1 | **Speed-line scanlines** | `repeating-linear-gradient(150deg, ...)` — diagonal racing stripes at the angle of an RB car body line, replacing horizontal scanlines. Yellow + red tints, ~1-2% opacity. |
| RB-2 | **Tricolor active tab** | Active tab top border uses `linear-gradient(90deg, var(--rb-blue) 0%, var(--neon-red) 50%, var(--rb-yellow) 100%)` — mirrors the side livery tricolor. |
| RB-3 | **Podium-champagne editor sunset** | Bottom 22% of every editor pane fades transparent → red → yellow → champagne gold. Like the moment a winning car crosses the line and the team sprays the bottle. |
| RB-4 | **RB stage lighting** | Multi-corner radial gradients on the editor: yellow top-left (acceleration zone), red top-right (DRS zone), champagne bottom-right (finish line glow). |
| RB-5 | **DRS-zone status bar** | Yellow 1px top hairline + neon-yellow inset highlight + red glow underneath. Evokes the moment DRS is enabled — yellow flash before green. |
| RB-6 | **RB livery-stripe sidebar columns** | Sidebar/auxbar gradient column borders are red ⇄ yellow ⇄ red instead of the rainbow. Looks like the side stripe of an RB car. |
| RB-7 | **Brake-disc cursor caret** | Cursor caret has a vertical red → yellow gradient core + 4-tier halo (red 4px / red-soft 12px / yellow 24px / yellow-faint 48px). Looks like a carbon brake disc glowing under braking. |
| RB-8 | **Yellow activity-bar active** | Active activity-bar icon turns RB yellow with red glow (the "winning car" stand-out). |
| RB-9 | **Caution-flag dirty indicator** | Tab dirty `•` indicator turns yellow with neon-yellow halo — the F1 caution flag. |
| RB-10 | **RBR red primary buttons** | Primary buttons are RB red gradient with white uppercase text + 0.4px tracking; hover flips the gradient to RB yellow with dark navy text (the brand-color transition). |
| RB-11 | **Pit-lane amber terminal** | Terminal panel scanlines switch from phosphor green to F1 pit-lane amber/yellow. Same "command center" feel, RB-flavored. |
| RB-12 | **Boot prompt RBR re-color** | The single-fire ASCII boot intro is recolored to RB red text + yellow halo + uppercase. Copy: `▶ ORACLE RED BULL RACING · RB21 ONLINE · LIGHTS OUT — AND AWAY WE GO`. Plays once on window mount, then `opacity: 0` forever. |

### What's inherited from Aurora Axis (unchanged)

- 65+ visual moves from v1-v5 of Aurora (active line indicator, cursor halo geometry, hex activity-bar selection, segmented-LED status bar, CRT scanline architecture, find-widget corner brackets, glassmorphism on small popups, button conic-gradient sweep on hover, button glitch on press, hex sweep on activity-bar inactive icons, tab close button rotation, workbench inset glow, hex dot grid on aux panel, Cursor chat polish, code lens, parameter hints, inlay hints, hover widget brackets, breadcrumb hover underline, notification close rotation, scrollbar shadow tint, breakpoint glow, lightbulb glow, extension list gradient titles, suggest widget icon glow)
- v5 Axis additions (chrome restraint, editor sunset, stage lighting, vignette, visionOS 8-layer spatial shadows, Raycast light-catcher borders, Glassmorphism 2.0 saturate-lensing, 3D hover tilt, boot prompt cinematic, mask-image list fades, refined 8px corner radii)

The RB theme is, in essence, **Aurora Axis with the livery swapped + 12 race-flavored decoration moves on top**.

## Memory Footprint

| Theme | Approx. extra RAM (renderer) | Visual feel |
|---|---|---|
| Default Dark+ (no overrides) | 0 MB | Stock VS Code |
| Aurora Dusk v1-v5 (last) | ~4-6 MB | Calm at rest, fireworks on touch (Tokyo Night palette) |
| **Oracle Red Bull Racing (RB21)** | **~4-6 MB** | Same architecture, RB21 paddock-console identity |
| Ferrari Scuderia F1 v7 (archived) | ~150-200 MB | Vegas casino at 3 a.m. |

Identical memory footprint to Aurora Axis — only colors and 12 decoration moves changed; no new infinite animations, no new fixed overlays, no new heavy filters.

## Installation

### Prerequisites

```bash
brew install --cask font-fira-code
cursor --install-extension be5invis.vscode-custom-css
```

### Apply

1. Copy `red-bull-racing.css` to your Cursor user themes folder:

   ```bash
   cp red-bull-racing.css "$HOME/Library/Application Support/Cursor/User/themes/"
   ```

2. Merge `settings-snippet.json` into your `settings.json` at `$HOME/Library/Application Support/Cursor/User/settings.json`. The snippet contains:
   - All editor experience flags (font, ligatures, sticky scroll, etc.)
   - The full `workbench.colorCustomizations[Default Dark+]` block (RB palette)
   - The full `editor.tokenColorCustomizations[Default Dark+]` block (RB palette)
   - The `vscode_custom_css.imports` entry pointing at the CSS file

3. Run **"Enable Custom CSS and JS"** from the command palette (`Cmd+Shift+P`).

4. Reload window. macOS may show a one-time "Cursor is corrupted" warning — this is expected, it's the cost of the `vscode_custom_css` extension patching the renderer. Click "OK" and you're done.

### Switching between themes

Both Aurora and RBR ship CSS files into the same themes folder. To switch:

```jsonc
"vscode_custom_css.imports": [
  // pick ONE:
  "file:///.../themes/red-bull-racing.css"
  // "file:///.../themes/aurora-dusk.css"
]
```

Re-run **"Enable Custom CSS and JS"** and reload. Color JSON also needs to flip — easiest is to keep two settings.json snapshots and `cp` between them, or maintain both palettes in your settings under a switch (manual).

## Files

| File | Purpose |
|---|---|
| `red-bull-racing.css` | The Layer 2 stylesheet (1,756 lines, RB21 livery + 12 RB overrides) |
| `settings-snippet.json` | The Layer 1+ portable settings block (~70 keys, RB palette) |
| `README.md` | This file |

## Rollback

To go back to plain Default Dark+ with no customizations:

1. Remove the `red-bull-racing.css` from `vscode_custom_css.imports` (set to `[]`)
2. Run **"Disable Custom CSS and JS"** from the command palette
3. Optionally delete the `[Default Dark+]` blocks from `workbench.colorCustomizations` and `editor.tokenColorCustomizations`

To switch to the Aurora theme (Tokyo Night palette), see [`../aurora-dusk/`](../aurora-dusk/). To switch to the Ferrari "Screencast Mode" theme for demos, see [`../ferrari-scuderia-f1/`](../ferrari-scuderia-f1/).
