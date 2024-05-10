# 🗒️ Config Files 

# Default config files
The two main config files are located at
`~/.config/catnip/`.

The first file, called `config.toml`, is the file in which you configure the looks of catnip and in the second file, called `distros.toml`, you can find the definitions off all the distro logos used by catnip.

> **NOTE:** The config files are written in [toml](toml.io)

# Custom file paths
Using the `-c` and `-a` argument, you can define custom locations for these two files. 
*For example:*
```shell
$ catnip -c ~/my-custom-config.toml -a ~/my-custom-distros.toml
```