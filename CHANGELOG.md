# Changelog

All notable changes to PaperJury are documented in this file.

## [1.1.0] - 2026-06-12

The trivia-flood fix (F3), from real user feedback: "阻断 AI 去关注非常细微没有价值的
问题" (stop the AI from chasing tiny, worthless issues). Backward-compatible; no
schema bump, existing ledgers render identically until a mode is set.

### Added

- **The significance floor, now in code.** `node scripts/ledger.js floor
  <ledger.json>` returns `{fixable, excluded}`: the drafter's input is exactly the
  valid-fixable MAJOR rows, and any valid-fixable non-major is excluded with its id
  reported (read-only, never silent). This is the floor `references/auto-mode.md`
  had promised; it is now the normative builder of the drafter's fixable set
  (review-engine-v3.md step 13 / SEAM 4). A polish item escalated to trial is
  promoted to `significance: major` as part of the escalation contract, so a
  later valid-fixable verdict on it passes the floor.
- **Collapsed ledger view.** `LEDGER.json` meta gains an optional `display_mode`
  (`show`|`collapse`; absent = `show`, the previous behavior byte-for-byte). In
  `collapse`, `LEDGER.md` keeps majors as itemized table rows and folds minors
  into a "Minor digest": open/queued minors one compact line each (a pending
  decision is never hidden), terminal minors as per-status count lines, plus a
  never-drop footer. Render-only -- counts, the completion gate, statuses, and
  routing are untouched, and full detail stays in `LEDGER.json`. New commands:
  `node scripts/ledger.js mode <ledger.json> <show|collapse>` and
  `node scripts/ledger.js init ... --display <show|collapse>`. Auto mode
  initializes collapsed; review mode keeps the flat table by default.

### Notes

- The minor/mechanical fixes themselves still happen (the polish track is
  unchanged); the flood is treated at the presentation layer, never by dropping
  work. Issues are never silently dropped.
- `reason_code: batched-nit` remains in the schema as RESERVED: the composite-
  packing design it anticipated was evaluated against real run data and rejected
  (see `docs/AUTO_MODE_DESIGN.md` changelog, 2026-06-12, which also records the
  formal override of the 2026-06-10 design-debate archive's ship recommendation).

## [1.0.0] - 2026-06-10

First stable release, aligned with the Codex port's v1.0.

### Added

- **Soft update reminders.** `scripts/check-update.js` soft-checks stable GitHub
  release tags at PaperJury startup and prints a non-blocking update notice
  (plugin and clone routes). Silent when GitHub is unreachable; disable with
  `PAPERJURY_DISABLE_UPDATE_CHECK=1`.

### Changed

- **Dogfood sample PDFs restored to the repo.** `original_draft.pdf` and
  `revised_draft.pdf` live in `samples/dogfood/` again, so the public repo is
  self-contained; they are no longer distributed as release assets.
- **Version promoted to 1.0.0** across the plugin manifest, marketplace listing,
  package manifest, and `SKILL.md` frontmatter. The `v0.5.0` release and tag are
  superseded by `v1.0.0`.

## [0.5.0] - 2026-06-05

### Added

- **Claude Code plugin packaging.** PaperJury can now be installed as a Claude Code
  plugin from a self-hosted marketplace, alongside the existing clone-as-skill install.
  - `.claude-plugin/plugin.json` — plugin manifest. Declares the skill at the repo
    root (`"skills": ["./"]`, root-as-skill) so `SKILL.md` does not move and the
    plain-skill install keeps working.
  - `.claude-plugin/marketplace.json` — self-hosted marketplace listing this one
    plugin (`source: "./"`).
  - Install: `/plugin marketplace add u7079256/paperjury` then
    `/plugin install paperjury@u7079256`.

### Notes

- This change is additive and non-breaking: `SKILL.md` stays at the repo root and is
  still auto-discovered as a plain skill, so the existing `~/.claude/skills/paperjury`
  install (clone-as-skill) is unaffected.
- The plugin manifest version tracks the skill engine version in `SKILL.md` frontmatter.
- This is the first tracked changelog entry; it documents the packaging change shipped
  on top of the existing 0.5.0 engine, not the full engine history.
