# PRV-FWD - Proeve.net Forwarding Service

Ein eleganter URL-Weiterleitungsservice im Stil von proeve.net mit erweiterten Features.

## Features

- ✅ Direkte URL-Weiterleitung
- ✅ Verzeichnis-basierte Weiterleitung
- ✅ Fünf flexible Weiterleitungsmodi
- ✅ HTML-formatierte Warnhinweise
- ✅ URL-Validierung
- ✅ Elegantes, responsives Design
- ✅ "Zurück zu Proeve.net" Button
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
Weiterleitung nach X Sekunden mit Countdown und Skip-Button:
```
go.proeve.net?fwd=https://example.com&mode=auto&delay=5
```
- `mode=auto` - Standard (kann weggelassen werden)
- `delay=5` - Wartezeit in Sekunden (Standard: 2)
- **Button:** "Jetzt weiterleiten" + "Zurück zu Proeve.net"

#### 2. Sofortige Weiterleitung
Direkte Weiterleitung ohne Verzögerung:
```
go.proeve.net?fwd=https://example.com&mode=instant
```

#### 3. Warten erforderlich (NEU)
Nutzer muss X Sekunden warten, kein Skip-Button:
```
go.proeve.net?fwd=https://example.com&mode=wait&delay=10
```
- **Text:** "Bitte warten Sie X Sekunden..."
- **Kein Skip-Button**, nur "Zurück zu Proeve.net"
- Ideal für wichtige Hinweise, die gelesen werden müssen

#### 4. Button-Klick erforderlich
Weiterleitung nur nach manuellem Klick:
```
go.proeve.net?fwd=https://example.com&mode=button
```
- **Keine automatische Weiterleitung**
- **Button:** "Weiter zur Zielseite" + "Zurück zu Proeve.net"

#### 5. Button nach Verzögerung
Button wird erst nach X Sekunden klickbar:
```
go.proeve.net?fwd=https://example.com&mode=button-delay&delay=10
```
- **Text:** "Bitte warten Sie X Sekunden..."
- **Button disabled** während Countdown
- Nach Ablauf: "Weiter zur Zielseite" + "Zurück zu Proeve.net"

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
- `WARNING_TEXT` - Optionaler Warntext (**unterstützt HTML-Formatierung!**)
- `WARNING_MODE` - Weiterleitungsmodus für Warnung:
  - `auto` - Automatische Weiterleitung mit Skip-Button (Standard)
  - `wait` - Warten erforderlich, kein Skip-Button
  - `button` - Button-Klick erforderlich
  - `button-delay` - Button wird nach X Sekunden aktiviert
- `WARNING_DELAY` - Wartezeit in Sekunden (Standard: 5)

### HTML-Formatierung in Warnhinweisen

Warnhinweise unterstützen HTML-Formatierung für bessere Lesbarkeit:

**Verfügbare HTML-Tags:**
- `<strong>Text</strong>` - Fettdruck (goldene Farbe)
- `<em>Text</em>` - Kursiv
- `<h3>Überschrift</h3>` - Unterüberschrift (goldene Farbe)
- `<p>Absatz</p>` - Textabsatz
- `<ul><li>Punkt</li></ul>` - Aufzählung
- `<ol><li>Punkt</li></ol>` - Nummerierte Liste

**Beispiele:**

```
# Einfache Weiterleitung ohne Warnung
shop;https://proeve.net/shop

# Mit einfachem Text-Warnung
external1;https://example.com;Sie verlassen proeve.net;auto;5

# Mit HTML-formatierter Warnung
external2;https://example.com;<h3>⚠️ Externe Website</h3><p>Sie verlassen <strong>proeve.net</strong>.</p><p><em>Hinweis:</em> Keine Verantwortung für externe Inhalte.</p>;auto;8

# Mit Liste und Button-Klick
partner;https://partner.com;<h3>Partner-Website</h3><p>Folgende Punkte beachten:</p><ul><li>Datenschutz gilt dort</li><li>Separate AGB</li></ul>;button

# Mit Warnung, Warten erforderlich (kein Skip)
warning;https://external.com;<p><strong>Wichtig:</strong> Bitte lesen Sie diesen Hinweis aufmerksam.</p><p>Sie müssen 10 Sekunden warten, bevor Sie fortfahren können.</p>;wait;10

# Mit Warnung, Button nach Verzögerung
delayed;https://site.com;<p>Ihre Anfrage wird verarbeitet...</p>;button-delay;5
```

## Parameter-Kombinationen

### Direkte Links

| URL | Verhalten |
|-----|----------|
| `?fwd=URL` | Auto-Redirect nach 2 Sek + Skip-Button |
| `?fwd=URL&mode=instant` | Sofort |
| `?fwd=URL&mode=auto&delay=10` | Auto nach 10 Sek + Skip-Button |
| `?fwd=URL&mode=wait&delay=8` | Warten 8 Sek (kein Skip) |
| `?fwd=URL&mode=button` | Button-Klick |
| `?fwd=URL&mode=button-delay&delay=5` | Button nach 5 Sek |

### Verzeichnis-Links

| URL | Verhalten |
|-----|----------|
| `?fwd-v=ID` | Gemäß Verzeichnis-Einstellung |
| `?fwd-v=ID&mode=button` | Überschreibt Verzeichnis-Modus |
| `?fwd-v=ID&delay=15` | Überschreibt Verzeichnis-Delay |

**Hinweis:** URL-Parameter (`mode`, `delay`) überschreiben die Einstellungen aus `directory.txt`.

## UI-Elemente

### Buttons

Alle Ansichten haben jetzt konsistent die Buttons:

1. **Haupt-Button** (gold):
   - "Jetzt weiterleiten" (bei `auto` während Countdown)
   - "Weiter zur Zielseite" (bei `button` oder nach `button-delay`)
   - Disabled bei `button-delay` während Countdown

2. **Zurück-Button** (transparent mit goldenem Rand):
   - "Zurück zu Proeve.net"
   - Immer verfügbar (außer bei `instant`)

### Texte

- **Countdown:** "Weiterleitung in X Sekunden..." (bei `auto` mit Skip-Button)
- **Warten:** "Bitte warten Sie X Sekunden..." (bei `wait` ohne Skip-Button oder `button-delay`)
- **Nach Countdown:** "Sie können jetzt fortfahren" (bei `button-delay`)

## Design

Die Website verwendet einen eleganten, dunklen Stil mit goldenen Akzenten, inspiriert vom klassisch-modernen Design von proeve.net.

### Farbschema
- Hintergrund: Dunkle Gradienten (#0f0f0f bis #1a1a1a)
- Akzentfarbe: Gold (#d4af37)
- Text: Helles Grau (#e8e8e8)
- Buttons: Gold mit Hover-Effekt

### Warnbox-Formatierung

- **Hintergrund:** Halbtransparentes Gold
- **Rahmen:** 2px goldene Umrandung
- **Überschriften:** Goldene Farbe
- **Listen:** Eingerückt mit Aufzählungszeichen
- **Strong-Tags:** Goldene Hervorhebung

## Technische Details

### Weiterleitungsmodi

1. **instant** - Sofortige Weiterleitung ohne UI
2. **auto** - Countdown mit automatischer Weiterleitung + Skip-Button
3. **wait** - Countdown mit Pflicht-Wartezeit (kein Skip-Button)
4. **button** - Manuelle Bestätigung erforderlich
5. **button-delay** - Button wird nach Countdown aktiviert

### Sicherheit

- URL-Validierung (nur HTTP/HTTPS)
- HTML-Escaping für URLs in JavaScript
- XSS-Schutz durch kontrollierte HTML-Ausgabe
- Fehlerbehandlung mit Fallback zu proeve.net
- Delay-Limit: 0-300 Sekunden

### Kompatibilität

- **Alte Links bleiben funktionsfähig!**
- Standard-Verhalten ohne Parameter: Auto-Redirect nach 2 Sekunden
- Abwärtskompatibel mit bestehenden Links
- Responsive Design für Desktop und Mobile

## Use Cases

### 1. Affiliate-Links mit Warnung
```
affiliate;https://partner-shop.com;<h3>Partner-Link</h3><p>Dies ist ein <strong>Affiliate-Link</strong>.</p><p>Durch Ihren Kauf unterstützen Sie proeve.net.</p>;auto;5
```

### 2. Externe Downloads mit Pflicht-Wartezeit
```
download;https://external-host.com/file.zip;<p><strong>Sicherheitshinweis:</strong></p><p>Sie laden eine Datei von einem externen Server.</p><ul><li>Scannen Sie Dateien vor dem Öffnen</li><li>Proeve.net übernimmt keine Haftung</li></ul>;wait;10
```

### 3. Ticket-Shop mit sofortiger Weiterleitung
```
tickets;https://tickets.proeve.net
# Kein Warnhinweis, direkte Weiterleitung nach 2 Sekunden
```

### 4. Wichtige Hinweise mit Button nach Verzögerung
```
important;https://important-site.com;<h3>⚠️ Wichtige Information</h3><p>Bitte lesen Sie folgende Hinweise:</p><ol><li>Punkt 1</li><li>Punkt 2</li><li>Punkt 3</li></ol><p>Der Button wird in 15 Sekunden freigeschaltet.</p>;button-delay;15
```

## Deployment

Diese Website läuft auf GitHub Pages.

### Custom Domain Setup

1. CNAME-Datei erstellt mit: `go.proeve.net`
2. DNS CNAME-Record: `go` → `jakobneukirchner.github.io`
3. GitHub Pages aktiviert auf `main` branch

## Changelog

### V2.1.0 (Februar 2026)
- ✨ **NEU:** `wait` Modus - Pflicht-Wartezeit ohne Skip-Button
- ✨ **NEU:** HTML-Formatierung in Warnhinweisen
- ✨ **NEU:** "Zurück zu Proeve.net" Button in allen Ansichten
- 📝 Verbesserte Texte: "Bitte warten Sie X Sekunden" statt "Button verfügbar in"
- 💎 Styling für formatierte Warnhinweise (Listen, Überschriften, etc.)
- 🐛 Bugfix: Konsistente Button-Anzeige

### V2.0.0 (Februar 2026)
- ✨ Neue Weiterleitungsmodi (instant, auto, button, button-delay)
- ✨ Verzeichnis-Warnhinweise
- ✨ Flexible Delay-Einstellungen
- ✨ Countdown-Timer
- ✨ Verbesserte UI mit Buttons
- ✅ Abwärtskompatibilität gewährleistet

### V1.1.1 (Januar 2026)
- Initial release mit Basis-Funktionalität

## Lizenz

Dieses Projekt wurde für proeve.net erstellt.
