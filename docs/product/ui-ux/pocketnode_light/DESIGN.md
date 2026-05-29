---
name: PocketNode Light
colors:
  surface: '#f8f9ff'
  surface-dim: '#cbdbf5'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e5eeff'
  surface-container-high: '#dce9ff'
  surface-container-highest: '#d3e4fe'
  on-surface: '#0b1c30'
  on-surface-variant: '#464554'
  inverse-surface: '#213145'
  inverse-on-surface: '#eaf1ff'
  outline: '#767586'
  outline-variant: '#c7c4d7'
  surface-tint: '#494bd6'
  primary: '#4648d4'
  on-primary: '#ffffff'
  primary-container: '#6063ee'
  on-primary-container: '#fffbff'
  inverse-primary: '#c0c1ff'
  secondary: '#565e74'
  on-secondary: '#ffffff'
  secondary-container: '#dae2fd'
  on-secondary-container: '#5c647a'
  tertiary: '#595c5e'
  on-tertiary: '#ffffff'
  tertiary-container: '#727577'
  on-tertiary-container: '#fbfdff'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#e1e0ff'
  primary-fixed-dim: '#c0c1ff'
  on-primary-fixed: '#07006c'
  on-primary-fixed-variant: '#2f2ebe'
  secondary-fixed: '#dae2fd'
  secondary-fixed-dim: '#bec6e0'
  on-secondary-fixed: '#131b2e'
  on-secondary-fixed-variant: '#3f465c'
  tertiary-fixed: '#e0e3e5'
  tertiary-fixed-dim: '#c4c7c9'
  on-tertiary-fixed: '#191c1e'
  on-tertiary-fixed-variant: '#444749'
  background: '#f8f9ff'
  on-background: '#0b1c30'
  surface-variant: '#d3e4fe'
typography:
  headline-xl:
    fontFamily: Geist
    fontSize: 40px
    fontWeight: '700'
    lineHeight: 48px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Geist
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
    letterSpacing: -0.01em
  headline-lg-mobile:
    fontFamily: Geist
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-md:
    fontFamily: Geist
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  body-lg:
    fontFamily: Geist
    fontSize: 18px
    fontWeight: '400'
    lineHeight: 28px
  body-md:
    fontFamily: Geist
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  label-md:
    fontFamily: Geist
    fontSize: 14px
    fontWeight: '500'
    lineHeight: 20px
    letterSpacing: 0.01em
  label-sm:
    fontFamily: Geist
    fontSize: 12px
    fontWeight: '600'
    lineHeight: 16px
    letterSpacing: 0.05em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  base: 4px
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  gutter: 20px
  margin-mobile: 16px
  margin-desktop: 48px
---

## Brand & Style

This design system is engineered for the modern fintech landscape, prioritizing clarity, trust, and professional efficiency. The brand personality is dependable and sophisticated, moving away from "dark-mode" gamer aesthetics toward a "clean-tech" editorial feel. 

The design style follows a **Modern Professional** aesthetic:
- **Cleanliness:** High use of white space to reduce cognitive load during financial decision-making.
- **Precision:** Utilizing the technical prowess of the Geist typeface to imply accuracy and data integrity.
- **Softness:** Using rounded geometries to make the financial experience feel approachable and human, rather than cold or institutional.

## Colors

The palette is anchored by a vibrant Indigo primary, serving as the "action" color for primary buttons, active states, and brand highlights. 

- **Backgrounds:** The primary surface is `#ffffff`. Secondary surfaces (sidebars, cards) utilize `#f8fafc` to create subtle depth without relying on heavy borders.
- **Typography:** Headlines and primary body text use a high-contrast Dark Slate (`#0f172a`) to ensure maximum legibility. Secondary labels use Slate (`#64748b`).
- **Feedback:** Success states use a deep emerald, while errors use a soft but clear crimson, maintaining the professional tone.

## Typography

This design system leverages **Geist** for its monospaced-influenced precision and modern grotesque readability. 

- **Hierarchy:** Use `headline-xl` sparingly for dashboard overviews. `headline-md` is the standard for card titles.
- **Data Display:** For financial figures, use `body-md` with `tabular-nums` enabled to ensure columns of numbers align perfectly.
- **Scalability:** On mobile devices, `headline-lg` automatically scales down to `headline-lg-mobile` to prevent awkward line breaks in currency displays.

## Layout & Spacing

A **Fixed-Fluid Hybrid** grid is utilized. Content containers have a max-width of 1280px on desktop but fluidly resize down to mobile widths.

- **Grid:** A 12-column grid system for desktop; 4-column for mobile.
- **Rhythm:** An 8px linear scale governs all padding and margins. 
- **Density:** Financial tables should use `sm` (8px) vertical padding to maximize information density, while marketing-heavy pages should use `xl` (32px) to feel premium and airy.

## Elevation & Depth

In light mode, depth is achieved through **Tonal Layering** and soft, ambient shadows.

- **Level 0 (Background):** `#ffffff` - The canvas.
- **Level 1 (Cards/Sidebar):** `#f8fafc` - Used for layout containers.
- **Level 2 (Popovers/Modals):** `#ffffff` with a "Financial Shadow" — a subtle, multi-layered shadow: `0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1)`.
- **Level 3 (Active Elements):** Primary color Indigo shadows are used only for active focus states to guide user attention.

## Shapes

The "Round Four" aesthetic is implemented via the **Rounded** (Level 2) setting. 

- **Standard Elements:** Buttons, inputs, and small cards use a `0.5rem` (8px) radius.
- **Large Containers:** Dashboard widgets and main content blocks use `1rem` (16px) for a softer, modern layout feel.
- **Selection States:** Checkboxes and toggle tracks use a slightly smaller radius (4px) to maintain a crisp look at small scales.

## Components

- **Buttons:** Primary buttons use `#6366f1` with white text. Secondary buttons use a light slate ghost-style background (`#f1f5f9`) with slate text.
- **Input Fields:** Use a 1px border of `#e2e8f0`. On focus, the border transitions to the primary Indigo with a 2px outer "halo" at 20% opacity.
- **Cards:** No borders. Use the Level 1 surface color (`#f8fafc`) or a Level 2 shadow on white to distinguish sections.
- **Status Chips:** Use a "Low Signal" approach: soft background tints with high-contrast text (e.g., Success = Light Green background + Dark Green text) to maintain professional restraint.
- **Data Tables:** Horizontal zebra-striping is discouraged. Use thin `#f1f5f9` dividers to maintain the clean, airy aesthetic.