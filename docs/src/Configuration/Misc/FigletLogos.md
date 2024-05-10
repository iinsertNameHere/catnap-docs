# 🦖 FigletLogos Configuration

**File:** `config.toml`

The `[misc.figletLogos]` sections contains variables to configure *Figlet generated text logos*.

> **NOTE:** For this to work, the optional dependency `figlet` has to be installed.

## Enable/Disable
To enable or disable `figletLogos`, just set the `enable` variable to `true`/`false`.

```toml
enable = true 
```

## Color
The color option defines what color the *Figlet generated text*, is displayed in.

*Example: Use color Foreground-Bright-Green*
```toml
color = "{GN}"
```

## Font
The `figlet` font file to use when generating a `figletLogo`.
This value can also be a path, but please use only absolute paths.

```toml
font = "big"
```

## Margin
This option defines the `Top`, `Left` and `Right` margins for the `figletLogo`.

*`margin = [4, 1, 2]`, would be:*
```txt
             :             ╭────────────╮
             :             │ > user     │
             :             │ > hname    │
  _          :             ├────────────┤
 | |    ___   __ _  ___    │ > uptime   │
 | |   / _ \ / _` |/ _ \   │ > distro   │
.| |__| (_) | (_| | (_) |..│ > shell    │
 |_____\___/ \__, |\___/   │ > packages │
             |___/         │ > disk1    │
                           │ > disk2    │
                           ╰────────────╯
```