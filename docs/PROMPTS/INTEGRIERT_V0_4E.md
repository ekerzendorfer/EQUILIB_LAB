# Änderungs-Prompt – integrierter Prototyp v0.4e

**Basis:** `prototyp/integriert-v0.4d/index.html` · **Ziel:** `prototyp/integriert-v0.4e/index.html` · **Datum:** 01.11.2026

## Auftrag (Nutzerfeedback)

> Ja, machen wir mit v0.4e – Oberfläche vereinfachen. Globale Apfel-Steuerung im Chemie-Reiter ausblenden, veraltete Preset-Buttons entfernen und den chemischen Reaktionsraum samt Stoffbalken vergrößern.

## Umsetzungsvorgaben

1. Die globale Apfel-/Stechhebersteuerung bleibt im DOM erhalten, da Apfelmodell und Story darauf angewiesen sind; nur bei aktivem Chemie-Tab mittels `body.chem-active` und CSS ausblenden. Beim Reiterwechsel wieder einblenden.
2. Alte Presets `#defaults` und `#story-preset` samt Event-Listenern entfernen, keine Null-Referenzen verursachen. Anfangsstandard aus dem bestehenden `STORY_PRESET` übernehmen; Reset setzt Zustand statt Parametervorgabe zurück.
3. Chemie-Bereich breiter anordnen. **Gemeinsamen Reaktionsraum** als Standard starten und Kacheln als Alternative beibehalten. Canvas flüssig bis volle Spaltenbreite; Konzentrationsbalken und externer Wasserbalken höher und lesbarer; responsive Einspaltenlayout.
4. Status-/Rückmeldung A-Zugabe/Wasserentzug direkt sichtbar lassen; lange Modellhinweise einklappbar halten. Den Bild-/Chemie-Rechenkern nicht verändern.
5. Root und alle früheren Prototypen unangetastet lassen. Eingebettete Bilder und Offline-Einzel-HTML-Format erhalten.
6. Nach Quellcodeprüfungen Dokumentation und kompakte Übergabe aktualisieren; Browser- und Offlineabnahme gesondert ausweisen.

## Tatsächliche Änderungen

`body.chem-active` via `setView`; CSS-Main bis 1480 px, Chemie-Spalten 1,75 : 0,75, Canvas ohne CSS-Maximalbreite 720 px, Stoffbalken 20 px; Chemie-Start `chemView=\"room\"` mit passendem `hidden`/`aria-pressed`; entfernte Preset-Event-Listener/Buttons und entfernte `DEFAULTS`; kompakte Störhinweise, Modellnotizen via `details`. Keine Änderung der Rechenformeln.

**Prüfung:** siehe [PRUEFPROTOKOLL_V0_4E_2026-11-01.md](../PRUEFPROTOKOLL_V0_4E_2026-11-01.md). Browser-Sichtabnahme offen.
