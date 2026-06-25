# Config Language

All catnap config files are written in a small, purpose-built config language. Files use the `.cat` extension.

> [!NOTE]
> This page is a complete technical reference for the language. If you just want to get started editing your config, [Quick Start](QuickStart.md) is the better place to begin.

---

## Comments

Single-line comments start with `;` and run to the end of the line:

```
; This is a comment
$layout = "inline"   ; inline comment
```

Multi-line comments are delimited by `;*` and `*;`:

```
;* ─────────────────────────────────
   Catppuccin Mocha - catnap theme
   ───────────────────────────────── *;
```

---

## Imports

Load and process another `.cat` file. The path is relative to the importing file.

```
import "distros.cat"
import "themes/catppuccin-mocha.cat"
```

Imports are evaluated before the rest of the file. This is how themes work: imported first, their variable definitions are in place before stats and colors are resolved.

---

## Variables

Variables start with `$`. Assign with `=`:

```
$name = value
```

**The last assigned value always wins.** Variable resolution happens after the entire file (and all its imports) is parsed, not at the point of assignment. This means:

```
$var1 = 12
$var2 = $var1
$var1 = 40

; $var2 resolves to 40, not 12
```

This also applies across imports. If `distros.cat` uses `$blue` in its art lines, and you redefine `$blue` after the import statement, the distros will use your new value:

```
import "distros.cat"    ; uses $blue internally

$blue = #89b4fa         ; this value applies to the distros too
```

---

## Value types

### String

Double-quoted text. Used for labels, paths, layout names, and city names.

```
$layout   = "inline"
$location = "London"
```

### Integer

A bare number. Used for margin and padding values.

```
$stats_margin_top = 2
$graph_width      = 20
```

### Boolean

`true` or `false`. Used for feature flags.

```
graph   = true
enabled = false
```

### Char

A single character in single quotes. Distinct from strings, and only used for `icon` and `symbol` fields in stat entries. Double quotes cause a parse error here.

```
icon   = ''
symbol = ''
```

### Color

Three notations are accepted wherever a color value is expected:

| Notation | Syntax | Example | Result |
|---|---|---|---|
| Hex | `#rrggbb` | `#f38ba8` | 24-bit ANSI escape (requires true-color terminal) |
| RGB | `(r g b)` | `(255 165 0)` | 24-bit ANSI escape, space-separated, no commas |
| ANSI code | `!n` | `!31` | Standard ANSI escape `\e[31m` |

```
$red    = #f38ba8       ; hex
$orange = (255 165 0)   ; RGB - spaces, no commas
$blue   = !34           ; raw ANSI code
```

All three resolve to ANSI escape sequences at startup. Hex and RGB require a terminal with true-color support.

### Variable reference

A `$name` used as a value resolves to that variable's final value (after all assignments in the entire file):

```
$accent     = #cba6f7
$stat_color = $accent   ; resolves to whatever $accent ends up being
```

---

## Lists

Lists hold multiple items, one per line, enclosed in `[` and `]`. No commas between items.

```
$items = [
    "first"
    "second"
    $somevar
]
```

The two lists used in practice are `$stats` and `$distros`. Both follow this list syntax. Only the item types inside differ.

---

## Stat objects

A stat object describes one entry in a stats block. It starts with `@{`:

```
@{id="statid"  key=value  key=value}
```

Stat objects can be stored in any variable or list, but in practice they are used as items in the `$stats` list. The recognized fields are:

| Field | Type | Description |
|---|---|---|
| `id` | string | Which stat to display. See [Stats](Config_Stats.md) for all IDs. |
| `icon` | char | Icon shown to the left of the label |
| `name` | string | Label text |
| `color` | color or variable | Color applied to icon and label |
| `enabled` | boolean | Set to `false` to skip this entry without removing it |
| `symbol` | char | Only meaningful for the `colors` stat. The swatch character. |
| `graph` | boolean | Only meaningful for stats that output a percentage. Renders a progress bar. |
| `graph_style` | string | Bar style. Only meaningful when `graph=true`. |
| `graph_width` | integer | Bar width in characters. Only meaningful when `graph=true`. |
| `graph_color_fg` | color | Filled-portion color. Only meaningful when `graph=true`. |
| `graph_color_bg` | color | Empty-portion color. Only meaningful when `graph=true`. |

A separator is a stat object with no icon or name, only an `id`:

```
@{id="separator"}
```

### Example

```
$stats = [
    @{id="username"  icon=''  name="user"    color=$red}
    @{id="hostname"  icon=''  name="host"    color=$yellow}
    @{id="separator"}
    @{id="memory"    icon=''  name="memory"  color=$yellow  graph=true}
    @{id="gpu"       icon=''  name="gpu"     color=$magenta  enabled=false}
    @{id="colors"    icon=''  name="colors"  color=$reset   symbol=''}
]
```

---

## Art objects

An art object defines a distro ASCII logo. It starts with `%{`:

```
%{id="name"  art=["line 1" "line 2"]  margin=[top left right]}
```

Art objects can be stored in any variable or list, but in practice they are used as items in the `$distros` list. The recognized fields are:

| Field | Type | Description |
|---|---|---|
| `id` | string or list of strings | Distro name(s) that map to this logo. A list enables aliases. |
| `art` | list of strings | Art lines, one string per row |
| `margin` | list of integers | Spacing around the logo (1, 2, or 3 values) |

### Example

```
$distros = [
    %{  id="arch"
        art=[
            "{$blue}      /\\      "
            "{$blue}     /  \\     "
        ]
        margin=[2 2 3]
    }

    %{  id=["mint" "linuxmint"]
        art=["..."]
        margin=[0 2 2]
    }
]
```

---

## String interpolation

Inside art line strings, switch color mid-line with `{$varname}`:

```
"{$blue}    /\\ /\\    "
"{$red}text here {$reset}back to terminal default"
```

All variables that resolve to a color work inside interpolation braces.

---

## Configuration variables

These are the variable names catnap reads by name when building its internal config. Other variables are valid to define (for reuse), but only these have a special meaning to the tool.

| Variable | Type | Required | Default | Description |
|---|---|---|---|---|
| `$stats` | list of stat objects | yes | | The stats to display, in order |
| `$distros` | list of art objects | yes | | All distro logo definitions |
| `$layout` | string | yes | | Layout mode: `"inline"`, `"art_on_top"`, `"stats_on_top"` |
| `$border_style` | string | yes | | Border style: `"single"`, `"double"`, `"dashed"`, `"dotted"`, `"none"` |
| `$border_color` | color | no | `!0` | Color of the border characters |
| `$text_color` | color | no | `!0` | Color of stat values on the right side |
| `$stats_margin_top` | integer | no | `0` | Blank lines above the stats block |
| `$location` | string | no | `""` | City name for the weather stat |
| `$graph_width` | integer | no | `15` | Default progress bar width for graph-enabled stats |

The 17 pre-injected color variables (`$red`, `$blue`, etc.) are also recognized. See [Colors](Colors.md) for the full list.

---

## Quick reference

```
; single-line comment

;* multi-line
   comment *;

import "other.cat"

$str    = "hello"           ; string
$num    = 42                ; integer
$flag   = true              ; boolean
$hex    = #f38ba8           ; hex color
$rgb    = (255 100 50)      ; RGB color - spaces, no commas
$ansi   = !31               ; ANSI color code
$ref    = $other            ; variable reference (resolves to final value of $other)

$list = [                   ; list - no commas between items
    "item1"
    $ref
]

; Stat objects
@{id="statid"  icon=''  name="label"  color=$red}
@{id="separator"}
@{id="gpu"  icon=''  name="gpu"  color=$magenta  enabled=false}

; Art objects
%{id="archlinux"  art=["  /\\  " " /  \\ "]  margin=[2 2 3]}
%{id=["mint" "linuxmint"]  art=["..."]  margin=[0 2 2]}

; Color interpolation in strings
$line = "{$blue}hello {$reset}world"
```
