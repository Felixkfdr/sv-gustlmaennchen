# SV Gustlmännchen

Die Vereinsseite der Hobbyliga-Truppe: Trainingstermine eintragen, abstimmen, wer kann — und
den Strafkatalog vor Augen haben.

Kein Build: `index.html`, das Wappen `wappen.svg` und der Ordner `spieler/` mit den Fotos. Die
Schriften Oswald und Barlow kommen von Google Fonts; ohne Netz fällt die Seite auf Systemschriften
zurück und bleibt bedienbar.

Die Seite hat zwei Ebenen:

- **Startseite** — für alle sichtbar: Begrüßung, die Mannschaft mit 18 Plätzen, „Über den Verein",
  „Dritte Halbzeit" und die Anmeldung.
- **Interner Bereich** — erst nach der Anmeldung: Kader, Kalender, Abstimmung, Strafkatalog.

## Benutzen

`index.html` im Browser öffnen — das war's. Fehlen `wappen.svg` oder die Fotos, bleibt die Seite
bedienbar, es fehlen nur die Bilder.

1. **Anmelden** — Name (Rückennummer optional) und das **Vereinspasswort**. Erst danach erscheinen
   Kader, Kalender, Abstimmung und Strafkatalog.

   > Das Passwort ist ein Sichtschutz, kein Zugangsschutz. Die Seite läuft komplett im Browser des
   > Betrachters; wer den Quelltext liest, kommt an alles. Es hält Neugierige fern, keinen
   > Entschlossenen. Echter Schutz geht nur mit einem Server.
2. **Kalender** — Tag anklicken, Uhrzeit eintragen, fertig; der Ort ist freiwillig. Wer einen Termin
   einträgt, steht automatisch auf „dabei". Ein Punkt im Kalender zeigt, dass an dem Tag etwas ansteht,
   die Zahl darin die Zusagen; wird der Punkt grün, findet das Training statt.
3. **Abstimmung** — zu jedem Termin *Bin dabei*, *Vielleicht* oder *Kann nicht*. Nochmal auf dieselbe
   Antwort klicken nimmt sie zurück. Kommen genug Zusagen zusammen, springt der Termin auf
   **Training findet statt**.
4. **Strafkatalog** — die übliche Liste, erweiterbar. Zeilen lassen sich über das × löschen.
   Gerechnet wird in **Gustl**: ein Gustl sind 1,48 €, der Eurobetrag steht klein unter jedem Wert.
   Zu spät zum Training kostet 1 Gustl je angefangene 5 Minuten, höchstens 5 Gustl.

Die Schwelle („Training findet statt ab _n_ Zusagen") steht oben in der Abstimmung und lässt sich
jederzeit ändern — Standard sind 8.

## Die Mannschaft: 18 Plätze

Die Plätze auf der Startseite stehen in `MANNSCHAFT` oben im `<script>`-Block. Ein gefüllter Platz
sieht so aus:

```js
{ nr: 7, name: 'Sepp', pos: 'Mittelfeld', bild: 'spieler/sepp.jpg',
  bier: 'Radler', stark: 'Freistöße', seit: 2026,
  spruch: 'Steht unten auf dem Spickzettel.' },
```

`name` und `pos` stehen auf dem Platz, der Rest landet im Spickzettel, der beim Überfahren mit der
Maus aufklappt und bei einem Klick (oder Tipp am Handy) stehen bleibt. Alles außer `nr` darf fehlen;
ein Eintrag ohne `name` bleibt ein freier Platz.

Fotos kommen nach `spieler/` — quadratisch, etwa 400 × 400 Pixel. Fehlt die Datei, zeigt der Platz
die Initialen. Mehr dazu in `spieler/README.md`.

## Vereinspasswort ändern

Im Quelltext steht nur die Prüfsumme, nicht das Passwort selbst. Zum Ändern:

1. Seite im Browser öffnen, Entwicklerkonsole aufmachen (F12).
2. `pruefsumme('neuesPasswort')` eingeben.
3. Den achtstelligen Rückgabewert bei `var PASSWORT = '…'` im `<script>`-Block eintragen.

**Das Passwort selbst gehört nicht ins Repo** — weder in die README noch in einen Commit. Sagt es
der Mannschaft beim Training.

## Daten

Alles landet im `localStorage` des jeweiligen Browsers, unter dem Schlüssel `svg-hobbyliga-v1`.
Das heißt: **jeder sieht erst einmal nur seine eigenen Eintragungen.** Für eine echte gemeinsame
Abstimmung über mehrere Geräte hinweg bräuchte es einen kleinen Server (oder einen gehosteten
Datendienst), der Kader, Termine und Stimmen hält — die Seite ist so gebaut, dass dafür nur
`load()` und `save()` im `<script>`-Block ausgetauscht werden müssen.

Im privaten Modus mancher Browser ist `localStorage` gesperrt; dann funktioniert alles wie gewohnt,
die Daten sind aber nach dem Schließen des Tabs weg.

## Anpassen

Oben im `<script>`-Block:

| Konstante | Bedeutung |
| --- | --- |
| `GUSTL_EUR` | was ein Gustl in Euro kostet (1,48) |
| `DEFAULT_PENALTIES` | Strafkatalog, mit dem eine frische Seite startet — Beträge in Gustl |
| `STORE` | Schlüssel im `localStorage` |
| `MANNSCHAFT` | die 18 Plätze (siehe oben) |
| `PASSWORT` | Prüfsumme des Vereinspassworts (siehe oben) |

Das Aussehen hängt an den Farbtokens ganz oben im `<style>`-Block — warmes Papier (`--ground`,
`--paper`), Vereinsgrün (`--pitch`, `--band`) und das Gold des Wappens (`--gold`). Darunter stehen
dieselben Tokens zweimal für die dunkle Darstellung: einmal nach Systemeinstellung, einmal für
`<html data-theme="dark">`. Komponenten greifen nur auf Tokens zu, eine Farbe ändert man also an
genau einer Stelle.

Schriften: Oswald für Überschriften, Knöpfe und Beträge (`--display`), Barlow für alles andere
(`--sans`).

**Wappen:** `wappen.svg`, aus der Vorlage `FINAL_GUSTLMÄNNERS.pdf` verlustfrei als Vektor übernommen.
Es trägt die Farben Grün `#3A6242` und Gold `#CAA56D`; das Gold steckt als `--gold` auch in der
Zierleiste unter dem Kopf. Die Größe regelt `.wappen { width: … }` im `<style>`-Block.

## Lizenz

MIT
