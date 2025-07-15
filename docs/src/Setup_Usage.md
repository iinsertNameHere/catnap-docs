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
This will show the commit hash your version of catnap is built on.

## Get a list of arguments:
```bash
$ catnap --help
```

## Get the stats value:
```bash
$ catnap -g <stat>
```
This will output the value of the stat to standard output.

## Change the location of the config.toml file
```bash
$ catnap -c <path>
```
>**Tip:**
>By default, Catnap will use the `$XDG_CONFIG_HOME/catnap/config.toml` or `~/.config/catnap/config.toml` if the `$XDG_CONFIG_HOME` environment variable is not set.

## Change the location of the distros.toml file
```bash
$ catnap -a <path>
```
>**Tip:**
>By default, Catnap will use the `$XDG_CONFIG_HOME/catnap/distros.toml` or `~/.config/catnap/distros.toml` if the `$XDG_CONFIG_HOME` environment variable is not set.

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

## Enable or disable Figlet logos
```bash
$ catnap -fe <on/off>
```

## Changes the margin (whitespace) of the Figlet logo
```bash
$ catnap -fm <matgin>
```
The format for the margin is: x,x,x (where x is a number)

## Changes the font used for Figlet
```bash
$ catnap -ff <font file>
```
>**Tip:**
>You will need a Figlet font file for this option, otherwise it will error out. You can get font files at <http://www.figlet.org/fontdb.cgi>
