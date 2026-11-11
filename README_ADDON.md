# DDEV Add-on: of-sw

## Overview

Internes DDEV-Add-on für Shopware-Projekte. Stellt die Watcher-Ports über den DDEV-Router, PHP- und MySQL-Performance-Einstellungen, Custom Commands und die Adminer-Umgebungsdatei bereit. `shopware-cli` wird nicht mitgeliefert; sie ist in Shopware-DDEV-Projekten bereits enthalten.

**Hinweis:** Der Adminer-Service selbst wird über das separate Add-on `ddev/ddev-adminer` bereitgestellt. Dieses Add-on liefert nur die `.env.adminer`-Konfiguration mit, damit sie nicht manuell angelegt werden muss.

## Installation

Use the `owner/repo` form to install the latest stable GitHub Release:

```bash
ddev add-on get aneufeld23/ddev-of-sw
ddev restart
```

Do **not** pass the repository homepage URL (`https://github.com/aneufeld23/ddev-of-sw`). DDEV treats any `https://` argument as a tarball download; the homepage is HTML, which leads to `gzip: invalid header` when unpacking.

To install a branch instead of a release, use a real archive URL:

```bash
ddev add-on get https://github.com/aneufeld23/ddev-of-sw/archive/refs/heads/main.tar.gz
ddev restart
```

For local development:

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
| `ddev ip` | Image proxy in the web container at `https://<project>.ddev.site:9996` |
| `ddev hip` | Same as `ddev ip`; the proxy stays in the container so the router can own port 9996 |

`config.watch.yaml` publishes the watcher ports through `ddev-router`. The router binds each host port once and selects the project by hostname, so several projects can keep the standard container ports:

| Service | URL |
| ------- | --- |
| Administration watch | `https://<project>.ddev.site:5173` |
| Storefront watch | `https://<project>.ddev.site:9998` |
| Storefront assets | `https://<project>.ddev.site:9999` |
| Image proxy | `https://<project>.ddev.site:9996` |

Remove a project-local `.ddev/docker-compose.watch.yaml` that binds `5173`, `9998`, `9999`, or `9996` on the host. It conflicts with the router.

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
