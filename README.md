# SV Gustlmännchen

Die Vereinsseite der Hobbyliga-Truppe: Trainingstermine eintragen, abstimmen, wer kann — und
den Strafkatalog vor Augen haben.

Zwei Dateien, kein Build, keine Abhängigkeiten: `index.html` und das Wappen `wappen.svg`.

## Benutzen

`index.html` im Browser öffnen — das war's. `wappen.svg` muss daneben liegen, sonst fehlt nur das
Wappen; die Seite funktioniert trotzdem.

1. **Anmelden** — einmal mit Namen (Rückennummer optional) eintragen. Kader, Kalender, Abstimmung und
   Strafkatalog sind erst nach der Anmeldung zu sehen; ohne Anmeldung bleiben nur die Anmeldung selbst
   und „Über den Verein" sichtbar. Das ist ein Sichtschutz, kein Zugangsschutz — die Seite liegt
   beim Betrachter im Browser, wer den Quelltext liest, sieht alles.
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

Die Vereinsfarben Grün und Weiß stecken in den CSS-Variablen `--pitch`, `--pitch-2` und `--on-pitch`
ganz oben im `<style>`-Block; ein Dark-Mode-Satz derselben Variablen steht direkt darunter.

**Wappen:** `wappen.svg`, aus der Vorlage `FINAL_GUSTLMÄNNERS.pdf` verlustfrei als Vektor übernommen.
Es trägt die Farben Grün `#3A6242` und Gold `#CAA56D`; das Gold steckt als `--gold` auch in der
Zierleiste unter dem Kopf. Die Größe regelt `.wappen { width: … }` im `<style>`-Block.

## Lizenz

MIT
