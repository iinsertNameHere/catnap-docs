# 🚩 Main Misc Configuration

**File:** `config.toml`

## Layout
Using the `layout` variable you can define how the logo and stats will be arranged.
- Use `Inline` to place the logo and stats next to each other.
- Use `ArtOnTop` to place the logo on top of the stats.
- Use `StatsOnTop` to place the stats on top of the logo.

```toml
layout = "Inline"
```

In the example above, the `logo` and `stats` will be placed next to each other.

## Stats Margin Top
The `stats_margin_top` dictates how many lines the `StatsBlock` will be placed down.

*`stats_margin_top` is set to `3`:*
```
$ catnap
    :
    : 3x
    :
╭────────────╮
│ > user     │
│ > hname    │
├────────────┤
│ > uptime   │
│ > distro   │
│ > shell    │
│ > packages │
╰────────────╯
```

*`stats_margin_top` is set to `1`:*
```
$ catnap
    : 1x
╭────────────╮
│ > user     │
│ > hname    │
├────────────┤
│ > uptime   │
│ > distro   │
│ > shell    │
│ > packages │
╰────────────╯
```

> **NOTE:** This config variable is `optional` and can be removed.
