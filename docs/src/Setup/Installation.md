# 🪡 Installing Catnap

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
