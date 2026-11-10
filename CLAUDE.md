# Mondwald – Anweisungen für Claude Code

Lern- und Bewegungs-App für zwei Geschwister (5 J. Vorschule, 8 J. 2. Klasse, Bayern). Statische Web-App, gehostet über **GitHub Pages** (Branch `main`, Ordner Root). Läuft auf einem Android-Tablet in Chrome.

## Arbeitsweise
- **Selbstständig arbeiten, keine Rückfragen.** Nimm die erste offene Aufgabe aus `docs/AUFGABEN.md`, entscheide Umsetzung, Inhalt und Design selbst und setze sie um. Frage nur, wenn eine Aufgabe ohne Info des Nutzers wirklich unlösbar ist oder Sicherheit/Kindgerechtheit betroffen ist.
- **Kontingent sparen:** Nur die Dateien bzw. Abschnitte lesen, die du brauchst. Gezielte Edits statt Dateien neu schreiben. Keine langen Erklärungen im Terminal. Mehrere zusammenhängende Teilaufgaben in einem Durchgang erledigen.
- **Nach jeder Aufgabe:**
  1. Prüfen: JS-Syntax prüfen (`node --check` für jede JS-Datei bzw. das extrahierte Script), bei Grafik/Animation einen Screenshot per Playwright ansehen (siehe `docs/ARCHITEKTUR.md`, Abschnitt Testen).
  2. In `docs/AUFGABEN.md` abhaken und in `docs/CHANGELOG.md` eine Zeile ergänzen.
  3. `git commit` mit kurzer deutscher Nachricht.
- **Am Ende einer Sitzung** `git push`. Das veröffentlicht automatisch über GitHub Pages. Danach dem Nutzer in 3–5 Zeilen auf Deutsch sagen, was neu ist.

## Feste Regeln
- **Keine Build-Tools, kein Framework-Zwang:** Alles muss als statische Dateien direkt auf GitHub Pages laufen. Externe Skripte nur mit fester Versionsnummer. Google Fonts ist erlaubt. Keine Tracking- oder Werbedienste.
- **Spielstände nie kaputt machen:** localStorage-Schlüssel `mondwald-v1` beibehalten. Neue Felder immer in `migrate()` mit Standardwerten ergänzen. Sicherungscodes mit Präfix `MW1:` müssen weiter einlesbar bleiben.
- **Kindgerecht:** freundlich, keine gruseligen oder gewalttätigen Darstellungen (Schwert und Schild sind Deko, kein Kampf), Sicherheitshinweise bei riskanteren Turnübungen. Keine echten Namen der Kinder in den Code.
- **Bedienung:** große Touch-Ziele, Querformat bevorzugt, hell/dunkel über Farb-Tokens, `prefers-reduced-motion` respektieren, flüssig auf einem Mittelklasse-Tablet.
- **Texte:** Deutsch mit typografischen Anführungszeichen („ “ ’).
- **Nicht Teil dieses Projekts:** die Musik-Lern-Funktion bzw. der Keyboard-Pfad. Nicht anfangen. Die vorhandene Hintergrundmusik bleibt, nur Fehler beheben.

## Wo was steht
- `index.html`: die App (später ggf. aufgeteilt, siehe Aufgabe 0)
- `docs/ARCHITEKTUR.md`: Datenmodell, Code-Aufbau, Figuren-Rig, Animationen, Testen
- `docs/AUFGABEN.md`: priorisierte Aufgabenliste
- `docs/CHANGELOG.md`: Änderungsprotokoll
