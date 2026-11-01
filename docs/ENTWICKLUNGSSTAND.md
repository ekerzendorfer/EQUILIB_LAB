# EQUILIB_LAB – aktueller Entwicklungsstand und Übergabe

**Stand:** 01.11.2026 · **Projekt:** CHEMIE mit KI – GLEICHGEWICHTS-LAB  
**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB  
**Aktuelle Testversion:** **V0.5** unter `prototyp/integriert-v0.5/index.html`  
**Live-Testpfad (öffentlich zugänglich, nicht im Portal beworben):** https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.5/  
**Freigegebene Root-Startfassung:** `main/index.html` weiterhin v0.3e.

## Versionsübersicht

| Version | Datei | Stand |
|---|---|---|
| v0.3e | `index.html` und `prototyp/integriert-v0.3e/index.html` | Bewährte Apfel-/Stechheberfassung, unverändert |
| v0.4a | `prototyp/integriert-v0.4a/index.html` | Erstes Chemie-Modell A+B⇌C+D |
| v0.4b | `prototyp/integriert-v0.4b/index.html` | Variable k-Werte, K/Q, gemeinsamer Reaktionsraum |
| v0.4c | `prototyp/integriert-v0.4c/index.html` | Einmalzugabe A +0,20 mol/L und Q/K-/Zielwertneuberechnung; vom Nutzer als gut funktionierend bestätigt |
| v0.4d | `prototyp/integriert-v0.4d/index.html` | Laufender D-(Wasser-)Entzug, Sammelgefäß, Live-Balken, getrennte Startteilchen, Reglerkopplung und Schnelllauf ×10; mathematisch geprüft |
| **v0.4e** | `prototyp/integriert-v0.4e/index.html` | **Neu:** Apfelsteuerung im Chemie-Reiter ausgeblendet, historische Presets entfernt, Reaktionsraum standardmäßig geöffnet und vergrößert, Stoffbalken höher, Hilfetexte kompakter; JS/HTML-Quelltextprüfung bestanden, Browserabnahme vom Nutzer erfolgreich bestätigt |
| **v0.4f** | `prototyp/integriert-v0.4f/index.html` | Katalysator EIN/AUS (3× beide Raten, K gleich), Basisfaktor 0,6, D-Auskreiser 10 %, 12 interne Teilschritte und violette Eingriffsmarken; numerisch geprüft, danach vom Nutzer im Browser bestätigt |
| **v0.4g** | `prototyp/integriert-v0.4g/index.html` | 20–80 °C, Arrhenius und K(T), synchronisierter Mini-Konzentrationsverlauf; am 01.11.2026 im Browser erfolgreich geprüft |
| **V0.5** | `prototyp/integriert-v0.5/index.html` | Feinschliff Kopf/Version/Canvas-Titel, ratengekoppelte orange/rote Ringereignisse, Pause stoppt Animation; numerisch/syntaktisch geprüft, Browser-/Offlineabnahme offen |

**Aktuelles Prüfprotokoll:** [V0.5](PRUEFPROTOKOLL_V0_5_2026-11-01.md). **Dokumentation:** [Abschlussstand V0.5](DOKUMENTATION_V0_5.md). Die Browserabnahme von v0.4g ist erfolgt; die von V0.5 noch offen. Die folgenden Abschnitte zu v0.4d sind historisch und beschreiben den vorigen 25%-Auskreiser, nicht v0.4f. Rechenkern-Referenzen: [v0.4d-Prüfprotokoll](PRUEFPROTOKOLL_V0_4D_2026-11-01.md).

## Leitplanken

- Niederschwelliges Einzel-HTML, ohne Netz, ohne externe Bibliotheken, mit **zehn eingebetteten Bildern** für den Workshop Februar 2027.
- Drei ursprüngliche Perspektiven **Geschichte, Modell, Vergleich** einschließlich synchronisierter Apfelphasen und Stechheber-Rechenkern nicht umbauen.
- Chemie bleibt ein **eigenständiger Rechenkern** und eigene Reaktionsansicht; formal A+B⇌C+D, D=Wasser.
- Versionierte Prototypverzeichnisse beibehalten; Root nur nach expliziter Freigabe anheben.
- Nach jedem Entwicklungsschritt diesen Stand und die Übergabe im Repository aktualisieren.

## v0.4d – unveränderter Funktionsumfang und Regeln

**1. Wasserauskreiser:** Button schaltet kontinuierliche Entfernung von D ein/aus. Pro tatsächlichem Rechenschritt wird nach der Reaktion `0,25 × D_vor_Entzug` abgeführt; ausgekreiste Menge wird gesammelt. Es wird **keine größere Portion D schlagartig entnommen**. Wasserentzug ist bei laufendem Modell zuschaltbar, ebenso abschaltbar. Konstante **K=kHin/kRueck bleibt gleich**; Q sinkt mit entzogenem D. Während des Entzugs offen, **keine behauptete stationäre Gleichgewichtslage**. Bei fortgesetztem Entzug geht C im Startfall gegen 1, A/B/D gegen 0.

**2. Bilanzen:** Ohne A-Zugabe `A+C=1`, `B+C=1`, `D+gesammelt=C`. Bei +0,20 A: `A+C=1,2`, `B+C=1` und bei dauerndem D-Entzug C→1, A→0,2 (B limitierend). Gesammeltes Wasser wird als eigener externer Balken gezeigt.

**3. Teilchenansicht:** Gemeinsamer Reaktionsraum (720×320 Canvas): bei Schritt 0 und Pause vor Start bewegen sich Edukte A+B links, Produkte C+D rechts einer gestrichelten Mitteltrennlinie. Start/Einzelschritt gibt den gesamten Raum frei. Reset stellt Trennung wieder her; nach jedem realen Schritt wird die Verteilung an die gerechneten Stoffbestände angepasst. Zusammenstöße bleiben symbolisch und laufen auch während Pause weiter.

**4. Mengenbalken:** Linker Reaktionsraum erhält mehr Platz; stets sichtbare vier Live-Stoffbalken für A/B/C/D (Konzentration + gerundete Symbolteilchen); darunter zusätzlich **Wasser im Sammelbehälter**, das ausdrücklich außerhalb der Reaktionsmischung liegt. Rechte Raten-/GG-Spalte verkleinert; mobile Darstellung einspaltig.

**5. Kopplung der Bedienelemente:** Apfel-Transportregler pHin/pRueck und Chemie-kHin/kRueck spiegeln die **numerischen** Reglerwerte beidseitig. Chemie begrenzt sich auf 0,02–0,20 (K 0,1–10). Beim Apfel dürfen 0 und 0,01 weiter eingestellt werden; in der Chemie wird 0,02 verwendet. Nur die **Raten** werden gekoppelt, nicht die Startbestände (Apfel 50/0, Chemie 1/1/0/0), und **nicht die mathematischen Gesetze** (Apfel lineare Transferanteile, Chemie bimolekulare Raten). Änderungen bei Pause setzen beide Versuche auf Schritt 0. Anfangs nun Apfel-Storypreset 0,08/0,04 => Chemie K=2; für K=1 beide auf 0,08 einstellen.

**6. Präsentation:** Schalter **Schnelllauf ×10** beschleunigt ausschließlich die zeitliche Abfolge der Rechenschritte, nicht das physikalische Rechenmodell; während Lauf umschaltbar. Das ist bei 300 Schritten eine Darstellungszeitverkürzung von ca. 285 auf 28,5 Sekunden (ohne Render-Overhead).

**7. v0.4c weiterhin:** Einmalige A-Zugabe +0,20 mol/L mit Q-/K-Erklärung, Markierung als senkrechter Sprung, Neuberechnung des geschlossenen GG (wenn D-Entzug ausgeschaltet) und Reset.

## Fachlicher Kurzstand und Prüfung

```text
vHin = kHin*A*B, vRueck = kRueck*C*D
delta = (vHin-vRueck) * dt, dt=1, auf verfügbare Bestände begrenzt
A', B' = A-delta, B-delta; C'=C+delta
D_vor = D+delta; ausgetragen = Auskreiser? 0,25*D_vor : 0
D'=D_vor-ausgetragen; gesammelt'=gesammelt+ausgetragen
Kc = kHin/kRueck
```

Rechen- und Quellcodeprüfungen:
- Ohne Auskreiser unveränderte geschlossene GG-Zielwerte: K1 = 0,5/0,5/0,5/0,5; K0,1: C=D=0,240253; K10: C=D=0,759747.
- Auskreiser bei K1, 300 Schritte: **A=B=0,047841; C=0,952159; D=0,000456; gesammelt=0,951703**.
- Auskreiser + A-Zugabe +0,20: Nach 700 Schritten nahezu **A=0,200019; B=0,000019; C=0,999981**, richtige Stoffgrenze.
- Auskreiser abschalten: geschlossenes GG aus Restgemisch erreicht; entfernte Menge bleibt draußen.
- Bilanzabweichungen in geprüften Fällen kleiner als 1e-8; keine negativen Stoffbestände. Komplette JavaScript-Syntax erfolgreich geprüft; zehn integrierte `data:image/`-Bildquellen erhalten; HTML-IDs eindeutig.

**Wichtig:** Dies sind automatisierte Rechenkern- und Quellcodeprüfungen, **keine** echte visuelle Browser-, Klick-, Mobil- oder Offline-Abnahme. Die neue Testversion muss im Browser ausprobiert werden. Details und Testgang im Prüfprotokoll.

## Bekannte Grenzen / nächste Schritte

- Kontinuierlicher Entzug ist ein idealisiertes Modell mit vorgegebener Entnahmerate 25 %, kein realer Wasserabscheider (z.B. Dean-Stark) und kein genauer Estermechanismus.
- Bei Koppelung der Apfel- und Chemie-Regler werden nur Reglerzahlen gleichgesetzt, nicht Ratenkonstanten physikalisch identifiziert; fachlich in Unterrichtsbegleitung klarstellen.
- **Nächste Aufgabe:** v0.4e im Browser prüfen: Reiterwechsel mit Apfelsteuerung, entfernte Presets, gemeinsamer Chemie-Reaktionsraum als Startbild, vergrößertes Canvas und Live-Balken, Wasser EIN/AUS, Schnelllauf, A-Zugabe, K/Q, Reset und Altmodule. Doppelklick offline prüfen. **main/index.html bleibt unverändert**.

## GitHub-Technik-Hinweis

HTML ist ca. 2,6 MB groß. `mcp__GitHub__fetch_file` kann für solche großen Dateien **leeren Inhalt bei korrektem SHA** liefern. Blob-SHA aus `fetch_file.sha` holen und `mcp__GitHub__fetch_blob({repository_full_name:"ekerzendorfer/EQUILIB_LAB",blob_sha:...})` nutzen. Auf keinen Fall leeres `fetch_file.content` als Datei interpretieren oder hochladen. Versionierung beibehalten.

## Fortsetzungsprompt (direkt in neuen Chat kopieren)

> Wir arbeiten am GitHub-Repo `ekerzendorfer/EQUILIB_LAB`. Lies `docs/ENTWICKLUNGSSTAND.md` und `docs/PRUEFPROTOKOLL_V0_4D_2026-11-01.md`. Aktuelle Testfassung v0.4d unter `prototyp/integriert-v0.4d/index.html`; frühere v0.4c gut, root `index.html` noch freigegebene v0.3e. Chemie A+B⇌C+D, D=H₂O, mit kontinuierlichem Wasserabfluss 25% pro Rechenschritt, externem Sammelbehälter, K/Q, vier mitlaufenden Stoffbalken, getrenntem Vorstart im Reaktionsraum, gekoppelt eingestellten Apfel-/Chemie-Ratenreglern, A-Zugabe +0,20 und Schnelllauf ×10. Automatische mathematische Tests bestanden; Browser- und Offline-Abnahme fehlt. Unbedingt große GitHub-HTML via `fetch_blob` laden. Bitte an aktuellem Feedback orientiert gezielt weiterentwickeln, alte Versionen und Apfelmodell erhalten und nach jedem Entwicklungsschritt die Markdown-Übergabe aktualisieren.

## Feedback und Entwurf für Folgeschritte (01.11.2026)

Nach Nutzerfeedback zur bewährten v0.4d wurde der Quelltext geprüft: `Gesamtbestand A+B` und `Anfangsmenge A` wirken nur auf die ursprüngliche Apfel-/Stechheberrechnung; im Chemie-Reiter wird diese globale Bedienfläche unnötig angezeigt. Auch die historischen Buttons „Apfelkrieg-Vorgabe“ und „V0.2-Werte“ sollen aus der sichtbaren Oberfläche verschwinden. Der chemische Rechenkern bleibt mit den festen Anfangskonzentrationen A=B=1,000 mol/L und den 24 Symbolen pro mol/L unverändert.

**UI-Stufe v0.4e ist umgesetzt, aber noch nicht im Browser freigegeben.** [KONZEPT_V0_4E_BEDIENUNG_TEMPERATUR_KATALYSATOR.md](KONZEPT_V0_4E_BEDIENUNG_TEMPERATUR_KATALYSATOR.md). Vorgeschlagene Reihenfolge: v0.4e UI-Vereinfachung und vereinheitlichte Startwerte, v0.4f optionaler Säurekatalysator (beschleunigt **beide** Teilreaktionen ohne K-Verschiebung), v0.4g Temperatur (Arrhenius + van ’t Hoff; 20–60 °C als noch unverbindlicher Modellbereich, illustrative ΔrH° ausdrücklich deklarieren). Für erhöhte effektive k-Werte interne Substeps prüfen. Die Zahl der berechneten Teilchen bleibt symbolisch; die beiden Rechenkerne werden nicht zusammengelegt. **Root v0.3e und v0.4d sind unverändert; neu ist der separate v0.4e-Prototyp.**


## v0.4e – Oberfläche vereinfacht und Chemieansicht vergrößert (01.11.2026)

- **Gezielt nur in Chemie ausgeblendet:** Apfel-/Stechheber-`.status-panel`, `.controls` und originales `details.info` über die `chem-active`-Klasse am `body`; beim Wechsel zurück bleiben alle Apfel-Steuerungen sichtbar.
- **Entfernt:** zwei historische Preset-Buttons mit zugehörigen Handlern und das nicht mehr erreichbare `DEFAULTS`-Objekt. Einheitliche Apfel-Startvorgabe `STORY_PRESET` (M=50, A0=50, pHin=0,08, pRueck=0,04). **Reset hält die jeweils eingestellten Parameter**, setzt nur den Zustand auf Schritt 0.
- **Chemie standardmäßig als gemeinsamer Reaktionsraum**, weiterhin wahlweise die vier getrennten Partikelbestände. Chemie-Hauptbereich bis 1480 px, Spaltenverhältnis 1,75:0,75; Canvas nutzt die linke Spaltenbreite. Stoffbalken, Wassersammelbalken größer, responsive Anpassungen für kleinere Bildschirme.
- **Dynamische Rückmeldungen** zu A-Zugabe und Wasserabfluss sichtbar; detaillierte Modellhinweise und die Kollisions-Erklärung ausklappbar.
- **Keine Formel-Änderung** gegenüber v0.4d. Automatisch geprüft: 10 eingebettete Bilder, 131 eindeutige IDs, 123 JS-`$(id)`-Referenzen gültig, JS-Syntax bestanden. **Sicht-, Browserklick- und Offline-Abnahme offen**.
- [Live-Test v0.4e](https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4e/) · [Prüfprotokoll](PRUEFPROTOKOLL_V0_4E_2026-11-01.md) · [Übergabe](UEBERGABE_v0.4e.md) · [Änderungs-Prompt](PROMPTS/INTEGRIERT_V0_4E.md).

**Fachlich folgende Schritte:** Nach Sichtfreigabe v0.4f Katalysator (beschleunigt beide Reaktionen, K unverändert); danach v0.4g Temperatureffekt (eigene thermodynamische Modellannahmen und numerisch stabile Zeitintegration). **Root bleibt v0.3e bis zur ausdrücklichen Freigabe.**

## v0.4f – Säurekatalysator und langsamere Wasserentnahme (01.11.2026)

**Status:** [v0.4f als separate HTML-Testfassung](https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4f/), automatisierte Modell- und Syntaxprüfung bestanden; Browser-/Offlineabnahme durch den Nutzer noch offen. **v0.4e war vom Nutzer erfolgreich im Browser geprüft.**

- Chemie-Basiszeitfaktor 0,6 (nur im Chemie-Rechenkern) und Schalter für dreifache Beschleunigung **beider** effektiver k-Werte. Die miteinander gekoppelten Apfel-/Chemie-Basisregler bleiben erhalten; Apfel-Rechenkern nicht verändert. Der Quotient K und die geschlossene Gleichgewichtslage ändern sich durch den Katalysator nicht.
- Im Diagramm violette Linien für Kat EIN/AUS; im Schaltmoment bleiben Konzentrationen gleich. Die k-eff-Werte und der Katalysatorzustand werden angezeigt.
- Wasserentzug auf 10 % des D-Bestands je äußerem Schritt verringert (vorher 25 %). Zwischen zwei äußeren Schritten 12 interne Euler-Teilschritte für stabilere Reaktionskinetik bei Katalyse; offene Bilanzen bleiben erhalten.
- Modell qualitativ an die Ethylacetat-Synthese angelehnt, nicht an real gemessene k-Werte. Änderungen von `K(T)` sind ausdrücklich **nicht** Teil dieser Version.
- [Aktuelles Prüfprotokoll](PRUEFPROTOKOLL_V0_4F_2026-11-01.md) · [Übergabe](UEBERGABE_v0.4f.md). Die historischen v0.4d/v0.4e-Zahlenbeispiele gelten nur für die damaligen Rechenparameter.

**Folgestufe v0.4g:** 20–80 °C im 10-°C-Raster als Nutzerwunsch. Konstante k-Referenz und ΔrH° noch entscheiden und fachlich begründen; Arrhenius/van ’t Hoff konsistent umsetzen, kein unveränderter K-Wert für Temperaturänderungen behaupten. Root bis zur Freigabe v0.3e.


## 01.11.2026 – v0.4g Temperaturmodell / Mini-Verlauf

Ausgehend von der vom Nutzer im Browser freigegebenen v0.4f wurde v0.4g als separate Offline-HTML-Version mit isothermer Temperatureinstellung (20–80 °C, 10-°C-Schritte) entwickelt. Mit Referenz 60 °C und temperaturabhängigen Arrhenius-Konstanten (Ea,hin=60 kJ/mol, Ea,rück=63,6 kJ/mol) ist die geringe exotherme Gleichgewichtsverschiebung (ΔrH≈−3,6 kJ/mol) konsistent integriert. Die Temperatur ist während des Laufs schaltbar; rosa Diagrammmarker und sofortige k-/K-Anzeige bei unveränderten Momentankonzentrationen. Ein platzsparendes SVG-Mini-Diagramm wird aus denselben Kurven wie das große Diagramm abgeleitet. Regression über 56 Kombinationen sowie offenen Wasserentzug: Bilanz, Positivität, Temperatureffekt und Katalysatorinvarianz bestanden. Browserabnahme noch offen.


## 01.11.2026 – V0.5 Abschluss der Funktionsentwicklung

Der Nutzer hat v0.4g im Browser bestätigt. V0.5 als eigener Ordner, keine Änderung an Root/älteren Testständen: Kopfuntertitel und Version, Canvas-Textausrichtung, ratengekoppelte farblich unterschiedene Hin-/Rückreaktionsringe, eingefrorenes Pausenbild. Fachlich sind es symbolische Brutto-Ereignisse, keine echte Molekulardynamik. Zwei getrennte didaktische Materialien (MC und Lösungen), Abschlussdokumentation und 180-Minuten-Workshopkonzept liegen vor. Die vollständige Browser-/Offlineabnahme von V0.5 steht noch aus. [Materialübersicht](DOKUMENTATION_V0_5.md).
