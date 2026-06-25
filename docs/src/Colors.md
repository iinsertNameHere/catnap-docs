# Colors

Catnap resolves all color values at startup into ANSI escape sequences. Three notations are accepted anywhere a color value is used: in stat `color` fields, variable assignments, and theme files.

---

## Notations

### Hex

`#` followed by six hex digits. Produces a 24-bit true-color escape. Requires a terminal with true-color support.

```
$red  = #f38ba8
$blue = #89b4fa
```

### RGB

Three space-separated integers in parentheses. Equivalent to hex, also 24-bit. No commas.

```
$orange = (255 165 0)
$purple = (180 100 240)
```

### ANSI code

`!` followed by a standard ANSI color number. Uses your terminal's built-in palette, so the shade is controlled by your terminal theme.

```
$red  = !31
$blue = !34
```

Standard ANSI codes: `!30`-`!37` (8 colors), `!90`-`!97` (bright variants), `!0` (reset all).

---

## Pre-injected variables

These are available in every config without definition. They default to ANSI codes so they adapt to your terminal's color scheme. Themes override them with explicit hex values.

| Variable | Default | Description |
|---|---|---|
| `$black` | `!30` | Black |
| `$red` | `!31` | Red |
| `$green` | `!32` | Green |
| `$yellow` | `!33` | Yellow |
| `$blue` | `!34` | Blue |
| `$magenta` | `!35` | Magenta |
| `$cyan` | `!36` | Cyan |
| `$white` | `!37` | White |
| `$bright_black` | `!90` | Bright black (grey) |
| `$bright_red` | `!91` | Bright red |
| `$bright_green` | `!92` | Bright green |
| `$bright_yellow` | `!93` | Bright yellow |
| `$bright_blue` | `!94` | Bright blue |
| `$bright_magenta` | `!95` | Bright magenta |
| `$bright_cyan` | `!96` | Bright cyan |
| `$bright_white` | `!97` | Bright white |
| `$reset` | `!0` | Reset all attributes |
| `$text_color` | `!0` | Color of stat values (right side of the stats block) |
| `$border_color` | `!0` | Color of the border characters |

---

## Defining custom colors

Define your own variables and reference them anywhere a color is accepted:

```
$brand   = #7c3aed
$warning = (255 180 0)

$stats = [
    @{id="cpu"  icon=''  name="cpu"  color=$brand}
]
```

---

## Colors in art lines

Inside art line strings, switch color mid-line using `{$varname}` interpolation:

```
"{$blue}    /\\ /\\    "
"{$red}left {$green}right {$reset}back to terminal default"
```

Any pre-injected or custom color variable works inside the braces. Use `{$reset}` to stop a colored section from bleeding into subsequent lines or the stats block.
