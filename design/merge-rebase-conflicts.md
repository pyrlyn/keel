# Merge, rebase, and conflict resolver

## Purpose

Support merge and rebase as first-class, recoverable operations, and provide a conflict resolver that makes ours/theirs/base and remaining work obvious. This screen covers both the operation setup and the in-progress resolver.

## Layout

**Setup view:** choose the incoming ref (merge) or new base (rebase), show a preview (commits that will be brought in, fast-forward possibility), and options (no-ff, rebase vs. merge when arriving from Pull). Primary actions: Start, Cancel.

**In-progress view:** a banner in the workspace and a dedicated resolver: list of conflicted files, a three-pane or stacked comparison (base, ours, theirs) plus the resolved result, and actions to continue, skip (rebase), or abort.

## Components

- Operation selector: Merge, Rebase (cherry-pick and revert reuse the resolver)
- Preview of commits and potential conflicts when we can estimate them
- Conflicted file list with resolution status
- Comparison panes and a result editor or hunk chooser
- Actions: take ours, take theirs, take base, mark resolved, mark unresolved
- Continue, Skip, Abort
- Hook and mid-commit message editor when the operation stops for a message

## States

- **Empty:** No merge or rebase in progress; show the setup form. If there is nothing to merge (already up to date), say so.
- **Loading:** Computing merge preview, applying a rebase step, or writing the index after a resolution.
- **Error:** Conflicted state, hook failure, stop for user edit, or unrecoverable apply error. The repository must visibly remain in the mid-operation state with Abort available. Never hide a `.git/MERGE_HEAD` or rebase-apply state.

## Interactions

- Abort asks for confirmation if resolutions or in-progress commit messages would be lost.
- Marking a file resolved is blocked until conflict markers are gone, or the user explicitly confirms remaining markers.
- Continue runs the next step and reports if new conflicts appear.
- External mergetool invocation is an optional escape hatch.
- Navigating away keeps the in-progress banner visible.

## Keyboard shortcuts (proposed)

- `⌘Enter` continue when all conflicts are resolved
- Arrow keys move between conflicted files and hunks
- `O` / `T` take ours or theirs for the selected hunk (labeled in the UI so this is learnable)
- `Escape` focuses Abort only; it does not abort immediately

## Accessibility notes

- “Ours” and “theirs” are explained in context (e.g. current branch vs. incoming), because the words are easy to mix up.
- Conflict remaining counts are announced when they change.
- The result pane is a labeled editor region; panes have headings.
- Color for ours/theirs is accompanied by text labels.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
