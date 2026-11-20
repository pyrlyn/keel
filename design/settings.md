# Settings

## Purpose

Provide a curated place for Keel preferences and the Git settings the app needs, split between application UI and Git identity or behavior, at global and repository scope.

## Layout

A settings window or a workspace pane with a sidebar of sections: General, Appearance, Git identity, Signing, Remotes and credentials, Integrations (hosts), Keybindings, and About. A banner at the top of repo-scoped pages names the current repository. Each field shows whether it is global or local and should not silently overwrite unexpected Git config.

## Components

- Section navigation
- Identity: user.name, user.email (global and repo-local override)
- Pull strategy default, default branch name for new repos, init options
- Signing: enable, key or SSH signing preference
- Appearance: theme (system, light, dark), font size, diff options defaults
- Integrations: GitHub and other hosts (connected accounts), later
- Keybinding viewer and editor (even if v1 only supports presets)
- External tools: Git binary path, editor, mergetool
- About: version, license (when decided), links to docs

## States

- **Empty:** Unlikely for the screen itself; individual lists (accounts, keys) can be empty with an add action.
- **Loading:** Reading Git config or probing the Git binary and signing keys.
- **Error:** Config write failed, invalid email, missing Git binary, or host auth failed. Keep other sections usable; show field-level errors.

## Interactions

- Saving a repo-local override does not rewrite the global value unless the user is on the global page.
- Changing the Git binary path re-runs a version check.
- Resetting a field to “inherit global” is explicit.
- Dangerous options (skip hooks by default, always force) are not offered as standing defaults.

## Keyboard shortcuts (proposed)

- `⌘,` opens Settings
- Search inside settings if the list grows (`⌘F`)
- Standard text field shortcuts apply

## Accessibility notes

- Every control has a visible label; tooltips are not the only label.
- Scope (global vs. this repository) is announced with the field.
- Theme changes preserve contrast requirements; do not rely on color alone in previews.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
