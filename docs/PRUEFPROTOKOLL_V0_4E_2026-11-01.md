# EQUILIB_LAB – Prüfprotokoll v0.4e (01.11.2026)

**Version:** `prototyp/integriert-v0.4e/index.html` · **Basis:** v0.4d · **Status:** automatisierte Quellcode-Prüfung bestanden, manuelle Browser-, Mobil- und Offline-Sichtabnahme ausständig.

## Umsetzung und erwartete UI-Wirkung

1. Im Reiter **Chemisches Gleichgewicht** werden die ausschließlich zum Apfel-/Stechhebermodell gehörenden `main > .status-panel`, `main > .controls` und `main > details.info` über eine an `setView('chem')` gebundene `body.chem-active`-Klasse ausgeblendet. In **Geschichte**, **Modell**, **Vergleich** ist die Bedienung weiterhin sichtbar.
2. Zwei historische Preset-Buttons und ihre Event-Handler sind entfernt; es gibt nur mehr einen Apfel-Startstandard (`STORY_PRESET`: M=50, A0=50, B0=0, pHin=0,08, pRueck=0,04). Die Regler für M, A0 und p bleiben in den drei Apfelansichten. **Reset setzt den Zustand bei unveränderten aktuellen Parametern zurück**, keine Vorgabewiederherstellung.
3. Chemischer Reaktionsraum ist beim erstmaligen Öffnen Standardansicht, die getrennten Bestände sind weiterhin umschaltbar. Chemie-Layout bis max. 1480 px statt bisher 1200 px Hauptbreite, linke/rechte Spalten ca. 70:30, Canvas ohne starre 720-px-CSS-Obergrenze; Live-Balken höher, deutlicher.
4. Dynamische Meldungen zu A-Zugabe und D-Entzug bleiben direkt sichtbar. Erläuternde Langtexte zu Störungen und Kollisionen stehen in aufklappbaren Details.
5. Chemischer Rechenkern einschließlich A-Zugabe (+0,20 mol/L), laufendem Wasserentzug (25 % von D pro Reaktionsschritt), 24 Symbolen pro mol/L, k-Kopplung, Schnelllauf ×10 und bestehenden Bilanz-/Diagrammregeln bleibt unverändert. Ebenso die ursprüngliche Apfel-/Stechheberrechnung.

## Automatisch geprüft (Quelltext)

- HTML-Datei im GitHub-Repo neu erstellt und als eigener Blob wieder eingelesen; **2.622.720 Zeichen** statt 2.621.243 Zeichen der v0.4d.
- JavaScript-Quelltext mit `new Function(script)` vollständig syntaktisch geparst: **bestanden**.
- **131 HTML-IDs, ohne Dubletten**; **123 direkte `$(\"id\")`-Zugriffe**, sämtliche Ziel-IDs existieren.
- **10 eingebettete `data:image/`-Quellen** erhalten; altes Storybildmaterial unverändert.
- Entfernte Preset-IDs nicht mehr im JavaScript referenziert.
- Startzustand `chemView=\"room\"` konsistent mit `hidden`- und `aria-pressed`-Attributen; CSS für kontextabhängige Ausblendung vorhanden.
- Ursprungsdatei `prototyp/integriert-v0.4d/index.html`, frühere Stände und freigegebene Root-`index.html` nicht geändert.

## Manuelle Browserabnahme – noch offen

| Aktion | Erwartung |
|---|---|
| Geschichte öffnen | Globale Status-/Startwertregler sichtbar, keine historischen Presets |
| Apfel-Regler ändern, Schritt/Reset | Werte und Apfel-/Stechheberdarstellungen folgen; Reset übernimmt letzte Parameter |
| Zu Chemisches Gleichgewicht wechseln | Apfel-Steuerungen und Apfelhilfe verschwinden vollständig |
| Chemie erstmals öffnen | Gemeinsamer großer Reaktionsraum mit 24 A + 24 B links; C/D zunächst 0; Live-Balken darunter |
| Getrennte Stoffbestände wählen | Vier Kachelansichten erscheinen und Rückwechsel zum Reaktionsraum funktioniert |
| Chemie Start/Pause/Schritt/Reset | Animierter Reaktionsraum, Bilanzbalken, Chemie-Kennzahlen und Konzentrationsgraph laufen synchron |
| A zugeben, D auskreisen, Schnelllauf ×10 | Bisherige v0.4d-Wirkungen; dynamische Rückmeldungen bleiben sichtbar |
| Wechsel zurück zu Modell/Vergleich/Geschichte | Apfel-Steuerung und alte Simulation wieder sichtbar; keine fehlerhaften Reiter |
| Laptop/Projektor/ca. 390 px | Kein horizontales Überlaufen, Stoffbalken lesbar, Karten werden einspaltig |
| Offline öffnen | Eine einzelne heruntergeladene HTML-Datei funktioniert ohne Netz |

**Grenzen:** Die automatisierte Prüfung ersetzt keine echten Browserklicks, Canvas-Sichtprüfung, Mobil- oder Offlineabnahme. Fachliche Rechenreferenzen der **unveränderten** v0.4d sind in `docs/PRUEFPROTOKOLL_V0_4D_2026-11-01.md` dokumentiert.

## Nächste Entscheidung

Nach Browserfreigabe v0.4e als neue UI-Basis verwenden; anschließend den **Säurekatalysator** als eigenen v0.4f-Schritt modellieren und prüfen (beide Teilraten beeinflussen, K bei konstanter Temperatur unverändert). Temperatur erst danach separat.
