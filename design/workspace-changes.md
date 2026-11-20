# Main workspace and changes

## Purpose

This is the primary working screen: a durable chrome around the current repository, with the Changes view as the default center. The user should see what is modified, stage or discard work, and move into commit, diff, history, and other views without losing context.

## Layout

A typical three-zone workspace:

- **Chrome:** repository name, current branch, ahead/behind or sync status, and a compact operation badge (merge in progress, rebase, etc.).
- **Navigation:** a sidebar or activity rail for Changes, History, Branches, Stash, Remotes, Tags, and Settings.
- **Changes body:** a file list (unstaged, staged, conflicted, untracked) and a diff pane for the selected path. Filters and a search field sit above the list.

The commit composer may be docked at the bottom or side of this screen; its detailed spec is in [commit-composer.md](commit-composer.md). The diff pane follows [diff-viewer.md](diff-viewer.md).

## Components

- Window title / repo identity
- Branch switcher control
- Sync indicator and button (fetch/pull/push summary)
- In-progress operation banner (merge, rebase, cherry-pick) with a link to the resolver
- File list grouped by status, with path, status icon, and optional submodule badge
- Stage, unstage, discard, and “stage hunk” actions
- Filter chips (all, staged, unstaged, conflicted) and path search
- Diff pane
- Docked commit composer (optional layout variant)

## States

- **Empty:** Clean working tree; a calm “No local changes” message, with shortcuts into History or Pull.
- **Loading:** Computing status for a large tree; show partial results if possible and a progress indication.
- **Error:** Status failed (corrupt repo, permissions, hook, or submodule issues). Show the error, a retry action, and keep navigation available.

## Interactions

- Selecting a file updates the diff pane.
- Stage/unstage can apply to a file, a hunk, or a selected line range.
- Discard asks for confirmation when the change cannot be recovered from Git.
- Double-click may open the file in the system editor or a configured external editor (open decision: in-app editor is a non-goal).
- The in-progress banner stays visible until the operation completes or is aborted.
- Drag-and-drop of paths into the list is not required for v1.

## Keyboard shortcuts (proposed)

- `⌘1` focuses Changes
- `S` / `U` stage or unstage the selection
- `⌘Enter` focuses or submits the commit composer (see that spec)
- `⌘R` refresh status
- `J` / `K` move between files
- `[` / `]` move between hunks
- `⌘B` branch switcher (final binding TBD vs. bold in other apps)

## Accessibility notes

- File status is exposed in text (Modified, Staged, Conflicted), not only color.
- The file list and diff pane have a documented focus order; focus is not trapped in the diff.
- Live status refresh should not reset focus or scroll without user intent.
- Operation banners are announced as alerts when a merge or rebase starts or fails.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
