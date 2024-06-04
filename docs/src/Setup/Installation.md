# 🪡 Installing Catnap

## Arch Linux
If you are using any Arch-based distro with access to the [AUR](https://aur.archlinux.org/), you can install the [catnap-git](https://aur.archlinux.org/packages/catnap-git) package using your preferred AUR helper.
```sh
$ paru -S catnap-git
```

## Build from source

**1.** Install all dependencies:
- **Required:**
    - Build dependencies: `nim, gzip`
    - Runtime dependencies: `pcre`, `usbutils`

- **Optional:**
    - `figlet`: For figlet logos mode.
    - `viu`: For image mode.
    - `curl`: For weather stat.
    - `pciutils`: For GPU stat.

**2.** Clone the official catnap repository:
```shell
git clone https://github.com/iinsertNameHere/catnap.git
```

**3.** Change dir into repository:
```shell
cd ./catnap
```

**4.** Run install using **nim**:
```shell
nim install
```
This will automatically build catnap and install it inside of your `/usr/local/bin` folder.

> **IMPORTANT**:
> For the default icons to work, make sure you set a [NerdFont](https://www.nerdfonts.com/) as you terminal font. In addition, for the weather module to work, you will need a font that supports emojis.
