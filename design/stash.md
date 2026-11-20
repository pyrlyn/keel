# Stash

## Purpose

Let the user save, inspect, apply, pop, and drop stashes, including optional untracked files, with a clear preview of stash contents before changing the working tree.

## Layout

A list of stashes (stash@{n}, message, date, branch it was made on) and a detail/diff pane for the selected stash. A primary action creates a new stash from the current changes. Apply, pop, and drop sit on the selected item, with drop and pop confirmed.

## Components

- Stash list
- Create stash control: message, include untracked, include ignored (rare, confirmed)
- Detail: message, metadata, file list, and diff
- Apply, Pop, Drop, Branch-from-stash (if offered in v1)
- Conflict banner if apply or pop conflicts (hands off to the conflict resolver)

## States

- **Empty:** No stashes; short explanation and a Create action if the working tree is dirty. If the tree is clean, Create is disabled with a reason.
- **Loading:** Listing stashes or computing a stash diff.
- **Error:** Apply/pop/drop failed, or the stash ref is missing. Keep the list if possible and show the error.

## Interactions

- Create stash can leave the working tree clean; if it fails mid-way, report clearly.
- Apply keeps the stash; pop applies then drops only on success.
- Drop requires confirmation.
- Applying onto a dirty tree is allowed when Git allows it; if not, explain and offer to stash or commit first.
- Conflicts enter the standard resolver; abort should leave the user with a documented state.

## Keyboard shortcuts (proposed)

- `⌘Shift+S` create stash (final binding TBD)
- `Return` apply the selected stash (with a preference or modifier for pop — do not pop accidentally)
- `Delete` starts drop confirmation
- `J` / `K` move between stashes

## Accessibility notes

- Stash indexes and messages are both part of the accessible row name.
- Disabled Create explains why in text.
- Confirmation dialogs name the stash being dropped.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
