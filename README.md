# ddev-of-sw

Internes DDEV-Add-on für Shopware-Projekte. Stellt gemeinsame DDEV-Konfigurationen und Custom Commands bereit, damit interne Projekte per `ddev add-on get` aktuell gehalten werden können.

## Installation

Das Add-on ist intern und nicht in der öffentlichen DDEV-Add-on-Registry gelistet. Installiere es direkt aus dem internen Repository oder lokal:

```bash
# Internes Git-Repository
ddev add-on get aneufeld23/ddev-of-sw
ddev restart

# Lokaler Pfad (Entwicklung)
ddev add-on get /Users/andreasneufeld/Projekte/ddev-addon
ddev restart
```

Nach der Installation `.ddev/` ins Versionskontrollsystem committen.

## Update

Um die Add-on-Dateien auf den neuesten Stand zu bringen:

```bash
ddev add-on get aneufeld23/ddev-of-sw
ddev restart
```

Dateien mit `#ddev-generated` werden dabei ersetzt, solange sie nicht manuell geändert wurden.

## Voraussetzungen

- DDEV >= v1.24.10
- Shopware-DDEV-Projekt (`shopware-cli` ist dort bereits enthalten)
- Für Adminer: separates `ddev/ddev-adminer` Add-on (dieses Add-on liefert nur `.env.adminer` mit)

## Enthaltene Dateien

| Datei | Zweck |
| ----- | ----- |
| `.env.adminer` | Adminer-Plugin-Konfiguration (Service kommt aus `ddev-adminer`) |
| `config.watcher.yaml` | Watcher-Ports und Web-Environment |
| `mysql/my.cnf` | MySQL-`sql_mode` und `group_concat_max_len` |
| `php/shopware.ini` | Shopware-PHP-Performance-Einstellungen (ohne `opcache.validate_timestamps = 0`) |
| `commands/web/*` | Shopware- und Console-Shortcuts |
| `commands/host/hip` | Image-Proxy vom Host |

## Commands

| Command | Beschreibung |
| ------- | ------------ |
| `ddev sw` | Storefront-Watch |
| `ddev sb` | Storefront-Build |
| `ddev sbf` | Storefront-Build mit `--force-install-dependencies` |
| `ddev ab` | Admin-Build |
| `ddev abf` | Admin-Build mit `--force-install-dependencies` |
| `ddev aw` | Admin-Watch |
| `ddev cli` | `shopware-cli` Wrapper |
| `ddev bc` | `php bin/console` Wrapper |
| `ddev cc` | Cache leeren |
| `ddev cca` | Alle Caches leeren |
| `ddev ip` | Image-Proxy (Web, Port 9997) |
| `ddev hip` | Image-Proxy (Host, Port 9997) |

## Entwicklung

```bash
# Tests lokal ausführen (bats-core erforderlich)
bats ./tests/test.bats --filter-tags '!release'

# Add-on-Update-Checker
curl -fsSL https://ddev.com/s/addon-update-checker.sh | bash
```

## Lizenz

Internes Projekt – nur für den internen Gebrauch.
