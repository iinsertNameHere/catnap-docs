# 💻 Usage


## Run catnip in you terminal:
```bash
$ catnip
```
This will use the default config files

## Change the distro icon:
```bash
$ catnip -d <distro>
```
This will use the specified distro logo as long as it is in the distros.toml file.

## Check the current version:
```bash
$ catnip -v
```
This will show the commit hash your version of catnip is build on.

## Get a list of arguments:
```bash
$ catnip --help
```

## Get the stats value:
```bash
$ catnip -g <stat>
```
This will output the value of the stat into standard output.

## Change the location of the config.toml file
```bash
$ catnip -c <path>
```
>**Tip:**
>By default, Catnip will use the `$XDG_CONFIG_HOME/catnip/config.toml` or `~/.config/catnip/config.toml` if the `$XDG_CONFIG_HOME` environment variable is not set.

## Change the location of the distros.toml file
```bash
$ catnip -a <path>
```
>**Tip:**
>By default, Catnip will use the `$XDG_CONFIG_HOME/catnip/distros.toml` or `~/.config/catnip/distros.toml` if the `$XDG_CONFIG_HOME` environment variable is not set.

## Change the margin (whitespace) for the logo
```bash
$ catnip -m <margin>
```
The format for the margin is: x,x,x (where x is a number)

## Change the layout
```bash
$ catnip -l <layout>
```
This changes the layout of the logo or stats
Available layouts:
- StatsOnTop
- ArtOnTop
- Inline

## Enable or disable Figlet logos
```bash
$ catnip -fe <on/off>
```

## Changes the margin (whitespace) of the Figlet logo
```bash
$ catnip -fm <matgin>
```
The format for the margin is: x,x,x (where x is a number)

## Changes the font used for Figlet
```bash
$ catnip -ff <font file>
```
>**Tip:**
>You will need a Figlet font file for this option, otherwise it will error out. You can get font files at http://www.figlet.org/fontdb.cgi
