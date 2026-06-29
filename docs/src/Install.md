# Installation

There are four ways to install catnap. Pick the one that fits your situation:

| Method | Good for |
|---|---|
| [Quick install](#quick-install) | Good for most users. Gets you running in under a minute |
| [From source](#from-source) | Contributors and developers who want the latest code |
| [GitHub release (manual)](#manual-install-from-a-github-release) | Installing without the script, or scripting your own setup |
| [Static build from source](#static-build-from-source) | Building a fully self-contained binary yourself |

---

## Quick install

The easiest and fastest way to install catnap is using the release install helper script. It detects your architecture, downloads the right static binary and config files from the latest GitHub release, and puts everything in place. The binaries are statically linked, so catnap has no runtime dependencies after install. The script itself requires `bash`, `curl`, and `tar` to be available on your system.

```shell
# Download the install script
curl -Lo install.sh https://raw.githubusercontent.com/iinsertNameHere/catnap/main/install.sh

# Install catnap
sudo bash ./install.sh
```

> [!WARNING]
> As a general rule, always review scripts before running them as root. You can read the install script on [GitHub](https://github.com/iinsertNameHere/catnap/blob/main/install.sh) before downloading.

**Updating:** Run the script again. It will show your currently installed version alongside the latest and ask before proceeding:

```shell
sudo bash install.sh
```

**Uninstalling:**

```shell
sudo bash install.sh uninstall
```

---

## From source

Build catnap yourself if you want the latest unreleased changes or plan to contribute. This produces a dynamically linked binary that depends on `pcre` and `usbutils` at runtime.

**Dependencies:**

| Dependency | Purpose |
|---|---|
| `nim` | Build toolchain (v2.x+) |
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
> `nim install` requires `sudo` to write to `/usr/local/bin/`. To install without sudo, run `nim setup` instead. It builds the binary (placed in `bin/catnap` locally) and copies the config files to `~/.config/catnap/`. This lets you place the binary wherever you like.

**3.** Verify:

```shell
catnap
```

**Updating:** Pull the latest changes and reinstall:

```shell
git pull
nim install
```

Your config files in `~/.config/catnap/` are not overwritten by `nim install`. Only the binary is replaced.

> [!WARNING]
> If you have local edits in the cloned source `config/` directory, `git pull` may produce merge conflicts there. Your installed config in `~/.config/catnap/` is always separate and is not affected by git operations.

---

## Manual install from a GitHub release

Pre-built statically linked binaries are published on the [GitHub releases page](https://github.com/iinsertNameHere/catnap/releases). They have no external runtime dependencies.

Available binaries:

| File | Architecture |
|---|---|
| `catnap-{version}-x86_64` | 64-bit x86 - most desktops and laptops |
| `catnap-{version}-aarch64` | 64-bit ARM - Raspberry Pi 4+, ARM servers |
| `catnap-{version}-armv7l` | 32-bit ARM |
| `catnap-{version}-i686` | 32-bit x86 |

**1.** Download the binary for your architecture and move it to your PATH. Replace `x86_64` with your arch if needed:

```shell
VERSION=$(curl -Ls -o /dev/null -w '%{url_effective}' https://github.com/iinsertNameHere/catnap/releases/latest | grep -oE 'v[0-9]+\.[0-9]+\.[0-9]+')
curl -Lo catnap "https://github.com/iinsertNameHere/catnap/releases/download/${VERSION}/catnap-${VERSION}-x86_64"
chmod +x catnap
sudo mv catnap /usr/local/bin/
```

**2.** Download the config tarball from the same release and copy the files into place:

```shell
VERSION=$(catnap -v | cut -d' ' -f2)
curl -Lo catnap-config.tar.gz \
  "https://github.com/iinsertNameHere/catnap/releases/download/${VERSION}/catnap-${VERSION}-config.tar.gz"
tar xf catnap-config.tar.gz
mkdir -p ~/.config/catnap/themes
cp config/config.cat   ~/.config/catnap/
cp config/distros.cat  ~/.config/catnap/
cp config/themes/*.cat ~/.config/catnap/themes/
```

**3.** Verify:

```shell
catnap
```

> [!NOTE]
> The default config uses [Nerd Font](https://www.nerdfonts.com/) glyphs for icons. Set a Nerd Font as your terminal font or the icons will show as boxes. The weather stat also requires a font with emoji support.

**Updating:** Download the new binary and replace the old one:

```shell
VERSION=$(curl -Ls -o /dev/null -w '%{url_effective}' https://github.com/iinsertNameHere/catnap/releases/latest | grep -oE 'v[0-9]+\.[0-9]+\.[0-9]+')
curl -Lo catnap "https://github.com/iinsertNameHere/catnap/releases/download/${VERSION}/catnap-${VERSION}-x86_64"
chmod +x catnap
sudo mv catnap /usr/local/bin/
```

Config files are not touched by a binary update. If a new release adds new config variables, the defaults built into the binary apply automatically.

---

## Static build from source

This produces a fully self-contained binary with no runtime dependencies, built using musl libc. Useful if you want a portable binary you can move between systems or distribute yourself.

**Dependencies:**

| Dependency | Purpose |
|---|---|
| `nim` | Build toolchain (v2.x+) |
| `musl-tools` | Provides `musl-gcc` for native x86_64 static builds |

**1.** Clone the repository:

```shell
git clone https://github.com/iinsertNameHere/catnap.git
cd catnap
```

**2.** Build the static PCRE libraries (only needed once):

```shell
nim installPcre
nim installPcre2
```

**3.** Build the static binary:

```shell
nim static_release
```

The binary is placed at `bin/catnap`.

**4.** Install the binary and config files:

```shell
nim install_cfg
sudo nim install_bin
```

**5.** Verify:

```shell
catnap
```

> [!NOTE]
> If `musl-gcc` is not on your PATH, set the `MUSLCC` environment variable before building: `MUSLCC=x86_64-linux-musl-gcc nim static_release`

**Updating:** Pull and rebuild:

```shell
git pull
nim static_release
sudo nim install_bin
```

The PCRE libraries only need to be rebuilt if you switch musl toolchains or the pcre version changes.
