# Stats

Stats are defined as a list assigned to `$stats` in `config.cat`. Display order matches list order.

> [!NOTE]
> `$stats` **must** be defined. Catnap cannot start without it.

> [!WARNING]
> The `packages`, `gpu`, and `weather` stats are slow. They run external commands or make network requests. Disable any you do not need.

---

## Stat entry syntax

```
@{id="statid"  icon=''  name="label"  color=$variable}
```

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string | yes | Which stat to display - see table below |
| `icon` | char | yes | Icon shown to the left of the label |
| `name` | string | yes | Label text |
| `color` | color or variable | yes | Color applied to icon and label |
| `enabled` | boolean | no | Set to `false` to hide this entry without removing it |

> [!IMPORTANT]
> `icon` must be a **char literal** in single quotes (`''`). Double quotes cause a parse error.

---

## Available stats

| ID | Description | Notes |
|---|---|---|
| `username` | Current user name | |
| `hostname` | Machine hostname | |
| `uptime` | System uptime | |
| `distro` | Distro name and architecture | |
| `kernel` | Kernel version | |
| `desktop` | Desktop environment or WM | |
| `shell` | Current shell | |
| `terminal` | Terminal emulator | |
| `cpu` | CPU model name | |
| `cpu_usage` | CPU usage percentage | Delta-based, shows `N/A` on first run |
| `memory` | RAM used / total | |
| `battery` | Battery percentage and charge status | |
| `gpu` | GPU model | Requires `glxinfo`. Slow. |
| `packages` | Installed package count | Depends on package manager. Slow. |
| `weather` | Current weather | Requires `curl` and emoji font. Slow. |
| `colors` | Terminal color swatch | Requires `symbol` field - see below |
| `disk_0`, `disk_1`, ... | Disk usage by mount index | Linux only |

> [!TIP]
> Run `catnap -g disks` to list all detected mount points and their `disk_N` index numbers.

---

## Separator

Draws a horizontal rule inside the stats block:

```
@{id="separator"}
```

Any number of separators can appear anywhere in the list.

---

## Colors stat

Shows a row of terminal color swatches. Requires a `symbol` char field - the character repeated once per color swatch:

```
@{id="colors"  icon=''  name="colors"  color=$reset  symbol=''}
```

---

## Disabling a stat

Use `enabled=false` to hide an entry without removing it from your config:

```
@{id="gpu"  icon='󱔐'  name="gpu"  color=$magenta  enabled=false}
```

You can also comment the line out with `;`:

```
; @{id="packages"  icon=''  name="pkgs"  color=$red}
```

---

## Reordering

Move lines up or down in the list. Display order exactly matches list order.

---

## Progress bar graphs

Stats that output a percentage value can show an inline progress bar. Add `graph=true` to the stat entry:

```
@{id="memory"    icon=''  name="memory"    color=$yellow  graph=true}
@{id="cpu_usage" icon='%'  name="cpu use"   color=$red     graph=true}
@{id="disk_0"    icon=''  name="disk"      color=$green   graph=true}
@{id="battery"   icon=''  name="battery"   color=$green   graph=true}
```

Stats that do not output a percentage (like `username` or `kernel`) will ignore `graph=true`.

The bar appears before the raw value: `▰▰▰▰▰▰▰▰▱▱▱▱ 67%`

### Graph options

These fields are per-stat only. The only global fallback is `$graph_width`.

| Field | Type | Default | Description |
|---|---|---|---|
| `graph_style` | string | `"precise"` | Bar rendering style - see table below |
| `graph_width` | integer | value of `$graph_width` | Width in characters |
| `graph_color_fg` | color | `$text_color` | Filled-portion color |
| `graph_color_bg` | color | `$text_color` | Empty-portion color |

### Bar styles

| Style | Example | Description |
|---|---|---|
| `"precise"` | `\|███▌      \|` | Sub-pixel 1/8-block precision (default) |
| `"blocks"` | `████░░░░░░` | Full-block and light-shade characters |
| `"thin"` | `▰▰▰▰▱▱▱▱▱` | Thin fill and empty bars |
| `"ascii"` | `[####------]` | ASCII-only, works in any terminal |
| `"dots"` | `●●●●○○○○○` | Filled and empty circles |
| `"pacman"` | `[---C   ooo]` | Inspired by the progress bar in the pacman package manager (Arch Linux) |

### Setting the global width

The `$graph_width` variable in `config.cat` sets the default bar width for all graph-enabled stats. Individual stats can override it with their own `graph_width` field.

```
$graph_width = 15   ; default for all graph-enabled stats
```

### Example with mixed styles

```
$graph_width = 15

$stats = [
    @{id="memory"
        icon=''  name="memory"  color=$yellow
        graph=true  graph_style="pacman"  graph_color_fg=$yellow}

    @{id="battery"
        icon=''  name="battery"  color=$green
        graph=true  graph_style="thin"  graph_color_fg=$green}

    @{id="cpu_usage"
        icon='%'  name="cpu use"  color=$red
        graph=true}

    @{id="disk_0"
        icon=''  name="disk"  color=$green
        graph=true  graph_width=20}
]
```

---

## Full example

```
$stats = [
    @{id="username"  icon=''   name="user"      color=$red}
    @{id="hostname"  icon=''   name="hostname"  color=$yellow}
    @{id="uptime"    icon=''   name="uptime"    color=$blue}
    @{id="separator"}
    @{id="distro"    icon=''   name="distro"    color=$green}
    @{id="kernel"    icon=''   name="kernel"    color=$magenta}
    @{id="packages"  icon=''  name="packages"  color=$red  enabled=false}
    @{id="separator"}
    @{id="desktop"   icon=''   name="desktop"   color=$cyan}
    @{id="terminal"  icon=''   name="term"      color=$red}
    @{id="shell"     icon=''   name="shell"     color=$magenta}
    @{id="separator"}
    @{id="cpu"       icon=''   name="cpu"       color=$red}
    @{id="cpu_usage" icon='%'  name="cpu use"   color=$red    graph=true}
    @{id="memory"    icon=''   name="memory"    color=$yellow
        graph=true  graph_style="pacman"  graph_color_fg=$yellow}
    @{id="disk_0"    icon=''   name="disk"      color=$green  graph=true}
    @{id="battery"   icon=''   name="battery"   color=$green
        graph=true  graph_style="thin"  graph_color_fg=$green}
    @{id="separator"}
    @{id="weather"   icon=''   name="weather"   color=$blue}
    @{id="colors"    icon=''   name="colors"    color=$reset  symbol=''}
]
```
