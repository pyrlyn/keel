# Welcome and onboarding

## Purpose

Introduce Keel to a first-time user, confirm that Git is available, and get them to an open repository quickly. Returning users should be able to skip or barely see this flow.

## Layout

A simple full-window welcome: product name and short promise at the top, a primary action group in the center (open a repository, clone, create), a list of recent repositories if any exist, and a discreet link to settings or documentation. Onboarding steps, when shown, are a short sequence rather than a long carousel.

## Components

- App wordmark and one-line description
- Primary buttons: Open repository, Clone repository, Create repository
- Recent repositories list (name, path, last opened)
- Optional first-run checks: Git availability, name/email identity, default clone location
- Skip / “Don't show again” for tutorial tips
- Footer links: Settings, documentation (later)

## States

- **Empty:** No recents; emphasize Open, Clone, and Create. If Git identity is unset, show a non-blocking prompt.
- **Loading:** Checking Git, scanning recents, or preparing a clone destination.
- **Error:** Git binary missing or broken, recents path no longer exists, or first-run check failed. Offer a path to Settings and a way to dismiss the broken recent.

## Interactions

- Open uses a native folder picker and then enters the main workspace.
- Clone asks for a URL (and later a host picker) and a local path, then shows progress.
- Create initializes a new repository at a chosen path.
- Clicking a recent opens it; a context menu can remove it from the list or reveal it in the file manager.
- Closing the welcome window with no repo open leaves the picker/welcome, not a blank workspace.

## Keyboard shortcuts (proposed)

- `Return` activates the default action (last repo if one exists, otherwise Open)
- `⌘O` / `Ctrl+O` open a repository
- `⌘Shift+O` clone
- `⌘N` create a repository
- Arrow keys move through recents

## Accessibility notes

- Buttons and recents are full keyboard targets with visible focus.
- Status of first-run checks is announced to assistive technology, not color-only.
- Decorative wordmark is ignored by screen readers; the heading is the accessible name “Keel”.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
