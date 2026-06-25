# Quick Start

You have installed catnap and run it once. This page walks through the most common customisations in a few minutes.

---

## What got installed

```
~/.config/catnap/
├── config.cat              ← main config, edit this
├── distros.cat             ← distro art, imported by config.cat
└── themes/
    └── catppuccin-mocha.cat
```

`config.cat` is the only file you normally need to touch. It imports `distros.cat` automatically.

---

## Apply a theme

Add one line at the very top of `config.cat`, before anything else:

```
import "themes/catppuccin-mocha.cat"

import "distros.cat"
...
```

The theme must be imported first so its color definitions are in place before stats are resolved. See [Themes](Config_Themes.md) for writing your own.

---

## Change which stats appear

Find the `$stats` list in `config.cat`. To hide a stat without deleting it, use `enabled=false`:

```
@{id="gpu"  icon=''  name="gpu"  color=$magenta  enabled=false}
```

You can also comment it out with `;`:

```
; @{id="packages"  icon=''  name="pkgs"  color=$red}
```

Reorder by moving lines. The display order matches the list order exactly.

```
$stats = [
    @{id="username"  icon=''  name="user"    color=$red}
    @{id="hostname"  icon=''  name="host"    color=$yellow}
    @{id="separator"}
    @{id="distro"    icon=''  name="distro"  color=$green}
    @{id="kernel"    icon=''  name="kernel"  color=$magenta}
    @{id="packages"  icon=''  name="pkgs"    color=$red  enabled=false}
    @{id="separator"}
    @{id="memory"    icon=''  name="memory"  color=$yellow  graph=true}
    @{id="colors"    icon=''  name="colors"  color=$reset   symbol=''}
]
```

---

## Change the layout

```
$layout = "art_on_top"
```

| Value | Effect |
|---|---|
| `"inline"` | Logo and stats side by side (default) |
| `"art_on_top"` | Logo above stats |
| `"stats_on_top"` | Stats above logo |

---

## Change the border style

```
$border_style = "double"
```

| Value | Border |
|---|---|
| `"single"` | `╭─╮ │ ╰─╯` (default) |
| `"double"` | `╔═╗ ║ ╚═╝` |
| `"dashed"` | `╭┄╮ ┊ ╰┄╯` |
| `"dotted"` | `•••  ┇  •••` |
| `"none"` | No border |

---

## Test a single stat

Use `-g` to print one stat value and exit. This is useful for checking that a stat works before adding it to your config, or for feeding a value into a script or status bar (such as Waybar):

```shell
catnap -g memory
catnap -g cpu_usage
catnap -g disks        # lists all detected disk mounts and their disk_N index numbers

# Example: use in a shell script
MEMORY=$(catnap -g memory)
echo "RAM: $MEMORY"
```

---

## Try a different distro logo

```shell
catnap -d arch
catnap -d void
catnap -d tux          # tux is the default/fallback logo
```

---

## Next steps

- [Config Language](Language.md): full language reference
- [Stats](Config_Stats.md): all stat IDs and graph options
- [Looks](Config_Looks.md): all layout and style variables
- [Distro Art](Config_Distros.md): adding or customising logos
- [Themes](Config_Themes.md): writing your own theme
