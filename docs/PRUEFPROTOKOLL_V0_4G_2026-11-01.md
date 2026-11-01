# EQUILIB_LAB – Prüfprotokoll v0.4g (01.11.2026)

**Testversion:** [v0.4g](../prototyp/integriert-v0.4g/index.html) · [GitHub Pages](https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4g/) · **Basis:** vom Nutzer im Browser freigegebene v0.4f. Root-index weiterhin v0.3e.

## Neuerungen

- Temperaturregler 20–80 °C in Schritten zu 10 °C; Referenztemperatur 60 °C entspricht exakt dem bisherigen Zeitmaß von v0.4f.
- Arrhenius-Temperaturfaktoren für Hin- und Rückreaktion: Eₐ,hin = **60 kJ/mol (ausdrückliche Modellannahme)**, Eₐ,rück = **63,6 kJ/mol**; damit Eₐ,hin − Eₐ,rück = ΔᵣH = −3,6 kJ/mol. ΔᵣH stützt sich auf kalorimetrische Literatur zu diesem Stoffsystem, ist hier als temperaturunabhängig angenähert.
- K(T) aus dem Quotienten der effektiven Konstanten; mathematisch konsistent mit van ’t Hoff. Erhöhung von T beschleunigt beide Richtungen und senkt K leicht (exothermer Fall).
- Temperatur darf während des Laufs geändert werden, **ohne Konzentrationssprung**; die Änderung wirkt ab dem nächsten Zeitschritt; rosa Ereignislinien im großen und Mini-Graphen.
- Mini-Graph direkt unter Raten/Gleichgewicht im rechten Bereich; er übernimmt dieselben SVG-Kurven und Ereignislinien aus dem großen Diagramm (ohne winzige Textlabels). Das große Diagramm bleibt bestehen.
- Katalysator ×3 auf beide Geschwindigkeiten unverändert; Temperatur und Katalysator sind unabhängig. Apfelmodell, 24 Symbole/mol/L, A-Zugabe und Wasserauskreiser (10 %) bleiben erhalten.
- Reset löscht Eingriffsmarkierungen und setzt Stoffbestände zurück, **behält die gewählte Temperatur** wie die k-Basiswerte bei.

## Automatische Prüfungen am ursprünglichen Modellcode

- Vollständiges eingebettetes JS: erfolgreich mit new Function kompiliert.
- IDs: 139 eindeutig, direkte $()-Zugriffe alle vorhanden; 10 eingebettete Bilddateien unverändert.
- Getestete Kombinationen: 56 geschlossene Rechnungen = 7 Temperaturen × 2 Katalysatorzustände × 4 Basis-k-Paare, je 600 Simulationsschritte.
- Größte Bilanzabweichung einschließlich offenem Wasserabfluss: 1.021e-14, Stoffkonzentrationen nichtnegativ.
- 60 °C ohne Kat k_eff,hin = 0.048, k_eff,rück = 0.024 (Basis 0,08/0,04); K = 2.000.
- Hinreaktions-Geschwindigkeitsfaktoren relativ zu 60 °C: 20 °C 0.052, 80 °C 3.410.
- K(T)/K(60 °C): 20 °C 1.194, 80 °C 0.929.
- Kat ×3 auf beide k-Werte bei 20/60/80 °C, K jeweils unverändert.
- Bei Wasserabfluss im besonders schnellen Grenzfall 80 °C/Kat EIN und Basis 0,20/0,20 bestanden die offenen Stoffbilanzen ebenfalls.

**Grenzen:** Keine echte Browser-/Offline-Sichtprüfung durch die automatische Testausführung. Keine empirische Kalibrierung der absoluten Reaktionszeiten, keine reale Phasengleichgewichtsrechnung. Bei 80 °C ist Ethanolsiedeverhalten im offenen Laborversuch relevant, wird im isothermen Modell aber nicht berücksichtigt.

## Fachquellen

- Golikova et al., 2020, *Journal of Thermal Analysis and Calorimetry*, kalorimetrisch ΔᵣH = −3,6 ± 0,2 kJ/mol: https://doi.org/10.1007/s10973-019-08488-y
- Atalay, 1994, temperaturabhängige Veresterungskinetik: https://doi.org/10.1002/apj.5500020210
- OpenStax Organic Chemistry, Fischer-Veresterung (fachlicher Mechanismus, nicht eins zu eins simuliert): https://openstax.org/books/organic-chemistry/pages/21-3-reactions-of-carboxylic-acids

## Browserabnahme (noch offen)

Temperaturslider 20, 60, 80 °C ohne Kat beobachten; v0.4f bei 60 °C vergleichen; während des Laufs 60→80→20 °C ändern, K/effektive k-Werte und rosa Marker prüfen, ohne Konzentrationssprung; Kat EIN/AUS bei unterschiedlichen T prüfen; A-Zugabe + D-Auskreisen + ×10; Mini- und Hauptdiagramm synchron; 390-px-Ansicht und Offline-Doppelklick.
