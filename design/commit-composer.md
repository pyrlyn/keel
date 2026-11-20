# Commit composer

## Purpose

Let the user write a commit message and create a commit from the staged changes (or an explicitly chosen “commit all staged” set), including amend and common trailers, with a clear preview of what will be recorded.

## Layout

A compact panel docked to the Changes workspace (bottom or side), expandable to a taller message editor. Contains a subject field, an optional body, a summary of staged files, and primary/secondary actions (Commit, Amend). Advanced options (sign, empty, no-verify) are hidden behind a disclosure, not shown by default.

## Components

- Subject field (recommended 50–72 character guidance, not a hard block unless configured)
- Body text area
- Staged file count and short list or “N files”
- Commit button, Amend toggle or button (disabled when amend is unsafe)
- Optional trailers: Co-authored-by
- Disclosure: GPG/SSH sign, include date, allow empty, skip hooks (dangerous, labeled)
- Warning region (amend of a published commit, merge in progress, nothing staged)

## States

- **Empty:** No staged changes; Commit disabled with an explanation. Offer “stage all and commit” only as an explicit action, never as a silent default.
- **Loading:** Commit in progress (hooks running); fields disabled, progress shown.
- **Error:** Hook failure, signing failure, empty message, or index lock. Keep the message text; show the error and a way to retry or open hook output.

## Interactions

- Commit uses only staged changes unless the user explicitly chooses otherwise.
- Amend is offered when HEAD is a local, unpublished commit the user just made; amending a commit that has been pushed requires an extra confirmation.
- Closing the app or switching views must not lose an unsent message (preserve draft locally).
- Success clears the message (or offers to keep it) and returns focus to the file list.

## Keyboard shortcuts (proposed)

- `⌘Enter` commit
- `⌘Shift+Enter` amend, when allowed
- `⌘Z` standard text undo in the message fields
- `Escape` collapses the expanded composer without discarding the draft (unless the user clears it)

## Accessibility notes

- Subject and body have visible labels, not placeholder-only labels.
- Warnings are announced and associated with the Commit action.
- Character guidance is advisory text, not color alone.
- Hook error output is in a readable, focusable region.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
