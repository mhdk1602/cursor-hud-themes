# Scuderia F1 — Ferrari SF-26 Edition · **PIT WALL HUD v7 "CONN-POD ONLINE"**

> *"Lights out and away we go."*

---

> ## ⚠️ ARCHIVED — "Screencast Mode" Only
>
> **As of May 2026, this theme is no longer the daily driver.** It has been archived as `screencast-mode.css` because the runtime overhead — 8 fixed-position SVG overlays, 9 infinite `@keyframes` animations, multiple `filter: drop-shadow()` declarations, and base64-embedded animated SVGs with SMIL — was consistently pushing the Cursor renderer to ~200MB+ extra RAM and causing UI thrash on long-running editor sessions.
>
> **Use only when:**
> - Recording a screencast or demo video (the visual density reads great on camera)
> - Showing off the Cursor IDE to clients or in a deck
> - You've quit every other Electron app and have RAM headroom to burn
>
> **Daily driver replacement:** `cursor-themes/aurora-dusk/` — same Tokyo Night-derived palette, magenta + rose accent split, but built with strict zero-runtime-cost discipline.
>
> **To enable Screencast Mode:**
> ```bash
> cp cursor-themes/ferrari-scuderia-f1/screencast-mode.css \
>    "$HOME/Library/Application Support/Cursor/User/themes/tron-neon-glow.css"
> ```
> Then add `"file:///Users/<you>/Library/Application Support/Cursor/User/themes/tron-neon-glow.css"` to `vscode_custom_css.imports` in settings.json and run "Enable Custom CSS and JS" from the command palette.

---

A Cursor IDE theme inspired by Scuderia Ferrari's 2026 SF-26 livery **and** the LOCCENT mission-control density of Pacific Rim's Shatterdome. Each panel becomes a codenamed station with status badges, telemetry, scan lines, plasma exhaust vents, animated radar, sparkline graphs, and a per-file dossier card. Not a color theme — a **command center skin** for your IDE.

**v6 finishes the Conn-Pod.** Every region of the workbench has:
- A codename label (`▸ GARAGE :: ASSET BAY`, `▸ TELEMETRY :: COMMS UPLINK`, `▸ STRATEGY :: RACE ENGINEER`)
- A pulsing status badge (`● LIVE`, `● ACTIVE`, `FP-2 ● CLASSIFIED`)
- Angular HUD corner frames with notched cutouts (Pacific Rim style)
- Live race-data telemetry strip in the status bar (`ERS 87% │ TIRE C3 │ DRS ENABLED │ BAL +2 │ LAP 1:18.347`)
- A drifting horizontal scan line through the editor every 8s (LOCCENT scanning)
- Pulsing plasma exhaust vents above the status bar
- A slowly-rotating halo behind the steering-wheel watermark

**v6 adds the four "Shatterdome elements"** the v5 was still missing:

1. **Per-file dossier card** — a small classification HUD that appears in the top-right of the editor and changes its content based on the active file's extension. Open a `.py` file and it reads `▸ PYTHON :: NEURAL ASSET MODULE / CLEARANCE: BCG-AI-LEAD / VER 3.11.7 ● ACTIVE`. Open a `.sql` file and it switches to `▸ SQL :: DATA STREAM PIPELINE / DIALECT: POSTGRES 16 / QUERY ENGINE ● READY`. Powered by CSS `:has()` matching `aria-label` of the active tab — 14 file types covered out of the box.
2. **Animated radar** — a fully-animated SVG radar with rotating sweep beam, four pulsing blips at different frequencies, concentric range rings, compass cardinals, and a glowing center dot. Sits at the bottom of the workbench beside the steering wheel.
3. **Telemetry sparklines panel** — an SVG card with three live displays: a `PLASMA CORE TEMP` waveform that morphs over 6 seconds, a `TIRE WEAR · C3` percentage bar that subtly oscillates, and a `POWER OUTPUT · MGU-K` segmented bar with a flashing redline cell. Bottom of workbench, left of the radar.
4. **SF-26 mech profile** — a stylized front-view F1 car silhouette (replacing v5's plain SF shield) embedded in the title bar far-right. Halo + nose + front wing + helmet visible, gold endplate stripes, `▸ MACRO · SF-26 PROFILE` callsign header with a pulsing `LIVE` dot.

All four are pure-SVG (animated via SVG's native `<animate>` and `<animateTransform>` — no JS needed), embedded as base64 data URIs in the CSS for one-file portability.

## What Makes This Theme Different

Most IDE themes apply colors. This one renders an **F1 cockpit overlay** on top of your editor with three coordinated visual systems:

1. **Steering Wheel HUD (in the editor pane)** — a full Ferrari-style steering wheel watermark in the bottom-right corner of the editor itself, with a 15-LED rev counter (green → amber → red → blue shift indicator), center display showing gear "7" and "312 KPH", Scuderia Ferrari shield, DRS / BOX buttons, rotary differential and brake-balance dials, and paddle shifter hints. Anchored to `.part.editor > .content` so it lives **inside** the editor — the chat panel and terminal sit BESIDE the editor, never on top of it, so the wheel is never blocked. Responsive via media queries: shrinks gracefully when you open the chat panel and tucks tighter into the corner.

2. **F1 Rev Counter (in the activity bar)** — a vertical 5-LED telemetry strip in the dedicated **ENG** section of the activity bar (the leftmost strip of the IDE — always visible, never blocks any UI). The lights are not a passive loop: they **react to actual activity**.
   - **Idle**: bottom green LED slowly breathes (engine running, system ready).
   - **Action**: when ANY loading spinner is present in the workbench (agent thinking, file save, command running, autocomplete fetching, indexing, syncing), the full rev sequence fires — green → amber → red → all-on → BLUE SHIFT flash → reset, looping until the action completes. Triggered via CSS `:has(.codicon-loading.codicon-modifier-spin)` and friends.

3. **Drifting Racing Stripes** — diagonal Rosso Corsa + Pirelli white speed lines that subtly drift across the entire workbench background, anchored fixed to the viewport with `mix-blend-mode: screen` so they only ADD light over dark areas (never muddy text).

Plus the rest of the cockpit:

- **Animated HUD corners** on sidebar, panel, and auxiliary bar panes
- **Breathing glow** that pulses across all major panels
- **Tachometer-style tab indicator** — active tabs glow with a traveling red/gold gradient
- **Power Mode** particles tuned to red glow
- **Carbon fiber grid** background pattern

## Why It's Always Visible (v3 architecture)

Earlier versions of this theme had two visibility bugs:

- **v1**: watermark on `.part.editor > .content::after` got hidden when a terminal or panel covered the editor.
- **v2**: watermark on `.monaco-workbench::after` (fixed positioning, `z-index: 9999`) was theoretically global, but `mix-blend-mode: screen` made it nearly invisible against the dark-red auxiliary bar (chat panel) background, AND the auxiliary bar's stacking context interfered with the z-index.

**v3 (current)** fixes both:

- The wheel is anchored to `.part.editor > .content::after` with `position: absolute`. The editor pane is the most reliably-visible region of the workbench — chat and terminal sit BESIDE it, never on top. The wheel scales/moves with the editor and is **never blocked**. `mix-blend-mode` is removed entirely; we use a plain semi-transparent overlay.
- The F1 lights are moved out of the title bar (where they overlapped the search bar) into a dedicated section of the activity bar, where they don't block any UI and are always visible.
- A `:has()` selector ties the rev-counter animation to actual loading state, so the lights now **mean something** instead of looping in the background.

## Color Palette

| Name            | Hex       | Usage                                      |
|-----------------|-----------|---------------------------------------------|
| Rosso Corsa     | `#FF2020` | Primary accent — keywords, borders, glows   |
| Bright Red      | `#FF4444` | Functions, bracket pairs, cursor            |
| Cherry Red      | `#FF1744` | `self`/`this`, errors, redline LEDs         |
| Gold / Amber    | `#FFB800` | Strings, highlights, badge accents          |
| Shell Gold      | `#FFA000` | Decorators, git modified                    |
| Pirelli Yellow  | `#FFEE00` | Numbers, warnings, badges, SF shield        |
| Orange Flame    | `#FF6B20` | Types, class names                          |
| Pirelli White   | `#F5F5F5` | 2026 SF-26 livery accent (subtle stripes)   |
| Carbon Grey     | `#6A5555` | Comments                                    |
| Wine Black      | `#0E0608` | Editor background                           |
| Deep Carbon     | `#0A0406` | Sidebar / panel backgrounds                 |
| Pit Dark        | `#080304` | Activity bar / title bar                    |

## Installation

### Prerequisites

- [Cursor IDE](https://cursor.sh/)
- [Custom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css) extension

### Steps

1. **Copy the CSS file** to your Cursor user themes directory:

   ```bash
   mkdir -p ~/Library/Application\ Support/Cursor/User/themes/
   cp ferrari-scuderia-f1.css ~/Library/Application\ Support/Cursor/User/themes/
   ```

2. **Add the CSS import** to your `settings.json`:

   ```json
   "vscode_custom_css.imports": [
       "file:///Users/YOUR_USERNAME/Library/Application%20Support/Cursor/User/themes/ferrari-scuderia-f1.css"
   ]
   ```

3. **Copy the color settings** from `settings-snippet.json` into your `settings.json` under `workbench.colorCustomizations` and `editor.tokenColorCustomizations`.

4. **Activate the theme**:
   - Open Command Palette (`Cmd+Shift+P`)
   - Run `Reload Custom CSS and JS`
   - Run `Developer: Reload Window`

### Optional Extensions

These extensions enhance the experience but are not required:

| Extension | Setting |
|-----------|---------|
| **Power Mode** | Particles with red glow filter |
| **Material Icon Theme** | Folder color set to `#FF2020` |
| **VSCode Animations** | Slide + Indent transitions |
| **Error Lens** | Gutter icons + message background mode |

## Files

| File | Description |
|------|-------------|
| `ferrari-scuderia-f1.css` | Custom CSS — animations, glows, HUD corners, steering wheel watermark, F1 starting lights, drifting racing stripes |
| `steering-wheel.svg` | Source SVG for the Ferrari F1 steering wheel HUD watermark (for editing; the CSS uses a base64-encoded copy) |
| `velocity-core.svg` | Legacy V12 turbine SVG from the previous version (kept for reference) |
| `settings-snippet.json` | Color customization settings to paste into your `settings.json` |

## Animation Details

| Animation | Duration | Trigger | Effect |
|-----------|----------|---------|--------|
| `scan-line-drift` | 8s | always | Red 2px scan line drifts top-to-bottom across the editor (LOCCENT scanning) |
| `status-blink` | 1.6–2s | always | `● LIVE` and `● ACTIVE` badges pulse with hard cardiac rhythm |
| `telemetry-tick` | 3–4s | always | Status-bar race telemetry + sidebar `FP-2 ● CLASSIFIED` badge fade in/out subtly |
| `plasma-vent` | 3s | always | Three radial-gradient exhaust glows pulse above the status bar |
| `halo-spin` | 24s | always | Conic-gradient halo ring rotates slowly behind the steering wheel |
| `data-stream` | n/a | reserved | Used by future scrolling-data overlays |
| `f1-idle-pulse` | 2.6s loop | always | Activity-bar bottom LED slowly breathes green — "engine running" |
| `f1-rev-counter` | 2.4s loop | `:has(.codicon-loading.codicon-modifier-spin)` etc. | Activity-bar rev counter fires green→amber→red→BLUE SHIFT flash whenever any loading spinner is in the DOM (agent thinking, save, command run, autocomplete, indexing) |
| `wheel-wobble` | 6s | always | Steering wheel rotates ±4° back and forth, mimicking driver micro-corrections |
| `rev-pulse` | 2.4s | always | Steering wheel rev-counter LEDs glow brighter and dimmer in sync with the engine |
| `stripe-drift` | 18s | always | Diagonal racing stripes translate across the workbench background |
| `glow-breathe` | 5s | always | Panels pulse with inner red glow |
| `border-travel` | 2.5–3s | always | Active tab/activity bar indicator streams with red-gold gradient |
| `border-pulse` | 2s | always | HUD corner brackets fade in/out |
| `hud-flicker` | 2.5s | always | Badges and find widget occasionally flicker |
| `arc-reactor-glow` | 1.5s | always | Lightbulb icons breathe with red glow |

## PIT WALL Stations (v5 + v6)

Each panel is now a codenamed mission station:

| Panel              | Codename                                | Badge                   | Color    |
|--------------------|-----------------------------------------|-------------------------|----------|
| Title bar          | `▌SCUDERIA FERRARI :: SF-26 :: HOT LAP` | (F1 lights v4 + SF-26 mech profile v6)  | Rosso    |
| Sidebar            | `▸ GARAGE :: ASSET BAY`                 | `FP-2 ● CLASSIFIED`     | Amber    |
| Editor (top-right) | Per-file dossier card (varies by extension) | dossier text       | Amber    |
| Editor (frame)     | Notched HUD corners + drifting scan line| (the scan line itself)  | Rosso    |
| Activity bar       | `ENG` label                             | (rev-counter LEDs)      | Green→Red |
| Terminal / panel   | `▸ TELEMETRY :: COMMS UPLINK ● LIVE`    | `● LIVE`                | Rosso    |
| Aux bar (chat)     | `▸ STRATEGY :: RACE ENGINEER`           | `● ACTIVE`              | Amber    |
| Status bar         | `ERS 87% │ TIRE C3 │ DRS ENABLED │ BAL +2 │ LAP 1:18.347` | (plasma vents above)    | Amber    |
| Bottom-center      | **Telemetry sparklines** (plasma temp + tire wear + power) [v6] | `● ACTIVE` |  Rosso/Amber |
| Bottom-center-right| **Radar** with rotating sweep + pulsing blips [v6]            | (cardinal markings)     | Rosso    |
| Bottom-right       | Steering wheel watermark + rotating halo| (the wheel itself)      | Rosso    |

## File Dossier — supported extensions (v6)

The dossier card auto-detects the active tab's file type. Currently mapped:

| Extension     | Dossier classification                                 |
|---------------|--------------------------------------------------------|
| `.py`         | `▸ PYTHON :: NEURAL ASSET MODULE`                      |
| `.sql`        | `▸ SQL :: DATA STREAM PIPELINE`                        |
| `.md`         | `▸ MARKDOWN :: DOSSIER ARCHIVE`                        |
| `.css`        | `▸ CSS :: HUD COMPILER`                                |
| `.json`       | `▸ JSON :: CONFIG MATRIX`                              |
| `.ts` / `.tsx`| `▸ TYPESCRIPT :: REACTOR CORE`                         |
| `.js` / `.jsx`| `▸ JAVASCRIPT :: PROPULSION UNIT`                      |
| `.html`       | `▸ HTML :: COCKPIT FRAME`                              |
| `.yml` / `.yaml`| `▸ YAML :: PIT CREW SPEC`                            |
| `.sh` / `.zsh` / `.bash` | `▸ SHELL :: PIT RADIO`                      |
| `.pdf`        | `▸ PDF :: DOSSIER ARCHIVE`                             |
| `.txt`        | `▸ TXT :: COMMS LOG`                                   |
| `.csv`        | `▸ CSV :: TELEMETRY EXPORT`                            |
| `.mdc`        | `▸ MDC :: AGENT DIRECTIVE`                             |

To add a new extension, append a rule like:

```css
.monaco-workbench:has(.tab.active[aria-label$=".rs"]) .editor-group-container::before {
  content: "▸ RUST :: BORROW CHECKER\A   EDITION: 2024\A   CARGO  ●  READY" !important;
}
```

## v7 cinematic features (CONN-POD ONLINE)

v7 makes the IDE *feel* alive. Every state has visual response:

| ID  | Feature                       | Where it appears                              | Triggered by                                                         |
|-----|-------------------------------|------------------------------------------------|----------------------------------------------------------------------|
| D1  | Bootup sequence               | Full-screen overlay, plays once on launch      | Page load (each Cursor open / custom-CSS reload)                     |
| B1  | Agent CRT static              | Chat panel background gets animated noise      | Any spinner active (`:has(.codicon-loading.codicon-modifier-spin)`)  |
| D3  | Race flag overlay (yellow)    | Top-left of editor, waving banner              | Linter warning present (`:has(.codicon-warning):not(:has(.codicon-error))`) |
| D3  | Race flag overlay (red)       | Top-left of editor, RED FLAG SESSION HALTED    | Linter error present (`:has(.codicon-error)`)                        |
| A2  | Cockpit lock indicator        | Focused panel flares; non-focused panel dims   | `:focus-within` on editor or chat                                    |
| C1  | Tire wear gauge               | Bottom-center of viewport (4-tire SVG)         | Always                                                               |
| A1  | Cursor arc reactor            | Text cursor breathing halo                     | Always while editor is focused                                       |
| C2  | Pit board                     | Top-right of viewport (vertical lap times)     | Always (hidden below 1500px viewport)                                |
| C3  | Engine RPM bar                | Bottom edge of title bar                       | Always (oscillates 30%–92% width)                                    |
| E1  | Command palette = PIT RADIO   | Banner above Cmd+P widget                      | Cmd+P opens palette                                                  |
| E3  | Find widget = DRS ENABLED     | Green badge above find widget                  | Cmd+F opens find widget                                              |
| E4  | Tab fly-in animations         | New tabs slide from right                      | Tab is created                                                       |
| F1  | Helmet visor scratches        | Top of editor (subtle diagonal pattern)        | Always                                                               |
| F2  | Heat haze                     | Bottom edge of editor (animated blur)          | Always                                                               |
| F3  | Attendance counter            | Title bar far-right (`ATTENDANCE 156,847 ▲`)   | Always                                                               |
| G1  | TURBO mode                    | Stripes & rev counter ~3× speed                | All major panels open AND a spinner is active                        |
| G3  | CHAMPIONSHIP P1 status        | Gold "▲ P1 · ON PACE" badge bottom-left        | No errors AND no spinners                                            |

## Versions / Rollback

Previous versions are preserved in `versions/` for rollback:

| Version | File                              | Description                                                       |
|---------|-----------------------------------|-------------------------------------------------------------------|
| v5      | `versions/v5-pit-wall.css`        | PIT WALL HUD without the 4 final HUD widgets                      |
| v6      | `versions/v6-conn-pod.css`        | Adds dossier card, radar, sparklines, mech profile                |
| v7      | `versions/v7-conn-pod-online.css` | Current — adds bootup, CRT static, race flags, cockpit lock, tires, arc reactor cursor, pit board, RPM bar, palette/find skins, tab animations, visor scratches, heat haze, attendance counter, TURBO mode, P1 badge |

To roll back to v5, copy that file over `~/Library/Application Support/Cursor/User/themes/tron-neon-glow.css` and reload custom CSS.

The four v6 source SVGs (radar, sparklines panel, mech profile) are also preserved in `svgs/` for editing — re-base64 and re-embed in the CSS to update.

## SVG Watermark: F1 Steering Wheel

The `steering-wheel.svg` is a custom-designed Ferrari SF-style steering wheel rendered in pure SVG, featuring:

- **Carbon-fiber main body** — rectangular top, round bottom (the modern F1 wheel silhouette), with linear-gradient carbon fiber fill and Rosso Corsa rim outline
- **15-LED rev counter** at the top — five green LEDs (low/mid RPM) → five amber LEDs (high RPM) → three red LEDs (redline) → two blue LEDs (SHIFT NOW indicator). Each LED has a glowing core via `feGaussianBlur` filter
- **Center digital display** — black screen with red glow, showing current gear "7" in bold and "312 KPH" in Pirelli amber
- **Scuderia Ferrari shield** — yellow shield with black "SF" between the LEDs and the display screen
- **Dual grip handles** — angled ellipses with horizontal grip-texture lines on both sides
- **Buttons** — red **DRS** (Drag Reduction System), blue **BOX** (pit signal), and amber utility buttons
- **Rotary dials** — **DIFF** (differential) and **BBAL** (brake balance) at the bottom, with indicator pointers
- **Paddle shifters** — gold curved hints peeking from behind the wheel edges
- **Status indicator dots** — green/amber/red strip across the bottom (telemetry-style)

The SVG is embedded directly in the CSS as a base64 data URI for reliable loading in Cursor's Electron environment.

## How the Layered HUD Works

Three independent CSS layers, each anchored to a different region:

```
┌─────────────────────────────────────────────────────────────────────┐
│  STEERING WHEEL HUD          ← .part.editor > .content::after         │
│  position: absolute            opacity 0.65, no blend mode            │
│  Lives INSIDE the editor pane. Editor is always visible (chat &       │
│  terminal sit BESIDE it, not on top), so the wheel is always visible. │
│  Responsive: shrinks at 1600px and 1100px viewport widths.            │
├─────────────────────────────────────────────────────────────────────┤
│  DRIFTING RACING STRIPES     ← .monaco-workbench::before              │
│  position: fixed, z-index: 9998, mix-blend-mode: screen               │
│  Floats above the entire workbench, only ADDS light over dark areas.  │
├─────────────────────────────────────────────────────────────────────┤
│  F1 REV COUNTER + ENG LABEL  ← .part.activitybar::before / ::after    │
│  position: absolute, z-index: 10                                      │
│  Dedicated section in the leftmost activity bar. NEVER blocks any UI. │
│  Idle: dim green heartbeat. Action: full rev sequence triggered by    │
│  :has(.codicon-loading.codicon-modifier-spin) — fires whenever ANY    │
│  loading spinner appears (agent thinking, save, command, autocomplete,│
│  indexing, syncing).                                                  │
├─────────────────────────────────────────────────────────────────────┤
│  Cursor's normal UI                                                   │
└─────────────────────────────────────────────────────────────────────┘
```

### Why each layer was placed where it is

- **Wheel inside the editor**: solves the "where do I put it so it's never blocked?" problem definitively. The editor is the largest, most-always-visible region, and chat/terminal panels sit beside it (not on top). Anchoring the wheel inside the editor with `position: absolute` means it scales with the editor and stays in the corner regardless of layout.
- **Stripes on the workbench**: cosmetic background motion that should cover everything, so it gets `position: fixed` + `mix-blend-mode: screen` to layer over every panel without obscuring text.
- **Lights in the activity bar**: a dedicated leftmost strip that's always visible and has no functional UI in its center area. Perfect home for a small "telemetry" section. The `:has()` trigger turns the lights into a real activity indicator instead of decorative noise.

## Credits

Built for BCG's AI Engineering team by Hari. Inspired by the Ferrari SF-26's 2026 livery reveal and the seven seconds before "lights out."
