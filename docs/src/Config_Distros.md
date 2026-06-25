# Distro Art

Distro art is defined in `distros.cat` as a list assigned to `$distros`. Each entry maps one or more distro names to an ASCII logo and margin.

> [!NOTE]
> `$distros` **must** be defined (typically in `distros.cat`, imported by `config.cat`). Catnap needs it to resolve which logo to show.

---

## User-defined art

Most fetch tools ship their distro art hardcoded into the tool itself. Adding a new distro typically requires modifying the tool's source code or using a special flag to supply an external file for a single run. In catnap, all logos live in `distros.cat`, a plain text file you own and edit directly. You can add, remove, or modify any logo without touching the binary.

---

## Art block syntax

```
%{id="name"  art=["line 1" "line 2"]  margin=[top left right]}
```

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string or list of strings | yes | Distro name(s) that map to this logo |
| `art` | list of strings | yes | Art lines, one string per row |
| `margin` | list of integers | yes | Spacing around the logo |

---

## Aliases

To map multiple distro names to the same logo, pass a list for `id`. The first name is the canonical ID:

```
%{id=["mint" "linuxmint"]  art=["..."]  margin=[0 2 2]}
```

---

## Multi-line form

Spread the block across lines for readability:

```
%{  id="arch"
    art=[
        "{$blue}      /\\      "
        "{$blue}     /  \\     "
        "{$blue}    /\\   \\    "
        "{$blue}   /      \\   "
        "{$blue}  /   ,,   \\  "
        "{$blue} /   |  |  -\\ "
        "{$blue}/_-''    ''-_\\"
    ]
    margin=[2 2 3]
}
```

---

## Margin

Controls spacing around the logo. Takes 1, 2, or 3 space-separated integers (no commas):

| Format | Meaning |
|---|---|
| `[n]` | Same value on all sides |
| `[top sides]` | Top row, then left and right equally |
| `[top left right]` | Each side set independently |

```
margin=[0 2 3]   ; 0 top, 2 left, 3 right
margin=[2]       ; 2 on all sides
margin=[1 3]     ; 1 top, 3 left and right
```

### Margin diagram

*`margin=[0 0 0]`*

```
      /\      ╭────────────╮
     /  \     │  distro    │
    /\   \    │  kernel    │
   /      \   │  memory    │
  /   ,,   \  │  cpu       │
 /   |  |  -\ ╰────────────╯
/_-''    ''-_\
```

*`margin=[3 3 3]`*

```
                   ╭────────────╮
                   │  distro    │
                   │  kernel    │
          /\       │  memory    │
         /  \      │  cpu       │
        /\   \     ╰────────────╯
       /      \
      /   ,,   \
     /   |  |  -\
    /_-''    ''-_\
```

Override margin per-run with `catnap -m top,left,right`.

---

## Colors in art lines

Use `{$varname}` inside an art line string to switch color mid-line. All pre-injected and custom color variables work:

```
"{$blue}    /\\ /\\    "
"{$red}left {$green}right {$reset}terminal-default"
```

Use `{$reset}` at the end of colored sections to prevent the color bleeding into the stats block.

Multi-color example:

```
%{  id="centos"
    art=[
        "{$green} ____{$yellow}^{$magenta}____  "
        "{$green} |\\  {$yellow}|{$magenta}  /|  "
        "{$magenta}<---- {$blue}----> "
        "{$blue} |/__{$green}|{$yellow}__\\|  "
    ]
    margin=[2 3 2]
}
```

---

## The `default` logo

The entry with `"default"` as its `id` (or as one name in an alias list) is shown when catnap cannot identify the running distro. In the bundled `distros.cat`, the Tux penguin carries this role:

```
%{  id=["tux" "default"]
    art=[...]
    margin=[2 2 3]
}
```

If no `"default"` entry exists and catnap cannot match the distro, no logo is displayed.

---

## Adding a custom distro

Open `distros.cat` and add a new art block:

```
%{  id="mylinux"
    art=[
        "{$cyan}  __  __ "
        "{$cyan} |  \\/  |"
        "{$cyan} | |\\/| |"
        "{$cyan} |_|  |_|"
    ]
    margin=[3 3 3]
}
```

Test it with:

```shell
catnap -d mylinux
```

> [!TIP]
> If you add art for a distro that is not in the default `distros.cat`, consider submitting it as a pull request to the [catnap repository](https://github.com/iinsertNameHere/catnap) so other users of that distro benefit from it too.

---

## Full minimal example

```
$distros = [
    %{  id="arch"
        art=[
            "{$blue}      /\\      "
            "{$blue}     /  \\     "
            "{$blue}    /\\   \\    "
            "{$blue}   /      \\   "
            "{$blue}  /   ,,   \\  "
            "{$blue} /   |  |  -\\ "
            "{$blue}/_-''    ''-_\\"
        ]
        margin=[2 2 3]
    }

    %{  id=["tux" "default"]
        art=[
            "{$black}      .--.     "
            "{$black}     |o_o |    "
            "{$black}     |:_/ |    "
            "{$black}    //   \\ \\   "
            "{$yellow}   (|     | )  "
            "{$yellow}  /'\\_   _/`\\  "
            "{$yellow}  \\___)=(___/  "
        ]
        margin=[2 2 3]
    }
]
```
