# Command palette

## Purpose

Offer a single keyboard-driven entry point to commands, repository switching, and (optionally) commit or branch search, so experienced users can drive Keel without hunting through menus.

## Layout

A modal or floating panel centered in the current window: a search field on top, a ranked results list below, with command name, shortcut, and a short context (for example the current file or branch) when relevant. One result is always highlighted. Categories or subtle grouping (Commands, Repositories, Branches, Commits) may appear when the query is empty or when a prefix is used.

## Components

- Search field with placeholder that hints at prefixes (later: `>` commands, if needed)
- Result rows: icon, title, shortcut, subtitle
- Empty-query list: recent or frequent commands
- Footer hint for navigation keys
- Optional preview for a selected commit or branch (not required for v1)

## States

- **Empty:** No matches for the query; say so and keep the query editable. On first open with no query, show recents or a short default set — this is not an error state.
- **Loading:** Rare; if command registration or a commit search is still warming up, show a busy indicator in the list without blocking typing.
- **Error:** A command failed after being invoked; the palette should close and defer to the notifications/errors surface, unless the failure is “command unavailable”, in which case it can stay open with an explanation.

## Interactions

- Open from any workspace screen; Escape closes and returns focus to the previous surface.
- Enter runs the highlighted command. Some commands open a follow-up (e.g. create branch) instead of doing work immediately.
- Disabled commands remain visible when they are relevant but unavailable (nothing staged, no remotes), with a reason in the subtitle.
- Prefix filters, if any, are documented in this spec once chosen.
- The palette does not capture passwords or paste secrets into logs.

## Keyboard shortcuts (proposed)

- `⌘K` or `⌘P` opens the palette (final choice TBD; must not silently fight the repository pin shortcut)
- Arrow keys move the highlight; `Tab` should not trap the user in a dead cycle
- `Enter` invoke, `Escape` close
- Holding a modifier to preview is optional and TBD

## Accessibility notes

- The dialog has a name, “Command palette”, and focus moves to the search field on open, back to the invoker on close.
- The active result is announced as the selection changes.
- Shortcuts shown in the list are readable text, not only symbols that a screen reader would skip.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
