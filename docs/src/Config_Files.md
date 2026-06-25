# Config Files

## Default locations

Catnap searches for its config in this order:

1. `$XDG_CONFIG_HOME/catnap/config.cat` (if `$XDG_CONFIG_HOME` is set)
2. `~/.config/catnap/config.cat`
3. `/etc/catnap/config.cat` (system-wide fallback)

Use `-c <path>` to point catnap at any `.cat` file instead.

---

## What gets installed

Running `nim install` (or following the binary release setup) creates:

```
~/.config/catnap/
├── config.cat              ← main config, the entry point catnap reads
├── distros.cat             ← all distro ASCII art definitions
└── themes/
    └── catppuccin-mocha.cat
```

---

## config.cat

This is the file catnap reads at startup. It is responsible for:

- Optionally importing a theme
- Importing `distros.cat`
- Defining all required and optional configuration variables
- Defining the `$stats` list

The default `config.cat` installed by `nim install`:

```
import "distros.cat"

$layout           = "inline"
$border_style     = "single"
$border_color     = $white
$stats_margin_top = 0
$location         = ""

$graph_width      = 15

$stats = [
    @{id="username"  icon=''   name="user"      color=$red}
    @{id="hostname"  icon=''   name="hostname"  color=$yellow}
    @{id="uptime"    icon=''   name="uptime"    color=$blue}
    @{id="separator"}
    @{id="kernel"    icon=''   name="kernel"    color=$magenta}
    @{id="distro"    icon=''   name="distro"    color=$green}
    @{id="packages"  icon=''  name="packages"  color=$red}
    @{id="separator"}
    @{id="desktop"   icon=''   name="desktop"   color=$cyan}
    @{id="terminal"  icon=''   name="term"      color=$red}
    @{id="shell"     icon=''   name="shell"     color=$magenta}
    @{id="separator"}
    @{id="battery"   icon=''  name="battery"   color=$green}
    @{id="gpu"       icon='󱔐'  name="gpu"       color=$magenta}
    @{id="cpu"       icon=''  name="cpu"       color=$red}
    @{id="cpu_usage" icon='%'  name="cpu use"   color=$red}
    @{id="disk_0"    icon=''  name="disk"      color=$green}
    @{id="memory"    icon=''  name="memory"    color=$yellow}
    @{id="separator"}
    @{id="weather"   icon=''  name="weather"   color=$blue}
    @{id="colors"    icon=''   name="colors"    color=$reset  symbol=''}
]
```

---

## distros.cat

Defines the `$distros` list: all ASCII art logos and the distro names that map to them. Imported by `config.cat` with:

```
import "distros.cat"
```

You rarely need to edit this file directly. If you do add a custom logo, consider [submitting it](https://github.com/iinsertNameHere/catnap) so others can benefit. See [Distro Art](Config_Distros.md) for the full syntax.

---

## themes/

Theme files are small `.cat` files that override variables. Applied with a single import at the top of `config.cat`:

```
import "themes/catppuccin-mocha.cat"

import "distros.cat"
...
```

The theme import must come first so its variable definitions are in place before stats and colors are resolved. See [Themes](Config_Themes.md).

---

## Custom config path

Point catnap at any `.cat` file with `-c`:

```shell
catnap -c ~/dotfiles/catnap/config.cat
```

`import` statements inside that file resolve relative to its location, so `import "distros.cat"` looks for `distros.cat` in the same directory as the config file.
