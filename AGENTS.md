# AGENTS.md — layer-sqlite

Standalone candy repo for the `sqlite` layer — the SQLite command-line shell. The
candy lives in `charly.yml` at the repo root: the per-distro package sections, the
`check:` probes, and the embedded `skill:` entity projected into the marketplace
corpus as `/charly-infrastructure:sqlite`.

Canonical files:

- `charly.yml` — the `sqlite:` candy entity and the `sqlite-skill:` skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-infrastructure:sqlite` — the owning skill. The package, the CLI path,
  and the query-verification contract. Load before editing or troubleshooting the
  candy.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, `distro:` sections, `package_map`). Load
  before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- `charly box validate` at the repo root checks the manifest parses and
  validates.
- The candy's `plan:` `check:` steps are the functional evidence: the binary at
  `/usr/bin/sqlite3`, the recorded package, a 3.x version string, and a real
  in-memory query returning the stored row.
- Two distro arms (`arch`, `fedora`) are declared; a package change must keep
  both arms and the matching `check:` probe honest.

## Modify this repo

- Edit the `sqlite:` candy entity AND the `sqlite-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a package or
  path change not mirrored in the skill leaves the corpus stale.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
