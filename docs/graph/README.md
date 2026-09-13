# The architecture map — how it is produced

`knowledge-graph.json` is generated from the **private** Phoenix source tree and
copied here. It is the only public view of the codebase's structure.

## What it contains, and what it does not

Each node carries: `id`, `type`, `name`, `filePath`, a plain-English `summary`,
`tags`, `complexity`, and a size (`sizeLines` or `lineRange`).

**There are no source bodies in it.** It is a description of the code, not the
code. Checked before first publication: no absolute filesystem paths, no email
addresses, no embedded code blocks.

## Refresh procedure

Run on the machine that has the private clone:

1. `git pull` the private tree so the clone is current.
2. Run the analysis over that clone. **Do not run it in the main working tree** —
   that is what the separate clone is for, so generated output never pollutes
   the source.
3. Copy **two files** into this repository at `docs/graph/`:
   - `knowledge-graph.json`
   - `meta.json`
4. Commit and push. GitHub Pages picks it up; the viewer reads it at runtime, so
   there is nothing to rebuild.

### Before the first refresh: exclude the tooling

The private tree's `.understandignore` ships entirely commented out, so nothing
is excluded by default. Before generating a map intended for publication,
activate at least:

```
.claude/
Emails/
Info files/
```

`.claude/` is AI tooling configuration — fifteen-plus skill definitions plus
local settings. Harmless, but it is not architecture and it is noise in a public
map. `Emails/` holds draft correspondence and is gitignored in the private tree
for that reason.

## The staleness rule

`meta.json` records `lastAnalyzedAt` and `gitCommitHash`. **That is a build
stamp, and it exists to be read.** The viewer displays it prominently and warns
when the map is more than 30 days old.

This matters because a generated map is exactly the kind of artifact that is
true when written and quietly stops being true. If the date is old, believe the
shape and distrust the detail — and if it is very old, regenerate before
pointing anyone at it.

Known trap: the graph's own `project.description` is generated prose and can
carry claims that have since been superseded. It described Phoenix as running
from a "single kernel8.img" long after the build had split into per-board
images. Re-read it after each refresh.
