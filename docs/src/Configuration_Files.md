# 🗒️ Config Files 

# Default config files
The two main config files are located at `$XDG_CONFIG_HOME` or `~/.config/catnap/` if `$XDG_CONFIG_HOME` is not set.

The first file, called `config.toml`, is the file in which you configure the looks of catnap and in the second file, called `distros.toml`, you can find the definitions of all the distro logos used by catnap.

> **NOTE:** The config files are written in the [TOML](https://toml.io) configuration file format.

# Custom file paths
Using the `-c` and `-a` arguments, you can define custom locations for these two files. 

*For example:*
```shell
$ catnap -c /path/to/config.toml -a /path/to/distros.toml
```
