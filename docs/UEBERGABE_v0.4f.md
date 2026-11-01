# EQUILIB_LAB – Übergabe v0.4f (01.11.2026)

**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB · **Test:** https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4f/

**Status:** v0.4e wurde vom Nutzer am 1.11.2026 im Browser erfolgreich abgenommen (klarere Oberfläche). v0.4f ist implementiert und automatisiert geprüft, **Browser-/Offline-Abnahme v0.4f noch offen**. Root-`index.html` steht weiterhin auf v0.3e; die älteren Prototypen wurden nicht verändert.

## Neu in v0.4f

- Schaltbarer **Säurekatalysator (H₂SO₄ als Modell)** mit Faktor 3 auf **beide** effektiven Raten; Quotient K und geschlossene Gleichgewichtslage unverändert. Schalter funktioniert während der laufenden Reaktion, keine sprunghafte Konzentrationsänderung.
- Eigener chemischer Basiszeitfaktor `0,6` gegenüber den bisherigen chemischen k-Werten; Apfelregler und deren Werte bleiben unverändert gekoppelt. `k_eff = k_basis × 0,6 × (Kat?3:1)`.
- Wasserauskreiser `0,10` statt `0,25` des verfügbaren D **nach** jedem angezeigten Schritt.
- Numerische Stabilisierung: 12 innere Teilreaktionsschritte pro äußerem Simulationsschritt; D-Entzug einmal pro äußerem Schritt.
- Violette Katalysator-Ereignislinien und „Kat EIN/AUS“-Texte im Konzentrationsgraphen; bestehende A-/D-Markierungen erhalten; sichtbare effektive k-Konstanten.
- Fachliche Einordnung: qualitative Anlehnung an **Essigsäure + Ethanol ⇌ Ethylacetat + Wasser**, keine realen Messwerte, keine realen Reaktionsmechanismen.

## Prüfung

[Prüfprotokoll v0.4f](PRUEFPROTOKOLL_V0_4F_2026-11-01.md): echtes HTML-JS syntaktisch geprüft, IDs, 10 Bilder, dynamische Modelltests (3×, K-Erhaltung, 20/500 Schritte, geschlossene/offene Bilanzen) bestanden.

## Nächster Schritt

Zuerst v0.4f im Browser testen und eventuelles Nutzerfeedback korrigieren. Danach separater Schritt **v0.4g Temperatur (20–80 °C in 10-°C-Schritten)**. Referenztemperatur und K(T)-Modell **noch nicht entschieden**. Wichtig: Temperatur muss die Geschwindigkeiten und das thermodynamische K(T) verändern; bei einer konkreten Ethylacetat-Esterbildung Vorzeichen und Größe der Reaktionsenthalpie nicht ohne Quellen erfinden. Vor der Implementierung ein konsistentes, ausdrücklich illustratives T-Modell fachlich festlegen.

**Fortsetzungsprompt:** Öffne v0.4f und dieses Prüfprotokoll. Berücksichtige das Browserfeedback. Entwickle die Temperaturabhängigkeit erst nach separater Modellentscheidung und in neuer Versionsmappe `prototyp/integriert-v0.4g/`; ältere Dateien und Root nicht ändern. Den 2,6-MB-Quelltext nötigenfalls über `fetch_blob` statt `fetch_file` abrufen und nach dem Commit erneut prüfen.
