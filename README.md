# PRV-FWD - Proeve.net Forwarding Service

Ein eleganter URL-Weiterleitungsservice im Stil von proeve.net mit erweiterten Features.

## Features

- ✅ Direkte URL-Weiterleitung
- ✅ Verzeichnis-basierte Weiterleitung
- ✅ Fünf flexible Weiterleitungsmodi
- ✅ **HTML-formatierte Warnhinweise mit Variablen**
- ✅ **Live-Countdown in Warnungstexten**
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

#### 3. Warten erforderlich
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
- `WARNING_TEXT` - Optionaler Warntext (**unterstützt HTML + Variablen!**)
- `WARNING_MODE` - Weiterleitungsmodus:
  - `auto` - Automatische Weiterleitung mit Skip-Button (Standard)
  - `wait` - Warten erforderlich, kein Skip-Button
  - `button` - Button-Klick erforderlich
  - `button-delay` - Button wird nach X Sekunden aktiviert
- `WARNING_DELAY` - Wartezeit in Sekunden (Standard: 5)

## Variablen in Warnhinweisen (NEU! ✨)

Sie können **dynamische Variablen** in Ihren Warnhinweisen verwenden:

### Verfügbare Variablen

| Variable | Beschreibung | Beispiel-Ausgabe |
|----------|--------------|------------------|
| `{countdown}` | **Live-Countdown** (aktualisiert jede Sekunde) | 10, 9, 8, 7... |
| `{url}` | Ziel-URL | https://example.com |
| `{delay}` | Initiale Wartezeit (konstant) | 10 |

### Variable-Styling

- `{countdown}` - Groß, fett, goldene Farbe
- `{url}` - Monospace-Font, goldene Farbe
- `{delay}` - Fett, goldene Farbe

### Beispiele mit Variablen

**Einfaches Countdown-Display:**
```
test1;https://example.com;Noch {countdown} Sekunden...;auto;10
```

**Mit HTML-Formatierung:**
```
test2;https://example.com;<p>Weiterleitung in <strong>{countdown}</strong> Sekunden zu:</p><p>{url}</p>;auto;8
```

**Komplett mit allen Variablen:**
```
test3;https://example.com;<h3>Bitte warten</h3><p>Sie werden in {countdown} von {delay} Sekunden weitergeleitet.</p><p>Ziel: {url}</p>;wait;15
```

**Komplexes Beispiel:**
```
partner;https://partner.com;<h3>🔗 Partner-Link</h3><p>Sie werden in {countdown} Sekunden weitergeleitet zu:</p><p><strong>{url}</strong></p><ul><li>Gesamtwartezeit: {delay} Sekunden</li><li>Externe Partner-Website</li><li>Keine Haftung für externe Inhalte</li></ul>;auto;10
```

**Ohne Countdown (Button-Modus):**
```
external;https://external.com;<h3>⚠️ Externe Website</h3><p>Sie verlassen proeve.net und gehen zu:</p><p>{url}</p><p>Von insgesamt {delay} Sekunden Wartezeit.</p>;button
```

## HTML-Formatierung in Warnhinweisen

Warnhinweise unterstützen vollständige HTML-Formatierung:

### Verfügbare HTML-Tags

| Tag | Beschreibung | Beispiel |
|-----|--------------|----------|
| `<strong>` | Fettdruck (goldene Farbe) | `<strong>Wichtig</strong>` |
| `<em>` | Kursiv | `<em>Hinweis</em>` |
| `<h3>` | Unterüberschrift (goldene Farbe) | `<h3>⚠️ Achtung</h3>` |
| `<p>` | Textabsatz | `<p>Dies ist ein Absatz.</p>` |
| `<ul><li>` | Aufzählung | `<ul><li>Punkt 1</li></ul>` |
| `<ol><li>` | Nummerierte Liste | `<ol><li>Erster</li></ol>` |

### Kombinierte Beispiele

**Mit Emojis und Variablen:**
```
warning1;https://example.com;<h3>⏰ Zeitbasierte Weiterleitung</h3><p>Noch <strong>{countdown}</strong> Sekunden bis zur Weiterleitung.</p>;auto;8
```

**Mit Liste und URL:**
```
info;https://example.com;<h3>📌 Information</h3><p>Ziel: {url}</p><ul><li>Wartezeit: {delay} Sek</li><li>Verbleibend: {countdown} Sek</li></ul>;wait;12
```

**Affiliate-Link mit allen Features:**
```
affiliate;https://shop.com;<h3>🛒 Affiliate-Link</h3><p>Sie werden in {countdown} Sekunden zu unserem Partner weitergeleitet:</p><p><em>{url}</em></p><p>Durch Ihren Kauf unterstützen Sie proeve.net.</p><ul><li>Keine Mehrkosten für Sie</li><li>Provision für proeve.net</li><li>Wartezeit: {delay} Sekunden</li></ul>;auto;10
```

## Use Cases mit Variablen

### 1. Download-Warnung mit Live-Countdown
```
download;https://files.com/file.zip;<h3>⬇️ Download startet</h3><p>Ihr Download beginnt in {countdown} Sekunden.</p><p>Datei: {url}</p><p><strong>Hinweis:</strong> Scannen Sie Downloads vor dem Öffnen!</p>;wait;5
```

### 2. Affiliate Shop mit Transparenz
```
shop;https://partner-shop.com;<h3>🛒 Partner-Shop</h3><p>Weiterleitung in {countdown} Sekunden...</p><p><strong>Transparenz:</strong> Dies ist ein Affiliate-Link. Sie zahlen den gleichen Preis, wir erhalten eine kleine Provision.</p><p>Ziel: {url}</p>;auto;8
```

### 3. Externe Ressource mit Wartezeit
```
external;https://external-site.com;<h3>⚠️ Externe Ressource</h3><p>Sie verlassen proeve.net in {countdown} Sekunden.</p><p>Ziel: {url}</p><p>Bitte beachten Sie: Externe Seiten unterliegen eigenen Datenschutzbestimmungen.</p><ul><li>Verbleibende Zeit: {countdown} Sek</li><li>Gesamtzeit: {delay} Sek</li></ul>;wait;10
```

### 4. Ticket-Verkauf mit Button-Delay
```
tickets;https://tickets.proeve.net;<h3>🎫 Ticket-Shop</h3><p>Sie werden zum Ticketshop weitergeleitet.</p><p>Button wird in {countdown} Sekunden aktiv.</p><p>Ziel: {url}</p>;button-delay;5
```

### 5. Wichtige Meldung ohne Skip
```
important;https://important-site.com;<h3>🚨 Wichtige Information</h3><p><strong>Bitte lesen Sie aufmerksam:</strong></p><ol><li>Dies ist eine wichtige Mitteilung</li><li>Sie müssen {delay} Sekunden warten</li><li>Verbleibend: {countdown} Sekunden</li></ol><p>Ziel: {url}</p>;wait;15
```

## Technische Details

### Variablen-System

- **Live-Updates:** `{countdown}` aktualisiert sich jede Sekunde automatisch
- **Auto-Styling:** Variablen werden automatisch in goldener Farbe dargestellt
- **HTML-sicher:** URLs werden korrekt escaped
- **Performance:** Minimale DOM-Updates für flüssige Countdown-Animationen

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
- Variablen werden sicher in HTML eingebettet
- Fehlerbehandlung mit Fallback zu proeve.net
- Delay-Limit: 0-300 Sekunden

### Kompatibilität

- **Alte Links bleiben funktionsfähig!**
- Standard-Verhalten ohne Parameter: Auto-Redirect nach 2 Sekunden
- Abwärtskompatibel mit bestehenden Links ohne Variablen
- Responsive Design für Desktop und Mobile
- Alle Browser mit ES6-Support

## Design

Die Website verwendet einen eleganten, dunklen Stil mit goldenen Akzenten.

### Farbschema
- Hintergrund: Dunkle Gradienten (#0f0f0f bis #1a1a1a)
- Akzentfarbe: Gold (#d4af37)
- Text: Helles Grau (#e8e8e8)
- Variablen: Goldene Hervorhebung
- Buttons: Gold mit Hover-Effekt

## Deployment

Diese Website läuft auf GitHub Pages.

### Custom Domain Setup

1. CNAME-Datei erstellt mit: `go.proeve.net`
2. DNS CNAME-Record: `go` → `jakobneukirchner.github.io`
3. GitHub Pages aktiviert auf `main` branch

## Changelog

### V2.2.0 (Februar 2026)
- ✨ **NEU:** Variablen-System in Warnhinweisen
  - `{countdown}` - Live-Countdown mit Echtzeit-Updates
  - `{url}` - Dynamische URL-Anzeige
  - `{delay}` - Initiale Wartezeit
- ✨ Auto-Styling für Variablen (goldene Farbe, Formatierung)
- ✨ Live-Update-Mechanismus für Countdown
- 🐛 Bugfix: Interval-Cleanup bei vorzeitiger Weiterleitung

### V2.1.0 (Februar 2026)
- ✨ `wait` Modus - Pflicht-Wartezeit ohne Skip-Button
- ✨ HTML-Formatierung in Warnhinweisen
- ✨ "Zurück zu Proeve.net" Button in allen Ansichten
- 📝 Verbesserte Texte: "Bitte warten Sie X Sekunden"
- 💎 Styling für formatierte Warnhinweise

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
