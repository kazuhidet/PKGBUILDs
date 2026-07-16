# PKGBUILDs

# Arch Linux ARM Package Build Resources

This repository contains `PKGBUILD` files and related resources for building packages that are missing or not readily available for Arch Linux ARM.

The main purpose of this repository is to make it easier to build Pacman packages for `aarch64` environments, especially when the original packaging method depends on prebuilt packages for another distribution or architecture.

## Overview

Arch Linux ARM does not always provide the same package availability as Arch Linux on `x86_64`.

This repository collects packaging files, build scripts, patches, and other resources needed to build such packages locally for Arch Linux ARM.

## Packages

### rencal

This directory contains a `PKGBUILD` for building a Pacman package of [renCal](https://github.com/t4t5/rencal), created by Tristan.

renCal is a modern, open-source calendar application built for Omarchy.

The original packaging approach provided by Tristan's PKGBUILD extracts the Debian GNU/Linux `.deb` package and generates a Pacman package from it.

However, because a suitable `aarch64` package was not available for my Arch Linux ARM environment, this repository uses a different approach:

* Fetch the source code directly from the upstream GitHub repository
* Build the application from source
* Generate a Pacman package for Arch Linux ARM

This makes it possible to build renCal locally on `aarch64` without relying on a Debian package built for another architecture.

## Repository Structure

```text
.
├── rencal/
│   ├── PKGBUILD
│   └── related resources
└── README.md
```

## Requirements

To build packages from this repository, you need an Arch Linux ARM environment with the standard package build tools installed.

```bash
sudo pacman -S --needed base-devel git
```

Additional dependencies may be required depending on the package being built.

## Building a Package

Clone this repository:

```bash
git clone https://github.com/kazuhidet/PKGBUILDs
cd PKGBUILDs
```

Move into the package directory:

```bash
cd rencal
```

Build and install the package:

```bash
makepkg -si
```

### mozc

This directory contains packaging resources for building [Mozc](https://github.com/google/mozc) on Arch Linux ARM.

Mozc is an open-source Japanese input method developed by Google.

The existing AUR `PKGBUILD` for Mozc did not include `aarch64` as a supported build target. In addition, the original build process used a Bazel binary intended for the `x86_64` architecture when building the source code.

This version modifies the packaging process so that Mozc can be built properly on Arch Linux ARM / `aarch64` systems.

The main changes are:

* Add `aarch64` as a supported architecture
* Avoid relying on an `x86_64` Bazel binary during the build
* Adjust the build process for Arch Linux ARM environments

### fcitx5-mozc-ut

This directory contains packaging resources for building [fcitx5-mozc-ut](https://github.com/fcitx/mozc) on Arch Linux ARM.

Like Mozc, the existing AUR `PKGBUILD` for fcitx5-mozc-ut did not include `aarch64` as a supported build target. It also used a Bazel binary for the `x86_64` architecture when building the source code.

This version modifies the packaging process so that fcitx5-mozc-ut can be built properly on Arch Linux ARM / `aarch64` systems.

The main changes are:

* Add `aarch64` as a supported architecture
* Avoid relying on an `x86_64` Bazel binary during the build
* Adjust the build process for Arch Linux ARM environments

### rustdesk-bin

This directory contains a `PKGBUILD` for creating a Pacman package of [RustDesk](https://github.com/rustdesk/rustdesk).

RustDesk is an open-source remote desktop application written in Rust. It is commonly used as an alternative to remote desktop tools such as TeamViewer and AnyDesk.

Please note that this package does not build RustDesk from source. Instead, it repackages the official upstream `.deb` binary release into a Pacman package format for Arch Linux / Arch Linux ARM.

The `PKGBUILD` supports both `x86_64` and `aarch64` architectures:

* `x86_64` uses the official RustDesk `x86_64` Debian package
* `aarch64` uses the official RustDesk `aarch64` Debian package

The generated Pacman package is named `rustdesk-bin`, but it provides the `rustdesk` package name. It also conflicts with and replaces an existing `rustdesk` package, so it can be used as a drop-in replacement.

The package installs the RustDesk application files under `/usr/share/rustdesk` and provides the `rustdesk` command for launching the application.

This packaging method is useful for Arch Linux ARM environments because it allows RustDesk to be installed on `aarch64` systems using the official upstream binary release.

## Notes

These packaging files are intended primarily for Arch Linux ARM and `aarch64` systems.

They may also be useful as references for other Arch-based environments, but they are not guaranteed to work unchanged on every system.

## Disclaimer

This repository is not an official Arch Linux ARM package repository.

The included `PKGBUILD` files are provided for personal use and experimentation. Please review each file before building or installing any package.

renCal is developed by its original author. This repository only provides packaging resources for building it on Arch Linux ARM.

## License

Packaging files in this repository are provided under the license specified in this repository.

Upstream projects retain their own licenses.

