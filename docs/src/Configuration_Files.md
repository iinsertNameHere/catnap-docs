# 🗒️ Config Files 

# Default config files
The two main config files are located at `$XDG_CONFIG_HOME` or `~/.config/catnap/` if `$XDG_CONFIG_HOME` is not set.

In `config.toml` you configure the looks of catnap. In `distros.toml` you can find definitions for all distro logos used by catnap. In here you can also add custom logos.

> **NOTE:** The config files are written in the [TOML](https://toml.io) format.

# Custom file paths
Using the `-c` and `-a` arguments, you can define custom locations for these two files. 

*For example:*
```shell
$ catnap -c /path/to/config.toml -a /path/to/distros.toml
```
