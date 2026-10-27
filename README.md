![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/gaofengnan/forgejo-runner-debian/total)
![GitHub Downloads (all assets, latest release)](https://img.shields.io/github/downloads/gaofengnan/forgejo-runner-debian/latest/total)
![GitHub Release](https://img.shields.io/github/v/release/gaofengnan/forgejo-runner-debian)
![GitHub Release Date](https://img.shields.io/github/release-date/gaofengnan/forgejo-runner-debian?display_date=published_at)

# forgejo-runner for Debian

> Fork of [dariogriffo/forgejo-runner-debian](https://github.com/dariogriffo/forgejo-runner-debian) (MIT); the original packaging is by Dario Griffo. Served at [deb.gaofn.xyz](https://deb.gaofn.xyz) for Debian 12 (bookworm) and 13 (trixie).

This repository contains build scripts to produce the _unofficial_ Debian packages
(.deb) for [forgejo-runner](https://code.forgejo.org/forgejo/runner) hosted at [deb.gaofn.xyz](https://deb.gaofn.xyz)

Currently supported Debian distros are:
- Bookworm (v12)
- Trixie (v13)
- Forky (v14)
- Sid (testing)

**Upstream architectures:** amd64 and arm64 only.

This is an unofficial community project to provide a package that's easy to
install on Debian. If you're looking for the forgejo-runner source code, see
[forgejo-runner](https://code.forgejo.org/forgejo/runner).

## Install/Update

### The Debian way

```sh
sudo install -d -m 0755 /etc/apt/keyrings
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.gpg -o /etc/apt/keyrings/deb.gaofn.xyz.gpg
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.sources -o /etc/apt/sources.list.d/deb.gaofn.xyz.sources
# Debian 12 (bookworm): fetch deb.gaofn.xyz-bookworm.sources instead
sudo apt update
sudo apt install -y forgejo-runner
```

### Manual Installation

1. Download the .deb package for your Debian version available on
   the [Releases](https://github.com/gaofengnan/forgejo-runner-debian/releases) page.
2. Install the downloaded .deb package.

```sh
sudo dpkg -i <filename>.deb
```
## Updating

To update to a new version, just follow any of the installation methods above. There's no need to uninstall the old version; it will be updated correctly.

## Post-installation

After installing the package, register the runner against your Forgejo instance:

```sh
sudo -u forgejo-runner forgejo-runner register --config /etc/forgejo-runner/config.yml \
  --no-interactive --instance <https://your-forgejo-instance> --token <registration-token>
sudo systemctl start forgejo-runner
sudo systemctl enable forgejo-runner
```

The package automatically:
- Creates the `forgejo-runner` system user and group
- Creates `/var/lib/forgejo-runner` (work directory, owned by `forgejo-runner:forgejo-runner`, mode `750`)
- Creates `/etc/forgejo-runner` (config directory, owned by `root:forgejo-runner`, mode `770`)
- Installs the systemd service file

## Building

### Build for single architecture
```sh
./build.sh <forgejo_runner_version> <build_version> <architecture>
# Example: ./build.sh 12.13.0 1 arm64
```

### Build for all architectures
```sh
./build.sh <forgejo_runner_version> <build_version> all
# Example: ./build.sh 12.13.0 1 all
```

## Roadmap

- [x] Produce a .deb package on GitHub Releases
- [x] Multi-architecture support (amd64, arm64)
- [ ] Set up a debian mirror for easier updates

## Disclaimer

- This repo is not open for issues related to forgejo-runner. This repo is only for _unofficial_ Debian packaging.
