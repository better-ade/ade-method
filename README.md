# ade-method

How agents work in an ADE project: the rules, the four core roles, and ADE's BMAD v6 settings. Small on purpose:
everything else is loaded only when a task needs it.

```
rules.md          the method (installed in a project as .ade/rules.md): plan only as needed, build test-first,
                  the reviewer's verification run decides Done, review scaled to risk, cost rules, a section for
                  people who don't write code
agents/           the core roles, provider-neutral Markdown, no front matter:
                  product · architect · developer · reviewer
ade.json          what ADE reads: the core roles, the pinned specialist registry and BMAD commit, and the BMAD skills
                  a project gets by default, on demand, or never
bmad/custom/      overrides for BMAD v6 skills (copied into a project's _bmad/custom/)
templates/        the context store, decision log, role knowledge, coding standards, and the PR and commit
                  templates a project starts with
scripts/validate.mjs   the check this repo must pass: node scripts/validate.mjs
```

**Specialists** (frontend, backend, devops, sysadmin, security-reviewer, qa, analyst, monitor, support, and from
registry v1.1.0 forward-deployed) live in [ade-agent-registry](https://github.com/better-ade/ade-agent-registry),
pinned in `ade.json` (v1.0.0), and load only when a task needs one; `ade agent` reads the tag ade pins (v1.1.0).
**Skills and MCP servers** live in [ade-skills](https://github.com/better-ade/ade-skills).

Where it fits: [ade](https://github.com/better-ade/ade-cli) is the command, [ade-brain](https://github.com/better-ade/ade-brain)
the hub, ade-method (this repo) the rules, [ade-skills](https://github.com/better-ade/ade-skills) the skills,
[ade-secrets](https://github.com/better-ade/ade-secrets) the keys, [ade-terminal](https://github.com/better-ade/ade-terminal)
the desktop app, and [ade-computer](https://github.com/better-ade/ade-computer) an isolated desktop to run it in. More
at [ade.ardata.tech](https://ade.ardata.tech/).

## Using it

A project gets this repo at a pinned tag with [`ade init`](https://github.com/better-ade/ade-cli), run in the project.
It copies `rules.md` to `.ade/rules.md`, the core roles to `.ade/agents/`, `bmad/custom/` to `_bmad/custom/`, the
context store to `.ade/context/`, `templates/standards.md` to `docs/standards.md` and the `install_templates` in
`ade.json`; it never overwrites a file you have, and records the tag in `.ade/method-version`.

```bash
ade init                          # the tag ade pins (ade 0.2.8: v2.1.0)
ADE_METHOD_REF=v2.2.0 ade init    # the latest release
```

## Migrating from v1

v1 (tag `v1-final`) had a larger role set, BMAD v4 and a Claude-specific copy of the roles. In a v1 project, ADE
replaces `.ade/rules.md` and the four core role files, moves the retired role files and BMAD v4 into `.ade/archive/`,
and keeps `.ade/session.md` (the journal continues: one line per Done). Files a person edited are kept and reported,
never overwritten.

## Releasing

`node scripts/validate.mjs` passes, then tag `vX.Y.Z` on main.
