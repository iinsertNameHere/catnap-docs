# 💯 Stats Configuration

**File:** `config.toml`

> **NOTE:** The execution time of Catnap will increase when enabling the package manager, weather and GPU stats. Catnap **cannot** in any way decrease the time for the weather and package manager stats. This is due to the fact that the package manager stat is dependent on the speed of your distro's package manager, and the weather stat is dependent on your internet speed as well as the response time of the weather info website, [wttr.in](https://github.com/chubin/wttr.in).

## Icons
You can change the icon of any `stat` inside of the `[stats]` section.

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
Changing the color a `stat` is displayed in is as easy as changing the color code inside of the color field.

```toml
username  = {icon = ">", name = "user", color = "{YW}"}
```

In this example, the *username* `stat` would be displayed in bright Yellow.

## Disable/Enable Stats
In the case that you don't want a specific `stat` to be displayed, you can just comment it out.

```toml
uptime    = {icon = ">", name = "uptime", color = "(BE)"}
# distro    = {icon = ">", name = "distro", color = "(GN)"}
```

In this case, the *uptime* `stat` would be displayed but the *distro* `stat` would be hidden.

## Adjust stat Order
To adjust the order in which the stats are displayed, you only need to change the order of them inside of the config.

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
You can use `separators` to add a horizontal line across the `StatsBlock`.

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

You define a new `separator` using the prefix `sep_` and a unique name. The value of the `separator` can be anything as it's not used by catnap.

```toml
sep_[name] = "My very cool separator!!!"
```

You can add as many `separators` as you wish!

## Disk Stats
The disk stats are defined using the prefix `disk_` and an index number.

```toml
disk_[index] = {icon = ">", name = "disk", color = "(BE)"}
```

The disk with index `0` is always the system drive.

You can get all available *disk* `stats` using:
```shell
$ catnap -g disks
```
