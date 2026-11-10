# Aufgaben (von oben nach unten abarbeiten)

Nicht Teil dieses Projekts: Musik-Lern-Funktion bzw. Keyboard-Pfad.

## 0. Grundlage
- [ ] Code aufteilen ohne Build-Schritt: `index.html`, `css/style.css`, `js/` als ES-Module (z. B. `data.js`, `quiz.js`, `avatar.js`, `engine.js`, `music.js`, `app.js`). Verhalten und Spielstände bleiben identisch.
- [ ] Als installierbare Web-App (PWA) ausbauen: `manifest.webmanifest`, App-Icon (Mondwald-Motiv, SVG und PNG 192/512), Service Worker für den Offline-Betrieb mit Versionsnummer zum Cache-Leeren.
- [ ] Kleines Playwright-Testscript unter `tests/` (Startseite lädt ohne Fehler, eine Runde lässt sich durchklicken, Screenshot einer Animation). `package.json` nur für Entwicklungs-Werkzeuge.

## 1. Grafik deutlich verbessern (Schwerpunkt)
Einheitlicher Stil: gefüllte Cartoon-Formen mit dunklem Umriss (`#33302E`) wie bei den Avatar-Figuren, warme Mondwald-Farben, sanfte Schatten. Rahmenbedingungen: flüssig auf dem Tablet, keine schweren SVG-Filter in Animationen, hell/dunkel beachten.
- [ ] **Begleiter als gezeichnete Figuren** statt Emojis: Funkel (Glühwürmchen), Ulla (Eule), Nuss (Eichhörnchen), Flink (Fuchs), Silber (Hirsch), Glut (kleiner, freundlicher Mondrache). Mit Ruhe-Animation (atmen, blinzeln, Funkel schwebt und leuchtet). Gesperrte Begleiter als dunkle Silhouette.
- [ ] **Welt-Szene neu:**
  - mehrere Ebenen (Himmel, Mond mit Schein, ferner und naher Wald, Lichtung)
  - schwebende Glühwürmchen, leuchtende Pilze und Blumen
  - der Avatar steht auf der Lichtung, die Begleiter um ihn herum
  - Tag-Variante im hellen und Nacht-Variante im dunklen Modus
- [ ] **Übungs-Bühne:** statt leerer Box eine kleine Lichtung mit Turnmatte bzw. Moosboden, die Wand als Steinwand oder Baumstamm, die Linie als Leuchtpfad, das Kissen als Moospolster.
- [ ] **Avatar-Feinschliff:**
  - Gesichtsausdrücke (normal, freut sich bei „Geschafft!“, konzentriert bei Halteübungen), Blinzeln
  - Pfoten bzw. Hände passend zum Wesen
  - bessere Kleidung (Ärmel- und Hosenkanten, Rockfalten, Rüstungsplatten, Gürtelschnalle)
  - neuer Werkstatt-Bereich „Frisur“ für das Waldkind (mehrere freie Frisuren)
- [ ] **Oberfläche:**
  - eigene SVG-Icons statt Emojis (Kristall, Stern, Lautsprecher, Musik, Schloss, Zahnrad, Pfad-Symbole)
  - Knöpfe mit Tiefe, Fortschrittsbalken als leuchtender Pfad
  - sanfte Übergänge zwischen Bildschirmen
- [ ] **Belohnungs-Effekte:** Kristalle fliegen in den Zähler, Funken bzw. Konfetti bei neuer Stufe, Begleiter oder Werkstatt-Teil, kleine Freischalt-Zeremonie am Rundenende.
- [ ] **Rätsel-Grafiken:** einfache SVG-Illustrationen statt Emojis für Zähl- und Bildfragen (Äpfel, Fische, Tiere, Formen).

## 2. Animationen
- [ ] Alle Übungen auf IK-Frames umstellen (Rad 2–5, Wandlauf, Einschwingen, Handstand an der Wand, Bärengang, Brett, Liegestütz, Schiffchen). Hände und Füße rutschen nicht, der Kopf verschwindet nicht im Boden, Bewegungen wirken weich (Ein- und Ausschwingen, leichte Überzeichnung).
- [ ] Rad zusätzlich gespiegelt anbieten (andere Seite) bei der Stufe „Sauberes Rad“.

## 3. Elternbereich mit PIN
- [ ] 4-stellige PIN, beim ersten Öffnen festlegen; Zugang über einen unauffälligen Knopf auf der Profilauswahl.
- [ ] Fortschritt je Kind (Stufen, Kristalle, Runden), Stufe manuell setzen, Kristalle korrigieren.
- [ ] Rätselthemen ein- und ausschalten, optional Runden pro Tag begrenzen.
- [ ] Sicherung sowie „Ton & Stimme“ hierher verschieben.

## 4. Rätsel
- [ ] Mindestens 60 Rätsel je Profil, orientiert an LehrplanPLUS Bayern (Vorschule bzw. 2. Klasse: Mathe, Deutsch, HSU), kindgerecht und gern witzig.
- [ ] Schwierigkeit je Frage (1–3) und automatische Anpassung nach Trefferquote; kürzlich gestellte Fragen nicht wiederholen.

## 5. Welt lebendiger
- [ ] Begleiter mit Funktion (z. B. Ulla gibt einen Tipp bei einem Rätsel, einmal pro Runde).
- [ ] Gemeinsame Geschwister-Challenge (Kristalle beider Kinder zählen zusammen auf ein Ziel).
- [ ] Kleine Tagesaufgabe mit Bonus-Kristall.
