# Acrylic / Frosted Glass Design Language

This document distills the visual system, components, and interaction
patterns from your CSS into a reusable design language. Use it as a
blueprint to replicate the same aesthetic and UX in new projects.

------------------------------------------------------------------------

## 1) Core Principles

-   **Acrylic over dark photography**: Content sits on translucent panes
    with blur, over a fixed, high‑resolution background image.
-   **Low‑chroma neutrals + cool accents**: Text uses soft grays;
    accents remain white and desaturated teal‑gray alphas.
-   **Soft geometry**: 6--12px radii, 1px hairline borders, subtle depth
    via translucency rather than shadows.
-   **Readable at small sizes**: Base type 14px with compact spacing;
    careful contrast on glass.
-   **Responsive-first**: Two tuned breakpoints (≤768px and ≤480px)
    increase opacity/blur, spacing, and tap targets.

------------------------------------------------------------------------

## 2) Design Tokens

Declare these in `:root` and reference everywhere.

``` css
:root {
  --bg-color: #0c0c0d;                 /* page/base backdrop */
  --text-color: #e0e0e0;               /* primary text */
  --text-muted-color: #97b1b9;         /* secondary text */
  --border-color: rgba(151,177,185,.2);/* hairline borders */
  --accent-color: #ffffff;              /* highlights/active */
  --section-bg-color: rgba(255,255,255,.03);
  --button-bg-color: rgba(151,177,185,.15);
  --button-hover-bg-color: rgba(151,177,185,.3);
}
```

**Alpha scale (guideline):** 0.03, 0.05, 0.08, 0.10, 0.12, 0.15, 0.20,
0.30, 0.40 --- choose per surface hierarchy (see §4).

**Blur scale:** 10px (content panes), 20px (title bar), 25px (mobile
title bar).

**Radii scale:** 4px (logos), 6px (controls), 8px (sections/cards), 10px
(mobile buttons/inputs), 12px (containers).

**Stroke:** 1px solid using `--border-color` (increase to 0.3--0.4 alpha
on hover/active for affordance).

------------------------------------------------------------------------

## 3) Typography

-   **Family**: `Satoshi`, with
    `-apple-system, BlinkMacSystemFont, sans-serif` fallbacks.
-   **Weights used**: 400 (body), 500 (titles/buttons), 700 optional for
    emphasis.
-   **Base size**: 14px desktop; mobile headings scale up (16--18px).
-   **Tracking/line-height**: Default/normal; keep compact for glass
    surfaces.

**Import:**

``` css
@import url('https://api.fontshare.com/v2/css?f[]=satoshi@400,500,700&display=swap');
```

**Type roles** - Title Bar Title: 16px / 18px (mobile), 500 weight. -
Labels/Buttons: 14--15px, 500. - Meta (muted): 12--13px,
`--text-muted-color`.

------------------------------------------------------------------------

## 4) Surfaces & Elevation

Use translucency + blur to create depth (no heavy drop shadows).

  ------------------------------------------------------------------------------------------------------------------
  Layer          Example                   Fill (bg)                     Blur           Border
  -------------- ------------------------- ----------------------------- -------------- ----------------------------
  **L0** Page    `body`                    Photograph (cover, fixed)     ---            ---
                                           over `--bg-color`                            

  **L1**         `.main-container`         `rgba(12,12,13,.5)`           10px           1px `--border-color`
  Container                                                                             

  **L1** Title   `.title-bar`              `rgba(12,12,13,.1)`           20px (25px     1px bottom border
  Bar                                                                    mobile)        

  **L2**         `.section`,               `rgba(255,255,255,.05–.08)`   10px           1px
  Section/Card   `.search-result-item`,                                                 rgba(151,177,185,.10--.15)
                 `.status-log-container`                                                

  **L2** Sidebar `.sidebar`                `rgba(255,255,255,.05)`       10px           1px right border

  **Controls**   buttons/inputs            see §6                        ---            1px `--border-color`
  ------------------------------------------------------------------------------------------------------------------

**Background image guidance** - Use high-contrast, dark imagery; avoid
bright center areas behind body text. - Always
`background-attachment: fixed` and `background-size: cover` for the
acrylic illusion.

------------------------------------------------------------------------

## 5) Layout & Spacing

-   **Grid**: Flex layouts with gaps (12--20px). Sidebar fixed at
    **350px** on desktop.
-   **Container**: Max width **1200px**; height max **95vh**; border
    radius **12px**; overflow hidden.
-   **Content area**: 20px padding.
-   **Title bar**: 10px × 20px padding; elements spaced by 12px.
-   **Common gaps**: 4px (compact), 10--12px (row items), 15--20px
    (sections).

**Responsive** - **Breakpoint ≤768px**: Switch to column layout;
increase opacities, blur, and spacings; sticky title bar. - **Breakpoint
≤480px**: Further tighten layout; smaller logo; tuned heights.

------------------------------------------------------------------------

## 6) Controls & States

### Buttons

-   **Default**: `--button-bg-color` (α .15), 1px `--border-color`,
    radius 6px (8--10px on mobile).
-   **Hover**: `--button-hover-bg-color` (α .30), border α \~.40.
-   **Active (touch)**: slight scale (0.95--0.98) and maintain hover
    fill.
-   **Text**: `--text-color`, weight 500, 12--18px padding depending on
    context.

### Inputs

-   **Text**: Full width, 12px padding, fill `rgba(255,255,255,.05)`,
    1px `--border-color`, radius 6px.
-   **File**: Slightly higher α (0.08 default, 0.12 hover). Custom file
    button uses α .25 / .40 on hover.

### Tabs / Segmented controls

-   **Container**: `--section-bg-color` with 4--6px padding, radius 8px.
-   **Item**: Default muted text; **active** uses `--accent-color` text
    and `--button-hover-bg-color` fill.

### Radios (visual)

-   Hide native input; styled labels become segments. Checked state
    mirrors Tab active fill.

------------------------------------------------------------------------

## 7) Components (spec)

### Title Bar

-   Flex row, space-between; backdrop blur 20px (25px mobile); sticky on
    mobile; bottom hairline.
-   Logo 64px (desktop), 52px (tablet), 26px (XS), radius 4--6px.
-   Title 16px/18px, 500.

### Main Container

-   Column flex wrapper; acrylic pane with blur 10px; radius 12px; 1px
    border; overflow hidden.

### Sidebar

-   350px fixed width; vertical stack with 20px padding; right border;
    acrylic fill α .05; blur 10px.

### Content Area

-   Flexible column; 20px padding; scrollable.

### Sections

-   Used for grouped controls; fill α .05--.08; blur 10px; radius
    8--12px; 1px border α .10--.15; 15--18px padding.

### Status Log

-   Fixed height 250px (180px mobile), monospaced 13px; success/error
    color accents.

### Progress Bar

-   Track: `--section-bg-color`, 6--12px height; Bar:
    `--text-muted-color`.

### Search Results Item

-   Horizontal media object; 10--18px padding; 8--12px radius; album art
    50--75px with 4--6px radius; title 500; artist muted 12--14px.

### Footer

-   Floating at bottom-right; small (11--12px) muted text; acrylic chip
    on mobile.

------------------------------------------------------------------------

## 8) Motion & Interaction

-   **State transitions**: `transition: all .2s–.3s ease` across
    interactive elements.
-   **Mobile tap feedback**: scale to 0.95--0.98 on press.
-   Prefer **subtle motion**; avoid large shadows or long easings on
    glass.
-   (Optional) Add
    `@media (prefers-reduced-motion: reduce) { * { transition: none !important; } }`
    in new projects for accessibility.

------------------------------------------------------------------------

## 9) Accessibility & Contrast

-   Aim for **4.5:1** on primary text; use higher α backgrounds (≥.08)
    behind small text over busy photos.
-   Reserve pure white (`--accent-color`) for active states & key text
    only.
-   Increase control sizes on touch (≥44px target); already tuned at
    ≤768px.

------------------------------------------------------------------------

## 10) Implementation Checklist (new project)

1)  Import Satoshi; define tokens from §2.
2)  Set `body` background image (dark, high-res), fixed & cover; base
    text color to `--text-color`.
3)  Create acrylic panes: container, title bar, sidebar, sections with
    blurs per §4.
4)  Implement controls: buttons, inputs, segmented controls;
    hover/active states.
5)  Apply layout: 1200px max width, 20px paddings, 12--20px gaps, 350px
    sidebar.
6)  Add responsive rules at 768px and 480px with opacity/blur/spacing
    adjustments.
7)  Validate contrast; tune background α where needed.

------------------------------------------------------------------------

## 11) Code Snippets (starter)

**Reset & page**

``` css
* { box-sizing: border-box; }
html, body { height: 100%; margin: 0; }
body { font: 14px 'Satoshi', -apple-system, BlinkMacSystemFont, sans-serif; color: var(--text-color); }
```

**Acrylic utility**

``` css
.glass-10 { background: rgba(255,255,255,.05); backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px); }
.glass-20 { background: rgba(12,12,13,.10);  backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px); }
.border-1 { border: 1px solid var(--border-color); }
.rad-6 { border-radius: 6px; } .rad-8 { border-radius: 8px; } .rad-12 { border-radius: 12px; }
```

**Button**

``` css
.btn { background: var(--button-bg-color); color: var(--text-color); border: 1px solid var(--border-color);
       border-radius: 6px; padding: 12px 18px; font: 500 14px 'Satoshi', sans-serif; transition: all .2s ease; }
.btn:hover { background: var(--button-hover-bg-color); border-color: rgba(151,177,185,.4); }
.btn:active { transform: scale(.98); }
```

**Segmented control**

``` css
.segmented { display:flex; gap:4px; padding:4px; border-radius:8px; background: var(--section-bg-color); }
.segmented .item { flex:1; text-align:center; padding:8px; color: var(--text-muted-color); border-radius:6px; }
.segmented .item.is-active { color: var(--accent-color); background: var(--button-hover-bg-color); }
```

**Inputs**

``` css
.input { width:100%; padding:12px; background: rgba(255,255,255,.05); border:1px solid var(--border-color);
         border-radius:6px; color: var(--text-color); font: 14px 'Satoshi', sans-serif; }
```

**Breakpoints**

``` css
@media (max-width: 768px){
  .title-bar{ backdrop-filter: blur(25px); -webkit-backdrop-filter: blur(25px); padding:15px 20px; }
  .btn, .input { border-radius:10px; }
}
@media (max-width: 480px){
  .title-bar .logo{ width:26px; height:26px; }
}
```

------------------------------------------------------------------------

## 12) Naming & File Organization

-   `tokens.css` -- variables, utilities.
-   `layout.css` -- core structure (container, sidebar, content, title
    bar).
-   `components.css` -- buttons, inputs, tabs, progress, cards.
-   `responsive.css` -- media queries for ≤768px and ≤480px.

------------------------------------------------------------------------

## 13) Theming Knobs (safe to vary)

-   **Background image**: swap per project; keep dark and low-detail
    behind text.
-   **Accent intensity**: tweak `--button-*` alphas ±0.05 to match
    photography.
-   **Blur**: 8--12px for content panes; 18--24px for headers.
-   **Radius**: remain within 6--12px family.

------------------------------------------------------------------------

## 14) Do / Don't

**Do** - Keep borders hairline and neutral. - Use muted text for
secondary info. - Increase opacity behind dense text blocks.

**Don't** - Stack multiple translucent layers without adequate
contrast. - Use saturated accent colors over busy photos. - Rely on
heavy shadows to imply depth.

------------------------------------------------------------------------

### Quick Start (copy into new project)

1.  Copy §2 tokens and import Satoshi.
2.  Add §11 utilities.
3.  Build panes and controls per §4--§7.

That's it---you'll get the same acrylic, frosted‑glass character with
consistent spacing, radii, blurs, and muted palette.

