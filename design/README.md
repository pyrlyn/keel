# Keel design specifications

This folder holds screen-by-screen design specifications for **Keel**. These documents describe purpose, layout, components, states, interactions, keyboard shortcuts, and accessibility for each application screen.

## Binding to Figma

These specifications will be bound to a Figma design file. Each screen doc has a **Figma** section with:

- A placeholder for the Figma file link (TBD until the file exists)
- A placeholder for that screen's frame link
- A “last synced” date

Until the Figma file is created, every link is recorded as **TBD** and every “last synced” value is **never**.

## Synchronization rule

**Design documents in this folder must stay synchronized with the Figma design and must be kept updated.**

Whenever the Figma design changes:

1. Update the corresponding screen specification in the same change (or immediately after, in the same pull request / commit series).
2. Refresh the frame link if the frame was replaced or moved.
3. Set **Last synced** to the date the doc was aligned with Figma.
4. Note any intentional lag (for example, a spike exploring a layout that is not yet approved) explicitly in the screen doc — do not leave silent drift.

The inverse is also required: if a screen spec changes the intended UX, the Figma file must be updated to match, and the Figma section should be refreshed.

If Figma and a screen doc disagree, that is a defect in the documentation or the design file, not a “pick whichever is convenient” situation. Resolve the disagreement and record the new synced state.

## Figma file

- **Figma file:** TBD
- **Figma project / library:** TBD

## Screens

| Screen | Spec |
| --- | --- |
| Welcome and onboarding | [welcome-onboarding.md](welcome-onboarding.md) |
| Repository picker | [repository-picker.md](repository-picker.md) |
| Main workspace / changes | [workspace-changes.md](workspace-changes.md) |
| Commit composer | [commit-composer.md](commit-composer.md) |
| History and graph | [history-graph.md](history-graph.md) |
| Diff viewer | [diff-viewer.md](diff-viewer.md) |
| Branches | [branches.md](branches.md) |
| Merge, rebase, and conflict resolver | [merge-rebase-conflicts.md](merge-rebase-conflicts.md) |
| Blame | [blame.md](blame.md) |
| Stash | [stash.md](stash.md) |
| Remotes and sync | [remotes-sync.md](remotes-sync.md) |
| Tags | [tags.md](tags.md) |
| Settings | [settings.md](settings.md) |
| Command palette | [command-palette.md](command-palette.md) |
| Notifications and errors | [notifications-errors.md](notifications-errors.md) |

## Shared conventions

Until Figma defines tokens, treat the following as planning conventions:

- One primary workspace window per repository, with additional windows allowed.
- Persistent chrome: sidebar or activity navigation, title area with repo and branch, and a status/sync indicator.
- Destructive actions require confirmation when they can discard uncommitted work or rewrite published history.
- Empty, loading, and error states are mandatory for every screen that loads data.
- Keyboard shortcuts below are proposals; the final scheme is an open product decision and must be updated here when chosen.
