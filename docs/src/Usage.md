# Usage

```shell
catnap [options]
```

With no flags, catnap reads `~/.config/catnap/config.cat` (or `$XDG_CONFIG_HOME/catnap/config.cat`) and prints the fetch output.

---

## Flags

### `-c` / `--config <path>`

Use a custom config file instead of the default.

```shell
catnap -c ~/dotfiles/catnap/config.cat
```

`import` statements inside the file resolve relative to that file's location, so `import "distros.cat"` looks for `distros.cat` next to it.

---

### `-d` / `--distroid <id>`

Override which distro logo is displayed, regardless of what the system reports.

```shell
catnap -d arch
catnap -d void
catnap -d tux
```

The ID must match an entry defined in your `distros.cat`. Run `catnap -g distro` to see what catnap detects automatically.

---

### `-g` / `--grep <stat>`

Print a single stat value to stdout and exit.

```shell
catnap -g username
catnap -g memory
catnap -g cpu_usage
catnap -g disks        # lists all detected mounts and their disk_N index numbers
```

This is useful for testing individual stats while building your config, and for integrating catnap into scripts or status bars (such as Waybar or i3blocks):

```shell
# Shell script example
MEMORY=$(catnap -g memory)
UPTIME=$(catnap -g uptime)
echo "$UPTIME | $MEMORY"
```

---

### `-l` / `--layout <layout>`

Override the layout for this run without editing the config.

```shell
catnap -l art_on_top
```

Available values: `inline`, `art_on_top`, `stats_on_top`. See [Looks](Config_Looks.md) for details.

---

### `-m` / `--margin <top,left,right>`

Override the logo margin for this run. Values are comma-separated integers.

```shell
catnap -m 0,2,3
catnap -m 2,2,2
```

---

### `-n` / `--no-cache`

Clear the cache before running. Use this if a stat is showing a stale value.

```shell
catnap -n
```

---

### `-v` / `--version`

Print the catnap version and exit.

```shell
catnap -v
```

---

### `-h` / `--help`

Print a summary of all flags plus the full list of available stat names and distro IDs.

```shell
catnap -h
```
