# 🪡 Installing Catnip

## Arch
If you are using any arch based distro with access to the [AUR](https://aur.archlinux.org/), you can install the [catnip-git](https://aur.archlinux.org/packages/catnip-git) package using your preferred aur helper.
```sh
$ yay -S catnip-git
```

## Build from source

**1.** Install all dependencies:
- **Required:**
`nim, pcre, gzip, usbutils`
- **Optional:** `figlet, viu`

**2.** Clone the official catnip repository:
```shell
git clone https://github.com/iinsertNameHere/catnip.git
```

**3.** Change dir into repository:
```shell
cd ./catnip
```

**4.** Run install using **nim**:
```shell
nim install
```
This will autommaticly build catnip and install it inside of your `/usr/local/bin` folder.

> **IMPORTANT**:
> For the default icons to work, make sure you set a [NerdFont](https://www.nerdfonts.com/) as you terminal font.