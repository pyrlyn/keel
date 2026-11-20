# Repository picker

## Purpose

Let the user find, open, pin, and manage local repositories (and start a clone) without already being inside a workspace. This can appear as the welcome continuation, a standalone “Open” window, or a switcher from an open workspace.

## Layout

A list-and-detail or single-column list of known repositories: recents, favorites/pins, and optionally a directory scan result. A search field at the top. Actions to open, pin, remove from the list, reveal in the file manager, clone, or add an existing path. Detail (when present) shows path, current branch if cheap to read, and last opened time.

## Components

- Search / filter field
- Sections: Pinned, Recent, Other
- Repository row: name, path, optional branch or dirty indicator
- Add existing, Clone, Create actions
- Context menu per row
- Optional “switch repository” mode when a workspace is already open

## States

- **Empty:** No known repositories; prompt to open, clone, or create.
- **Loading:** Reading recents, validating paths, or a clone/open in progress.
- **Error:** Path missing, not a Git repository, permission denied, or clone failed. Keep the list usable and show the error on the affected row or in a banner.

## Interactions

- Single click selects; double click or Open enters the workspace.
- Pin/unpin moves a row between sections.
- Removing a row does not delete the repository on disk; deleting on disk is not offered here.
- Invalid paths can be forgotten or relocated (re-point to a new folder).
- Opening a repo that is already open focuses the existing window unless the user asks for a new window.

## Keyboard shortcuts (proposed)

- Type-ahead or `⌘F` focuses search
- Arrow keys and `Return` open the selected repo
- `⌘O` add/open existing
- `⌘P` pin or unpin (if it does not conflict with the command palette; final bindings TBD)
- `Escape` closes the picker when used as a switcher

## Accessibility notes

- List is a proper list or table with row names that include the folder name and path.
- Dirty or missing-path indicators have text equivalents, not only icons or color.
- Search results updates are announced without stealing focus from the field.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
