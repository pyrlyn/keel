# Branches

## Purpose

Give a clear inventory of local and remote-tracking branches, and the actions to create, switch, rename, delete, and set upstreams without leaving Keel.

## Layout

A list of branches grouped into Current, Local, and Remote. A search field and filters (local only, stale, already merged). A detail pane or inspector shows last commit, upstream, ahead/behind, and associated pull request when host integration is available. The current branch is also always visible in the workspace chrome.

## Components

- Search and filters
- Branch rows: name, upstream, ahead/behind, last commit subject and date
- Current branch indicator
- Actions: checkout, create, rename, delete, set/unset upstream, merge into current, rebase onto, publish
- Create-branch dialog: name, start point (HEAD, another ref, or commit)
- Checkout-with-dirty-tree dialog: stash, bring changes, or abort

## States

- **Empty:** Unusual (HEAD should exist after the first commit). For a brand-new repo, show the default branch and invite a first commit.
- **Loading:** Refreshing remotes or ahead/behind counts; show names first, then divergence.
- **Error:** Checkout rejected, delete rejected (unmerged or checked out), or upstream query failed. Keep the list and display the error.

## Interactions

- Double-click or Checkout switches branch.
- Delete of a local branch that is not merged, or of a remote branch, requires confirmation.
- Rename validates a legal ref name and offers to update the upstream.
- Publishing a local branch uses the remotes-and-sync stack.
- Selecting a remote branch offers checkout as a new local branch tracking it.

## Keyboard shortcuts (proposed)

- `⌘3` opens Branches (number assignments TBD)
- `⌘N` or `C` create branch when this view is focused
- `Return` checkout
- `/` search
- `Delete` starts the delete flow, never deletes immediately

## Accessibility notes

- Current branch is announced and not conveyed only by bold or color.
- Ahead/behind is numeric text (“2 ahead, 1 behind”), not only arrows.
- Dialogs for dirty checkout and delete have clear default and cancel buttons, with focus in the dialog.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
