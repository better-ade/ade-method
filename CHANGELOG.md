# Changelog

## Unreleased

- Specialists come from ade-agent-registry v1.1.0 (adds `forward-deployed`), the tag ade-cli already reads.

## 2.2.0

- Rule: AI attribution in commits and PRs follows the project's setting (`HUB_AI_ATTRIBUTION`; off unless the owner turns it on), instead of the fixed "no AI attribution" (owner decision 2026-11-23).
- `scripts/validate.mjs` checks that the rule names the setting.

## 2.1.0

- Rule: every commit and PR has the standard shape (overview, implementation, verification, Definition of Done checklist, related).
- Templates: `.github/pull_request_template.md` and `.ade/commit-template.txt`, listed in `ade.json` `install_templates`.

## 2.0.0

- Rebuilt small: four core roles, BMAD v6 only (pinned), specialists from ade-agent-registry v1.0.0, review scaled to risk, a section for people who don't write code.
