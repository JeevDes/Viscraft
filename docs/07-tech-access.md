# Tech access

How to reconnect to the Viscraft Framer project and this repo from a fresh session. Useful for either collaborator, since both are working via Claude CLI.

## Framer project

- Name: Viscraft, Project ID: `sFkAsTdY4Br19dZHQBSe`
- URL: https://framer.com/projects/Viscraft--sFkAsTdY4Br19dZHQBSe
- Reconnect: run `npx @framer/agent@latest session new "sFkAsTdY4Br19dZHQBSe"` (or the full project URL above) — this opens a browser approval prompt and prints a session ID. Use that session ID with `-s <id>` on every subsequent command.
- First-time setup on a new machine: run `npx @framer/agent@latest setup` once — installs the `/framer` and `/framer-code-components` skills into `~/.claude/skills` and `~/.agents/skills`.
- Read the `/framer` skill's generated task map before any canvas/CMS/component work (it's regenerated per-machine by `session new`).
- Per `01-overview.md`: work on a Framer branch, never publish to live. Framer branching is a Pro, project-level feature — create a branch before making changes each time you pick this back up.

## This repo

- Remote: https://github.com/JeevDes/Viscraft
- Site itself has no code export — this repo is docs/wireframes/assets only, not the site's source.
- Two people work on this independently via Claude CLI on the same remote — pull/fetch explicitly before starting work each session, don't assume local state is current. Prefer a branch + deliberate merge over committing straight to `main`.

See [`05-build-log.md`](05-build-log.md) for what has actually been built so far, and [`01-overview.md`](01-overview.md) for the project brief this all serves.
