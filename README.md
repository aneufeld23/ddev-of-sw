# ddev-of-sw

Internes DDEV-Add-on für Shopware-Projekte. Stellt gemeinsame DDEV-Konfigurationen und Custom Commands bereit, damit interne Projekte per `ddev add-on get` aktuell gehalten werden können.

## Installation

Das Add-on ist intern und nicht in der öffentlichen DDEV-Add-on-Registry gelistet. Installiere es direkt aus dem internen Repository oder lokal:

```bash
# Normale Installation (neuestes stabiles GitHub-Release)
ddev add-on get aneufeld23/ddev-of-sw
ddev restart
```

**Nicht** die Repository-Startseite als URL verwenden. `ddev add-on get` behandelt jede `https://`-Adresse als Tarball-Archiv. `https://github.com/aneufeld23/ddev-of-sw` ist die HTML-Seite — DDEV speichert sie als `.tar.gz` und bricht beim Entpacken mit `gzip: invalid header` ab.

Wenn du kein Release, sondern einen Branch installieren willst, eine echte Archiv-URL nutzen:

```bash
ddev add-on get https://github.com/aneufeld23/ddev-of-sw/archive/refs/heads/main.tar.gz
ddev restart
```

Nach der Installation `.ddev/` ins Versionskontrollsystem committen.

## Update

`ddev add-on get aneufeld23/ddev-of-sw` installiert das neueste stabile GitHub-Release, nicht den letzten Commit auf `main`.

```bash
ddev add-on get aneufeld23/ddev-of-sw
ddev restart
```

Bestimmte Version:

```bash
ddev add-on get aneufeld23/ddev-of-sw --version v1.2.3
ddev restart
```

Dateien mit `#ddev-generated` werden dabei ersetzt, solange sie nicht manuell geändert wurden.

## Versionierung

Versionen sind GitHub-Releases mit SemVer und `v`-Präfix, zum Beispiel `v1.2.3`. Ohne so ein Release kann DDEV `aneufeld23/ddev-of-sw` nicht auflösen.

Release erzeugen: Tag auf dem gewünschten Commit setzen und pushen. Die Action `.github/workflows/release.yml` legt das GitHub-Release an.

```bash
git tag v1.0.0
git push origin v1.0.0
```

Tags mit Suffix wie `v1.1.0-rc.1` werden als Pre-Release markiert. `ddev add-on get` ohne `--version` ignoriert sie. Installation dann mit `--version v1.1.0-rc.1`.

Release-Tarballs nutzen `git archive`. In [`.gitattributes`](.gitattributes) darf `export-ignore` für `.gitattributes` nur die Datei im Repository-Root treffen (`/.gitattributes`), sonst fehlen Einträge aus `install.yaml` wie `commands/.gitattributes` im Archiv.

## Voraussetzungen

- DDEV >= v1.24.10
- Shopware-DDEV-Projekt (`shopware-cli` ist dort bereits enthalten)
- Für Adminer: separates `ddev/ddev-adminer` Add-on (dieses Add-on liefert nur `.env.adminer` mit)

## Enthaltene Dateien

| Datei | Zweck |
| ----- | ----- |
| `.env.adminer` | Adminer-Plugin-Konfiguration (Service kommt aus `ddev-adminer`) |
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
