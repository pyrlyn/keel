# Notifications and errors

## Purpose

Surface success, progress, warning, and error feedback without blocking the whole app, and give durable access to failures (hooks, auth, sync, conflicts) with a way to retry or copy details. This is a system surface used by every other screen.

## Layout

Transient toasts or banners appear in a consistent corner or under the workspace chrome. A history or “activity” drawer collects recent events so a dismissed toast is not lost. Blocking modal dialogs are reserved for confirmations and unrecoverable choices, not for ordinary errors.

## Components

- Toast/banner with severity (info, success, warning, error), title, short message, and optional actions (Retry, View, Open resolver, Copy details)
- Progress toast for long operations (fetch, clone, rebase step) with cancel when supported
- Activity history list
- Modal confirmation (discard, hard reset, force-with-lease, abort merge)
- Expandable technical detail (Git stderr, hook output) hidden by default
- Link into Settings when the fix is configuration

## States

- **Empty:** No current toasts; the activity history can still be empty on first launch (“No recent activity”).
- **Loading:** A progress event is running; it should update in place rather than spam new toasts.
- **Error:** Failures appear as error toasts or banners and are recorded in history. If an operation leaves the repo mid-merge or mid-rebase, the workspace banner from the conflict spec stays up in addition to the toast.

## Interactions

- Toasts auto-dismiss for success and info; errors stay until dismissed or acted on.
- Retry re-invokes the same operation with the same parameters when it is safe.
- Copy details copies a redacted message (no credentials, tokens, or private key material).
- Multiple simultaneous events stack; they do not cover each other without a “+N more” or a queue in the activity drawer.
- Confirmations always have an explicit cancel and do not bind Enter to a destructive default.

## Keyboard shortcuts (proposed)

- `Escape` dismisses the topmost toast or closes the activity drawer, and never confirms a destructive dialog
- A shortcut to open activity history (TBD, perhaps `⌘Shift+A`)
- Within a dialog, `Enter` confirms only when the default is non-destructive

## Accessibility notes

- New errors are announced as alerts; success toasts are polite and should not interrupt typing mid-keystroke if avoidable.
- Severity is in text, not only color or icon.
- Toasts are reachable by keyboard and do not steal caret focus from the commit message unless the error is about that field.
- Motion can be reduced when the system reduce-motion preference is set.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
