# CLAUDE.md

Guidance for Claude Code (and other AI assistants) working in this repository.

## What this repository is

`abhinavb66/Claude-sandbox` — a scratch repository for experimenting with Claude
Code. Per `README.md`: *"Repo for Claude code to play"*.

**Current state: the repository is effectively empty.** As of the latest commit
on `main` it contains exactly one tracked file:

```
.
└── README.md      # 2 lines: title + one-line description
```

There is no application code, no package manifest (`package.json`,
`pyproject.toml`, `go.mod`, `Cargo.toml`, …), no dependency lockfile, no test
suite, no linter or formatter config, no CI workflows (`.github/`), and no
`.gitignore`. History is a single commit, `ec27f71 Initial commit`.

**Do not infer a stack that isn't here.** There are no build, test, or lint
commands to run, because nothing defines any. If you are asked to "run the
tests" or "build the project," the honest answer is that neither exists yet —
say so rather than guessing at a toolchain.

## Working in a greenfield repo

Because this is a sandbox with no established conventions, the first
substantive change sets them. When adding code:

- **Pick and commit to one stack.** Add the manifest (`package.json`,
  `pyproject.toml`, etc.) in the same change as the first source file, so the
  project is runnable from a clean clone.
- **Add a `.gitignore` before the first build.** Nothing currently prevents
  `node_modules/`, `__pycache__/`, `.venv/`, `dist/`, or editor files from being
  committed.
- **Update this file in the same commit.** Every section below marked
  *(to be filled in)* should stop being a placeholder as soon as the
  corresponding thing exists. A `CLAUDE.md` describing a repo that has moved on
  is worse than none.
- **Prefer the smallest thing that works.** This is a sandbox; scaffolding a
  full framework for a one-file experiment is usually the wrong call. Match the
  scale of what was actually asked for.

## Commands *(to be filled in)*

| Purpose | Command |
| --- | --- |
| Install dependencies | — none defined |
| Build | — none defined |
| Run tests | — none defined |
| Lint / format | — none defined |

Populate this table the moment a manifest with scripts lands. Prefer recording
the exact invocation (`npm test`, `pytest -q`, `cargo test`) over prose.

## Architecture *(to be filled in)*

Nothing to describe yet. When code exists, document here the things that are
not obvious from reading a single file: how the pieces fit together, where the
entry point is, which boundaries matter, and any decision a newcomer would
otherwise have to reverse-engineer. Skip anything a file listing already makes
clear.

## Git workflow

This repository is worked on primarily through Claude Code sessions, which
imposes a specific branching convention:

- **Default branch:** `main`.
- **Never commit directly to `main`.** Work happens on a session-designated
  feature branch, typically named `claude/<short-topic>-<suffix>` (for example,
  the branch this file was authored on: `claude/claude-md-docs-au0912`). Create
  it locally if it does not exist.
- **Push with upstream tracking:** `git push -u origin <branch-name>`. On
  network failure, retry up to four times with exponential backoff
  (2s, 4s, 8s, 16s). Do not retry on non-network failures — read the error.
- **Do not open a pull request unless explicitly asked.** Pushing the branch is
  the deliverable by default.
- **A merged PR is finished.** If the designated branch's PR has already been
  merged, do not stack new commits on it. Restart the branch from the latest
  `main`
  (`git fetch origin main && git checkout -B <branch> origin/main`) and push the
  follow-up work as a new change. Preserve any unmerged commits by rebasing
  them onto the new base rather than discarding them.
- **Commit messages:** imperative mood, one-line summary, body only when the
  *why* is not obvious from the diff.

## Conventions for changes

- Match the surrounding code's style — naming, comment density, and idiom —
  once there is surrounding code to match.
- Keep the working tree clean: no stray scratch files, generated output, or
  debug scripts in commits. Use the session scratchpad directory for temporary
  work.
- Report outcomes plainly. If something was skipped, blocked, or unverified,
  state that explicitly rather than implying completeness.

## Environment notes

Sessions here may run in an ephemeral remote container: the repo is cloned
fresh at start and the container is reclaimed after inactivity. **Anything
worth keeping must be committed and pushed** — uncommitted work does not
survive the session. GitHub operations go through the GitHub MCP tools
(`mcp__github__*`); the `gh` CLI is not available.
