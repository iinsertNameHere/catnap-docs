# Installation

---

## From a GitHub release

Pre-built statically linked binaries are published on the [GitHub releases page](https://github.com/iinsertNameHere/catnap/releases). They have no external runtime dependencies.

Available binaries:

| File | Architecture |
|---|---|
| `catnap-linux-x86_64` | 64-bit x86 - most desktops and laptops |
| `catnap-linux-aarch64` | 64-bit ARM - Raspberry Pi 4+, ARM servers |
| `catnap-linux-armv7` | 32-bit ARM |
| `catnap-linux-i686` | 32-bit x86 |

**1.** Download the binary for your architecture, make it executable, and move it to your PATH:

```shell
curl -Lo catnap \
  https://github.com/iinsertNameHere/catnap/releases/latest/download/catnap-linux-x86_64
chmod +x catnap
sudo mv catnap /usr/local/bin/
```

**2.** Download the source tarball from the same release to get the config files, then copy them into place:

```shell
curl -Lo catnap-src.tar.gz \
  https://github.com/iinsertNameHere/catnap/releases/latest/download/catnap-$(catnap -v | cut -d' ' -f2)-source.tar.gz
tar xf catnap-src.tar.gz
mkdir -p ~/.config/catnap/themes
cp catnap/config/config.cat     ~/.config/catnap/
cp catnap/config/distros.cat    ~/.config/catnap/
cp catnap/config/themes/*.cat   ~/.config/catnap/themes/
```

**3.** Verify:

```shell
catnap
```

> [!NOTE]
> The default config uses [Nerd Font](https://www.nerdfonts.com/) glyphs for icons. Set a Nerd Font as your terminal font or icons will display as boxes. The weather stat also requires a font with emoji support.

---

## Updating (release)

Download the new binary and replace the old one:

```shell
curl -Lo catnap \
  https://github.com/iinsertNameHere/catnap/releases/latest/download/catnap-linux-x86_64
chmod +x catnap
sudo mv catnap /usr/local/bin/
```

Config files are not touched by a binary update. If a new release adds new config variables, the defaults built into the binary apply automatically.

---

## From source

**Dependencies:**

| Dependency | Purpose |
|---|---|
| `nim` | Build toolchain (2.x recommended) |
| `gzip` | Build toolchain |
| `pcre` | Runtime (regex) |
| `usbutils` | Runtime (hardware info) |

**1.** Clone the repository:

```shell
git clone https://github.com/iinsertNameHere/catnap.git
cd catnap
```

**2.** Build and install:

```shell
nim install
```

This compiles catnap in release mode, installs the binary to `/usr/local/bin/`, and copies the default config files to `~/.config/catnap/`:

```
~/.config/catnap/
├── config.cat
├── distros.cat
└── themes/
    └── catppuccin-mocha.cat
```

> [!NOTE]
> `nim install` requires `sudo` to write to `/usr/local/bin/`. To install without sudo, use `nim setup` instead. It builds the binary (placed in `bin/catnap` locally) and copies the config files to `~/.config/catnap/`, but does not install the binary to your PATH.

**3.** Verify:

```shell
catnap
```

---

## Updating (source)

Pull the latest changes and reinstall:

```shell
git pull
nim install
```

Your config files in `~/.config/catnap/` are not overwritten by `nim install`. Only the binary is replaced.

> [!WARNING]
> If you have local edits in the cloned source `config/` directory, `git pull` may produce merge conflicts there. Your installed config in `~/.config/catnap/` is always separate and is not affected by git operations.
