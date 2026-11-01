# EQUILIB_LAB – aktueller Entwicklungsstand und Übergabe

**Stand:** 01.11.2026 · **Projekt:** CHEMIE mit KI – GLEICHGEWICHTS-LAB  
**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB  
**Aktuelle Testversion:** **v0.4d** unter `prototyp/integriert-v0.4d/index.html`  
**Live-Test:** https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4d/  
**Freigegebene Root-Startfassung:** `main/index.html` weiterhin v0.3e.

## Versionsübersicht

| Version | Datei | Stand |
|---|---|---|
| v0.3e | `index.html` und `prototyp/integriert-v0.3e/index.html` | Bewährte Apfel-/Stechheberfassung, unverändert |
| v0.4a | `prototyp/integriert-v0.4a/index.html` | Erstes Chemie-Modell A+B⇌C+D |
| v0.4b | `prototyp/integriert-v0.4b/index.html` | Variable k-Werte, K/Q, gemeinsamer Reaktionsraum |
| v0.4c | `prototyp/integriert-v0.4c/index.html` | Einmalzugabe A +0,20 mol/L und Q/K-/Zielwertneuberechnung; vom Nutzer als gut funktionierend bestätigt |
| **v0.4d** | `prototyp/integriert-v0.4d/index.html` | **Neu:** laufender D-(Wasser-)Entzug, externes Sammelgefäß, vier Live-Balken, vor Start getrennte Teilchen, bidirektionale Reglerkopplung und Schnelllauf ×10; automatischer Rechentest bestanden, Sichtabnahme offen |

**Neu erstelltes Prüfprotokoll:** [PRUEFPROTOKOLL_V0_4D_2026-11-01.md](PRUEFPROTOKOLL_V0_4D_2026-11-01.md).

## Leitplanken

- Niederschwelliges Einzel-HTML, ohne Netz, ohne externe Bibliotheken, mit **zehn eingebetteten Bildern** für den Workshop Februar 2027.
- Drei ursprüngliche Perspektiven **Geschichte, Modell, Vergleich** einschließlich synchronisierter Apfelphasen und Stechheber-Rechenkern nicht umbauen.
- Chemie bleibt ein **eigenständiger Rechenkern** und eigene Reaktionsansicht; formal A+B⇌C+D, D=Wasser.
- Versionierte Prototypverzeichnisse beibehalten; Root nur nach expliziter Freigabe anheben.
- Nach jedem Entwicklungsschritt diesen Stand und die Übergabe im Repository aktualisieren.

## v0.4d – Funktionsumfang und Regeln

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
- **Nächste Aufgabe:** v0.4d im Browser testen: getrennte Ausgangsteilchen, Freigabe nach Start, vier Balken und Sammelgefäß, Wasser EIN/AUS, Schnelllauf, A-Zugabe, K/Q, Apfel- und Chemie-Regler, Reset und Altmodule. Doppelklick offline prüfen. Falls nötig, Korrekturversion v0.4e; **main/index.html bleibt unverändert**.

## GitHub-Technik-Hinweis

HTML ist ca. 2,6 MB groß. `mcp__GitHub__fetch_file` kann für solche großen Dateien **leeren Inhalt bei korrektem SHA** liefern. Blob-SHA aus `fetch_file.sha` holen und `mcp__GitHub__fetch_blob({repository_full_name:"ekerzendorfer/EQUILIB_LAB",blob_sha:...})` nutzen. Auf keinen Fall leeres `fetch_file.content` als Datei interpretieren oder hochladen. Versionierung beibehalten.

## Fortsetzungsprompt (direkt in neuen Chat kopieren)

> Wir arbeiten am GitHub-Repo `ekerzendorfer/EQUILIB_LAB`. Lies `docs/ENTWICKLUNGSSTAND.md` und `docs/PRUEFPROTOKOLL_V0_4D_2026-11-01.md`. Aktuelle Testfassung v0.4d unter `prototyp/integriert-v0.4d/index.html`; frühere v0.4c gut, root `index.html` noch freigegebene v0.3e. Chemie A+B⇌C+D, D=H₂O, mit kontinuierlichem Wasserabfluss 25% pro Rechenschritt, externem Sammelbehälter, K/Q, vier mitlaufenden Stoffbalken, getrenntem Vorstart im Reaktionsraum, gekoppelt eingestellten Apfel-/Chemie-Ratenreglern, A-Zugabe +0,20 und Schnelllauf ×10. Automatische mathematische Tests bestanden; Browser- und Offline-Abnahme fehlt. Unbedingt große GitHub-HTML via `fetch_blob` laden. Bitte an aktuellem Feedback orientiert gezielt weiterentwickeln, alte Versionen und Apfelmodell erhalten und nach jedem Entwicklungsschritt die Markdown-Übergabe aktualisieren.
