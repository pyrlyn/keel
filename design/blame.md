# Blame

## Purpose

Show line-by-line authorship and revision for a file at a chosen commit, and let the user walk history for a line or region.

## Layout

A file view: gutter with revision, author, and date per line or per group of adjacent lines from the same commit, plus the file text. A header chooses the path and the commit (default: HEAD or the commit the user arrived from). A detail popover or side panel shows the full commit message for the selected line's revision. Optional minimap of blame groups later; not required for v1.

## Components

- Path and commit selector
- Blame gutter (hash, author, date)
- File text, read-only, with syntax highlighting if the diff viewer already has it
- Commit detail panel
- Actions: open commit in History, show diff for that revision, follow to older revision, open at previous change for this line
- Toggle: follow renames when Git can

## States

- **Empty:** No file selected; prompt to pick a path or arrive from the diff viewer or history.
- **Loading:** Computing blame for a large file; show a progress state. First screenful can appear before the rest if the backend allows.
- **Error:** File not in that commit, binary file, or blame failed. Offer to show the file without blame or to pick another revision.

## Interactions

- Click a gutter group to select that commit and highlight its lines.
- “Older” walks to the parent that last changed the line.
- Opening History selects the same commit and, if possible, the path filter.
- Line wrap and font size follow the diff viewer settings.

## Keyboard shortcuts (proposed)

- Arrow keys move by line; `⌥↑` / `⌥↓` (or `Alt`) jump to the previous/next blame group
- `Return` opens the selected commit in History
- `[` older revision for the current line
- `⌘F` search in the file

## Accessibility notes

- Each line exposes author, date, and short hash in the accessible name or a row description, not only in a color block.
- Grouped lines do not hide authorship from a screen reader when visually collapsed into one gutter label.
- The text view is read-only but selectable for copy.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
