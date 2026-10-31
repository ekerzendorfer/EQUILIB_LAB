# Integriert V0.3a – Dynamische symbolische Vogelperspektive

**Stand:** 31.10.2026  
**Implementierung:** [prototyp/integriert-v0.3a/index.html](../../prototyp/integriert-v0.3a/index.html)  
**Rückfallversion:** [integriert-v0.3](../../prototyp/integriert-v0.3/index.html); alle älteren Versionen bleiben erhalten.

## Änderungsumfang

1. Titelzeile und Fußzeile zeigen **V0.3a**. Die weiterhin angebotene Schaltfläche **V0.2-Werte** bezeichnet ein historisches Parameter-Preset, nicht die Programmversion.
2. Symbolische Vogelperspektive im Reiter **Modell**: Insgesamt 60 proportional zu A und B aufgeteilte Kreise nutzen zwei quadratische 8×8-Raster. Bei aktivem Transport wird pro Simulationsschritt je besetzter Seite eine Position gegen eine freie ausgetauscht, auch wenn die Mengen nahezu stationär sind. Die Kreise werden **nicht** als individuell verfolgte Teilchen behandelt.
3. Eine gerade neu besetzte Position leuchtet kurz gelb auf (CSS-Animation von 1,25 Sekunden bei Standardintervall 0,95 Sekunden; höchstens bis zum nächsten veränderten Simulationsschritt). Die Hervorhebung bleibt nicht dauerhaft. Für reduzierte Bewegung entfällt die Animation.
4. Bei mindestens drei nahezu stationären Schritten mit **zwei positiven Gegenströmen** darf die **reine Bildsymbolzahl** kurz um ein Symbol in beide Richtungen pendeln (0/+1/0/−1; sofern beide Seiten genügend Symbole besitzen). Die Summe bleibt 60. **Dies ist eine didaktische Illustrationskonvention, keine aus dem deterministischen Modell berechnete stochastische Fluktuation.**
5. Die in V0.3 vorhandene Vergleichsansicht verwendet Kopien der Vogelperspektive; die Positionsbelegung wird somit automatisch übernommen. Eine eigene didaktische Ausgestaltung des Bereichs **Vergleich** sowie die Kopplung der fünf Story-Bildphasen bleiben Gegenstand von **V0.3b**.

## Unverändert

- Rechenkern `calculateTransfers()`, `advanceOneStep()` und sämtliche Modellparameter.
- Kontinuierliche ME-Bestände, Transportmengen, Datenhistorie und Diagrammwerte.
- Alle eingebetteten Bilder, die manuellen Story-Phasen und das Offline-Ein-Datei-Prinzip.

## Durchgeführte Prüfungen

- JavaScript-Syntaxprüfung der vollständigen Script-Sektion: **bestanden**.
- Rechenkern und eingebettete Phasendaten gegenüber V0.3: **unverändert**.
- Numerischer Modell-Test über 160 Schritte: **bestanden**; Summe der Symbole stets 60, angezeigte Anzahl gleich tatsächlicher SVG-Belegung.
- Regelmäßige Positionsänderung und Markierung auf beiden Seiten bei aktiven Gegenströmen: **bestanden**.
- Nahe stationär beobachtete Symbolverteilungen 19/41, 20/40 und 21/39 bei weiterhin konstant 60 Bildsymbolen: **bestanden**.
- Erneutes Rendern ohne neuen Schritt darf keine neue Position wählen: **bestanden**.
- **Ausständig:** echter visueller Desktop-/Mobil-Browser-Test, Offline-Doppelklick-Test sowie didaktische Sichtabnahme. Automatisierte Logikprüfungen ersetzen diese Tests nicht.

## Kurze Sichtprüfliste

1. V0.3a herunterladen, lokal durch Doppelklick öffnen; die Versionsangabe im Kopf und Fuß prüfen.
2. Reiter **Modell** auswählen, mehrere **Einzelschritte** ausführen: pro Schritt neue sichtbare Positionen und kurze gelbe Akzente erwarten.
3. Simulation starten, bis die Statusanzeige **praktisch stationär** meldet: die beiden Modellwerte nähern sich konstanten Zahlen, während Kreise weiterhin die Position wechseln und gelegentlich ein Symbol mehr oder weniger dargestellt wird.
4. Pause/Start, Reset und Presetwechsel prüfen. Nach Reset keine alte Markierung oder alte Symbolverteilung übernehmen.
5. Reiterwechsel während des Laufs sowie schmalen Bildschirm prüfen. Die Bildgeschichte bleibt in V0.3a absichtlich manuell.

**Didaktisches Kernziel:** Ein dynamisches Gleichgewicht wird nicht als Stillstand wahrgenommen. Gleichwohl dürfen die bewusst animierten Bildsymbole nicht mit einem stochastisch berechneten Teilchenmodell verwechselt werden.
