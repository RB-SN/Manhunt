<p align="center"><img src="logo.png" width="220" alt="Manhunt Neuheim"></p>

# Manhunt Neuheim

Ein Versteck- und Fangspiel für Schülerinnen und Schüler im Dorf Neuheim, angelehnt an «Manhunt» und «Hide & Seek». Die Web-App läuft im Browser, man muss nichts installieren.

## Funktionen

- **Pings:** Der Standort der Gejagten wird regelmässig an die Fänger gesendet.
- **Joker für Gejagte:** Unsichtbar, Fake-Ping, Schutzschild, Verzögerung
- **Joker für Fänger:** Sofort-Ping, Ja/Nein-Frage, Foto-Pflicht, Freeze
- **Freeze:** Ist ein Fänger näher als 30 m, müssen die Gejagten im Versteck bleiben.
- **Keine Gruppenbildung:** Kommen sich zwei gejagte Teams auf weniger als 50 m nahe, haben sie 2 Min. Zeit, sich zu trennen. Sonst wird ihr Live-Standort für die Fänger sichtbar.
- **Gefangene Teams werden zu Fängern.**
- **Punkte und Tagesrangliste:** Punkte gibt es für überlebte Minuten und für Fänge.
- **Zonen:** Grünes Spielfeld und rote Sperrzonen werden auf der Karte eingezeichnet und lassen sich als Standard speichern.
- **Lehrer-Dashboard:** Live-Karte, Runden steuern, Fänge prüfen, Nachrichten und Notfall-Knopf
- **Demo-Modus** mit simulierten Teams

Alle Werte wie Zeiten, Abstände und Punkte lassen sich in der App unter *Einstellungen* anpassen.

## Online stellen mit GitHub Pages

1. Auf github.com ein **neues Repository** erstellen, z.B. `manhunt-neuheim`. Es muss **Public** sein, damit GitHub Pages gratis ist.
2. **Add file → Upload files** wählen und diese Dateien hochladen:
   - `index.html`
   - `logo.png`
   - `README.md`
   - `.nojekyll`
   - `database.rules.json`
   
   Danach auf **Commit changes** klicken.
   > Tipp: `.nojekyll` beginnt mit einem Punkt und ist darum auf Mac und Windows oft versteckt. Die Datei ist nicht zwingend, schadet aber nicht.
3. Unter **Settings → Pages** bei *Source* «**Deploy from a branch**» wählen, dann Branch **main** und Ordner **/ (root)**. Auf **Save** klicken.
4. Nach 1–2 Minuten ist die Seite online unter:
   `https://DEIN-BENUTZERNAME.github.io/manhunt-neuheim/`

Für eine neue Version der App lädst du einfach die neue `index.html` hoch und überschreibst damit die alte.

## Datenbank einrichten (Firebase, einmalig, gratis)

1. Auf [console.firebase.google.com](https://console.firebase.google.com) mit **Projekt hinzufügen** ein Projekt erstellen. Google Analytics kann aus bleiben.
2. Unter **Build → Realtime Database → Datenbank erstellen** den Standort **Belgien (europe-west1)** wählen und mit dem **Testmodus** starten.
3. Im Tab **Regeln** den Inhalt von `database.rules.json` einfügen und auf **Veröffentlichen** klicken.
   Ohne diesen Schritt sperrt der Testmodus die Datenbank nach 30 Tagen.
4. Über das Zahnrad zu **Projekteinstellungen → Meine Apps → Web-App (`</>`)** gehen und eine App registrieren. Hosting braucht es nicht.
5. Den Block `const firebaseConfig = { … }` kopieren.
6. Die GitHub-Pages-Seite öffnen, unter **Lehrperson** die Konfiguration einfügen und speichern.

Die Konfiguration wird automatisch im Beitritts-Link bzw. QR-Code mitgegeben. Die SuS müssen nichts einrichten.

## Ablauf am Spieltag

1. Unter Lehrperson auf **Neues Spiel erstellen** tippen. Die Standard-Zonen werden automatisch übernommen.
2. Mit **📲 QR** den QR-Code zeigen. Die SuS scannen ihn, wählen ihr Team und erlauben den Standortzugriff.
3. Im Tab **Live** prüfen, ob alle Teams 🟢 online sind.
4. Im Tab **Runde** die Fänger wählen und die Runde starten.
5. Nach dem Spieltag unter **Einstellungen → Spiel löschen** alle Daten entfernen.

**Wichtig:**
- Das Gerät der Spielleitung steuert das Spiel, etwa die Pings und das Rundenende. Es muss während der Runden **offen bleiben**.
- Auch die SuS-Handys müssen die Seite offen lassen. Die App hält den Bildschirm wach. Mobile Daten und ein voller Akku sind nötig.
- **iPhone:** Unter *Einstellungen → Datenschutz → Ortungsdienste → Safari-Websites* «Beim Verwenden» und «Genauer Standort» aktivieren.

## Datenschutz

- Während des Spiels werden die Standorte der Teams in der Firebase-Datenbank gespeichert, mit Standort EU (Belgien).
- Eltern und Schulleitung vorab informieren.
- Nach dem Spieltag die Daten in der App löschen: *Einstellungen → Spiel löschen*.
- Die Datenbank-Regeln erlauben Zugriff ohne Anmeldung. Geschützt sind die Daten nur dadurch, dass man den Spielcode bzw. Link kennen muss. Deshalb nur kurz benötigte Daten speichern und danach löschen.

## Technik

- Eine einzige Datei `index.html`, gebaut mit HTML, CSS und JavaScript, ohne Build-Schritt.
- [Leaflet](https://leafletjs.com) für die Karte
- Karten von [swisstopo](https://www.swisstopo.admin.ch): Landeskarte und Luftbild
- [Firebase Realtime Database](https://firebase.google.com/docs/database) für die Echtzeit-Daten
- [qrcode.js](https://github.com/davidshimjs/qrcodejs) für den QR-Code
