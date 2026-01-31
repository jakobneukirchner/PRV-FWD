# PRV-FWD - Proeve.net Forwarding Service

Ein eleganter URL-Weiterleitungsservice im Stil von proeve.net.

## Verwendung

### Direkte Weiterleitung
Verwenden Sie den `fwd` Parameter für direkte URL-Weiterleitungen:

```
go.proeve.net?fwd=https://example.com
```

### Verzeichnis-basierte Weiterleitung
Verwenden Sie den `fwd-v` Parameter für Weiterleitungen über das Verzeichnis:

```
go.proeve.net?fwd-v=go1
```

## Verzeichnis konfigurieren

Bearbeiten Sie die `directory.txt` Datei im folgenden Format:

```
ID;URL
```

Beispiel:
```
go1;https://google.com
go2;https://proeve.net
go3;https://example.com
```

## Design

Die Website verwendet einen eleganten, dunklen Stil mit goldenen Akzenten, inspiriert vom klassisch-modernen Design von proeve.net.

### Farbschema
- Hintergrund: Dunkle Gradienten (#0f0f0f bis #1a1a1a)
- Akzentfarbe: Gold (#d4af37)
- Text: Helles Grau (#e8e8e8)

## Features

- ✅ Direkte URL-Weiterleitung
- ✅ Verzeichnis-basierte Weiterleitung
- ✅ URL-Validierung
- ✅ Elegantes, responsives Design
- ✅ Automatische Weiterleitung nach 2 Sekunden
- ✅ Fehlerbehandlung mit manuellen Weiterleitungsoptionen
- ✅ Loading-Animation

## Deployment

Diese Website kann auf GitHub Pages, Netlify, Vercel oder jedem anderen statischen Hosting-Service bereitgestellt werden.

### GitHub Pages

1. Gehen Sie zu Repository Settings
2. Scrollen Sie zu "Pages"
3. Wählen Sie "main" branch als Source
4. Speichern Sie die Änderungen

## Lizenz

Dieses Projekt wurde für proeve.net erstellt.
