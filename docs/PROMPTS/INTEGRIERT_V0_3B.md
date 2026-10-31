# Integriert V0.3b – Synchroner Vergleich und automatische Bildphasen

**Stand:** 31.10.2026  
**Datei:** [prototyp/integriert-v0.3b/index.html](../../prototyp/integriert-v0.3b/index.html)  
**Rückfallversion:** [integriert-v0.3a](../../prototyp/integriert-v0.3a/index.html)

## Umsetzung

1. **Vergleich: dynamische Symbolgärten.** Die beiden 8×8-Gärten zeigen dieselben insgesamt 60 Kreispositionen wie „Modell“. Neu belegte Positionen werden in beiden Reitern kurz gelb hervorgehoben; auch nahe dem Gleichgewicht bleiben Positionswechsel und die rein symbolische gelegentliche ±1-Fluktuation aktiv. Die Vergleichs-SVGs werden nur einmal erzeugt, damit ein Reiterwechsel keine künstliche neue Animation startet.
2. **Vergleich: automatische Bildphasen.** Das Bild folgt der berechneten Annäherung vom Startbestand zum stationären Bestand: I bei Schritt 0/ohne Transport; II bei Fortschritt unter 19 %; III von 19 % bis unter 72 %; IV ab 72 % bis zur nachgewiesenen praktischen Stationarität; V ab drei aufeinanderfolgenden fast stationären Schritten bei aktiven Gegenströmen. Bilddateien wechseln nur bei einem Phasenübergang. Die fünf Bilder sind qualitative Illustrationen, keine exakte Darstellung gezählter Äpfel. Bei geänderten Parametern ist die Analogie nur eingeschränkt zutreffend. In „Geschichte“ bleiben die manuellen Phasenknöpfe erhalten.
3. **Vergleich: zweites Diagramm** unter den Bildern. Gleicher Zustand, identische Stufenlinien und dieselbe Historie wie in „Modell“. Beide Reiter bieten dieselbe synchronisierte Auswahl „Letzte 40 Schritte“ / „Volle Laufzeit“.
4. Titel und Fußzeile auf V0.3b gestellt. V0.3a und alle Vorversionen bleiben erhalten.

## Unverändert

- `makeInitialState()`, `calculateTransfers()`, `advanceOneStep()`, sämtliche Parameter und das Stationaritätskriterium.
- Originale WebP-Bildgeschichte und Offline-Ein-Datei-Betrieb.
- Deterministische Bestände und Raten; die frei verschobenen Bildkreise sind **kein stochastisches Rechenmodell**.

## Prüfungen

- JavaScript-Syntax der vollständigen Script-Sektion: **bestanden**.
- HTML-ID-Eindeutigkeit: **bestanden**.
- Vergleich der Rechenkernfunktionen mit V0.3a: **unverändert**.
- **Ausständig:** visueller Desktop-/Mobiltest, Offline-Doppelklick und fachliche Sichtabnahme.

### Sichtprüfliste

1. Mit Apfelkrieg-Vorgabe „Vergleich“ öffnen und Schritte ausführen: Die Bilder sollten in der Reihenfolge I–V automatisch wechseln.
2. Modell und Vergleich abwechselnd betrachten: gleiche Kreispositionen, kurze gelbe Markierungen und gelegentliche ±1-Symbolschwankung, ohne beim bloßen Reiterwechsel neu auszulosen.
3. Stufendiagramme vergleichen und zwischen „Letzte 40 Schritte“ und „Volle Laufzeit“ wechseln.
4. Reset/Parameteränderungen testen: Diagramm, Bildphase und Kreise müssen synchron neu beginnen.
5. Im Reiter „Geschichte“ weiterhin alle fünf Bilder manuell wechseln; Offline-Doppelklick und Mobilbreite prüfen.
