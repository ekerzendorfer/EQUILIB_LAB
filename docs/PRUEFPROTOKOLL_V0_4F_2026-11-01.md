# EQUILIB_LAB – Prüfprotokoll v0.4f (01.11.2026)

**Testversion:** [v0.4f](../prototyp/integriert-v0.4f/index.html) · [GitHub Pages](https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4f/) · **Basis:** vom Nutzer im Browser erfolgreich geprüfte v0.4e. **Status:** Quelltext- und Rechenprüfungen bestanden, Sicht-, Offline- und Interaktionstest der v0.4f durch den Nutzer ausständig. Freigegebene Root-`index.html` bleibt v0.3e.

## Änderungen

- Neuer Schalter **Säurekatalysator: AUS / EIN (×3)**, zur Laufzeit umschaltbar; Status und wirksame k-Werte sichtbar. Beispiel: Schwefelsäure `H₂SO₄` als **didaktischer Modellkatalysator**, keine Kalibrierung auf eine reale Laborveresterung.
- Separater chemischer Zeitfaktor `0,6` verlangsamt beide Reaktionsrichtungen in der Standardeinstellung: `k_eff,hin=0,6·k_basis,hin`, `k_eff,rück=0,6·k_basis,rück`. Mit Katalysator wird **jede** der beiden wirksamen Konstanten nochmals `×3` multipliziert. **K = kHin/kRueck bleibt deshalb unverändert**; die Gleichgewichtslage im geschlossenen System ist dieselbe.
- Im Konzentrationsdiagramm: violette vertikale Linien **„Kat EIN / Kat AUS“** bei tatsächlichem Schrittnummer-Eingriff. Der Eingriff ändert **keine Konzentration im Schaltmoment**, nur die nächsten Reaktionsschritte. Orange A-Zugabe und türkis D-Abfluss bleiben davon getrennt sichtbar.
- Numerische Integration mit **12 Euler-Teilschritten je angezeigtem Schritt**; in jedem inneren Teilschritt Begrenzung des Reaktionsfortschritts auf verfügbare Reaktanden, nichtnegative Stoffbestände. D-Entzug wird weiterhin erst **einmal nach dem vollständigen äußeren Reaktionsschritt** durchgeführt.
- **Wasserauskreiser: 10 %** statt 25 % des dann vorhandenen D pro äußerem Schritt. Er entfernt weiterhin keine Schlagportion, sondern kontinuierlich einen Modellanteil; die ×10-Taste bleibt eine reine Darstellungsbeschleunigung.
- Hilfetext nennt die **Synthese von Ethylacetat aus Essigsäure und Ethanol** als qualitatives Reaktionsbeispiel. Der echte Mechanismus, der Einfluss konzentrierter H₂SO₄ auf Wasser, Reaktionsenthalpien und reale Zeitmaße werden nicht simuliert. Temperatur ist **noch nicht implementiert**; diskutierter nächster Bereich v0.4g: **20–80 °C in 10-°C-Stufen**.

## Prüfungen am tatsächlichen v0.4f-Rechenkern

Das GitHub-HTML wurde erneut als Blob eingelesen. Der enthaltene originale Chemie-Rechenkern wurde für direkte dynamische Rechnungen extrahiert (nicht nur nachprogrammiert).

| Test | Ergebnis |
|---|---|
| Start mit `kHin=kRueck=0,08`: ohne Kat, bei c(A)=c(B)=1 | `vHin = 0,048` |
| Gleicher Startzustand mit Kat | `vHin = 0,144` → exakt Faktor 3 |
| `K=kHin/kRueck` trotz Schalter | unverändert: K = 1 im Testfall |
| Geschlossenes System nach 20 Schritten: C ohne Kat / mit Kat | `0,4272603` / `0,4985313` mol/L |
| Geschlossenes System nach 500 Schritten: C ohne / mit Kat | `0,5000000` / `0,5000000` mol/L |
| Geschlossene Bilanzen `A+C=1`, `B+D=1`, Nichtnegativität | bestanden, maximale Abweichung unter `1e-11` |
| D-Entzug 10 %, Kat aktiv, kHin=kRueck=0,20, 400 Schritte | C = `0,96933`; D = `0,000715`, A=B≈`0,03067` |
| Offene Bilanzen `A+C=1`, `B+C=1`, `D+gesammelt=C` | über 400 Schritte bestanden, Fehler unter `1e-10` |
| Vollständiges eingebettetes JavaScript `new Function(script)` | syntaktisch bestanden |
| HTML-ID-Referenzen und 10 eingebettete Bilder | 134 IDs eindeutig; alle direkten `$("id")`-Zugriffe auflösbar; alle 10 Bildquellen erhalten |

**Achtung zum Vergleich:** Mit `kHin=kRueck` ist K=1; in der normalen App-Startvorgabe `0,08/0,04` beträgt K=2. Die Gleichgewichtslage hängt von diesem Verhältnis ab, **nicht** vom Katalysator.

## Noch manuell im Browser prüfen

1. Beim Wechsel zum Chemie-Reiter Katalysatorschalter auf AUS, unveränderte v0.4e-Oberfläche und gemeinsame 24 A / 24 B; alte Apfelreiter weiterhin funktional.
2. Reaktion einige Schritte ohne Katalysator starten, im laufenden Versuch **EIN** schalten: vHin und vRueck sofort ×3, c(A–D) **im Augenblick des Klicks unverändert**, violette Linie im Diagramm, danach steilere Annäherung.
3. Während des Laufs **AUS** schalten: beide Raten wieder /3, Konzentrationen ohne Sprung, zweite violette Linie; dabei K vor und nach beiden Schaltungen identisch.
4. Reset: Katalysator AUS; Diagramm-Eingriffslinien verschwinden, Stoffbestände auf Startwerte. k-Regler bleiben bei den gewählten Basiskonstanten.
5. A-Zugabe bei eingeschalteter Katalyse und D-Entzug zuschalten; drei unterschiedliche Eingriffsmarker, fortlaufende Stoffbilanzen, D-Sammelmenge wächst; D-Entzug sichtbar langsamer als in v0.4e.
6. Schnelllauf ×10: Rechenfolge konsistent, keine Verdoppelung des chemischen Katalysatoreffekts.
7. Darstellung auf Projektor/Notebook und bei ca. 390 px, Offline-Doppelklick einer einzelnen HTML-Datei.

**Grenze der automatischen Prüfung:** Keine echte grafische Browser-Sichtprüfung; sie ist durch Rechen- und Syntaxprüfung nicht ersetzt.
