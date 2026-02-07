# PRV-FWD - Proeve.net Forwarding Service

Ein eleganter URL-Weiterleitungsservice im Stil von proeve.net mit erweiterten Features.

## Features

- ✅ Direkte URL-Weiterleitung
- ✅ Verzeichnis-basierte Weiterleitung
- ✅ Flexible Weiterleitungsmodi
- ✅ Warnhinweise für Verzeichnis-Links
- ✅ URL-Validierung
- ✅ Elegantes, responsives Design
- ✅ Fehlerbehandlung

## Verwendung

### Direkte Weiterleitung

Verwenden Sie den `fwd` Parameter für direkte URL-Weiterleitungen:

```
go.proeve.net?fwd=https://example.com
```

### Weiterleitungsmodi

Kontrollieren Sie das Weiterleitungsverhalten mit dem `mode` Parameter:

#### 1. Automatische Weiterleitung (Standard)
Weiterleitung nach X Sekunden mit Countdown:
```
go.proeve.net?fwd=https://example.com&mode=auto&delay=5
```
- `mode=auto` - Standard (kann weggelassen werden)
- `delay=5` - Wartezeit in Sekunden (Standard: 2)

#### 2. Sofortige Weiterleitung
Direkte Weiterleitung ohne Verzögerung:
```
go.proeve.net?fwd=https://example.com&mode=instant
```

#### 3. Button-Klick erforderlich
Weiterleitung nur nach manuellem Klick:
```
go.proeve.net?fwd=https://example.com&mode=button
```

#### 4. Button nach Verzögerung
Button wird erst nach X Sekunden klickbar:
```
go.proeve.net?fwd=https://example.com&mode=button-delay&delay=10
```

### Verzeichnis-basierte Weiterleitung

Verwenden Sie den `fwd-v` Parameter für Weiterleitungen über das Verzeichnis:

```
go.proeve.net?fwd-v=go1
```

## Verzeichnis konfigurieren

Bearbeiten Sie die `directory.txt` Datei im folgenden Format:

### Basis-Format
```
ID;URL
```
Beispiel:
```
go1;https://google.com
```

### Erweitert mit Warnhinweis
```
ID;URL;WARNING_TEXT;WARNING_MODE;WARNING_DELAY
```

**Parameter:**
- `ID` - Eindeutige Kennung für den Link
- `URL` - Ziel-URL
- `WARNING_TEXT` - Optionaler Warntext (erscheint vor Weiterleitung)
- `WARNING_MODE` - Weiterleitungsmodus für Warnung:
  - `auto` - Automatische Weiterleitung nach X Sekunden (Standard)
  - `button` - Button-Klick erforderlich
  - `button-delay` - Button wird nach X Sekunden aktiviert
- `WARNING_DELAY` - Wartezeit in Sekunden (Standard: 5)

**Beispiele:**

```
# Einfache Weiterleitung ohne Warnung
shop;https://proeve.net/shop

# Mit Warnung und auto redirect nach 5 Sekunden
external;https://example.com;Sie verlassen proeve.net;auto;5

# Mit Warnung, Button-Klick erforderlich
partner;https://partner-site.com;Dies ist eine Partner-Website;button

# Mit Warnung, Button nach 10 Sekunden
warning;https://external.com;Bitte lesen Sie diesen Hinweis;button-delay;10
```

## Parameter-Kombinationen

### Direkte Links

| URL | Verhalten |
|-----|----------|
| `?fwd=URL` | Auto-Redirect nach 2 Sek |
| `?fwd=URL&mode=instant` | Sofort |
| `?fwd=URL&mode=auto&delay=10` | Auto nach 10 Sek |
| `?fwd=URL&mode=button` | Button-Klick |
| `?fwd=URL&mode=button-delay&delay=5` | Button nach 5 Sek |

### Verzeichnis-Links

| URL | Verhalten |
|-----|----------|
| `?fwd-v=ID` | Gemäß Verzeichnis-Einstellung |
| `?fwd-v=ID&mode=button` | Überschreibt Verzeichnis-Modus |
| `?fwd-v=ID&delay=15` | Überschreibt Verzeichnis-Delay |

**Hinweis:** URL-Parameter (`mode`, `delay`) überschreiben die Einstellungen aus `directory.txt`.

## Design

Die Website verwendet einen eleganten, dunklen Stil mit goldenen Akzenten, inspiriert vom klassisch-modernen Design von proeve.net.

### Farbschema
- Hintergrund: Dunkle Gradienten (#0f0f0f bis #1a1a1a)
- Akzentfarbe: Gold (#d4af37)
- Text: Helles Grau (#e8e8e8)

## Technische Details

### Weiterleitungsmodi

1. **instant** - Sofortige Weiterleitung ohne UI
2. **auto** - Countdown mit automatischer Weiterleitung
3. **button** - Manuelle Bestätigung erforderlich
4. **button-delay** - Button wird nach Countdown aktiviert

### Sicherheit

- URL-Validierung (nur HTTP/HTTPS)
- XSS-Schutz durch HTML-Escaping
- Fehlerbehandlung mit Fallback zu proeve.net
- Delay-Limit: 0-300 Sekunden

### Kompatibilität

- **Alte Links bleiben funktionsfähig!**
- Standard-Verhalten ohne Parameter: Auto-Redirect nach 2 Sekunden
- Abwärtskompatibel mit bestehenden Links

## Deployment

Diese Website läuft auf GitHub Pages.

### Custom Domain Setup

1. CNAME-Datei erstellt mit: `go.proeve.net`
2. DNS CNAME-Record: `go` → `jakobneukirchner.github.io`
3. GitHub Pages aktiviert auf `main` branch

## Changelog

### V2.0.0 (Februar 2026)
- ✨ Neue Weiterleitungsmodi (instant, auto, button, button-delay)
- ✨ Verzeichnis-Warnhinweise
- ✨ Flexible Delay-Einstellungen
- ✨ Countdown-Timer
- ✨ Verbesserte UI mit Buttons
- ✨ Abbrechen-Option
- ✅ Abwärtskompatibilität gewährleistet

### V1.1.1 (Januar 2026)
- Initial release mit Basis-Funktionalität

## Lizenz

Dieses Projekt wurde für proeve.net erstellt.
