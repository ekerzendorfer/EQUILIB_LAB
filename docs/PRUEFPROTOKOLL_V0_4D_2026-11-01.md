# EQUILIB_LAB – Prüfprotokoll v0.4d (01.11.2026)

**Testdatei:** `prototyp/integriert-v0.4d/index.html`  
**Direktlink:** https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4d/  
**Basis:** v0.4c, unverändert archiviert; `main/index.html` weiterhin v0.3e.

## Neue Funktionen

1. **Kontinuierlicher Produktentzug D (Wasser):** Schalter „Wasser (D) auskreisen: EIN/AUS“. Nach jedem tatsächlichen Rechenschritt verlassen 25 % des gerade vorhandenen D das System. Keine schlagartige Einmalentnahme; gesammeltes D wird kumuliert angezeigt. Wasserentzug kann im laufenden/pausierten Versuch beliebig ein- oder ausgeschaltet werden. Reset löscht die Sammelmenge und die Ereignismarkierungen.
2. **Offenes System didaktisch korrekt:** Während des Auskreisens wird *kein* Zielwert eines geschlossenen Gleichgewichts behauptet. Angezeigt ist der asymptotische Grenzfall bei dauerhaftem Entzug; die Konstante K = kHin/kRueck bleibt unverändert. Q verschiebt sich durch D-Abfluss.
3. **Gemeinsamer Reaktionsraum:** Vor Start/ nach Reset bewegen sich A und B links einer gestrichelten Mitteltrennlinie, C und D (anfangs keine) rechts. Bei Start/Einzelschritt verschwindet die Trennung und die Teilchen bewegen sich durch den gemeinsamen Raum; bei Pause laufen die rein symbolischen Bewegungen weiter. Kollisionen lösen keine zusätzlichen Rechenschritte aus.
4. **Mitlaufende Stoffbalken:** Vier Balken A/B/C/D immer sichtbar, unabhängig von der Teilchenansicht. Konzentration und gerundete Symbolzahl (24 pro 1 mol/L) werden parallel angezeigt. Darunter ein fünfter, ausdrücklich *externer* Sammelbehälterbalken für entnommenes Wasser. Reaktionsratenpanel ist etwas schmaler, linke Teilchenvisualisierung breiter.
5. **Reglerkopplung:** Schieberegler pHin/pRueck der Apfelanalogie und kHin/kRueck des Chemie-Moduls synchronisieren im gemeinsamen Zahlenbereich 0,02–0,20 bidirektional. Bei Änderungen werden die entsprechenden Versuche zurückgesetzt; die Rechenkerne bleiben unabhängig. Apfelwert 0/0,01 bleibt zulässig, Chemie wird aus fachlichen Gründen auf 0,02 begrenzt. **Es handelt sich um eine numerische Reglerkopplung, keine physikalische Gleichsetzung der Parameter.** Die Apfel-Startmengen 50/0 und Chemie-Startkonzentrationen 1/1/0/0 bleiben getrennt.
6. **Schnelllauf ×10:** Umschaltbar im Chemie-Toolbar (auch während des Laufens), damit die Annäherung an nahezu vollständige Umsetzung im Workshop praktikabel ist.
7. **A-Zugabe aus v0.4c:** Einmalzugabe +0,20 mol/L, Q-Reaktion und vertikale Sprungmarkierung unverändert; gleichzeitiger D-Entzug wird bilanziert.

## Mathematisches Modell

Formale Reaktion A + B ⇌ C + D (D als Wasser).

```text
vHin = kHin · A · B               (0,02 <= kHin <= 0,20)
vRueck = kRueck · C · D           (0,02 <= kRueck <= 0,20)
delta = clamp(vHin-vRueck, -min(C,D), min(A,B))       (dt=1)
A' = A-delta; B' = B-delta; C' = C+delta
D_vor_Entzug = D+delta
wenn Auskreiser EIN: WasserAbfluss = 0,25 · D_vor_Entzug
sonst: WasserAbfluss = 0
D' = D_vor_Entzug-WasserAbfluss
gesammelt' = gesammelt + WasserAbfluss
```

Für das gewählte Startsystem sind zu jedem Zeitpunkt, einschließlich A-Zugabe und D-Abfluss, invariant:
- **A + C** (ändert sich nur bei einer A-Zugabe).
- **B + C**.
- **D + gesammelt = C** (anfänglich C=D=gesammelt=0).

Bei unbeschränktem D-Entzug nähert sich C dem kleineren der Werte A+C und B+C. Werden zu Beginn je 1 mol/L A und B eingesetzt, gilt im Grenzfall A→0, B→0, C→1, D→0. Bei nachträglich +0,20 mol/L A ist A im Grenzfall 0,20 und C 1,00, da B limitierend ist.

**Modellgrenze:** Idealisierter offener Stoffstrom, konstanter rechnerischer Reaktionsraum; kein physikalisch genauer Wasserabscheider, kein realer Esterbildungsmechanismus und keine raumaufgelöste chemische Kollisionstheorie. 25 % ist ein vorgegebener didaktischer Entnahmeanteil.

## Automatisch geprüfte Fälle

| Fall | Konfiguration | Ergebnis nach vielen Schritten |
|---|---|---|
| Geschlossen, K=1 | 0,08/0,08, 600 Schritte | A=B=C=D = 0,500000 |
| Geschlossen, K=0,1 | 0,02/0,20, 600 Schritte | A=B=0,759747; C=D=0,240253 |
| Geschlossen, K=10 | 0,20/0,02, 600 Schritte | A=B=0,240253; C=D=0,759747 |
| Kontinuierlicher D-Abfluss | 0,08/0,08, ab Anfang 300 Schritte | A=B=0,047841; C=0,952159; D=0,000456; gesammelt=0,951703 |
| A-Zugabe + D-Abfluss | A=1,20, B=1,0, 700 Schritte | A=0,200019; B=0,000019; C=0,999981; D=0,00000078; gesammelt=0,999980 |
| Entzug aktiv bis Schritt 150, danach aus | 0,08/0,08, 650 Schritte | A=B=0,083868; C=0,916132; D=0,007678; gesammelt=0,908454; Hin- und Rückrate wieder gleich |

**Geprüft:** JavaScript-Syntaxkompilierung der kompletten Single-HTML-Datei, 132 eindeutige DOM-IDs (vor Schnelllauf-Ergänzung; Schnelllauf-ID zusätzlich), 10 eingebettete Bildquellen, kein externer Bibliotheksbedarf, Nichtnegativität aller berechneten Stoffbestände und Bilanzfehler maximal ca. 2×10⁻¹⁵ in den gerechneten Szenarien. Die Grafik-/Bedienlogik wurde statisch kontrolliert.

**Noch offen:** echter grafischer Browserklicktest, Laufzeit-/Layoutprüfung auf Notebook/Beamer/Mobilgerät, Doppelklick im Offlinebetrieb und manuelle Prüfung aller Ein-/Ausschaltkombinationen.

## Empfohlener manueller Abnahmerundgang

1. Testversion öffnen, Reiter „Chemisches Gleichgewicht“ und „Gemeinsamer Reaktionsraum“ wählen. Bei **Schritt 0** liegen die 24 A- und 24 B-Symbole links; rechts noch kein D/C; die Mitteltrennlinie ist sichtbar. Nach Reset wieder so. Mit Start bzw. Einzelschritt wird die Trennlinie aufgehoben. Auch bei Pause sollen Partikel weiterlaufen.
2. Für einen K=1-Versuch **kRueck von 0,04 auf 0,08** stellen (beide Regler 0,08). Aufgrund der neuen Kopplung startet die Chemieansicht nach dem Apfel-Storypreset zunächst **bei 0,08/0,04, K=2**; das ist eine beabsichtigte Änderung gegenüber v0.4c. Danach Apfelreiter kontrollieren: pRueck steht ebenfalls auf 0,08.
3. Reset; Wasserentzug vor Start einschalten und Schnelllauf ×10 aktivieren. Schritt 100 ungefähr A=B 0,1275 / C 0,8725 / D 0,0034; Schritt 300 ungefähr A=B 0,0478 / C 0,9522 / D 0,0005. Sammelbehälterbalken füllt sich; Reaktionsraum zeigt wenige A/B und sehr wenige D.
4. Wasserentzug ausschalten, laufen lassen: Die restliche Reaktionsmischung nähert sich *ihrem neuen* Gleichgewicht, das gesammelte Wasser bleibt extern.
5. Reset: kein gesammeltes D, keine Auskreiser-Markierungen, Wasserentzug AUS, Partikel getrennt. A-Zugabe bei laufendem Auskreiser und während Pause ausprobieren; Bilanz A+C=1,2, B+C=1, D+gesammelt=C.
6. Reglerwechsel in beiden Richtungen testen. Historische Apfelphasen und alten Stechheber/Story-Modus gezielt kontrollieren; 0 und 0,01 bleiben in der Apfelansicht möglich.
7. HTML per lokaler Datei öffnen, ohne Netzverbindung benutzen, und bei schmaler Breite sowie Projektor testen.

Keine Freigabe der Root-HTML vor Nutzerabnahme.
