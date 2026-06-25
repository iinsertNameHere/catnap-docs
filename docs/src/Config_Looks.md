# Looks

These top-level variables in `config.cat` control layout and visual style.

> [!NOTE]
> `$layout` and `$border_style` **must** be defined. Catnap cannot start without them.

---

## `$layout`

Arranges the distro logo and stats block relative to each other.

```
$layout = "inline"
```

| Value | Description |
|---|---|
| `"inline"` | Logo and stats side by side (default) |
| `"art_on_top"` | Logo printed above the stats |
| `"stats_on_top"` | Stats printed above the logo |

Override per-run with `catnap -l <value>`.

---

## `$border_style`

Characters used to draw the box around the stats block.

```
$border_style = "single"
```

| Value | Description |
|---|---|
| `"single"` | Solid single-line box (default) |
| `"double"` | Double-line box |
| `"dashed"` | Dashed lines |
| `"dotted"` | Dotted lines |
| `"none"` | No border characters |

---

## `$border_color`

Color of the border characters.

```
$border_color = $white
$border_color = #585b70
```

Pre-injected and defaults to `!0` (terminal default color) if not set.

---

## `$text_color`

Color applied to stat values, the text on the right side of the stats block.

```
$text_color = $white
$text_color = #cdd6f4
```

Pre-injected and defaults to `!0` (terminal default color) if not set. Themes typically define this to match their palette.

---

## `$stats_margin_top`

Number of blank lines above the stats block. Useful with `"inline"` layout when you want the stats to start lower than the top of a tall logo.

```
$stats_margin_top = 3
```

Defaults to `0`.

---

## `$location`

City name passed to the weather stat. If empty or omitted, catnap attempts to auto-detect your location via IP.

```
$location = "London"
```

Only relevant if `weather` is in your `$stats` list.

---

## `$graph_width`

Default bar width (in characters) for all graph-enabled stats. Individual stat entries can override it with their own `graph_width` field.

```
$graph_width = 15
```

See [Stats](Config_Stats.md) for per-stat graph options.

---

## Minimal valid example

```
$layout           = "inline"
$border_style     = "single"
$border_color     = $white
$stats_margin_top = 0
$location         = ""
```
