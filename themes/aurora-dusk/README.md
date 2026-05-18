# Aurora Dusk → Aurora **AXIS** (v5) — Cursor IDE Theme

> *Calm at rest. Fireworks on touch.*
> Tokyo-Night palette, Linear restraint, Raycast accent discipline, visionOS spatial depth, Synthwave horizon. Zero-RAM daily driver.

A premium dark theme for Cursor / VS Code, built with strict zero-RAM-overhead discipline. Now in its fifth iteration ("Aurora Axis") — the same Tokyo-Night-derived palette evolved into a **dual-state design**: a Linear-quiet workspace at idle, that explodes with Synthwave/HUD fireworks the moment you interact with anything.

This is the **daily-driver replacement** for the archived [Ferrari Scuderia F1 v7](../ferrari-scuderia-f1/) theme — same Tokyo-Night-derived palette, but built without the runtime overhead that made the Ferrari theme unsustainable for long editor sessions.

---

## Design Doctrine (v5 "AXIS")

> **Calm at rest. Fireworks on touch.**

Almost every cyberpunk theme is loud everywhere — visual fatigue. Almost every Linear/Raycast clone is calm everywhere — emotionally flat. **Aurora Axis** is the synthesis nobody is doing:

- **Idle chrome**: dimmed, quiet, soft hairlines, recessive — Linear's *"structure should be felt not seen"*.
- **Editor pane**: ambient sunset horizon at the bottom, multi-corner stage lighting (cyan/magenta/rose washes at 2-3% opacity), subtle vignette. Becomes the visual hero.
- **Widgets/popups**: when summoned, they appear with **visionOS-grade 8-layer spatial shadows**, **Raycast light-catcher borders** (`1px solid rgba(255,255,255,0.08)`), and **Glassmorphism 2.0 lensing** (`backdrop-filter: saturate(180%)` makes colors behind the glass *pop*).
- **Interactions**: every hover, focus, and click triggers single-fire fireworks — 3D button tilt, rotating conic-gradient borders, glitch displacement, hex sweeps, gradient reveals.
- **One-time cinematics**: a 1.4s ASCII boot prompt (`▶ AURORA::AXIS · CONN-POD ONLINE · CLEARANCE GRANTED`) fades in then vanishes on every window mount.

**Three foundational rules (unchanged across all iterations):**

1. **Color discipline** — One palette of 8 colors, every color has a tier and a job. No stray accents.
2. **Surgical accent** — Magenta = "you are here". Rose = "important / mutable". Blue = friendly default. Gold = warnings + types. They never blur.
3. **Static composition over motion** — All ambient polish via static styles. The only motion is hover/focus/active transitions or single-fire `forwards` keyframes. Idle CPU/GPU cost = zero.

## Palette — Brighter "Storm" Variant

The base is Tokyo Night Storm (brighter editor `#1F2335`), with the chrome (`#16161E`) deliberately kept dark to maximize contrast between the editor and the surrounding panels. Accents are pushed to higher saturation than the original Tokyo Night palette for more visual punch.

| Token | Hex | Role | Used for |
|---|---|---|---|
| **Magenta** | `#C792EA` | Active state, you-are-here | Cursor caret (with halo), active tab gradient stop, focus ring, active activity-bar item, active panel border, list highlight match, active line gutter, badge background, progress bar, picker group label |
| **Rose** | `#FF6E8E` | Important / mutable | Errors, debug toolbar, breakpoints, `self`/`this`/`super`, HTML tags, deleted git lines, conflict markers, invalid syntax |
| **Blue** | `#82AAFF` | Default UI / structure | Inactive activity-bar icons, file tree folder icons, modified-git markers, breadcrumb separators, function calls, level-1 brackets, hyperlinks |
| **Gold** | `#FFCC66` | Warnings / types | Editor warnings, conflict resolution, type names (classes, interfaces, enums), function decorators, parameter inlay hints, find-match highlight |
| **Cyan** | `#89DDFF` | Info / interpolation | Info diagnostics, hint diagnostics, JSDoc/docstrings, escape sequences in strings, object property keys, CSS tag selectors, h3 markdown headers, middle stop of active-tab gradient |
| **Green** | `#B5E890` | Positive / additive | Strings, added git lines, success terminal decorations, untracked files |
| **Orange** | `#FFB387` | Numeric / literals | Numbers, booleans, null/undefined, constants, enum members, `await`/`async` keywords, CSS IDs |
| **Teal** | `#7AECD9` | Built-in / namespace | Built-in functions, primitives, regex literals, import/export keywords, namespaces, h4-h6 markdown headers |
| **Background** | `#1F2335` | Editor surface | Main editor background, gutter, peek view, breadcrumb bar, active tab |
| **Surface** | `#16161E` | Side surfaces | Sidebar, panel, status bar, title bar, activity bar (kept darker for contrast) |
| **Border** | `#3B4261` | Hairlines, separators | Indent guides (inactive), tree guides, group dividers, panel borders |
| **Border-strong** | `#414868` | Stronger separators | Editor widget borders, input borders |
| **Foreground** | `#C0CAF5` | Default text | Editor text, sidebar text, terminal text |
| **Foreground-bright** | `#CFD3F8` | Emphasized text | Active tab text, list item text, focused row |
| **Muted** | `#7280B0` | De-emphasized text | Comments, line numbers, inactive descriptions |
| **Muted-soft** | `#9AA5CE` | Soft secondary text | Inactive tab text, breadcrumb foreground |

## Architecture

### Layer 1+ — `settings.json` (zero RAM cost)

All polish that can be achieved through native Cursor / VS Code config. **No extension required.**

- **Workbench color overrides** (~280 surfaces) — every UI region tuned to the palette: notifications, peek view, diff editor (palette-tuned greens/reds), merge conflict markers, debug toolbar, breadcrumbs, inlay hints, sticky scroll, overview ruler, quick input, symbol icons (function/method/class/interface/variable/constant/etc.), terminal command decorations
- **Token color rules** (~45 rules) — covers regex literals (with distinct colors for character classes, quantifiers, anchors, groups), string escape sequences, async/await, JSDoc/docstrings, markdown headers tiered by level (H1=magenta, H2=blue, H3=cyan, H4-6=teal), import/export keywords, booleans/null/undefined, type aliases vs class instantiation, CSS class vs ID selectors, diff markers
- **Editor experience** — Fira Code with ligatures, semantic highlighting, sticky scroll, indent guides, breadcrumbs, custom title bar, custom window title template, refined minimap, padded editor (16px top/bottom), inlay hints on with refined font size, custom cursor width

### Layer 2 — `aurora-dusk.css` v5 "Aurora Axis" (≤6 MB cost)

A 1555-line static stylesheet that delivers the *calm-at-rest, fireworks-on-touch* doctrine. Chrome panels get whisper-soft CRT scanlines (~1% opacity, half of v4) so they recede; the editor pane gets ambient stage lighting + sunset horizon + vignette so it pops; widgets get 8-layer visionOS spatial shadows + Raycast light-catcher borders + Glassmorphism 2.0 saturate-lensing when summoned. Code text stays in the readable Tokyo Night palette.

**Hacker-tier visual moves (all static at idle):**

| # | Element | Trick |
|---|---|---|
| 1 | **CRT scan-lines on all chrome** | `repeating-linear-gradient` at 2-3% opacity, every 2px on sidebar/aux/panel/statusbar/titlebar. Rasterized once into a tile texture by the compositor → infinitely cheap |
| 2 | **Active line indicator** | Neon magenta→cyan→rose gradient bar on the left edge of the cursor's line via `border-image` |
| 3 | **Active tab** | Neon top border (3-stop gradient) + solid neon-magenta filename with 3-tier text-shadow glow + ambient outer shadow |
| 4 | **Tab hover (chromatic aberration)** | Inactive tab labels get an RGB ghost on hover via `text-shadow: -1px 0 rose, 1px 0 cyan` — looks like a glitchy CRT |
| 5 | **Cursor caret** | Vertical magenta→cyan gradient column + 4-tier neon halo (4px / 12px / 24px / 48px) |
| 6 | **Activity bar active item** | Hexagonal selection background via `clip-path: polygon()` with neon gradient fill, 1px neon border, and 18px+36px outer glow |
| 7 | **Activity bar hover** | Icon scales 1.12× + neon magenta + text-shadow halo |
| 8 | **Status bar** | Dual-axis segmented-LED display (vertical 2px scan + horizontal 3px scan) + neon rainbow top border with 12px glow |
| 9 | **Status bar items** | Hover gets 1px neon ring + 14px outer glow + neon text-shadow |
| 10 | **Sidebar / aux panel gradient column** | Each gets a vertical neon-rainbow `border-image` on its inner edge — looks like a fiber-optic strip |
| 11 | **Find widget** | 8 sci-fi corner brackets (14px × 1.5px) drawn with perpendicular `background-image` gradients. No SVG, no extra DOM |
| 12 | **Quick input / Cmd+Shift+P** | Glassmorphism: `backdrop-filter: blur(16px) saturate(160%)` + 16px corner brackets + 48px+96px outer glow — looks like a HUD popup |
| 13 | **Suggest widget** | Heavy glass (12px blur + 140% saturation), focused row gets neon gradient sweep with inset border glow |
| 14 | **Inline chat / composer focus** | `@property --aurora-angle` + single-fire 1.4s `aurora-sweep` — conic-gradient rainbow border revolves once around the input then locks. Zero animation cost at idle. |
| 15 | **Buttons** | 4-tier neon hover stack (1px ring + 12px tight + 28px cyan + 56px rose) + text glow + press feedback |
| 16 | **Diff editor** | Neon green/rose scan-beam gradients fading right-to-transparent (instead of flat tints) |
| 17 | **Notifications** | 4px gradient `border-image` left accent + 12px backdrop-blur + 24px ambient glow |
| 18 | **Window controls** | 16px neon halo + 1px inset ring + 32px cyan ambient on hover |
| 19 | **Title bar** | CRT scan-lines + rainbow `border-image` bottom hairline + soft magenta ambient |
| 20 | **Sidebar section headers** | UPPERCASE 11px tracking-wide labels with magenta→cyan gradient underline + magenta text-shadow halo |
| 21 | **Editor group header** | Neon rainbow gradient bottom rule + ambient magenta shadow |
| 22 | **Peek view** | 2px neon rainbow gradient title border + 18px ambient glow |
| 23 | **Bottom panel** | Neon rainbow gradient top border |
| 24 | **Sticky scroll** | 2px gradient `border-image` separator that brightens to neon-magenta in the center |
| 25 | **Minimap slider** | ALWAYS gradient (not just on hover) — magenta→cyan with neon brighten on hover/active |
| 26 | **Scrollbar slider** | ALWAYS gradient with neon hover and active states |
| 27 | **Breadcrumbs tail** | Gradient text via `background-clip: text` (magenta→cyan) |
| 28 | **List rows** | Neon gradient sweep on hover (magenta-to-transparent), focused+selected gets inset border glow |
| 29 | **Badges** | Magenta→rose gradient pill with 10px+20px neon shadow stack |
| 30 | **Progress bar** | Full 4-stop neon rainbow (magenta→cyan→gold→rose) with neon glow |
| 31 | **Bracket-pair active guide** | Neon magenta with 6px glow |
| 32 | **Inputs** | Focused inputs get 1px neon ring + 16px tight glow + 32px cyan ambient |

**v4 "Pulse" iteration adds (all single-fire on hover/active — free at idle):**

| # | Element | Trick |
|---|---|---|
| 33 | **Buttons — rotating gradient on hover** | CSS `@property --btn-angle` + 1.2s `forwards` keyframe rotates a 5-stop conic-gradient border ONCE around the button when hovered. Free at idle, fires per hover-enter. |
| 34 | **Buttons — glitch on click** | 220ms single-fire `glitch-press` keyframe combines `filter: hue-rotate(±30deg)` + `transform: translate(±1px)` for an RGB-displacement effect on every press. |
| 35 | **Activity bar inactive icons — hex sweep on hover** | `@property --hex-angle` + 1.5s `forwards` keyframe rotates a hexagonal `clip-path` conic-gradient ghost behind unselected icons when hovered. |
| 36 | **Tab dirty indicator** | The `•` modified-file dot gets neon-magenta color + 14px text-shadow halo |
| 37 | **Tab close button** | Hover triggers `rotate(90deg) scale(1.18)` + neon-rose color + 16px text-shadow halo |
| 38 | **Workbench inset glow** | 1px neon-magenta inset outline + 48px ambient + 96px cyan ambient on the entire workbench. Painted once, cached. |
| 39 | **Aux panel hex dot grid** | `radial-gradient` 1px dots on a 24×24 grid layered ON TOP of the existing scanlines — Tron-style holographic surface |
| 40 | **Cursor chat — message bubbles** | Each message gets a magenta→cyan gradient `border-image` left rail + soft hover background sweep |
| 41 | **Cursor chat — tool call boxes** | 8×8px corner brackets via the same 4-gradient pattern as the find widget + ambient magenta glow |
| 42 | **Cursor chat — context pills** | Magenta outlined pill with gradient bg; hover doubles the bg gradient intensity + adds 24px outer glow |
| 43 | **Code lens** | Italic magenta hint above functions; hover brightens to neon-magenta with 6px text-shadow |
| 44 | **Parameter hints widget** | 10px corner brackets + 10px backdrop-blur + active parameter gets neon-magenta with text-shadow |
| 45 | **Inlay hints** | Subtle gradient pill (cyan→magenta) with rounded corners + 1px cyan outline |
| 46 | **Hover widget corner brackets** | 12px sci-fi corner brackets matching the find widget aesthetic |
| 47 | **Breadcrumb hover underline** | 1px gradient line grows from left via `transform: scaleX(0→1)` over 250ms |
| 48 | **Notification close button** | Hover = `rotate(90deg) scale(1.15)` + neon-rose + 8px halo |
| 49 | **Editor scrollbar shadow** | Magenta-tinted inset glow instead of black |
| 50 | **Breakpoint glyphs** | Neon-rose halo + `scale(1.18)` on hover |
| 51 | **Lightbulb / quick-fix** | Neon-gold color + 18px halo + scale on hover |
| 52 | **Extension list titles** | Magenta→cyan gradient text via `background-clip: text` |
| 53 | **Suggest widget icon** | Focused row icon gets 8px neon-magenta text-shadow |

**v5 "Axis" iteration adds (research-driven; calm at rest, fireworks on touch):**

| # | Element | Trick | Inspiration |
|---|---|---|---|
| 54 | **Chrome restraint** | CRT scanline alpha cut 50% (0.020 → 0.010), rainbow column accents cut 70% (now whisper-thin). Chrome recedes so editor pops. | Linear UI refresh 2026 |
| 55 | **Editor sunset horizon** | Static 20%-tall purple→magenta `linear-gradient` at the bottom of every editor pane. Looks like sunset over the code. | Synthwave '84 |
| 56 | **Editor stage lighting** | Three corner radial-gradients on the editor (cyan top-left, magenta top-right, rose bottom-right) at 2-3% opacity. Ambient HUD lighting. | Pacific Rim Loccent / JARVIS |
| 57 | **Editor vignette** | Inset `box-shadow` (80px + 160px black at 10-20% alpha) on every editor pane. Subtle "looking through a window" depth. | visionOS / cinema |
| 58 | **visionOS spatial shadows** | All popups (quick input, suggest, hover, find, notifications, parameter hints) get 5-layer ambient shadow stacks (1px → 32px → 64px) + 2-layer colored neon halos + top-edge inset highlight. Real depth. | visionOS depth model |
| 59 | **Raycast light-catcher borders** | Every glass widget gets `1px solid rgba(255,255,255,0.06-0.10)` simulating light catching the edge of a glass surface. | Raycast design system |
| 60 | **Glassmorphism 2.0 lensing** | All `backdrop-filter` calls bumped from `saturate(160%)` → `saturate(180%) brightness(1.05)`. Colors behind the glass *pop* through it. | Glassmorphism 2.0 (2026) |
| 61 | **3D button hover tilt** | `perspective: 800px` + `rotateX(2deg) rotateY(-1deg)` on `:hover`, inverse rotate on `:active`. Buttons "come toward you" then push back. Premium. | visionOS / Linear |
| 62 | **Boot prompt cinematic** | Single-fire 1.4s `axis-boot` keyframe on `.monaco-workbench::after`: ASCII text `▶ AURORA::AXIS · CONN-POD ONLINE · CLEARANCE GRANTED` fades in (letter-spacing animates 12px → 6px), holds, fades out. Plays once on every window mount, then `opacity: 0` forever. ~1.4s of GPU work then $0. | Cinematic boot sequences |
| 63 | **Mask-image list fade** | Sidebar + auxbar list bottoms get `mask-image: linear-gradient(black, transparent)` — items fade out softly at the scroll boundary instead of harsh cut. | Linear's "calmer interface" refresh |
| 64 | **Phosphor terminal CRT** | Just the terminal panel (xterm-screen, xterm-viewport) gets green-tinted scanlines (`rgba(0, 255, 130, 0.022)` every 2px + secondary line every 6px). Mr. Robot phosphor vibe, scoped to the actual terminal. | Mr. Robot / amber phosphor CRT |
| 65 | **Refined corner radii** | All popup widgets bumped to `border-radius: 8px` (from 4-5px) for visionOS-friendly geometry. Buttons → 8px, button gradient borders → 10px. | visionOS corner language |

### What Aurora **does NOT** do (by design)

| Anti-pattern | Why we avoid it |
|---|---|
| `position: fixed` overlays (steering wheels, radars, watermarks) | Allocate full-viewport GPU buffers, force constant compositor passes |
| `filter: blur()` / `drop-shadow()` on large elements | Each filter creates an offscreen render buffer at element size |
| `backdrop-filter` on **large** surfaces | Reads & blurs everything behind the element on every paint |
| `mix-blend-mode` on large surfaces | Forces dedicated compositor passes |
| Infinite `@keyframes` animations | Constant repaints forever, even when the editor is idle |
| Embedded SVGs with `<animate>` SMIL tags | Run independent animation pipelines parallel to CSS |
| `:has()` on common DOM nodes (`.codicon-loading`, `.tab`, `.row`) | Re-evaluated on every DOM mutation — in an editor, that's constant |
| Base64 SVGs above 1KB embedded in CSS | Increase parsed-CSS size, slow down style recalculation |
| `text-shadow` on dense text panels | Each shadow is a per-glyph offscreen render |

### What we DO use (that looks expensive but isn't)

| Technique | Why it's free |
|---|---|
| `conic-gradient`, `linear-gradient`, `repeating-linear-gradient` | Painted once when the element first renders; cached as a texture by the compositor |
| `clip-path: polygon(...)` | One-time GPU mask op; cached; no per-frame cost |
| `background-clip: text` (gradient text) | Text is masked against a static gradient; rendered once per font cache hit |
| `box-shadow` with multiple layers on **small** elements (cursor, badges, window controls, status items) | Cheap because shadow cost scales with element area — a 2px cursor's halo costs ~2µs per repaint |
| `border-image` with linear/conic gradients | Treated like a regular border background — painted once |
| `backdrop-filter: blur` on **small** popups (suggest, hover, command palette) | Compositor reads + blurs the area behind the popup once when it appears, then caches the result. ~30ms one-time cost. |
| `transition:` on hover/focus/active | Only fires during user interaction. Idle = zero. |
| Single-fire `animation: ... forwards` triggered by `:focus-within` | Runs once per focus event then locks at the end frame. ~1.6s of compositor work per focus, then 0. |
| CSS `@property` + animatable `<angle>` for sweep effects | Built-in browser primitive. The angle interpolation happens on the GPU. |

## Memory Footprint Comparison

| Theme | Approx. extra RAM (renderer) | Visual feel |
|---|---|---|
| Default Dark+ (no overrides) | 0 MB | Stock VS Code |
| Previous Dusk (JSON only, ~100 colors) | 0 MB | Pleasant but flat |
| Aurora Dusk v1 (Layer 1+ JSON + Layer 2 static CSS) | ~2 MB | Pleasant + accent discipline |
| Aurora Neon v2 | ~2-3 MB | Brighter, more interactive |
| Aurora Terminal v3 (hacker mode) | ~3-4 MB | Terminal-grade scanlined chrome |
| Aurora Pulse v4 (interactive fireworks) | ~3-5 MB | + button conic sweeps, hex hover, gradient text |
| **Aurora AXIS v5 (calm at rest, fireworks on touch)** | **~4-6 MB** | Linear-quiet chrome + Synthwave editor + visionOS popups |
| Ferrari v7 "Conn-Pod" (archived) | ~150-200 MB | Vegas casino at 3 a.m. |

## Installation

### Prerequisites

```bash
brew install --cask font-fira-code
cursor --install-extension be5invis.vscode-custom-css
```

### Apply

1. Copy `aurora-dusk.css` to your Cursor user themes folder:
   ```bash
   cp aurora-dusk.css "$HOME/Library/Application Support/Cursor/User/themes/"
   ```

2. Merge `settings-snippet.json` into your `settings.json` at `$HOME/Library/Application Support/Cursor/User/settings.json`. The snippet contains:
   - All editor experience flags (font, ligatures, sticky scroll, etc.)
   - The full `workbench.colorCustomizations[Default Dark+]` block
   - The full `editor.tokenColorCustomizations[Default Dark+]` block
   - The `vscode_custom_css.imports` entry pointing at the CSS file

3. Run **"Enable Custom CSS and JS"** from the command palette (`Cmd+Shift+P`).

4. Reload window. macOS may show a one-time "Cursor is corrupted" warning — this is expected, it's the cost of the `vscode_custom_css` extension patching the renderer. Click "OK" and you're done.

### Update path after Cursor upgrades

Each time Cursor updates, you may need to re-run **"Enable Custom CSS and JS"** to re-inject the stylesheet. The settings.json customizations persist automatically.

## Files

| File | Purpose |
|---|---|
| `aurora-dusk.css` | The Layer 2 stylesheet (1555 lines, v5 "Aurora Axis" — strict zero-RAM rules + Glassmorphism 2.0 on small popups only) |
| `settings-snippet.json` | The Layer 1+ portable settings block (70 keys) |
| `README.md` | This file |

## Version History

| Version | Codename | Headline change |
|---|---|---|
| v1 | Aurora Dusk | Initial JSON + lightweight static CSS, accent discipline |
| v2 | Aurora Neon | Brighter, more saturated, more contrasting |
| v3 | Aurora Terminal | Hacker mode — CRT scanlines, chromatic aberration, neon-tier glows |
| v4 | Aurora Pulse | Interactive fireworks — button conic sweeps, hex hover, gradient text, chat polish |
| **v5** | **Aurora AXIS** | **Calm at rest, fireworks on touch — Linear-quiet chrome + Synthwave editor sunset + visionOS spatial widgets** |

## Rollback

To go back to plain Default Dark+ with no customizations:

1. Remove the `aurora-dusk.css` from `vscode_custom_css.imports` (set to `[]`)
2. Run **"Disable Custom CSS and JS"** from the command palette
3. Optionally delete the `[Default Dark+]` blocks from `workbench.colorCustomizations` and `editor.tokenColorCustomizations`

To switch to the Ferrari "Screencast Mode" theme for demos, see [`../ferrari-scuderia-f1/`](../ferrari-scuderia-f1/).
