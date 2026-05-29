---
name: PocketNode
colors:
  surface: '#0b1326'
  surface-dim: '#0b1326'
  surface-bright: '#31394d'
  surface-container-lowest: '#060e20'
  surface-container-low: '#131b2e'
  surface-container: '#171f33'
  surface-container-high: '#222a3d'
  surface-container-highest: '#2d3449'
  on-surface: '#dae2fd'
  on-surface-variant: '#c7c4d7'
  inverse-surface: '#dae2fd'
  inverse-on-surface: '#283044'
  outline: '#908fa0'
  outline-variant: '#464554'
  surface-tint: '#c0c1ff'
  primary: '#c0c1ff'
  on-primary: '#1000a9'
  primary-container: '#8083ff'
  on-primary-container: '#0d0096'
  inverse-primary: '#494bd6'
  secondary: '#4edea3'
  on-secondary: '#003824'
  secondary-container: '#00a572'
  on-secondary-container: '#00311f'
  tertiary: '#ffb2b7'
  on-tertiary: '#67001b'
  tertiary-container: '#ff516a'
  on-tertiary-container: '#5b0017'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#e1e0ff'
  primary-fixed-dim: '#c0c1ff'
  on-primary-fixed: '#07006c'
  on-primary-fixed-variant: '#2f2ebe'
  secondary-fixed: '#6ffbbe'
  secondary-fixed-dim: '#4edea3'
  on-secondary-fixed: '#002113'
  on-secondary-fixed-variant: '#005236'
  tertiary-fixed: '#ffdadb'
  tertiary-fixed-dim: '#ffb2b7'
  on-tertiary-fixed: '#40000d'
  on-tertiary-fixed-variant: '#92002a'
  background: '#0b1326'
  on-background: '#dae2fd'
  surface-variant: '#2d3449'
typography:
  headline-lg:
    fontFamily: Geist
    fontSize: 32px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: -0.02em
  headline-lg-mobile:
    fontFamily: Geist
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.2'
  headline-md:
    fontFamily: Geist
    fontSize: 24px
    fontWeight: '500'
    lineHeight: '1.3'
  body-lg:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.6'
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.6'
  body-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: '1.5'
  label-lg:
    fontFamily: Geist
    fontSize: 14px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: 0.05em
  label-md:
    fontFamily: Geist
    fontSize: 12px
    fontWeight: '500'
    lineHeight: '1.2'
    letterSpacing: 0.02em
  mono-data:
    fontFamily: Geist
    fontSize: 16px
    fontWeight: '500'
    lineHeight: '1.4'
    letterSpacing: -0.01em
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  unit: 4px
  gutter: 16px
  margin-mobile: 16px
  margin-desktop: 32px
  container-max: 1200px
---

## Brand & Style
The design system is anchored in the concept of "Local Sovereignty." It targets privacy-conscious individuals who treat their financial data as a sensitive, private asset. The aesthetic avoids the flighty, "cloud-native" look of consumer fintech, opting instead for a **Corporate Modern** style with a **Minimalist** finish. 

The emotional response should be one of "fortified clarity"—the user should feel that their data is structured, secure, and entirely under their control. This is achieved through a rigid layout, high-quality typography, and a deliberate lack of unnecessary ornamentation. The UI feels solid, like a well-built physical tool, emphasizing reliability over trendiness.

## Colors
The palette is built on a "Deep Trust" foundation. The default state is **Dark Mode**, reinforcing the private, "behind-the-scenes" nature of personal finance. 

- **Primary (Indigo):** Used for primary actions and brand presence. It signals professionalism and security.
- **Secondary (Emerald):** Reserved strictly for positive financial indicators: income, budget surpluses, and growth.
- **Tertiary (Coral):** Used for expenses, debt, and critical alerts. It provides a sharp, legible contrast against the dark background.
- **Neutral (Slate/Navy):** A range of deep greys and navies used for surfaces and containers to maintain a low-light, high-focus environment.

## Typography
The typography system prioritizes data legibility and systematic hierarchy. **Geist** is used for headlines and UI labels to provide a technical, modern edge, while **Inter** handles body text for maximum readability. 

A special `mono-data` style is utilized for all currency and numerical values. This ensures that columns of numbers align perfectly in tables and lists, facilitating quick scanning of financial balances. Headline weights remain moderate (500-600) to avoid an overly aggressive look, maintaining a professional demeanor.

## Layout & Spacing
The layout follows a **Fixed Grid** philosophy on desktop to maintain a sense of containment and order, while transitioning to a fluid model on mobile. 

- **Desktop:** A 12-column grid within a 1200px container. This "island" approach reinforces the "local node" concept—your data sits in a protected center.
- **Rhythm:** A 4px baseline grid governs all spacing. Vertical rhythm is strictly enforced to ensure data-heavy screens feel structured rather than cluttered.
- **Density:** High information density is encouraged. Padding within cards is kept tight (16px to 20px) to maximize the amount of financial data visible without scrolling.

## Elevation & Depth
Depth is signaled through **Tonal Layers** rather than shadows. In a dark-themed, privacy-focused hub, "elevation" is represented by lighter shades of the neutral palette.

- **Level 0 (Background):** The deepest neutral (#0F172A).
- **Level 1 (Cards/Containers):** A slightly lighter navy with a subtle 1px border (#1E293B).
- **Level 2 (Modals/Popovers):** The highest brightness level, using a very subtle outer glow in the primary color to indicate focus.

Instead of ambient shadows, this design system uses **low-contrast outlines**. A 1px border in a muted slate color provides the necessary definition between elements, creating a "blueprint" or "schematic" feel that aligns with the local-first technical aesthetic.

## Shapes
The shape language is **Soft (0.25rem)**. While sharp corners feel too aggressive, overly rounded corners (pills) feel too playful for a serious financial tool. 

Small border radii on buttons and cards provide a modern touch while maintaining a rigid, grid-like structure. This "near-square" aesthetic conveys stability and efficiency. Larger components like main content areas should not exceed `rounded-lg` (0.5rem).

## Components
- **Cards:** The primary organizational unit. Cards must have a 1px border. Backgrounds should be slightly lighter than the page background. Headers within cards should use `label-lg` for categorizing data.
- **Buttons:** Solid Indigo for primary actions. Ghost buttons (outline only) for secondary actions. Use `label-md` for button text to keep them crisp and compact.
- **Input Fields:** Darker than the card background to create a "inset" look. The focus state must use a prominent Indigo border.
- **Consent UI:** Distinctive "Permission Gate" components for data syncing. These use a unique background tint (subtle Indigo wash) and clear "Encrypted" or "Local Only" badges to reassure the user.
- **Data Rows:** Alternating background tints (zebra striping) for long lists of transactions, using `mono-data` for all numerical columns to ensure alignment.
- **Status Chips:** Small, condensed pills for "Cleared," "Pending," or "Flagged." Use the secondary (green) and tertiary (coral) colors with 10% opacity backgrounds and 100% opacity text.