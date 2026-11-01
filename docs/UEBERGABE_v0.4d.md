# EQUILIB_LAB – Übergabe v0.4d (01.11.2026)

**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB  
**Aktueller Test:** [prototyp/integriert-v0.4d/index.html](../prototyp/integriert-v0.4d/index.html) · https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4d/  
**Live-Dokumentation:** [ENTWICKLUNGSSTAND.md](ENTWICKLUNGSSTAND.md)  
**Tests:** [PRUEFPROTOKOLL_V0_4D_2026-11-01.md](PRUEFPROTOKOLL_V0_4D_2026-11-01.md)

**Geänderte/neu erstellte Dateien:** `prototyp/integriert-v0.4d/index.html`; `docs/ENTWICKLUNGSSTAND.md`; `docs/PRUEFPROTOKOLL_V0_4D_2026-11-01.md`; `docs/UEBERGABE_v0.4d.md`; `README.md`. Keine Änderung an `index.html` (v0.3e), v0.4a–v0.4c bleiben Archiv.

**Was fertig ist:** kontinuierlicher D-(Wasser-)Abfluss von 25 % des vorliegenden D pro Schritt mit EIN/AUS, externalisiertem Sammelbehälter und korrekten offenen Bilanzen; C-Produktion nimmt stark zu; vier Live-Konzentrations-/Teilchenbalken; rechter Bereich schmaler; gemeinsamer Reaktionsraum stellt A+B vor Start links der temporären Trennlinie dar und öffnet sich bei Start; Reset stellt Vorstart wieder her; rein symbolische Partikelbewegung bei Pause weiter aktiv; bidirektionale numerische Kopplung von Apfel-Transportreglern zu kHin/kRueck (gemeinsamer Bereich 0,02–0,20, chemische K-Begrenzung) und Schnelllauf ×10. Bestehende A-Einmalzugabe weiter verfügbar.

**Fachliche Caveats:** Bei D-Auskreisen *offenes System*, nicht geschlossenes GG; K bleibt konstant, Q reagiert. Nur Reglerwerte gekoppelt, Rechenmodelle bleiben unterschiedlich. Apfelwerte 0/0,01 werden für Chemie auf Mindestwert 0,02 abgebildet; Apfelanfang 50/0 ist unabhängig von Chemieanfang 1/1/0/0. Daher startet Chemie nach Storypreset jetzt mit 0,08/0,04 (K=2) statt zuvor K1. In Chemie kRueck auf 0,08 setzen, um K1 zu prüfen. Nach A-Zugabe plus dauerhaftem D-Entzug bleiben ca. 0,20 mol/L A wegen B-Limitierung übrig.

**Automatisch geprüft:** JavaScript parsebar; 10 Bild-Datenquellen; eindeutige HTML-IDs; Gleichgewichte K1/K0,1/K10 ohne D-Entzug; 300 Schritte K1 mit Auskreiser => A/B 0,04784, C 0,95216, D 0,000456; kombinierte A-Zugabe+D-Entzug; Auskreiser stoppen => neues GG; Erhaltung innerhalb 1e-8. Originale Apfel-/Stechheber-Routinen nicht geändert.

**Offen:** Browserklick- und Sichtabnahme; Prüfung offline / Projektor und schmaler Bildschirm; bei Bedarf v0.4e. Root erst nach Freigabe.

**Technischer Hinweis:** GitHub `fetch_file.content` kann bei der 2,6-MB-HTML leer sein; für Source `fetch_blob` mit aktuellem SHA verwenden.

## Direkt verwendbarer Übergabeprompt

> Setze EQUILIB_LAB auf Basis von `docs/ENTWICKLUNGSSTAND.md`, `docs/PRUEFPROTOKOLL_V0_4D_2026-11-01.md` und `prototyp/integriert-v0.4d/index.html` nahtlos fort. Bitte zuerst mein Feedback zur Browserabnahme von v0.4d einarbeiten. Derzeitiges Feature: offener D-Wasserentzug 25 %/Schritt, externer Sammelbehälter, Live-A/B/C/D-Balken, getrennte Teilchen vor Start, synchronisierte Ratenregler, Schnelllauf, A-Zugabe. Bewährte Story und alte Versionen unverändert, Root noch v0.3e. Source des großen GitHub-Blobs über `fetch_blob` lesen. Nach jeder Änderung Entwicklungsstand und Übergabe dokumentieren.
