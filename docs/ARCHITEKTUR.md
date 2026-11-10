# Architektur

## Überblick
- Ursprünglich **eine einzige Datei** `index.html` mit CSS und JS inline. Schrift: Baloo 2 (Google Fonts) mit Fallback.
- Farb-Tokens auf `:root`, dunkle Werte unter `@media (prefers-color-scheme: dark)` und `[data-theme="dark"]`.
- Bildschirme (`section.screen`): `s-profiles` → `s-world` → `s-round` → `s-end`, dazu `s-shop` (Avatar-Werkstatt). Dialoge: Profil ändern, Ton & Stimme, Sicherung.

## Datenmodell (localStorage `mondwald-v1`)
```
{ profiles: [ { id, name, level: 'klein'|'gross', total, rounds,
                paths: { hs:{s,c}, rad:{s,c} },          // Stufe (0-basiert) und Übungszähler
                look: { sp, fur, acc, out, cloth, head, back, hand } } ],
  settings: { music, vol, voice, rate, pitch } }
```
`migrate()` ergänzt fehlende Felder. Die Sicherung ist `'MW1:' + base64(JSON {app:'mondwald', v:1, date, data})`.

## Code-Abschnitte (Reihenfolge im Script)
1. **Daten:**
   - `COMPANIONS`: Begleiter mit Kristall-Schwelle
   - `STAGE_GOAL = 6`
   - `WARMUP`
   - `PATHS`: `hs`/`rad`, jeweils `klein`/`gross`, Stufen mit Übungen `{t,d,n,u:'x'|'s',anim,safe?}`
   - `ANIMS`
2. **Rätsel:** `QUIZ.klein`/`QUIZ.gross`, Format `{c, q, v?, a:[richtig, falsch…]}`
3. **Avatar-Bausteine:**
   - Listen: `SPECIES`, `COLORS`, `CLOTH`, `OUTFITS`, `HEADS`, `BACKS`, `HANDS`, `DEFAULT_LOOKS`
   - Freischaltung über `need:{crystals:n}` oder `need:{path:'hs'|'rad', stage:i}`
   - Zeichenfunktionen: `headSVG`, `tailSVG`, `backSVG`, `frontAccSVG`, `handSVG`, `shieldSVG` (lokales Koordinatensystem, oben = −y)
4. **Engine:**
   - `skel`, `ik2`/`ikPose`, `solveFrames`
   - `capsule`: abgerundete, verjüngte Gliedmaßen-Form
   - `makeFigure`: Ebenen, Umriss plus Füllung
   - `portraitSVG`, `mountAnim`
5. **App:**
   - Speicher/`migrate`
   - Stimme (`speak`, Web Speech API)
   - Musik (`Music`, live per WebAudio erzeugt; ruhig/aktiv, Ducking beim Vorlesen)
   - Einstellungen, Profile, Welt, Runde, Ende, Werkstatt (`TABS`, `isOpen`, `openKeys`, `newUnlocks`), Sicherung

## Spielregeln
- **Runde:** Aufwärmen → Rätsel → Handstand → Rätsel → Rad → Rätsel → Handstand → Rätsel → Rad → Rätsel.
- **Kristalle:** Pfad-Übung 2 💎, Aufwärmen 1 💎, richtige Antwort 1 💎. Übungen bestätigt das Kind selbst. Halteübungen (`u:'s'`) haben einen Countdown.
- **Stufen:** Nur Übungen der aktuellen Stufe zählen. Nach `STAGE_GOAL` Durchgängen wird die nächste Stufe freigeschaltet.
- **Begleiter und Werkstatt-Teile** werden über Gesamtkristalle (nie ausgegeben) bzw. Pfad-Stufen freigeschaltet.

## Figuren-Rig
- Längen: `LEN = {T:36, N:15, UA:20, FA:18, TH:24, SH:24}`, Boden `G = 200`, Animations-viewBox `30 56 240 156`.
- **Winkel:** 0° = unten, 90° = rechts, 180° = oben, `dir(a) = [sin a, cos a]` (SVG-y zeigt nach unten).
- **Pose** `P(t, a, b, l, m)`:
  - `t` = Rumpf (Hüfte → Hals)
  - `a`/`l` = vorderer bzw. rechter Arm/Bein, jeweils `[Ober, Unter]`
  - `b`/`m` = hinterer bzw. linker
- **Ansichten:** `side` (Handstand-Pfad) und `front` (Rad-Pfad).
- **Frames:** `{p, at, d}` mit Verankerung `at`:
  - `{hip:[x,y]}`
  - `{part:'hA'|'hB'|'fL'|'fM', x, y}`
  - `{keep:'hA'}` (Position aus dem vorigen Frame)
  - `{part, keepx:true, y}`
  - `{auto:true, x}` (tiefster Punkt inkl. Kopf auf den Boden)
- **Bevorzugt sind IK-Frames:** `{ik:{hip, t, hA, hB, fL, fM, arm, leg}, d}`. Hände und Füße stehen fest auf Zielpunkten. `arm`/`leg` = `'up'|'down'|'left'|'right'` wählt die Ellbogen- bzw. Kniestellung. Winkel werden automatisch auf den kürzesten Weg gebracht.
- **Zeichnen:**
  - Kopf-Faktor 1,45 in Animationen und 1,5 im Porträt, Kopf sitzt `LEN.N + 2.5` über dem Hals.
  - Reihenfolge der Ebenen: Rücken-Ausrüstung → hintere Glieder (Umriss, Füllung, Schatten) → Schwanz → Rumpf und vorderes Bein → Deko → Kopf → vorderer Arm (liegt über dem Kopf, damit er beim Handstand sichtbar ist) → Schild → Handgegenstand.
  - In Animationen werden keine Rücken- oder Handgegenstände gezeigt.
  - Über die Figur kommt ein Bodenstreifen, der Ohren und Füße am Boden sauber abschneidet.

## Testen
- **Syntax:** das Script aus `index.html` extrahieren und `node --check` ausführen (oder je Modul, falls aufgeteilt).
- **Optik:** Playwright (`npx playwright install chromium` einmalig) mit einem kleinen Script, das `index.html` lädt und Screenshots macht. Für Animationen: im Seitenkontext `solveFrames(ANIMS[name])` aufrufen, Zwischenbilder interpolieren, je Bild `makeFigure(svg, look, view, false, 1.45)(v)` zeichnen und einen Screenshot ansehen.
- **Rundendurchlauf:** Profil anklicken → „Runde starten“ → Stationen per Klick auf „Geschafft“ bzw. „Überspringen“ und Antworten durchlaufen, dabei auf `pageerror` achten.

## Hosting
- **GitHub Pages:** Branch `main`, Root. `.nojekyll` liegt bei. Jeder Push veröffentlicht nach ca. 1–2 Minuten.
- **Wichtig:** Der Spielstand hängt an der Adresse. Bei einem Umzug die Sicherung (Code) in der alten Version kopieren und in der neuen einspielen.
