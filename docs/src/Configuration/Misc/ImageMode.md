# 🖼️ ImageMode Configuration

**File:** `config.toml`

The `[misc.imageMode]` section is used to configure the `ImageMode` feature, which lets you display an image instead of ASCII Art inside of you terminal.

> **NOTE:** For this to work, the dependency `viu` has to be installed.

## Enable/Disable
To enable or disable `figletLogos`, just set the `enable` variable to `true`/`false`.

```toml
enable = true 
```

## Path
This variable is used to define the **absolute** image path to the image which should be displayed.

```toml
path = "/home/user/Pictures/foo.png"
```

## Scale
Use this config variable to set the scale of the image.
```toml
scale = 20
```

## Margin
The `margin` variable is used to set the `top`, `left` and `right` margins of the Image.

*For example: `margin = [3, 3, 4]`*
```txt
        :         ╭────────────╮
        :         │ > user     │
        :         │ > hname    │
   ╭─────────╮    ├────────────┤
   │         │    │ > uptime   │
   │   FOO   │    │ > distro   │
   │   PNG   │    │ > pac      │
...|         |....│ > shell    │
   ╰─────────╯    | > disk1    │
                  │ > disk2    │
                  ╰────────────╯
```
