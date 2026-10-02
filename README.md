# Lex Apps for umbrelOS

Community App Store für die privat betriebene Stundenzettel-Anwendung.

## Installation

1. In umbrelOS **App Store → Community App Stores** öffnen.
2. `https://github.com/lex-2610/Umbrel-Store-Repository` hinzufügen.
3. **Stundenzettel** oder **Snapchat Memories API** installieren.
4. Für Stundenzettel mit `admin` und dem in umbrelOS angezeigten App-Passwort anmelden.
5. Für die Snapchat Memories API den API-Endpunkt deiner Umbrel-Instanz in der iOS-App als Serveradresse eintragen.

## Speicherung und Zugriff

Die Web-Oberfläche läuft über Umbrels `app_proxy` auf Port `6066`. Intern hört
die Anwendung weiterhin auf Port `6060`. Sämtliche
SQLite-Datenbanken, Bilder, Uploads, Logs und Anwendungsbackups liegen unter
`${APP_DATA_DIR}/data` und bleiben bei Neustarts und Updates erhalten.

## Image und Updates

Das öffentliche Multi-Arch-Image
`ghcr.io/lex-2610/stundenzettel-umbrel:14.0.0` wird durch GitHub Actions direkt
aus Commit `7a03402317b3775029d207f7c547e28da16339d9` des privaten
Quellrepositorys `lex-2610/Template-Demo-Stundenzettel` gebaut. Anwendungscode
wird nicht in diesen Store kopiert.

Für ein Update werden Quell-Commit und Image-Version im Workflow sowie
Image-Tag, `version` und `releaseNotes` der App aktualisiert. Nach dem Push baut
GitHub Actions das neue Image; umbrelOS erkennt die höhere Manifest-Version als
Update.

## Snapchat Memories API

Die API stellt Medien und Metadaten für den iOS-Viewer bereit. Sie liest die Medien aus `${APP_DATA_DIR}/media` (read-only eingebunden). Dieser Ordner enthält deine importierten Medien und bleibt bei Updates erhalten. Vorschaubilder liegen im Container-Cache und werden bei Bedarf neu erzeugt. Die Installation setzt voraus, dass das öffentliche Image `ghcr.io/lex-2610/memorys-backend:v1.0.4` verfügbar ist.
