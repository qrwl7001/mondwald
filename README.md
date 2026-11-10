# Mondwald – Einrichtung

Diese Anleitung beschreibt, wie die App kostenlos über GitHub Pages online geht und wie du sie mit Claude Code weiterentwickelst.

## 1. App bei GitHub Pages veröffentlichen (einmalig, ca. 15 Minuten)

1. **GitHub-Konto** unter github.com anlegen (kostenlos).
2. **Neues Repository** anlegen, Name z. B. `mondwald`, Sichtbarkeit **Public**.
   Kostenloses GitHub Pages braucht ein öffentliches Repository. Die App enthält keine persönlichen Daten, da Namen und Spielstände nur auf dem Tablet gespeichert werden.
3. **Dateien hochladen:** Im neuen Repository „Add file“ → „Upload files“ wählen und den **Inhalt** dieses Ordners hineinziehen (`index.html`, `README.md`, `CLAUDE.md`, Ordner `docs`, `.nojekyll`, `.gitignore`), dann „Commit changes“.
   Werden die Dateien mit Punkt am Anfang nicht angezeigt, ist das für den Start kein Problem.
4. **Pages einschalten:** Im Repository „Settings“ → „Pages“ öffnen. Bei „Source“ „Deploy from a branch“ wählen, Branch `main` und Ordner `/ (root)` einstellen, dann „Save“.
5. Nach 1–2 Minuten läuft die App unter `https://DEIN-BENUTZERNAME.github.io/mondwald/`.

## 2. Spielstände mitnehmen

1. In der **alten** App (Claude-Link) auf der Profilauswahl „💾 Sicherung“ antippen und den Code kopieren.
2. In der **neuen** App (GitHub-Link) unter „💾 Sicherung“ den Code einfügen und „Einspielen“ tippen (zweimal bestätigen).
3. Auf dem Tablet in Chrome über das Drei-Punkte-Menü „Zum Startbildschirm hinzufügen“ wählen.

## 3. Weiterentwickeln mit Claude Code

Für Claude Code ist ein bezahltes Claude-Abo nötig.

1. **Claude Code installieren:** Am einfachsten über die Claude-Desktop-App, dort im Bereich „Code“ (keine Kommandozeile nötig). Alternativ im Terminal, siehe die offizielle Anleitung: https://code.claude.com/docs/en/quickstart
2. **Repository auf den Rechner holen:** Am bequemsten mit **GitHub Desktop** (desktop.github.com), dort „Clone repository“ wählen und `mondwald` auswählen.
3. **Claude Code im Ordner `mondwald` starten** und schreiben:
   > Lies CLAUDE.md und arbeite die nächsten offenen Aufgaben aus docs/AUFGABEN.md ab.
4. Claude arbeitet selbstständig, hakt Aufgaben ab und lädt am Ende der Sitzung hoch (`git push`). Die Tablet-App ist danach nach ca. 1–2 Minuten aktuell.
   Klappt das Hochladen aus Claude Code nicht, kannst du in GitHub Desktop auf „Push origin“ klicken.

## Tipps

- **Eigene Wünsche** einfach oben in `docs/AUFGABEN.md` eintragen oder Claude direkt sagen.
- **Alte Version zurückholen:** Jede Änderung ist in Git gespeichert. Claude kann eine frühere Version wiederherstellen („Mach die letzte Änderung rückgängig“).
- **Spielstände:** Ab und zu in der App eine Sicherung machen.
