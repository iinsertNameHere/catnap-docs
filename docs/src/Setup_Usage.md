# 💻 Usage


## Run catnap in you terminal:
```bash
$ catnap
```
This will use the default config files

## Change the distro icon:
```bash
$ catnap -d <distro>
```
This will use the specified distro logo as long as it is in the distros.toml file.

## Check the current version:
```bash
$ catnap -v
```

## Get a list of arguments:
```bash
$ catnap --help
```

## Grep just one value
```bash
$ catnap -g <stat>
```
This will output just the value of a stat to standard output.
This can be usefull for usage in scripts or waybar for example.

## Use custom config TOML file
```bash
$ catnap -c <path>
```
>**Tip:**
>By default, Catnap will use the `$XDG_CONFIG_HOME/catnap/config.toml` or `~/.config/catnap/config.toml` if `$XDG_CONFIG_HOME` is not set.

## Use custom distros TOML file
```bash
$ catnap -a <path>
```
>**Tip:**
>By default, Catnap will use the `$XDG_CONFIG_HOME/catnap/distros.toml` or `~/.config/catnap/distros.toml` if `$XDG_CONFIG_HOME` is not set.

## Change the margin (whitespace) for the logo
```bash
$ catnap -m <margin>
```
The format for the margin is: x,x,x (where x is a number)

## Change the layout
```bash
$ catnap -l <layout>
```
This changes the layout of the logo or stats

Available layouts:
- StatsOnTop
- ArtOnTop
- Inline
