# Remotes and sync

## Purpose

Manage remotes and run fetch, pull, and push with a clear view of ahead/behind state, authentication needs, and rejected updates.

## Layout

A remotes list (name, fetch/push URLs) plus a sync panel for the current branch: last fetched time, ahead/behind vs. upstream, and primary actions Fetch, Pull, Push. Dialogs or inspectors cover adding a remote, changing URLs, and pull/push options (rebase vs. merge, tags, force-with-lease). A log or activity area shows the last operation's output in human-readable form.

## Components

- Remote rows and add/edit/remove
- Current-branch upstream summary
- Fetch, Pull, Push buttons
- Options: prune on fetch, pull with rebase, push tags, set upstream, force-with-lease (never unlabeled force as the default)
- Credential or SSH agent prompt hook (OS-native where possible)
- Operation output / event list
- “Open on host” when hosting integration is configured

## States

- **Empty:** No remotes; prompt to add one or clone was local-only. Push/pull disabled with an explanation.
- **Loading:** Network operation in progress; buttons disable or show progress; cancelling is best-effort and must say if the operation may still complete on the remote.
- **Error:** Auth failure, network failure, non-fast-forward, hook rejection, or diverged histories. Errors include the next safe action (fetch first, pull, force-with-lease with warning, or open the divergence in History).

## Interactions

- Pull uses the configured default (open decision: merge vs. rebase) and can be overridden per action.
- Push without an upstream asks to set one.
- Force push is never the primary button; force-with-lease requires confirmation and a short explanation.
- Removing a remote does not delete local branches; say so in the confirm dialog.
- Auth failures should not require restarting the app; retry after credentials are supplied.

## Keyboard shortcuts (proposed)

- `⌘Shift+F` fetch
- `⌘Shift+L` pull (mnemonic: puLl; final scheme TBD)
- `⌘Shift+P` push
- `⌘Enter` confirms a focused sync dialog

## Accessibility notes

- Ahead/behind and last-fetched time are text, not only icons.
- Progress is announced, and errors are alerts with a retry action.
- Force-with-lease confirmation uses explicit language about rewriting remote history.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
