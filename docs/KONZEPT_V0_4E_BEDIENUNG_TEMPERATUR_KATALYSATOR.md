# EQUILIB_LAB – Konzeptentwurf für die nächsten Schritte (01.11.2026)

**Status:** Vorschlag aus dem Nutzerfeedback zu v0.4d; keine implementierte oder freigegebene neue Version.  
**Testbasis:** `prototyp/integriert-v0.4d/index.html`; `main/index.html` weiterhin v0.3e.  
**Fachgrundlage:** `docs/PRUEFPROTOKOLL_V0_4D_2026-11-01.md`.

## 1. Feststellungen aus dem Quelltext

- Die Regler `#total` (Gesamtbestand A+B) und `#initial-a` (Anfangsmenge A) gehören nur zum Apfel-/Stechhebermodell `settings/state`. Das chemische Modell `CHEM_PARAMS/chemState` beginnt separat mit A=B=1,000 mol/L, C=D=0; 24 Symbole pro mol/L.
- Die globale `.status-panel`, `.controls` und das originale `details.info` stehen **außerhalb** der Tab-Panels und bleiben im chemischen Reiter sichtbar. `.toolbar` wird dagegen in `setView` beim Chemie-Reiter bereits verborgen.
- Die p-Hin-/p-Rückregler des Apfelmodells und die k-Hin-/k-Rückregler der Chemie sind numerisch in v0.4d synchronisiert, trotz unterschiedlicher physikalischer Bedeutung.
- Die Buttons `#story-preset` und `#defaults` wählen nur historische Startparameter, keine eigenen Rechenmodi. Die voreingestellten Apfelwerte sind derzeit nicht identisch mit dem Story-Preset: DEFAULTS 50/50, pHin 0,06, pRueck 0,04; STORY_PRESET 50/50, pHin 0,08, pRueck 0,04.
- In der HTML-Kopfzeile von v0.4d steht noch irrtümlich „Integriert V0.4c“; bei nächstem Versionsschritt korrigieren.

## 2. Vorschlag v0.4e: Oberfläche vereinfachen (zuerst)

1. Im Chemie-Reiter die gesamten **Apfel-Status- und Einstellungsblöcke** einschließlich der dort unzutreffenden Hilfetexte ausblenden: `.status-panel`, `.controls`, `details.info`. Bei Geschichte, Modell, Vergleich bleiben sie erhalten.
2. Chemisches Reaktionsschema, Start/Pause, Schritt, Reset, A-Zugabe, Wasserauskreiser, Schnelllauf, k-Parameter und K/Q erhalten; den Reaktionsraum, die vier Live-Balken, externe Wassersammelmenge und Raten-/GG-Anzeige räumlich aufwerten. Erklärungstexte bei Bedarf in aufklappbaren Details.
3. Historische Toolbar-Buttons „Apfelkrieg-Vorgabe“ und „V0.2-Werte“ aus sichtbarer Bedienoberfläche entfernen. Für Geschichte/Modell/Vergleich einen **eindeutigen Startstandard** festlegen (naheliegend: Apfelkrieg-Preset 50/0, pHin=0,08, pRueck=0,04), ohne die älteren Archivversionen zu ändern. Reset-Semantik dokumentieren: Zustand zurücksetzen, Parameter bleiben, sofern ausdrücklich kein „Standardwerte wiederherstellen“ implementiert wird.
4. Bestehende bidirektionale Kopplung der **Basis**-Ratenregler vorerst erhalten; die Konsequenz der späteren Temperatur- und Katalysatorbedienung deutlich kennzeichnen. Temperatur/Katalysator dürfen Apfeltransportparameter nicht verändern.
5. Numerische Regressionstests: Apfelphasen, Stechheber, Chemie K0,1/K1/K10, A-Zugabe, kontinuierlicher D-Abfluss, offene Stoffbilanzen. Sichtprüfung am Laptop, Beamer, schmaler Breite und Offline-Doppelklick. Root unverändert.

## 3. Vorschlag v0.4f: Säurekatalysator – eigener kleiner Schritt

**Didaktischer Kern:** Katalysator erhöht Hin- UND Rückrate, **nicht** K bei gleicher Temperatur; die Gleichgewichtszusammensetzung bleibt für das geschlossene System unverändert. Der Hinweis „H₂SO₄ (Modellkatalysator)“ ist angebracht; reales Schwefelsäure-Milieu, Wasserbindung und Mechanismus werden **nicht** simuliert.

- Ein Schalter `Säurekatalysator AUS/EIN` (oder `ohne/mit H₂SO₄`); didaktischer Beispiel-Faktor `f=3` für **beide** effektiven Ratenkonstanten, nicht als gemessener Stoffwert ausgeben.
- `kHin_eff=f·kHin_basis`, `kRueck_eff=f·kRueck_basis`; `K=kHin_eff/kRueck_eff=kHin_basis/kRueck_basis`.
- Schalter während der Simulation: Raten ändern sich unmittelbar, Konzentrationen zunächst **nicht**. Neue bzw. alte Nettoreaktionsrate wirkt erst mit dem nächsten Rechenschritt. Ereignismarkierung im Konzentrationsgraphen.
- Im geschlossenen System Vergleich mit/ohne Katalysator: verschiedene Annäherungsdauer, **identische Endlage**. Beim offenen D-Auskreisen kann sich der zeitliche Verlauf durch konkurrierenden Abfluss unterscheiden; nicht als Änderung von K bezeichnen.
- Das gegenwärtige explizite Euler-`deltaT=1`-Verfahren ist für größere effektive k-Werte gegebenenfalls numerisch zu grob. Entweder kleine interne Teilzeitschritte (`dt=1/N`) pro angezeigtem Schritt verwenden oder einen nachweislich sicheren Parameterbereich, nicht lediglich negative Mengen abschneiden. Die 25%-D-Entnahme erfolgt einmal je äußerem Schritt und bleibt klar definiert.

## 4. Vorschlag v0.4g: Temperatur – fachlich bewusst etwas anspruchsvoller

**Keine reine Tempoeinstellung:** T verändert im Allgemeinen **beide** Richtungsraten und `K(T)`. Ein gemeinsamer Multiplikator beider k-Werte würde die thermodynamische Wirkung fälschlich verdecken.

- Vorschlag: eigener Chemie-Regler `20–60 °C` in 5-°C-Schritten, Referenz `T0=25 °C`. Kein Temperaturregler für die Apfelanalogie.
- Für eine **ausdrücklich illustrative Modellreaktion**, nicht als quantitatives Experiment einer konkreten Veresterung deklariert: z.B. `ΔrH°=-15 kJ/mol` (hier noch kein beschlossener Parameter). Der Wert und das Vorzeichen müssen sichtbar als Modellannahme gekennzeichnet sein.
- Vereinfachte van-'t-Hoff-Beziehung (K-Basis bei T0): `K(T)=K(T0)*exp[-ΔrH°/R*(1/T-1/T0)]`, absolute Temperaturen in Kelvin.
- Gleichzeitig Arrhenius-Temperaturabhängigkeit der beiden k-Werte, konsistent mit `Ea,hin-Ea,rueck=ΔrH°`. Alternative: Temperaturgeschwindigkeitsfaktor mal `sqrt(K(T)/K(T0))` für kHin und inverse Wurzel für kRueck, damit ihr Quotient exakt `K(T)` ergibt.
- T-Veränderung auch während des Versuchs möglich: Konzentrationen bleiben im Moment der Veränderung gleich, `K` und Raten ändern sich unmittelbar; `Q` aus den Konzentrationen bleibt initial unverändert; daraufhin Relaxation zur neuen Zusammensetzung. Diagramm-Ereignismarker `T 25→45 °C`.
- Aussage bei negativer angenommener Reaktionsenthalpie: Erwärmung fördert das Eduktgleichgewicht (K sinkt), obwohl Hin- und Rückreaktion kinetisch schneller werden können. Bei endothermer Annahme ist die Verschiebung umgekehrt. Wahl und Realitätsnähe der Veresterungsreaktion vor Umsetzung klären.
- Numerik bei gleichzeitiger Katalyse, Erwärmung, A-Zugabe und D-Entzug robust prüfen: interne Teilzeitschritte, Bilanz, Nichtnegativität, stabiler Grenzwert, keine künstlichen Oszillationen. Der Wasserauskreiser bleibt ein idealisierter 25%-Stoffstrom pro angezeigtem Schritt.

## 5. Beabsichtigte kompakte Präsentation

**Chemischer Reiter:** Reaktionsgleichung; schmale Werkzeugleiste mit Start/Pause/Schritt/Reset sowie A-Zugabe, Wasser EIN/AUS und Schnelllauf; Basiskonstanten kHin/kRueck; später T und Katalysator kompakt daneben; großer gemeinsamer Reaktionsraum und mitlaufende Stoffbestände; daneben Raten, Q/K und GG-Text; darunter Konzentrationsdiagramm. Modellgrenzen durch aufklappbare Details erreichbar.

**Geschichte/Modell/Vergleich:** bestehende Apfelsteuerung und vollständiger Rechenkern; historische Preset-Buttons visuell entfernen, eine einheitliche Ausgangsdefinition beibehalten.

## 6. Abgrenzung und Übergabe

Dieser Stand ist **nur ein fachlicher und UI-bezogener Vorschlag**; v0.4d bleibt die neueste implementierte Testversion, v0.3e die unveränderte Root. Keine neue HTML-Version und keine Browserabnahme in diesem Schritt.

**Fortsetzung:** zuerst v0.4e (UI und Presets) in einem **neuen** Prototypverzeichnis umsetzen und automatisch prüfen, Browserfreigabe abwarten; anschließend v0.4f (Katalysator) und v0.4g (Temperatur) mit getrennten Rechen- und Bedienabnahmen. Nach jeder implementierten Stufe `docs/ENTWICKLUNGSSTAND.md`, Prüfprotokoll, README und eine kompakte Übergabe im Repository aktualisieren.

**Fachquelle:** OpenStax Chemistry 2e, Kap. 13.3 „Shifting Equilibria: Le Châtelier’s Principle“ (Temperatur ändert K, Katalysator ändert nicht K); IUPAC Gold Book „catalyst“.


## Umsetzungsstand 01.11.2026

Die **UI-Stufe v0.4e wurde inzwischen als separater Prototyp** `prototyp/integriert-v0.4e/index.html` implementiert (Konzeptabschnitt 2; Browserfreigabe offen): Apfelsteuerung bei Chemie ausgeblendet, historische Presets entfernt, gemeinsame Chemie-Partikelanimation als Standardansicht, breiteres responsives Layout und größere Live-Balken. Das Apfel-Ausgangsstandard bleibt M=50, A0=50, pHin=0,08, pRueck=0,04. Reset übernimmt die veränderten Parameter. Lange Erläuterungen sind einklappbar; aktuelle Störungsmeldungen bleiben sichtbar.

Die Abschnitte **v0.4f Katalysator** und **v0.4g Temperatur** sind weiterhin ausschließlich fachliche Planungsentwürfe, **noch nicht implementiert**. Sie werden erst nach Abnahme der v0.4e-Oberfläche gesondert angegangen. [Aktuelle Übergabe](UEBERGABE_v0.4e.md) · [Prüfprotokoll](PRUEFPROTOKOLL_V0_4E_2026-11-01.md).
