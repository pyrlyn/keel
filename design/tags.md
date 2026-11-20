# Tags

## Purpose

List, create, inspect, delete, and push Git tags (lightweight and annotated), and jump from a tag to its commit.

## Layout

A filterable list of tags with name, type (lightweight or annotated), target commit, and date (tag date or commit date, labeled). A detail pane shows the annotation message, tagger, and the target commit summary, with a short diff entry point. Actions: create, delete, push (one or all), checkout, copy name.

## Components

- Search/filter
- Tag rows and type badges
- Detail: message, tagger, commit
- Create tag dialog: name, target (HEAD or picked commit), annotated vs. lightweight, message, optional sign
- Delete and push confirmations
- Link to History at the target commit

## States

- **Empty:** No tags; invite creation, with a short distinction between annotated and lightweight.
- **Loading:** Refreshing tags after fetch or computing the target commit.
- **Error:** Invalid name, signing failure, push rejected, or delete failed on a remote. Preserve the create-form message text.

## Interactions

- Creating an annotated tag requires a message; lightweight does not.
- Deleting a tag that exists on a remote is a two-step local vs. remote deletion; remote deletion is confirmed.
- Pushing a single tag is the default action; push-all-tags is secondary.
- Checkout of a tag warns about detached HEAD and can offer a branch.

## Keyboard shortcuts (proposed)

- `/` search
- `C` or `⌘N` create tag when the view is focused
- `Return` opens the target commit in History
- `Delete` starts the delete flow

## Accessibility notes

- Type (annotated vs. lightweight) is text, not only a badge color.
- Signed/unsigned state is announced.
- Dialogs label the target commit, not only the tag name.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
