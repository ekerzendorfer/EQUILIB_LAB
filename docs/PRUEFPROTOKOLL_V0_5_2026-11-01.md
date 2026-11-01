# Prüfprotokoll V0.5 – 01.11.2026

**Datei:** [prototyp/integriert-v0.5/index.html](../prototyp/integriert-v0.5/index.html)  
**Vorversion:** V0.4g am 01.11.2026 laut Nutzer erfolgreich im Browser geprüft. Root `index.html` bleibt unverändert.

## Umgesetzter Feinschliff

1. HTML-Titel, sichtbare Versionszeile und Footer auf **V0.5**.
2. Kopfuntertitel exakt: **Fallobstschlacht, Modell und chemisches Gleichgewicht**.
3. Canvas-Überschrift im Reaktionsraum: `ctx.textAlign="left"` vor `fillText`, weil vorher die zentrale Teilchenbeschriftung den Canvas-Kontext für die nächste Zeichnung verändert hatte.
4. Frühere Ringlogik: jede A-B- oder C-D-Kollision konnte Ringe auslösen. Neu: Die intern integrierten **positiven Brutto-Reaktionsfortschritte** von Hin- und Rückreaktion begrenzen ein Ereigniskonto je Richtung (`24 · Δξ_brutto` symbolisch, maximaler Rückstand 8 je Richtung). Nur bei passender Kollision **und** ausreichend Ereigniskonto wird eine Markierung erzeugt; orange für Hin, rot für Rück. Der makroskopische Rechenkern wird von den sichtbaren Kollisionsereignissen nicht beeinflusst.
5. Die beim nachträglichen Abgleichen gerundeter Symbolzahlen entstehenden Farbumstellungen erzeugen **keine eigenen Ringe** mehr.
6. Pause beendet sowohl den chemischen Zeitschritt-Timer als auch den Animations-Frame-Loop und leert ausstehende Ringe/Ereigniskonten. Einzelschritt bleibt bewusst als manuell ausgelöste Berechnung möglich.
7. Lernenden-Multiple-Choice als getrenntes Arbeitsblatt, **nicht in der App implementiert**. Lehrkraftlösungen separat.
8. Abschlussdokumentation und Workshop-Konzept ergänzen V0.5.

## Automatische Prüfungen beim Erzeugen

- Gesamtes eingebettetes JavaScript mit `new Function(script)` erfolgreich syntaktisch geprüft.
- HTML-`id`-Attribute auf doppelte IDs geprüft: **keine Duplikate**.
- **6 numerische Testläufe** (T=20/60/80 °C × Katalysator AUS/EIN; Standard-k=0,08/0,08) à **300 äußere Schritte**, mit Prüfung auf endliche, nichtnegative Stoffbestände und A+C=1, B+D=1 im geschlossenen System.
- Größter absoluter Erhaltungsfehler in diesen Läufen: **4,22·10⁻¹⁵ mol/L**.
- Kontrolle nach 300 Schritten: `K(20 °C)=1,1940`, `K(60 °C)=1,0000`, `K(80 °C)=0,9290`, jeweils **mit und ohne** Katalysator gleich.
- Bei 60 °C und Katalysator AUS im numerischen Endzustand: integrierter Hin- und Rückumsatz je Schritt jeweils ca. **0,012**; mit Katalysator EIN jeweils **0,036** (bei Konzentrationen ca. 0,5 / 0,5 / 0,5 / 0,5). Damit sind positive Umsätze beider Richtungen auch bei stationären Konzentrationen rechnerisch vorhanden.
- Die vorangegangene breite 56-Kombinationen-Regression ist im v0.4g-Prüfprotokoll dokumentiert; **nicht** als neuer v0.5-Test ausgegeben.

## Manuell noch abzunehmen

- [ ] V0.5 im Desktopbrowser öffnen: Kopfuntertitel, Version und vollständige Canvas-Überschrift.
- [ ] Start im Chemie-Reiter: zu Beginn orange Hin-Ringe, später auch rote Rück-Ringe; keine Dauer-Ringe nur wegen beliebiger A-B- oder C-D-Kollisionen.
- [ ] Bei angenähertem Gleichgewicht beide positiven Teilraten und fallweise beide Ringfarben sehen.
- [ ] **Pause:** Konzentrationen, Teilchenpositionen und Reaktionsringe bleiben still; bei **Einzelschritt** ändert sich die Rechnung genau einmal, obwohl der Automatiklauf pausiert.
- [ ] Katalysator EIN/AUS und T=20, 60, 80 °C: relative Ringereignishäufigkeit und mathematische Raten plausibel; keine Behauptung über reale absolute Zeit.
- [ ] Wasser auskreisen und A zugeben: Bestände, Stoffbilanzen und roter/orangefarbener Ereignisfilter bleiben konsistent.
- [ ] Wechsel der Teilchenansicht, Tabs, Reset, Schnelllauf ×10, Minigrafik und großes Diagramm.
- [ ] Notebook- und Projektorauflösung sowie offline per lokalem Doppelklick (ohne Netzwerk).
- [ ] Für den Workshop eine eigene Kopie unter anderem Namen öffnen; Root-Startfassung nicht überschreiben.

**Status:** Automatische Syntax-, Struktur- und sechs Modelltests bestanden; eine reale Browser-/Offlineabnahme von V0.5 wird ausdrücklich **nicht** behauptet.
