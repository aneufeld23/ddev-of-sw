# DDEV Add-on: of-sw

## Overview

Internes DDEV-Add-on für Shopware-Projekte. Stellt Watcher-Konfiguration, PHP- und MySQL-Performance-Einstellungen, Custom Commands und die Adminer-Umgebungsdatei bereit. `shopware-cli` wird nicht mitgeliefert; sie ist in Shopware-DDEV-Projekten bereits enthalten.

**Hinweis:** Der Adminer-Service selbst wird über das separate Add-on `ddev/ddev-adminer` bereitgestellt. Dieses Add-on liefert nur die `.env.adminer`-Konfiguration mit, damit sie nicht manuell angelegt werden muss.

## Installation

```bash
ddev add-on get aneufeld23/ddev-of-sw
ddev restart
```

Für lokale Entwicklung:

```bash
ddev add-on get /pfad/zu/ddev-of-sw
ddev restart
```

After installation, make sure to commit the `.ddev` directory to version control.

## Usage

| Command | Description |
| ------- | ----------- |
| `ddev sw` | Storefront watch |
| `ddev sb` | Storefront build |
| `ddev sbf` | Storefront build with forced dependency install |
| `ddev ab` | Admin build |
| `ddev abf` | Admin build with forced dependency install |
| `ddev aw` | Admin watch |
| `ddev cli` | `shopware-cli` wrapper |
| `ddev bc` | `php bin/console` wrapper |
| `ddev cc` | Clear cache |
| `ddev cca` | Clear all caches |
| `ddev ip` | Image proxy (web, port 9997) |
| `ddev hip` | Image proxy (host, port 9997) |

## Update

`ddev add-on get aneufeld23/ddev-of-sw` installs the latest stable GitHub Release.

```bash
ddev add-on get aneufeld23/ddev-of-sw
ddev add-on get aneufeld23/ddev-of-sw --version v1.2.3
ddev restart
```

Files marked with `#ddev-generated` are replaced on re-install unless manually modified.

## Credits

**Internes Add-on für Shopware-Projekte**
