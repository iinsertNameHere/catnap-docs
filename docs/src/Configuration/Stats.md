# 💯 Stats Configuration

**File:** `config.toml`

## Icons
You can change the icon of any `stat` in side of the `[stats]` section.

```toml
username  = {icon = ">", name = "user", color = "(RD)"}
```

In this example, the default icon of the username `stat` was changed.

## Names
To change the name of a `stat`, you can just repeat the step for `Icons`.

```toml
username  = {icon = ">", name = "username", color = "(RD)"}
```

Here, the name of the *usrname* `stat` was changed.

## Colors
Changing the color a `stat` is displayed in, is as easy as changing the color code inside of the color field.

```toml
username  = {icon = ">", name = "user", color = "{YW}"}
```

In this example, the *username* `stat` would be displayed in bright Yellow.

## Disable/Enable Stats
In the case that you don't want a specific `stat` to be displayed, you can just make it a comment.

```toml
uptime    = {icon = ">", name = "uptime", color = "(BE)"}
# distro    = {icon = ">", name = "distro", color = "(GN)"}
```

In this case, the *uptime* `stat` would be displayed and the *distro* `stat` would be hidden.

## Adjust stat Order
To adjust the order in which the stats are displayed, you only have to change the orde of them in side of the config.

*Order in this example: **cpu**, **distro**, **uptime***
```toml
cpu       = {icon = ">", name = "cpu", color = "(RD)"}
distro    = {icon = ">", name = "distro", color = "(GN)"}
uptime    = {icon = ">", name = "uptime", color = "(BE)"}
```

*Order in this example: **uptime**, **cpu**, **distro***
```toml
uptime    = {icon = ">", name = "uptime", color = "(BE)"}
cpu       = {icon = ">", name = "cpu", color = "(RD)"}
distro    = {icon = ">", name = "distro", color = "(GN)"}
```

## Separators
You can use `separators` to add a horrizontal line across the `StatsBlock`.

```txt
╭────────────╮
│ > user     │
│ > hname    │
├────────────┤ <-- Separator1
│ > uptime   │
│ > distro   │
│ > kernel   │
│ > desktp   │
│ > term     │
├────────────┤ <-- Separator2
│ > shell    │
│ > packages │
╰────────────╯
```

You define a new `separator` using the prefix `sep_` and a unique name. THe value of the `separator` can be anything as it's not used by catnip.

```toml
sep_[name] = "My very cool separator!!!"
```

You can add as many `separators` as you wish!

## Disk Stats
The disk stats are defined using the prefix `disk_` and a index number.

```toml
disk_[index] = {icon = ">", name = "disk", color = "(BE)"}
```

The disk with index `0` is always the system drive.

You can get all available *disk* `stats` using:
```shell
$ catnip -g disks
```