# History and graph

## Purpose

Show the commit history of the repository as a list and as a graph, so the user can understand branching, inspect a commit, compare, and start actions such as checkout, revert, cherry-pick, or reset.

## Layout

A two-pane view: a graph-and-list of commits on the left (or top), and a commit detail plus diff on the right (or bottom). A toolbar holds branch/ref filters, search (message, author, hash), path filter, and date range. The graph column shows parent links, merges, and ref labels (branches, tags, HEAD).

## Components

- Commit graph (lanes) and commit rows: short hash, subject, author, relative date, ref badges
- Filter and search toolbar
- Commit detail: full message, authors, parents, and changed files
- Diff of the selected commit (reuse the diff viewer)
- Context menu: checkout, create branch, cherry-pick, revert, reset (soft/mixed/hard), copy hash, open on host
- Multi-select for compare (two commits)

## States

- **Empty:** A repository with no commits yet; explain that history will appear after the first commit and link back to Changes.
- **Loading:** Walking history for a large repo; show incremental rows and a progress state. Path or graph computation may arrive after the first page of commits.
- **Error:** History read failed (corrupt object, shallow clone limitation, or backend error). Offer retry and a fallback to a simpler list if the graph fails.

## Interactions

- Click a commit to load detail and diff.
- Checkout of a non-branch commit warns about detached HEAD and offers to create a branch.
- Reset modes are named and explained; hard reset requires confirmation.
- Compare mode shows the diff between two selected commits.
- Filters are combinable and visible as chips that can be cleared.

## Keyboard shortcuts (proposed)

- `⌘2` opens History
- `J` / `K` or arrows move between commits
- `/` focuses search
- `C` checkout, `B` create branch, `R` revert (all with confirmation where destructive)
- `⌘C` copies the full commit hash when a commit is selected and the editor is not focused

## Accessibility notes

- Graph lanes are supplementary; each row must make sense as text (subject, refs, relation to HEAD).
- Merge commits are labeled in text, not only in the graph drawing.
- Color lanes are not the only way to distinguish branches.
- Virtualized lists still expose a meaningful item count and position to assistive technology when possible.

## Figma

- **Figma file:** TBD
- **Frame link:** TBD
- **Last synced:** never

This specification must stay synchronized with the Figma design. Update this section and the content above whenever the Figma frame changes.
