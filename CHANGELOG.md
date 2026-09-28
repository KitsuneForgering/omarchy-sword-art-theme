# Changelog

Notable changes to this theme, newest first. Versions before 0.4.0 were
informal milestones for readability, not `git tag` references; `0.4.0`
is this project's first tagged release.

## Unreleased

- New `Icons` section in the README: `papirus-icon-theme` documented as
  the package behind `icons.theme`, how Omarchy applies it to GTK 3 and
  GTK 4 applications, how to verify it, and how to override or remove
  it.
- New optional `hooks/theme-set.d/50-icon-theme`, which gives Omarchy's
  own launcher the icon set the active theme declares. The shell resolves
  application icons by scanning the XDG icon directories rather than by
  reading `icons.theme`, so the launcher ignored the theme's icons; the
  hook links them into a user icon directory the shell scans first. It
  installs the matching icon package when the theme's icon theme is
  missing, and can be limited to the links alone with
  `OMARCHY_ICON_THEME_NO_INSTALL=1`.
- Fixed the README install URL. The cloned theme directory is named after
  the repository, so the previous URL installed to `sword-art` while
  `omarchy theme set "Sword Art Omarchy"` looks for `sword-art-omarchy`.
- The README no longer claims `Yaru-blue-dark` icons; it now matches the
  `Papirus-Dark` that `icons.theme` has declared since after 0.4.0.
- `tests/validate-theme.sh` now checks the hook is present and that the
  README documents both the declared icon theme and the hook install
  path; CI shellchecks the hook too.

## 0.4.0 — 2026-09-14 to 2026-09-16

- Interface screenshots and compatibility notes in the README
  (`docs/screenshots/`).
- `shell.toml` validated against Omarchy's TOML schema and shell
  surface tokens in CI, with a matching unittest suite.
- Launcher now shares the `[menu]` surface instead of a separate one.
- Raised `muted` and `dark_foreground` contrast to WCAG AA (4.5:1+)
  against the `#08090a` background.
- Added an automated WCAG AA contrast gate to `tests/validate-config.py`,
  covering every text/background token pair, including alpha-blended
  highlights.
- Losslessly recompressed every tracked PNG (~80MB → ~72MB repo size).
- Reworked the Plymouth `unlock.png` wordmark with Aincrad-style HUD
  corner brackets and register lines.
- Synced `preview-unlock.png` with the new HUD-framed `unlock.png` so the
  Plymouth theme picker matches the actual unlock screen.
- Added `COMPATIBILITY.md` and a fan-project/unofficial disclaimer in
  the README.
- Added `[polkit]`, `[lock]`, and `[image-picker]` tokens to `shell.toml`,
  extending the carbon/cyan treatment to the auth prompt, lock screen,
  and background picker (new surfaces in Omarchy 4.0.4). Extended
  `tests/validate-config.py`'s schema and contrast checks to match.

## 0.3.0 — 2026-09-06 to 2026-09-12

- Added `tests/validate-config.py` and a CI workflow to run it.
- Reduced dependence on the `bright_*` color tokens.

## 0.2.0 — 2026-08-30

- README rewritten to describe the Aincrad-inspired interface and
  install steps; removed an unused preview asset.

## 0.1.0 — 2026-08-30

- Initial Sword Art Online–themed assets, wallpapers, and README.
