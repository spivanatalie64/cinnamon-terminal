# Cinnamon Terminal

> **A terminal for people who actually use terminals.**
> Forked from [GNOME Terminal](https://gitlab.gnome.org/GNOME/gnome-terminal), optimized for the [Cinnamon Desktop](https://github.com/linuxmint/cinnamon).

## Why Cinnamon Terminal?

GNOME Terminal was the gold standard for Linux terminals for over two decades. But the GNOME project has been on a trajectory that leaves a lot of users behind:

### The problem with modern GNOME Terminal

The GNOME project has been systematically removing X11 support from their applications. They're going **Wayland-only**, which is fine for some, but X11 isn't dead — and Cinnamon Desktop primarily runs on X11. Rather than maintaining coexistence, GNOME is stripping out features and breaking workflows.

### GNOME Console (kgx) is not the answer

GNOME decided that GNOME Terminal was too complex, so they created **GNOME Console** (kgx) as a replacement. And honestly, it sucks:

- ❌ **No tabs** — a modern terminal without tabs in 2026
- ❌ **No profiles** — can't save configurations for different workflows
- ❌ **No transparency** — can't customize your terminal appearance
- ❌ **Minimal to a fault** — they removed everything that made terminals useful
- ❌ **No dropdown mode** — can't quick-launch from a keyboard shortcut
- ❌ **No custom shortcuts** — you get what you get

Console is a terminal for people who don't actually use terminals. It looks pretty in screenshots but is painful to work in daily.

### What Cinnamon Terminal does about it

Cinnamon Terminal is our answer. We're forking GNOME Terminal and we're:

- ✅ **Keeping the features** — tabs, profiles, transparency, the whole toolkit
- ✅ **Keeping X11 support** — for people who actually use their desktops
- ✅ **Optimizing for Cinnamon** — deep integration with the Cinnamon Desktop ecosystem
- ✅ **Adding Wayland when ready** — not breaking X11 to do it
- ✅ **Tracking upstream security fixes** — we maintain, not abandon
- ✅ **Making our own releases** — AcreetionOS releases with our patches

**Cinnamon Terminal is the terminal that GNOME abandoned. We're adopting it.**

> X11 forever, Wayland when ready, features always.

## Repository Structure

This is the primary source repository for Cinnamon Terminal. All development happens here, on `gitlab.acreetionos.org`.

```
Cinnamon Terminal
├── src/          # Terminal application source code
├── data/         # Desktop files, icons, schemas
├── help/         # Documentation
├── po/           # Translations
├── subprojects/  # Vendored dependencies
├── meson.build   # Build system
└── README.md     # This file
```

## Mirrors

Cinnamon Terminal is mirrored to the following locations for convenience. These are **read-only mirrors** — all development and issue tracking happens on the primary repo.

| Platform | URL | Status |
|----------|-----|--------|
| **🌐 Primary (AcreetionOS GitLab)** | [gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal](https://gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal) | **Source of Truth** |
| **🪐 GitHub (AcreetionOS-Code org)** | [github.com/AcreetionOS-Code/cinnamon-terminal](https://github.com/AcreetionOS-Code/cinnamon-terminal) | Read-only mirror |
| **⭐ GitHub (spivanatalie64)** | [github.com/spivanatalie64/cinnamon-terminal](https://github.com/spivanatalie64/cinnamon-terminal) | Read-only mirror |
| **🔷 Codeberg** | [codeberg.org/sprunglesontheberg/cinnamon-terminal](https://codeberg.org/sprunglesontheberg/cinnamon-terminal) | Read-only mirror |
| **⬆️ Upstream (GNOME)** | [gitlab.gnome.org/GNOME/gnome-terminal](https://gitlab.gnome.org/GNOME/gnome-terminal) | Upstream source |

All mirrors are updated automatically from the primary repository.

## Branches

| Branch | Description |
|--------|-------------|
| `master` | Active development, tracking upstream with cinnamon patches |
| `cinnamon-*` | Cinnamon-specific feature branches |
| `gnome-*` | Upstream GNOME release branches (tracked for cherry-picks) |
| `acreetionos/*` | AcreetionOS-specific release branches |

## Building from Source

### Dependencies

You'll need the following build dependencies:

```bash
# On Arch Linux / AcreetionOS
sudo pacman -S base-devel meson ninja git \
    glib2 gtk3 gtk4 libadwaita vte3 dconf \
    pcre2 systemd-libs libxml2 itstool appstream-glib

# On Debian/Ubuntu
sudo apt-get build-dep gnome-terminal
sudo apt-get install meson ninja-build git g++ \
    libglib2.0-dev libgtk-3-dev libgtk-4-dev \
    libadwaita-1-dev libvte-2.91-dev libdconf-dev \
    libpcre2-dev libsystemd-dev libxml2-utils xsltproc itstool
```

### Build

```bash
git clone https://gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal.git
cd cinnamon-terminal
meson setup build --prefix=/usr
meson compile -C build
```

### Install

```bash
sudo meson install -C build
```

## Upstream Tracking

This fork tracks upstream [GNOME Terminal](https://gitlab.gnome.org/GNOME/gnome-terminal). We regularly rebase on upstream updates to pull in security fixes and improvements. Changes pushed upstream are never pushed back — this is a one-way fork with our own release cadence.

To see what's changed from upstream:

```bash
git log upstream/master..master
```

## Releases

Cinnamon Terminal follows a [CalVer](https://calver.org/) release scheme aligned with AcreetionOS releases. Tags are signed and releases are published on the [GitLab releases page](https://gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal/-/releases).

## Contributing

Issues and merge requests should be filed on the **[primary repository](https://gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal)**. Mirrors do not accept contributions directly.

We welcome:
- Bug reports and feature requests
- Merge requests with improvements
- Translations
- Packaging contributions

## License

Cinnamon Terminal is free software: you can redistribute it and/or modify it under the terms of the [GNU General Public License](COPYING) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

The documentation is licensed under:
- [GNU General Public License](COPYING), version 3.0 or later (the programme)
- [Creative Commons Attribution-ShareAlike 3.0](COPYING.GFDL) (the documentation)
- [GNU Free Documentation License](COPYING.GFDL) 1.3 only (the appstream data)

---

*Cinnamon Terminal — keeping terminals useful on Cinnamon Desktop.*
*Built with ❤️ by the AcreetionOS project.*
