# Keel product plan

This document is the working plan for **Keel**, a desktop Git client. It describes what we intend to build, what we will not build, and the decisions that are still open. It will be revised as design and architecture work proceeds.

**Status:** Planning.

## Goals

- Give developers a fast, focused desktop Git client that stays out of the way.
- Make the working tree, index, and history easy to understand at a glance.
- Cover the daily Git workflow completely: browse a repository, review status, stage, commit, branch, merge or rebase, resolve conflicts, inspect history, blame, diff, stash, sync with remotes, and manage tags and submodules.
- Prefer a keyboard-first, low-distraction interface, with a mouse and pointer workflow that is equally complete.
- Integrate with popular Git hosts (GitHub, GitLab, Bitbucket, and similar) without locking the product to a single host.
- Be trustworthy on real repositories: correct Git behavior, predictable performance, and clear error reporting.
- Keep design documentation synchronized with Figma as the visual design evolves.

## Non-goals

- Keel is not an IDE, text editor, or project build tool. Editing files is out of scope except where a conflict resolver or commit message needs a focused editor surface.
- Keel is not a Git hosting service, issue tracker, or CI/CD platform.
- Keel will not try to replace every `git` plumbing command or recover every expert edge case in v1.
- This repository will not contain application code during the planning phase; only structure and documentation.
- We will not invent a new version-control system. Keel is a client for Git.

## Target users

- Professional developers who use Git every day and want a dedicated client instead of an IDE-embedded VCS panel.
- People who prefer a keyboard-driven, visually clear Git workflow.
- Contributors and maintainers who work with hosted remotes (pull requests, forks, protected branches) but still need a strong local Git tool.
- New or occasional Git users who benefit from a clearer model of status, history, and conflicts — without being talked down to.

Personas will be refined once user research starts. For planning, the primary audience is daily practitioners; approachability for less frequent users is a secondary but important concern.

## Platforms

Keel is a desktop application. Mobile and web clients are out of scope for the first releases.

The platform strategy is still an open decision:

- **Option A:** macOS first, then Windows and Linux.
- **Option B:** Cross-platform from the first usable release (macOS, Windows, and Linux).

Whichever path we choose, v1 should feel native enough on each supported OS: system windowing, menus, keyboard shortcuts, file dialogs, and credential storage should follow platform conventions where they do not conflict with a consistent Keel workflow.

## Core features

The features below are the intended v1 surface area unless a later milestone explicitly defers one. Details of layout and interaction live in [`../design/README.md`](../design/README.md) and the per-screen specs.

### Repository browsing

Open one or more local repositories, remember recent and favorite workspaces, show the current branch, ahead/behind state, and a concise project identity (folder name, root path, remotes). Opening a repository should be fast even when the working tree is large.

### Status and staging

Show untracked, modified, staged, conflicted, renamed, and ignored-but-visible files. Support stage, unstage, partial (hunk and line) staging, discard with a clear confirmation when data would be lost, and path filtering or search.

### Commit

Compose a commit message (subject and body), amend when it is safe, add a co-author or trailer if the user asks, sign commits when configured, and show which files and hunks will be included. Prevent empty or accidental commits with clear feedback, not silent failure.

### Branches

List local and remote-tracking branches, create, rename, check out, and delete branches, set upstreams, and make the current branch obvious. Include a safe path for switching with uncommitted changes (stash, bring changes, or abort).

### Merge and rebase

Start a merge or rebase, preview what will happen, and continue, skip, or abort cleanly. Support common options (fast-forward vs. no-ff, interactive rebase in a later milestone if not v1) and never leave the repository in a mysterious mid-operation state without a recovery path.

### Conflict resolution

A first-class conflict resolver for merge, rebase, cherry-pick, and revert. Show ours, theirs, and base where available, allow per-hunk and per-file resolution, mark resolved, and explain remaining conflicts. This is a flagship feature, not an afterthought.

### History and graph

A commit graph and history view with filters (branch, author, path, date, message), parent and merge visualization, checkout of a commit in a detached or branch-creating flow, and actions such as revert, cherry-pick, reset (with explicit mode and danger levels), and compare.

### Blame

Line-by-line authorship and revision for a file at a chosen commit, with navigation to the introducing change and adjacent history. Handle renames when Git can follow them.

### Diff

Unified and, where practical, split diffs for working tree, index, and commit-to-commit comparisons. Word-level highlights, binary-file notices, large-diff warnings, and syntax-aware highlighting if it can be done without pulling in a full editor.

### Stash

List, create, apply, pop, drop, and inspect stashes, including untracked files when requested. Show stash contents before applying.

### Remotes, push, pull, and fetch

Manage remotes, fetch, pull (merge or rebase, per configuration and an explicit override), and push (including setting upstream, force-with-lease, and tags when asked). Surface authentication, rejected, and non-fast-forward cases clearly.

### Tags

List lightweight and annotated tags, create, delete, and push them, and jump from a tag to its commit.

### Submodules

Detect submodules, show their status, initialize, update, and synchronize them. Deep submodule editing can be phased, but v1 should not silently ignore submodule state.

### Hosting integration (GitHub and others)

Optional integration with GitHub, and later GitLab, Bitbucket, and similar hosts: clone from a host, open the current branch or pull request in a browser, list pull/merge requests related to the current branch, and respect authentication already present on the machine where possible. Keel remains a Git client first; host features must not block offline local work.

### Settings

Repository-local and global Git settings that Keel needs (user name and email, signing, default branch, pull strategy, ignore rules entry points, UI preferences, theme, keybindings). Do not expose every Git config key in v1; prefer a curated, documented set with an escape hatch to the config file.

Additional product surfaces specified in design docs — welcome and onboarding, a command palette, and notification or error toasts — support the features above and are part of the planned UX.

## Architecture options (open questions)

These are intentionally undecided. Spikes in a later milestone should compare options against performance, correctness, packaging, and the team's ability to maintain the stack.

- **UI toolkit:** fully native per platform (for example SwiftUI/AppKit, WinUI, GTK) versus a cross-platform toolkit (Compose Multiplatform, Flutter, Qt, Tauri, or similar). Electron is a last resort, not a default.
- **Git backend:** libgit2, a Rust stack such as gitoxide, shelling out to system `git`, or a hybrid (system `git` for writes and a library for status/diff). Correctness and staging/index fidelity matter more than purity.
- **Language and runtime:** depends on the UI and Git choices; candidates should be named in the architecture spike, not assumed here.
- **Process model:** single process versus a privileged or long-running Git worker to keep the UI responsive.
- **Performance strategy:** how to handle monorepos, huge working trees, many untracked files, and frequent file-system events (watchers, ignore rules, incremental status).
- **Credential and signing integration:** OS credential store, SSH agents, GPG/SSH signing, SSO and device flows for hosts.
- **Distribution and updates:** app bundles, signed updates, and package managers per platform.
- **Data and logging:** what is stored locally besides Git itself (recents, UI state) and how crash or diagnostic logs are kept without leaking secrets.

## Milestones and roadmap

Dates are not committed. Order is the planning sequence.

### M0 — Planning and documentation (current)

Repository structure, product plan, and screen specifications. Figma file still TBD. No application code.

### M1 — Visual design and architecture spike

Create the Figma file, bind frame links in `design/`, and settle the first architecture choices (platform, UI toolkit, Git backend) with a short written decision.

### M2 — Read-only local repository

Open a local repo, browse status, view diffs, inspect history/graph, and run blame. No writes yet, except perhaps harmless recents.

### M3 — Local writes

Stage (including hunks), commit, amend when safe, stash, and manage local branches. Solid undo or recovery messaging for destructive actions.

### M4 — Sync

Remotes, fetch, pull, push, tags, and credential basics. Clear handling of diverged branches.

### M5 — Merge, rebase, and conflicts

Merge and rebase flows plus the conflict resolver. Submodule status should be visible by the end of this milestone, even if deeper submodule workflows slip.

### M6 — Hosting integration

GitHub first, then a second host if the abstraction holds. Clone, pull-request context, and “open on host” actions.

### M7 — Polish

Command palette completeness, settings, accessibility, performance on large repos, onboarding, and release packaging.

## Risks

- **Correctness:** subtle Git index, encoding, line-ending, submodule, or hook behavior can diverge from system `git` and lose user trust.
- **Performance:** large monorepos and dirty trees are the usual place Git GUIs fail.
- **Mid-operation states:** a crash or quit during merge, rebase, or hook execution must be recoverable and obvious.
- **Scope creep:** host features, editing, and CI can distract from being an excellent Git client.
- **Cross-platform inconsistency:** if we go multi-platform, a lowest-common-denominator UI could feel poor everywhere.
- **Design drift:** screen specs and Figma can diverge unless updates are required in the same change.
- **Authentication complexity:** SSH, HTTPS, SSO, 2FA, and signing failures are a frequent source of “the app is broken” reports.
- **Uncertain architecture:** delaying the stack decision too long blocks M2; deciding too early without a spike can lock in a poor backend.

## Open decisions

- Platform strategy: macOS-first versus cross-platform from v1.
- UI toolkit and application language.
- Git backend (library, system `git`, or hybrid).
- License (and whether the client is open source, source-available, or proprietary).
- Pricing and distribution model.
- Default pull behavior (merge vs. rebase) and how loudly we expose it.
- Whether interactive rebase ships in v1 or immediately after.
- Depth of submodule support in v1.
- Which host is implemented first after the generic Git remote work (expected: GitHub) and how accounts are bound.
- Accessibility target level and localization plan (English first is assumed).
- Default keybinding scheme and whether it mirrors common Git clients or platform defaults.
- How tightly Figma is bound into the development workflow (link format, review checklist).

When a decision is made, it should be recorded here with a short rationale and a date, and any affected design specs should be updated.
