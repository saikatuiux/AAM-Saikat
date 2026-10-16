# Implementation Plan: Sidebar Readability & Expandable Project Descriptions

Enhance the visibility and legibility of the "Open to new roles & projects · Remote-friendly" sidebar status pill for clients and recruiters, and implement a smooth 2-line clamp with a "Show more ▾ / Hide ▴" toggle on all project card descriptions across archetype pages.

## Proposed Changes

### 1. Sidebar Availability Status Pill Optimization
- **Contrast & Legibility Enhancement**:
  - Increase text contrast using `--ink` (WCAG AAA compliant tone) instead of faint muted gray.
  - Bump font size from `0.65rem` to `0.72rem` and increase font-weight to `500` with subtle letter-spacing.
  - Refine the live green pulse indicator to ensure vibrant visibility against the surface.
  - Maintain crisp borders and background in both light mode and dark mode.

### 2. Two-Line Clamped Description with "Show more ▾ / Hide ▴" Toggle
- **CSS Clamp**:
  - Add `.showcase-desc-clamp` class with `-webkit-line-clamp: 2`, `display: -webkit-box`, `-webkit-box-orient: vertical`, and `overflow: hidden`.
  - When expanded (`.is-expanded`), line-clamp is removed and full description displays smoothly.
- **Toggle Button**:
  - Add a subtle, elegant text toggle (`Show more ▾` / `Hide ▴`) right below or inline with the clamped text.
  - Styled with minimal underline/arrow transition that matches the portfolio's typographic craft.
- **JavaScript Controller**:
  - Automatically wire up click handlers to toggle `.is-expanded` and switch button text between `Show more ▾` and `Hide ▴`.

## Verification Plan

### Automated Build Verification
- Run `compile_applet` to confirm no syntax or bundling errors.

### Visual & Interactive Verification
- Verify the sidebar status badge is prominently legible in both light and dark themes.
- Test category pages (SaaS Platforms, Dashboards, Fintech, Landing Pages, Mobile Apps):
  - Descriptions clamp cleanly to exactly 2 lines.
  - Clicking "Show more ▾" smoothly reveals the full text and updates button text to "Hide ▴".
  - Clicking "Hide ▴" re-clamps the description back to 2 lines without jumping.
