# EQUILIB_LAB – Übergabe v0.4e (01.11.2026)

**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB

- **Neuer Test:** [v0.4e – Oberfläche vereinfacht](../prototyp/integriert-v0.4e/index.html) · https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4e/
- **Aktueller Entwicklungsstand:** [ENTWICKLUNGSSTAND.md](ENTWICKLUNGSSTAND.md)
- **Tests:** [PRUEFPROTOKOLL_V0_4E_2026-11-01.md](PRUEFPROTOKOLL_V0_4E_2026-11-01.md)
- **Freigegebene Root-`index.html`:** weiterhin **v0.3e**. v0.4a–v0.4d und ältere Versionen unverändert.

## Geänderte bzw. neu erstellte Dateien

`prototyp/integriert-v0.4e/index.html` (neu); `docs/PRUEFPROTOKOLL_V0_4E_2026-11-01.md` (neu); `docs/UEBERGABE_v0.4e.md` (neu); `docs/ENTWICKLUNGSSTAND.md`, `README.md`, `docs/ENTWICKLUNG.md` (Dokumentation).

## Fertig in v0.4e

- Globale Apfel-Status-, Startwert- und Hilfe-Elemente **nur im Chemie-Reiter ausgeblendet**; in den drei übrigen Ansichten erhalten. `setView` schaltet `body.chem-active`.
- Historische Preset-Buttons sowie JS-Event-Handler entfernt; einheitlicher Apfel-Start M=50, A0=50, pHin=0,08, pRueck=0,04. Reset hält veränderte Parameter.
- Chemie **startet in der gemeinsamen Reaktionsraum-Ansicht** (24 A + 24 B symbolisch vor Start); Vierer-Kacheln bleiben wählbar.
- Hauptbreite im Chemie-Reiter bis 1480px, Verhältnis der Chemie-Spalten etwa 70:30, Canvas visuell größer; Stoff- und Sammelbalken höher, mobile Ansicht einspaltig.
- Zustandsmeldungen zu Eduktzugabe/Wasserentzug sichtbar; längere Erläuterungen einklappbar.
- Fehlerhafte Versionsanzeige v0.4c in Kopfzeile korrigiert.

## Was unverändert bleibt

Chemie: A+B⇌C+D; Anfang c(A)=c(B)=1, c(C)=c(D)=0 mol/L; 24 gerundete Symbole pro mol/L; Geschwindigkeitsgesetze zweiter Ordnung; A-Einmalzugabe +0,20; D-Abfluss 25 % je Rechenschritt; offene Bilanzen, K/Q, k-Kopplung zu Apfelreglern, Schnelllauf ×10; Stoffverlauf und animierte Teilchen. Apfel-/Stechheber-Rechenkern, Storybilder und ältere Prototypen bleiben unverändert. K ist bei einer aktuell veränderten Apfel-Vorgabe numerisch gekoppelt (Standard 0,08/0,04 => K=2).

## Prüfstatus / offene Probleme

Automatisch: JS-Syntax bestand; sämtliche 131 HTML-IDs eindeutig und 123 direkten JS-ID-Verweise auflösbar; 10 eingebettete Bilder erhalten; alte Preset-Verweise vollständig entfernt. Es erfolgte **noch keine echte Browser-Sichtabnahme, Projektor-, 390px- oder Offline-Doppelklick-Prüfung**. Eventuelle Layoutprobleme bitte anhand des Live-Tests sammeln.

## Nächster Entwicklungsschritt

Nach v0.4e-Abnahme möglichst v0.4f **Säurekatalysator** als getrennten fachlichen Schritt (gleicher Faktor auf Hin- und Rückrate, Gleichgewichtskonstante konstant, Stabilität bei erhöhten Raten sicherstellen); anschließend v0.4g **Temperaturabhängigkeit** unter expliziten Modellannahmen. Konzept: [KONZEPT_V0_4E_BEDIENUNG_TEMPERATUR_KATALYSATOR.md](KONZEPT_V0_4E_BEDIENUNG_TEMPERATUR_KATALYSATOR.md).

## Fortsetzungsprompt (für den nächsten Chat)

> Wir entwickeln EQUILIB_LAB im Repo `ekerzendorfer/EQUILIB_LAB` fort. Lies `docs/ENTWICKLUNGSSTAND.md`, `docs/UEBERGABE_v0.4e.md` und das v0.4e-Prüfprotokoll. Neuste Testfassung ist `prototyp/integriert-v0.4e/index.html` auf GitHub Pages; Root `index.html` bleibt v0.3e. v0.4e blendet die globalen Apfel-Steuerungen nur im Chemie-Reiter aus, entfernt alte Presets und vergrößert den gemeinsamen Chemie-Reaktionsraum mit Stoffbalken; die chemischen Rechenfunktionen aus v0.4d sind unverändert. Bitte mein Browserfeedback einarbeiten, alte Versionen erhalten und erst danach ggf. den Säurekatalysator als v0.4f umsetzen. Für die 2,6-MB-HTML GitHub `fetch_blob` statt möglicherweise leerem `fetch_file.content` verwenden. Nach Änderungen Entwicklungsstand, Prüfprotokoll und Übergabe im Repo aktualisieren.
