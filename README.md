# sqlite

The SQLite command-line shell for OpenCharly images — for creating and querying
self-contained SQLite databases.

The `sqlite` candy installs the `sqlite` package, which ships the `sqlite3` CLI at
`/usr/bin/sqlite3`. The binary runs SQL against an in-memory or on-disk SQLite
database.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `sqlite` |
| Binary | `/usr/bin/sqlite3` |
| Packages | `sqlite` (Fedora, Arch) |
| Distros | Fedora, Arch |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-sqlite:v2026.239.1638'
```

Then, inside the built image (or on a dev host):

```bash
sqlite3 --version
sqlite3 :memory: "CREATE TABLE t(x INTEGER); INSERT INTO t VALUES(42); SELECT x FROM t;"
```

The candy's `plan:` asserts the binary exists, the package is recorded, the
version is a 3.x string, and a real in-memory query returns the stored row — a
non-functional binary fails the check.

## Layout

- `charly.yml` — the `sqlite:` candy entity (the
  `distro.{arch,fedora}:` package sections and the `check:` probes) and the
  embedded `sqlite-skill:` skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-infrastructure:sqlite`
- Companion CLI bundle: `/charly-coder:dev-tools`
- Bundle: `/charly-openclaw:openclaw-full`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
