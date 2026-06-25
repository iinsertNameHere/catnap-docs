# Themes

A theme is a `.cat` file that redefines variables before the rest of `config.cat` is processed. Because of how [variable resolution](Language.md) works (last assignment wins), a theme import at the top of your config means the theme's values take effect everywhere, including stat colors and art line interpolation.

---

## Applying a theme

Add one `import` line at the very top of `config.cat`, before anything else:

```
import "themes/catppuccin-mocha.cat"

import "distros.cat"

$layout       = "inline"
$border_style = "single"
...
```

The theme import must come first so its definitions are in scope before stats and colors are resolved.

---

## Bundled theme: Catppuccin Mocha

The default installation includes `themes/catppuccin-mocha.cat`, a port of the [Catppuccin Mocha](https://github.com/catppuccin/catppuccin) palette. It overrides all 17 color variables and sets `$text_color` to match the palette's text color.

To apply it, add the import at the top of your `config.cat`:

```
import "themes/catppuccin-mocha.cat"
```

---

## Writing a custom theme

A theme only needs to redefine the variables you want to change. Omitted variables keep their defaults.

Create a file in `~/.config/catnap/themes/`:

```
; themes/my-theme.cat

$red     = #ff6e6e
$green   = #69ff94
$yellow  = #ffffa5
$blue    = #d6acff
$magenta = #ff92df
$cyan    = #a4ffff
$white   = #ffffff

$text_color   = #f8f8f2
$border_color = #44475a
```

Then import it at the top of `config.cat`:

```
import "themes/my-theme.cat"
```

---

## What a theme can override

Theoretically, a theme file can redefine **any** variable, not just colors. You could override `$stats_margin_top`, `$graph_width`, or even replace `$stats` or `$distros` entirely. In practice, themes are used for color variables, but there is no technical restriction.

Common variables to set in a theme:

| Variable | Effect |
|---|---|
| `$black` ... `$bright_white` | Applied wherever `color=$varname` is used in stats or art |
| `$text_color` | Color of stat values on the right side of the stats block |
| `$border_color` | Color of the border characters around the stats block |

---

## How themes affect art

Color interpolation in art lines (`{$red}`, `{$blue}`, etc.) resolves through theme values. If your theme sets `$blue = #89b4fa`, art lines using `{$blue}` render in that color. One theme file reskins both the stat labels and the ASCII logos.

---

## Switching themes

Change the import line at the top of `config.cat`. Since the last assigned value wins, only one theme can be meaningfully active at a time. Importing two themes means the second one's values overwrite the first where they overlap.
