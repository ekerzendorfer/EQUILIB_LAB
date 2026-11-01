# EQUILIB_LAB – Prüfprotokoll v0.4c (01.11.2026)

**Testversion:** `prototyp/integriert-v0.4c/index.html`  
**Basis:** v0.4b, unverändert archiviert.  
**Status:** JavaScript-Syntax- und Rechenkernprüfungen bestanden; interaktiver Browser-, visueller und Offline-Doppelklicktest **noch ausständig**.

## Neuer Umfang

- Einmalige, eindeutig beschriftete Zugabe von **0,20 mol/L Edukt A**, auch während des Laufs.
- c(A) steigt **im selben Simulationsschritt** um 0,20. c(B), c(C) und c(D) bleiben im Zugabemoment unverändert.
- Reaktionsquotient Q unmittelbar vor und nach der Störung; Anzeige Q < K, Q > K oder Q ≈ K. K = kHin/kRueck bleibt bei der reinen Stoffzugabe konstant.
- Numerische Neuberechnung der **vier** erwarteten Gleichgewichtskonzentrationen aus den aktuell zulässigen Reaktionswegen und k-Werten (Bisektionsverfahren auf vHin−vRueck=0).
- Störung im Stufendiagramm senkrecht und als Markierung „A +0,20“ gekennzeichnet; y-Skala wächst bei Konzentrationen oberhalb von 1,000 mol/L.
- Symbolpunkte der Einzelbestände wachsen bei Bedarf über 24 Punkte hinaus, damit Konzentrationen oberhalb von 1,000 sichtbar bleiben.
- Reaktionsraum wird durch das vorhandene Symbolteilchenmodell nachgeführt; Kollisionen beeinflussen die Rechengleichungen weiterhin nicht.
- Anzeigen für die tatsächlich geltenden Bilanzsummen, aktualisierte didaktische Hinweise.
- Einmalige Zugabe pro Versuch. Reset löscht Zugabe und Marker, Parameterverschiebung in Pause startet neuen Versuch.

## Fachlicher Kern

```text
A + B ⇌ C + D
vHin   = kHin * cA * cB
vRueck = kRueck * cC * cD
Kc     = kHin / kRueck
Qc     = (cC*cD)/(cA*cB), sofern der Nenner > 0

Störung zum Schritt n: cA(n)+=0,20 mol/L
cB(n),cC(n),cD(n) bleiben unmittelbar konstant.
Danach: delta = (vHin-vRueck)*Delta t,
cA,cB -= delta; cC,cD += delta.
```

Vor der Störung gilt bei Start 1/1/0/0: cA+cC=1, cB+cD=1. Nach der einmaligen Zugabe: **cA+cC=1,2, cB+cD=1**; während der nachfolgenden Reaktionsschritte bleiben diese beiden Summen konstant. Dies ist eine absichtliche äußere Störung, kein Erhaltungsfehler.

## Durchgeführte automatische Quellcode-/Mathematikprüfungen

1. Vollständiger v0.4c-JavaScript-Inhalt erfolgreich syntaktisch kompiliert (ohne Browserausführung).
2. Der ursprüngliche JavaScript-Block für Apfel/Stechheber vor dem eigenständigen Chemie-Modell blieb byte-/textidentisch.
3. Zehn eingebettete `data:image/`-Vorkommen vorhanden wie in v0.4b; keine Bildauslagerung.
4. Ohne Störung, kHin=kRueck=0,08: Schritt 1 A/B=0,92 und C/D=0,08; stationär alle 0,5.
5. Nach nachträglicher A-Zugabe von 0,20 und 900 weiteren Schritten: keine negativen Konzentrationen; `A+C=1,2`, `B+D=1,0` innerhalb 1e-9.
6. K=1 und A-Zugabe: neue Gleichgewichtskonzentrationen numerisch bestätigt: A=0,65454545; B=0,45454545; C=D=0,54545455.
7. Numerische Vorhersage des ungestörten K=10: C=D=0,75974693, und K=0,1: C=D=0,24025307.
8. Repository-Commit der v0.4c-Datei: `e92bc3f24b09ee0ed9d20dfcfa8fac7c5313f33f`.

**Nicht geprüft:** echte Klicks und Canvas-Animation im Browser, mobile Darstellung, lokaler Offlinebetrieb, exakte Sichtabnahme der Graph-Markierungen, Bedienung der Regler im Live-Betrieb.

## Nutzerabnahme – kleiner Rundgang

1. `https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4c/` öffnen, Chemie-Reiter wählen. Bei kHin=kRueck=0,08 zunächst die bestehenden Ansichten und den gemeinsamen Reaktionsraum testen.
2. Bis zu nahezu stationären Werten (alle circa 0,500) rechnen; dann **A zugeben (+0,20 mol/L)** klicken. Im **selben Schritt** A=0,700, B/C/D=0,500; K=1,00; Q sinkt von ~1 auf ca. **0,714**. Im Diagramm entsteht eine senkrechte Änderung nur bei A. Der Hinratenwert springt von ca. 0,0200 auf 0,0280, die Rückrate bleibt zunächst bei 0,0200.
3. Weiterlaufen lassen. Neues GG ungefähr A=0,655, B=0,455, C=D=0,545. Die Hin- und Rückrate sind dann wieder gleich, aber nicht null.
4. Reset, **direkt bei Schritt 0** A zugeben: A=1,200 und B=1,000, C/D=0,000. Y-Skala muss 1,200 erfassen; der gemeinsame Reaktionsraum und die separate Punktansicht dürfen keinen Teilchenüberschuss verschweigen.
5. Reset; kHin=0,20, kRueck=0,02 einstellen. K=10 und entsprechendes GG prüfen; bei A-Zugabe muss die Vorhersage der vier Zielwerte neu berechnet werden.
6. A-Zugabe nur einmal pro Versuch möglich; Reset oder Parameteränderung in Pause startet einen neuen Versuch. Bei laufendem Auto-Modus darf die Zugabe keine doppelte Rechenrunde verursachen.
7. Wechsel zwischen Geschichte/Modell/Vergleich und Chemie; die Apfelphasen und Apfelparameter bleiben unverändert.
8. HTML **lokal offline per Doppelklick** prüfen; Notebook/Projektor und schmale Fenster testen.

## Bekannte Grenzen / nächste Schritte

- Es handelt sich um ein formales kinetisches Reaktionsmodell mit vereinfachten Konzentrationen, kein quantitativer Mechanismus einer realen Esterbildung. Teilchenkollisionen sind ausschließlich symbolisch.
- Nur **eine A-Zugabe**; weder Produktentzug noch Temperatur-/Volumeneingriffe. Bewusst kleines v0.4c-Inkrement.
- v0.4c ist eine **Testfassung**. **Root `index.html` weiterhin v0.3e**, v0.4b bleibt archiviert.
- Nach manueller Browser-/Offline-Abnahme nur gezielte Fehlerkorrekturen durchführen. Erst dann über v0.4d entscheiden.
