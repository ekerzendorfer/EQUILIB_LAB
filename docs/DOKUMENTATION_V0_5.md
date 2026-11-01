# GLEICHGEWICHTS-LAB – Abschlussdokumentation V0.5

**Stand:** 01.11.2026 · **Status:** Entwicklungsabschluss / V0.5 als separat abgelegte Testfassung; Browser-/Offline-Endabnahme noch ausständig.  
**Datei:** [prototyp/integriert-v0.5/index.html](../prototyp/integriert-v0.5/index.html)  
**Grundsatz:** Ältere Stände und `index.html` im Repository-Root nicht überschreiben; V0.5 wird vorläufig nicht in das Applikationsportal übernommen.

## 1. Bildungsziele und Ebenen

Das GLEICHGEWICHTS-LAB soll das **dynamische Gleichgewicht** in drei Stufen erfahrbar machen:

1. **Fallobstschlacht / Geschichte:** anschauliche A↔B-Analogie. Trotz stationärer Bestände können in beide Richtungen Äpfel transportiert werden.
2. **Modell / Stechheber-Analogie:** diskreter, proportionaler Hin- und Rücktransfer; gemeinsame Rechnungen und Beobachtungen in der Vergleichsansicht.
3. **Chemisches Gleichgewicht:** **eigenständige** formale Reaktion A+B ⇌ C+D (D = H₂O in der Esterbildungsinterpretation). Stoffbestände, Reaktionsraten, Quotient Q, Gleichgewicht K, Störungen und Temperatur.

**Zentrale Einsicht:** `v_hin = v_rück > 0` bedeutet dynamisches Gleichgewicht; gleiche Konzentrationen sind **nicht erforderlich**. Die drei Ebenen sind Analogie, Modell und chemische Idealisierung, keine identischen physikalischen Systeme.

## 2. Formale Modelle

### Fallobst/Stechheber

Die aus dem vorhandenen Rechenkern verwendeten Transfers sind
`H_n = p_hin · A_n`, `R_n = p_rück · B_n`,
`A_(n+1)=A_n-H_n+R_n`, `B_(n+1)=B_n+H_n-R_n`.
Ohne Zu-/Abfuhr bleibt `A+B=M` invariant. Die gezeigten Punkte/Kugeln sind Visualisierung kontinuierlicher Modelleinheiten, keine einzelnen Äpfel oder Atome. Der Stechheber wird als einfaches Transferanalogon, nicht als hydrodynamisch kalibriertes Versuchsmodell gezeigt.

### Chemie: formale Kinetik

`A+B ⇌ C+D` mit
`v_hin=k_hin,eff·c_A·c_B`,
`v_rück=k_rück,eff·c_C·c_D`,
`dc_A/dt=dc_B/dt=-(v_hin-v_rück)`, `dc_C/dt=dc_D/dt=v_hin-v_rück`.
Die Umsetzung erfolgt über zwölf deterministische Euler-Teilschritte je angezeigtem Schritt; die Schrittweite ist ein **Modellschritt**, kein kalibrierter Zeitwert. Konzentrationen bleiben nichtnegativ. Als Idealmodell des geschlossenen, konstantvolumigen Systems gelten `Q_c=c_Cc_D/(c_Ac_B)` und im Gleichgewicht `K_c(T)=k_hin,eff/k_rück,eff`. Für reale Gemische sind Aktivitäten statt reiner Konzentrationen und reale Mechanismen nötig.

Anfangsbedingungen: `c(A)=c(B)=1,000 mol/L`, `c(C)=c(D)=0`. Die zwei k-Regler sind Basiskonstanten (0,02 bis 0,20 in Modellzeiteinheiten) und werden mit den Analog-Reglern gekoppelt, **obwohl die Rechenkerne unabhängig bleiben**. Bei 60 °C ohne Katalysator sind die effektiven k-Werte 0,6× Basiswert. Ein Reaktionsschritt ist damit **nicht** als reale Sekunde zu lesen.

### Eingriffe

- **A-Zugabe:** +0,20 mol/L als unmittelbarer Sprung von A; Q sinkt bei geeigneter Ausgangssituation, danach läuft die Modellreaktion weiter. Eine Zugabe pro Versuch.
- **Wasser (D) auskreisen:** nach jedem äußeren Reaktionsschritt 10 % des vorhandenen D in einen rechnerischen Sammelbehälter auslagern. Es handelt sich um ein **offenes System**, nicht um ein neu eingestelltes geschlossenes Gleichgewicht; der Wasserauskreiser ist idealisiert.
- **Säurekatalysator EIN:** beide effektiven k um Faktor 3 erhöht; das K bei gegebener Temperatur bleibt im Modell konstant. Säuremechanismus und eventuelle reale Wasserbindung sind **nicht** ausgerechnet.
- **Temperatur:** 20–80 °C in 10-°C-Schritten, Referenz 60 °C. Arrhenius-Gleichung mit **angenommener** `E_a,hin=60 kJ/mol`, `E_a,rück=63,6 kJ/mol`. `Δ_rH≈−3,6 kJ/mol` dient als Literatur-Anhaltspunkt; damit sind die Änderungen von `K(T)` im Modell konsistent. Es erfolgt keine Kalibrierung absoluter Reaktionszeiten. Beim Temperaturwechsel springen Konzentrationen nicht. Die Reaktionsenthalpie, Verdampfung, Mischung und Wärmeübertragung sind nicht simuliert.

### Gemeinsamer Reaktionsraum

- A/B/C/D sind bewegte, farbige 2-D-**Symbole**; ungefähr 24 Kreise je 1 mol/L, gerundet.
- Bewegungen und elastische Stöße sind schematisch und **kein** realer molekularer Mechanismus.
- Nur ausgewählte A-B-Kollisionen erhalten **orange** Markierung, nur ausgewählte C-D-Kollisionen **rote** Markierung. Das verfügbare Ereignisbudget ist an die **im letzten Schritt integrierten positiven Bruttoraten** beider Richtungen (×24 Symbolskalierung) gekoppelt. Bloße Kollisionen erzeugen keine Ringe mehr. Nicht jedes mögliche Ereignis muss tatsächlich sichtbar werden; ein Ring entspricht **keiner** experimentell nachgewiesenen Molekülreaktion.
- Der deterministische Rechenkern wird **nicht** von der Animation gesteuert: Symbolfarben und Stückzahlen werden aus den Konzentrationen abgeglichen. Die Ringereignisse beweisen keine molekulare 1:1-Umsetzung. Bruttoreaktionen bleiben im mathematischen Gleichgewicht möglich.
- **Pause** beendet Rechenschritte und Rahmenanimation, entfernt ausstehende Ringe. **Einzelschritt** ist die ausdrücklich vom Nutzer ausgelöste Ausnahme und führt genau einen Rechenschritt durch.
- Bei 20/80 °C ändert sich im Modell die Rate, **nicht die visuelle Teilchengeschwindigkeit**.

## 3. Grafiken und Bedienung

- Große Konzentrationsgrafik und platzsparende Miniansicht nutzen dieselben Daten und Ereignislinien.
- Stoffbalken, Zahlen, `K`, `Q`, Raten und Gleichgewichtsstatus folgen dem gleichen chemischen Zustandsobjekt.
- Tab „Geschichte“, „Modell“, „Vergleich“ mit eigenem A↔B-Rechenkern; Tab „Chemisches Gleichgewicht“ mit A+B⇌C+D.
- Start, Pause, Einzelschritt, Reset, Temp-Regler, Katalysator, Wasserentzug, A-Zugabe, Schnelllauf ×10.
- Die HTML-Datei enthält die notwendigen Bilder und arbeitet ohne CDN, Login oder externe Skripte offline. Die Versionshistorie bleibt in separaten Verzeichnissen.

## 4. Methodisch wichtige Grenzen

Das System ist eine **didaktisch plausible, rechnerisch konsistente Idealisierung**, keine realistische numerische Reproduktion eines Ethylacetat-Laborexperiments. Die Bruttoraten sind mathematische Größen einer formalen effektiven Kinetik; der tatsächliche Fischer-Veresterungsmechanismus enthält mehrere elementare Reaktionsschritte und Zwischenprodukte. Reaktionsmischungen sind nicht ideal; die Wasserentnahme wird als fixe 10-%-Regel vorgegeben. Das Labor-Temperaturverhalten bei 80 °C kann wegen flüchtiger Bestandteile vom isothermen Modell stark abweichen. Vermeiden: „ein Ring = eine reale molekulare Umsetzung“ oder „20 Modellschritte = 20 Sekunden“.

Quellen zum Temperatur-/Mechanismuskontext sind im [v0.4g-Prüfprotokoll](PRUEFPROTOKOLL_V0_4G_2026-11-01.md) genannt. Dort ist außerdem ausdrücklich dokumentiert, welche k-Werte **Modellannahmen** sind.

## 5. Abnahme und Verteilung

Der Nutzer hat v0.4g am 01.11.2026 positiv im Browser geprüft. V0.5 ist eine minimal modifizierte Fassung mit angepasster Beschriftung und Raten-Kopplung der visuellen Ereignisse; Syntax, IDs und numerische Stichproben wurden geprüft. **Browser, Projektor und Offline-Datei sind für V0.5 noch manuell zu prüfen.** [Prüfprotokoll](PRUEFPROTOKOLL_V0_5_2026-11-01.md).

Für den Februar-Workshop ist die **lokale HTML-Datei** geeignet. Das Repository ist derzeit **öffentlich**; GitHub-Pages-Pfade sind bei bekanntem Link erreichbar, selbst ohne Verlinkung im Portal. „Nicht veröffentlichen“ ist deshalb nur im Sinn von *nicht bewerben/nicht ins Portal integrieren* sichergestellt. Soll V0.5 wirklich nur einem geschlossenen Personenkreis zugänglich sein, darf die öffentliche GitHub-Pages-Version nicht als Zugriffsschutz verstanden werden.

## 6. Weitere Materialien

- [Multiple-Choice-Aufgaben für SEK II](AUSWERTUNGSAUFGABEN_V0_5.md)
- [Lösungen und didaktische Hinweise](LEHRKRAFT_LOESUNGEN_V0_5.md)
- [Dreistündiger Workshop im Februar 2027](WORKSHOP_FEBRUAR_2027_V0_5.md)
- [Prüfprotokoll V0.5](PRUEFPROTOKOLL_V0_5_2026-11-01.md)
- [Änderungs-Prompt](PROMPTS/INTEGRIERT_V0_5.md)
