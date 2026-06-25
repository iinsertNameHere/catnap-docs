# Catnap

Catnap is a fast fetch tool built around a config language, not a config file. Your distro art, color themes, and stats are all defined in plain `.cat` files you own and version alongside your dotfiles. It typically runs in under 10ms.

![Catnap running in a terminal](catnap.png)

---

> [!WARNING]
> **Upgrading from v1.x?** Catnap 2.0 replaced the TOML config system entirely. The old `config.toml` and `distros.toml` files are **not compatible** with v2. After upgrading, run `nim install` (or manually copy the new `.cat` files) to get a fresh default config. The new format is simpler and more expressive. See [Config Language](Language.md).

---

## Where to start

- **New install** - [Installation](Install.md)
- **Just installed, want a working config fast** - [Quick Start](QuickStart.md)
- **Learning the config format** - [Config Language](Language.md)
- **All CLI flags** - [Usage](Usage.md)
