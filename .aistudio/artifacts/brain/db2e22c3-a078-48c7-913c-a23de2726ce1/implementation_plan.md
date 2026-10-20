# Implementation Plan: Action Button UX Streamlining & Dark Mode Visibility

Apply UX laws (Hick's Law & Miller's Law) to reduce cognitive load and visual clutter from 4 competing buttons down to 2 clear primary choices, with secondary actions elegantly tucked into an overflow menu (`More ▾`). Ensure all links and text are prominently legible with WCAG AAA contrast in both light and dark modes.

## UX Architecture Analysis
- **Problem**: 4 buttons (`Case Study ↗`, `View in Figma ↗`, `View Prototype ↗`, `Live Site ↗`) displayed simultaneously create choice paralysis (Hick's Law: decision time increases logarithmically with the number and complexity of choices). Visually, 4 pills consume too much horizontal real estate and fight for user attention with the project title and metrics.
- **Solution**:
  1. **Primary Intent (Top 2 actions)**:
     - `Case Study ↗` (Reads the problem, metrics, and architecture breakdown)
     - `Prototype ↗` (Interactive tactile demonstration in emerald accent)
  2. **Secondary Intent (Overflow Menu `•••` / `Links ▾`)**:
     - Accessible dropdown containing `View in Figma ↗` and `Live Site ↗` (or direct links).
     - Clean dropdown card with outline border, subtle backdrop blur, and dark-mode compliant hover states.
  3. **Live Site Visibility Fix**:
     - Distinct outline pill with crisp `--ink` color in both themes, subtle border glow on hover, and clear typography.

## Proposed Changes

### 1. Styles (`index.html` CSS)
- Style `.showcase-actions-group` to hold:
  - `.quick-brief-btn` (Case Study)
  - `.showcase-action-link.action-proto` (Prototype)
  - `.showcase-overflow-wrap`:
    - `.showcase-overflow-btn` (Clean outline button with `•••` or `Links ▾`)
    - `.showcase-overflow-dropdown`: Floating popover with keyboard accessibility (`Esc`, click outside), smooth fade/scale animation, and high contrast links for `View in Figma` and `Live Site`.
- Add explicit dark mode rules (`[data-theme="dark"]`) for outline links ensuring text is bright `#f7f7f5` with emerald/amber hover glow.

### 2. Markup Refactoring across Showcase Feed
- Refactor the 15 project cards (including the 5 new SaaS platforms: Collablly, Docomate AI, Othership, Caboodle Services, Exelo):
  - Primary button 1: `Case Study ↗`
  - Primary button 2: `Prototype ↗`
  - Overflow button: `Links ▾` (or `More ▾`) containing:
    - `View in Figma ↗`
    - `Live Site ↗` (for products with live external links)

### 3. JavaScript Dropdown Controller
- Add lightweight dropdown toggle behavior:
  - Toggle `.is-open` on click.
  - Close when clicking outside or pressing `Escape`.
  - Close other open menus when a new one is opened.

## Verification Plan

### Automated Build Verification
- Run `compile_applet` to verify clean build without syntax errors.

### Visual & Interactive Verification
- Test in both Light Mode and Dark Mode:
  - Verify card header feels airy, uncluttered, and structured with only 2 primary buttons + 1 overflow menu.
  - Verify `Live Site` and `View in Figma` text inside the overflow menu are crisp and readable in dark mode.
  - Test keyboard navigation and click-away dismissal for dropdown menus.
