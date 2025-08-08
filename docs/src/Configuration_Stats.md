# 💯 Stats Configuration

**File:** `config.toml`

> **Note:** Enabling package manager, weather, and GPU stats will increase Catnap’s execution time.
> Catnap **cannot** speed up these stats:
>
> * **Package manager** speed depends on your distro’s package manager.
> * **Weather** speed depends on your internet connection and the response time of [wttr.in](https://github.com/chubin/wttr.in).

---

## Changing Icons

You can customize the icon for any stat in the `[stats]` section:

```toml
username = {icon = ">", name = "user", color = "(RD)"}
```

Here, the default icon for the `username` stat was changed to `>`.

---

## Renaming Stats

To rename a stat, just manupulate the `name` field:

```toml
username = {icon = ">", name = "username", color = "(RD)"}
```

Now the `username` stat will be displayed as **"username"** instead of its default name.

---

## Changing Colors

To change a stat’s display color, modify the `color` value:

```toml
username = {icon = ">", name = "user", color = "{YW}"}
```

This will display the `username` stat in **bright yellow**.

---

## Enabling or Disabling Stats

To hide a stat, simply comment out its line:

```toml
uptime = {icon = ">", name = "uptime", color = "(BE)"}
# distro = {icon = ">", name = "distro", color = "(GN)"}
```

Here, `uptime` is shown, while `distro` is hidden.

---

## Adjusting Stat Order

The display order is based on the order in the config file.
Example:

**Order:** CPU → Distro → Uptime

```toml
cpu    = {icon = ">", name = "cpu", color = "(RD)"}
distro = {icon = ">", name = "distro", color = "(GN)"}
uptime = {icon = ">", name = "uptime", color = "(BE)"}
```

**Order:** Uptime → CPU → Distro

```toml
uptime = {icon = ">", name = "uptime", color = "(BE)"}
cpu    = {icon = ">", name = "cpu", color = "(RD)"}
distro = {icon = ">", name = "distro", color = "(GN)"}
```

---

## Adding Separators

Separators create horizontal dividers in the stats block.

Example layout:

```txt
╭────────────╮
│ > user     │
│ > hname    │
├────────────┤  <-- Separator 1
│ > uptime   │
│ > distro   │
│ > kernel   │
│ > desktp   │
│ > term     │
├────────────┤  <-- Separator 2
│ > shell    │
│ > packages │
╰────────────╯
```

To add a separator:

```toml
sep_[name] = "Any text here (value not used by Catnap)"
```

You can add as many as you like.

---

## Disk Stats

Disk stats use the `disk_` prefix followed by an index number:

```toml
disk_[index] = {icon = ">", name = "disk", color = "(BE)"}
```

* `disk_0` is always the **system drive**.
* To list all available disks:

```sh
catnap -g disks
```