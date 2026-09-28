# Sword Art Omarchy

An [Omarchy](https://omarchy.org/) theme inspired by Season 1 of Sword Art
Online — the black leather-and-steel look of Aincrad's system windows:
carbon-black backgrounds textured like a woven coat, with the bright
cyan-blue "Link Start" glow burning through the dark.

## System interface

`shell.toml` adds an Aincrad-inspired interface to Omarchy versions with
support for shell surface themes:

- Pale, translucent notification cards and tooltips with dark text.
- Thin borders with a stronger left edge on menus, launcher, and popups.
- Cyan hover, keyboard focus, and selection treatments on dark controls.
- An HP-inspired green notification lifetime indicator; critical alerts
  retain their red urgency color.
- The polkit auth prompt, lock screen, and background/theme picker also
  carry the carbon/cyan treatment, with the same HP-red error state.

The terminal palette and carbon wallpapers stay dark. The interface screenshots below show the applied theme; the background
previews in the Backgrounds section show wallpaper artwork.
Shell geometry follows Omarchy's components; this theme does not add custom
HUD widgets or change window-manager settings.

## Interface screenshots

Captured on Omarchy **4.0.3-1**, at **1920×1080**, with the repository's
`shell.toml` applied. The local shell override sets `[font] base-size = 14`;
bar layout and installed applications reflect the capture machine.

![Overview: bar, menu, launcher and notification over the theme wallpaper](docs/screenshots/overview.png)

The overview above is a composite: real crops of the bar, menu, launcher, and
notification from the captures below, placed over the theme wallpaper.

| Desktop and bar | Main menu |
|---|---|
| ![Desktop and bar](docs/screenshots/desktop.png) | ![Main menu with cyan selection](docs/screenshots/menu.png) |

| Application launcher | Demonstration notification |
|---|---|
| ![Application launcher](docs/screenshots/launcher.png) | ![Pale notification card](docs/screenshots/notification.png) |

These captures show the desktop, menu selection, launcher, and normal
notification surface. Critical urgency, tooltips, and the lifetime animation
still require separate visual verification.

## Install

This theme targets **Omarchy 4 (Quattro)** and its Quickshell interface.
The shell tokens were checked against the installed **4.0.3-1** source;
that is the compatibility reference, not a claim that every earlier 4.x
release was tested. Omarchy 3 and older are not supported by this package.
See the [upstream Quattro overview](https://github.com/omacom/omarchy/pull/6231)
for the shell transition, and [COMPATIBILITY.md](COMPATIBILITY.md) for
which Omarchy versions have actually been checked.

Check your installed version with `omarchy version`, then install:

```bash
# The icon set this theme asks for. See the Icons section below.
omarchy pkg add papirus-icon-theme

# The theme itself. The name of the cloned directory is taken from the
# repository name, so the URL has to stay Sword-Art-Omarchy for the
# `omarchy theme set` line below to find it.
omarchy theme install https://github.com/KitsuneSemCalda/Sword-Art-Omarchy
omarchy theme set "Sword Art Omarchy"

# Optional: give Omarchy's own launcher the same icon set. See Icons.
omarchy hook install theme-set \
  ~/.config/omarchy/themes/sword-art-omarchy/hooks/theme-set.d/50-icon-theme
```

The application launcher shares the `[menu]` surface in `shell.toml`.
Machine-wide overrides in `~/.config/omarchy/shell.toml` take precedence
over theme values and can change the appearance.

## Palette

| | |
|---|---|
| Background | `#08090a` |
| Panel | `#16181b` |
| Accent (cyan) | `#3ee8ff` |
| Foreground | `#e9f2f5` |
| HP (red) | `#ff3b5c` |
| MP (blue) | `#4f8dff` |

Icons: `Papirus-Dark`.

## Icons

This theme asks for **`Papirus-Dark`**, declared in `icons.theme` at the
repository root. That name means nothing without the icon theme on disk,
and a theme cannot install packages itself, so install it first:

```bash
omarchy pkg add papirus-icon-theme
```

`Papirus-Dark` comes from that package, which Arch ships as
`papirus-icon-theme`. Without it Omarchy falls back to `Yaru-blue` and the
declaration has no visible effect.

### Applications

Every time the theme changes, Omarchy reads `icons.theme` and applies it
through `org.gnome.desktop.interface icon-theme`, so GTK 3 and GTK 4
applications follow the theme with no extra configuration:

```bash
gsettings get org.gnome.desktop.interface icon-theme  # 'Papirus-Dark'
gtk-query-settings | grep gtk-icon-theme-name         # GTK 3
gtk4-query-settings | grep gtk-icon-theme-name        # GTK 4
```

Applications that were already running keep the icons they started with.
Reopen them, or log out and back in, to see the new set.

### The Omarchy launcher

Omarchy's own bar and launcher do not read the icon theme. The shell
resolves every application icon by scanning the XDG icon directories for
`apps/` and `devices/` entries and using the first path it finds for a
name, so the launcher shows whichever icon set that scan reaches first,
whatever `icons.theme` says.

`hooks/theme-set.d/50-icon-theme` closes that gap. It links the icons of
the active theme into `~/.local/share/icons`, which the shell scans
before `/usr/share`, so the theme wins that scan:

```bash
omarchy hook install theme-set \
  ~/.config/omarchy/themes/sword-art-omarchy/hooks/theme-set.d/50-icon-theme
```

The hook runs after each theme change, needs no root, and needs no
restart: the launcher re-reads its icon index every time the menu opens.
It follows whichever theme is active, and if that theme's icon theme is
not installed it installs the icon package first, the same way the
`omarchy pkg add` line above does, asking for a password in your terminal
or through a desktop prompt depending on where the theme switch came
from. Set `OMARCHY_ICON_THEME_NO_INSTALL=1` in your environment to keep
the hook to the links alone. Remove the hook with:

```bash
rm ~/.config/omarchy/hooks/theme-set.d/50-icon-theme
```

Two limits are worth knowing. An application that ships its own icon —
Flatpak, AUR and Electron applications usually do — keeps it: only the
`Icon=` names that an installed `.desktop` file asks for *and* that the
icon theme provides are linked, a few dozen on a typical install. And the
system tray shows the icon the running application hands over, which no
icon theme can change.

To use a different icon set, edit `icons.theme` in your local copy of the
theme, or overlay a single file over the packaged theme:

```bash
mkdir -p ~/.config/omarchy/themes/sword-art-omarchy
echo "Papirus" > ~/.config/omarchy/themes/sword-art-omarchy/icons.theme
omarchy theme set "Sword Art Omarchy"
```

## Backgrounds

Three 4K wallpapers — carbon-fiber texture only, no HUD elements, no
text. Just the material and a hint of ambient light, so icons and
windows stay legible on top.

<table>
<tr>
<td width="33%">

![ember](backgrounds/1-ember.png)
**`1-ember.png`**
A quiet cyan glow low in the corner.

</td>
<td width="33%">

![horizon](backgrounds/2-horizon.png)
**`2-horizon.png`**
The same glow, opposite corner.

</td>
<td width="33%">

![void](backgrounds/3-void.png)
**`3-void.png`**
No glow at all — pure carbon.

</td>
</tr>
</table>

`backgrounds/omarchy.png` is the wordmark wallpaper included in the theme's
background rotation, and `unlock.png` is the small logo mark shown on the
Plymouth unlock screen — both share the same carbon/cyan treatment.

`preview.png` and `preview-unlock.png` are compact selector previews derived
from the same artwork. They keep the theme visible in both the main Omarchy
theme picker and the Plymouth unlock-screen picker without loading the full
4K wallpapers.

![omarchy wordmark](backgrounds/omarchy.png)

All backgrounds and UI marks are original, generated artwork — no frames or
art from the anime were used.

## Fan project

Sword Art Omarchy is an unofficial, non-commercial fan project. It is not
affiliated with, endorsed by, or produced in association with Reki
Kawahara, ASCII Media Works, A-1 Pictures, Aniplex, or any other rights
holder of the *Sword Art Online* franchise. "Sword Art Online," "Aincrad,"
and related names and marks are trademarks of their respective owners,
used here only to describe the visual inspiration for this theme. This
repository distributes only original artwork and configuration files, and
grants no rights to any *Sword Art Online* trademark or copyrighted asset.

## Development

Run the package checks locally with **Python 3.11+**, **ImageMagick**,
and **ShellCheck** installed:

```bash
shellcheck tests/validate-theme.sh hooks/theme-set.d/50-icon-theme
python3 -m unittest discover -s tests -p 'test_*.py'
bash tests/validate-theme.sh
```

GitHub Actions runs the same validation on every push and pull request.
The checks cover TOML parsing, the semantic palette, required shell sections,
unknown keys, color formats, alpha ranges, border widths, and image formats.
The shell validator covers the subset used by this theme; extend its schema
when adding new supported Omarchy tokens.

`hooks/theme-set.d/50-icon-theme` is optional, so it is not run by the
validator. It links icon files and can install an icon package, so test it
where a wrong path or name matters: point it at a theme, run
`omarchy theme set`, and check
`~/.local/share/icons/.omarchy-theme-icons/<theme>/` holds symlinks that
resolve:

```bash
find ~/.local/share/icons/.omarchy-theme-icons/ -xtype l
```

### Visual verification

Automated checks do not verify rendering. The interface screenshots above
record the captured states; the artwork previews are not UI evidence.
Before adding screenshots or publishing a visual update:

1. Apply the repository version of the theme and record `omarchy version`.
2. Check the bar, application launcher, menus, and popups, including mouse
   hover, keyboard focus, and selected items.
3. Check normal and critical notifications: pale cards, legible dark text,
   a green lifetime indicator, and preserved red urgency. Check tooltips too.
4. Record any machine-wide shell overrides. Capture only the intended UI,
   with no private windows or notification content, into `docs/screenshots/`.
5. Embed the screenshots here with captions naming the surface and Omarchy
   version. Keep the existing picker previews as artwork.
