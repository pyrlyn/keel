# Diff viewer

## Purpose

Present a readable diff for working-tree changes, staged changes, and commit-to-commit comparisons, including hunk and line selection for staging where applicable.

## Layout

A file header (path, old/new modes, rename, binary flag) above a scrollable diff. Support unified view first; split (side-by-side) view as a toggle. Hunk headers are sticky or easily reachable. A toolbar offers wrap, whitespace ignore, word-diff, and “expand context”.

## Components

- Path header and status (added, deleted, modified, renamed, copied)
- View toggle: unified / split
- Options: ignore whitespace, word-level highlights, context lines
- Hunk blocks with stage/unstage/discard actions when the diff is of the working tree or index
- Line number gutters (old and new)
- Binary or large-file placeholder
- Image diff later if feasible; not required to block v1 text diffs

## States

- **Empty:** No file selected, or the file has no textual diff (clean, or identical after whitespace ignore). Explain which case applies.
- **Loading:** Computing a large diff; show a progress state and a warning if the file is very large, with an option to still open it.
- **Error:** Diff failed (binary misdetected, submodule, or I/O error). Show why and offer “open externally” where useful.

## Interactions

- Click a hunk or drag across lines to select a range for stage/unstage/discard (Changes context only).
- Clicking a line number may open blame or an external editor at that line (open decision).
- Toggle options should not lose scroll position of the current hunk if possible.
- Renames show old and new paths clearly.

## Keyboard shortcuts (proposed)

- `[` / `]` previous or next hunk
- `S` / `U` stage or unstage the selected hunk or lines (Changes context)
- `W` toggle ignore whitespace
- `D` toggle unified/split
- `⌘F` search within the diff

## Accessibility notes

- Added and removed lines are marked with text (“added”, “removed”) or typographic prefixes, not only green and red.
- Split view remains usable at high zoom and with a screen reader (prefer unified as the accessible default if split is confusing).
- Keyboard selection of hunks is documented and visible.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
