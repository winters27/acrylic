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

... (rest of doc omitted for brevity)
