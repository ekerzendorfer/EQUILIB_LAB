# GLEICHGEWICHTS-LAB – Workshop-Aufgaben auf Basis V0.2

**Stand:** 19. Oktober 2026  
**Verbindlicher Referenzstand:** [V0.2 – index.html](../prototyp/v0.2/index.html)  
**Status:** Aufgabenideen, **nicht** implementierte oder getestete App-Funktionen. V0.2 bleibt als sichere Rückfallversion unverändert.

## 1. Workshop-Prinzip

Die Teilnehmenden entwickeln **nicht die gesamte App neu**. Sie erhalten die funktionierende, offlinefähige Datei `index.html` aus V0.2, speichern vor Änderungen eine Kopie und bearbeiten **eine** sinnvolle Erweiterung mit ihrem verfügbaren KI-Modell bzw. gemeinsam am Beamer.

Jede Gruppe dokumentiert knapp:
1. **Wunsch aus Unterrichtssicht:** Was soll die App können und warum?
2. **Selbst formulierter Änderungs-Prompt:** Welche Funktion soll ergänzt werden, welche vorhandenen Teile müssen unberührt bleiben?
3. **Ergebnis:** Welche Änderung ist gelungen?
4. **Prüfung:** Mit welchem konkreten Test wurde sie fachlich und technisch bewertet?
5. **Korrektur:** Welcher Folgeprompt war nötig?

Die folgenden Aufgabenblätter enthalten deshalb **Anforderungen und Prüffälle**, keine fertig vorgegebenen Endlösungen. Hilfsprompts können bei Bedarf später zur Verfügung stehen. Eigene Änderungen werden lokal gespeichert; ein GitHub-Konto ist nicht erforderlich.

**Schutzregel für alle Aufgaben:** Die Simulationsformeln `calculateTransfers(state, settings)` und `advanceOneStep(state, settings)` aus V0.2 nur nach ausdrücklicher fachlicher Begründung ändern. Für A und B gilt bei jedem deterministischen Schritt:

```text
hin   = pForward * A_alt
rueck = pBackward * B_alt
A_neu = A_alt - hin + rueck
B_neu = B_alt + hin - rueck
A_neu + B_neu = M
```

## 2. Aufgabenkarte A: Abspielgeschwindigkeit

**Niveau:** Einstieg • ca. 15–25 Minuten, abhängig von Modell und Vorkenntnissen.

**Unterrichtsnutzen:** In der Anfangsphase soll der Prozess langsam verfolgt werden können; längere Läufe können beschleunigt werden.

**Anforderung:** Umschalter, beispielsweise **langsam – normal – schnell**, der sowohl den Abstand zwischen Modellschritten als auch die visuelle Dauer einer Kugelbewegung steuert. Die Raten `pForward`/`pBackward` bleiben ausdrücklich unverändert: **Abspieltempo ist nicht Reaktions-/Transportgeschwindigkeit des mathematischen Modells**.

**Prüffälle:**
- Drei Geschwindigkeitsstufen liefern nach derselben Schrittzahl exakt dieselben Bestände A/B.
- Während des Laufs umschalten; kein zweiter Timer, keine verlorenen Schritte.
- Pause hält Modell und animierte Kugeln an.
- Einzelschritt berechnet weiterhin genau einen Rechenschritt.
- Anzeige der gewählten Geschwindigkeit; lokal/offline weiter nutzbar.

**Technischer Hinweis:** V0.2 verwendet `setInterval(oneStep, settings.intervalMs)` und CSS-Animationen. Bei Geschwindigkeitswechsel muss der Timer sauber neu eingerichtet werden; auch die visuelle Dauer wird angepasst.

## 3. Aufgabenkarte B: Großansicht des Diagramms

**Niveau:** Einstieg bis mittel • ca. 20–30 Minuten.

**Unterrichtsnutzen:** Analyse der frühen, stufenförmigen Änderungen, insbesondere auf einem Notebook oder am Beamer.

**Anforderung:** Klick auf Diagramm oder einen ausdrücklich beschrifteten Knopf **„Diagramm vergrößern“** öffnet eine große, gut lesbare Ansicht (Dialog/Overlay oder Vollbildbereich), die geschlossen werden kann. Bestehende Ansichtsumschaltung **„Letzte 40 Schritte“ / „Volle Laufzeit“** muss erhalten bleiben.

**Prüffälle:**
- Vergrößern und Schließen ohne Änderung des Modellzustands oder der Historie.
- Nach mindestens 130 Schritten sind Anfangsphase und Stufenform in der Gesamtdarstellung erkennbar.
- Achsen, Legende und Menge in Modelleinheiten bleiben lesbar.
- Bedienung auch mit Tastatur möglich (Schließen-Knopf; idealerweise Esc).
- Kein neues Diagramm mit anderen Daten erzeugen; bestehende SVG-Grafik kann genutzt oder neu gerendert werden.

**Technischer Hinweis:** Die Diagrammzeichenfunktion heißt in V0.2 `renderStepChart()`. Die SVG-ID lautet `chart`.

## 4. Aufgabenkarte C: Datenexport

**Niveau:** Mittel • ca. 25–40 Minuten.

**Unterrichtsnutzen:** Mess-/Modelldaten für Tabellenkalkulation, Auswertung, Unterrichtsgespräch und Ergebnissicherung verfügbar machen.

**Anforderung:** **CSV-Export der vollständigen Historie** mit Simulationsschritt `n`, `A_n` und `B_n`; sinnvoll ergänzt durch berechnete Hin-/Rücktransporte sowie die verwendeten Anfangsparameter. Alle echten Rechenwerte sollen exportiert werden – nicht lediglich die auf zwei Dezimalstellen gerundeten Anzeigetexte.

**Vorschlag zur Kompatibilität mit deutschsprachigem Excel:** UTF-8 mit BOM, Semikolon als Feldtrennzeichen, Dezimalkomma konsistent verwenden; Alternativformat mit Punkt/Komma darf angeboten werden, muss jedoch klar beschriftet sein.

**Prüffälle:**
- Standardwerte: erste Zeilen n=0 mit A=50/B=0, n=1 mit A=47/B=3, n=2 mit A=44,3/B=5,7.
- Bei „Letzte 40 Schritte“ trotzdem **alle Daten seit n=0** exportieren.
- `A_n+B_n=M` für alle Zeilen, abgesehen von numerischer Rundung.
- CSV lässt sich in Excel/LibreOffice importieren.
- Es erfolgt kein Versand der Daten an einen Server.

**Klären:** Wie werden *Transporte für nächsten Schritt* versus *beim Übergang zum aktuellen Schritt ausgeführte Transporte* in der CSV beschriftet? In V0.2 werden die **nächsten erwarteten Transporte** in der Oberfläche angezeigt. Die Exportspalten müssen semantisch eindeutig sein.

## 5. Aufgabenkarte D: Grafikexport

**Niveau:** Mittel bis fortgeschritten • ca. 25–45 Minuten.

**Unterrichtsnutzen:** Diagramm in Arbeitsblätter, Protokolle, Präsentationen und Ergebnissicherung einfügen.

**Anforderung:** Diagramm mit Achsen und Legende als **SVG** herunterladen; optional zusätzlich PNG. Die aktuelle Ansicht (40 Schritte oder ganze Laufzeit) soll exportierbar sein. Ein SVG-Download ist als erstes Ziel sinnvoll, weil die Grafik bereits als SVG erstellt wird und ohne zusätzliche Bibliotheken übernommen werden kann.

**Prüffälle:**
- Export zeigt dieselben Daten wie die aktuell sichtbare Diagrammansicht.
- Beschriftungen, Achsen, Farben und Hintergrund sind im heruntergeladenen Bild enthalten.
- SVG lässt sich lokal öffnen und als Vektorgrafik einfügen.
- PNG-Export nur, wenn er in einer wirklich offlinefähigen Variante gelingt.
- Keine Mutation des Rechenkerns, keine externen Ressourcen.

## 6. Aufgabenkarte E: „Rauschen“ und Gleichgewichtsfluktuationen

**Niveau:** **Fortgeschrittene Forschungs-/Diskussionsaufgabe**; nicht verpflichtend im Februarworkshop.

Der Wunsch lautet: Wenn das **dynamische Gleichgewicht** erreicht ist, sollen geringe, wechselnde Verschiebungen A ↔ B sichtbar sein. Fachlich sind **zwei verschiedene Phänomene** zu unterscheiden:

### E1 – Simuliertes Messrauschen (leichtere Darstellungsaufgabe)

Kleine zufällige Schwankungen werden **nur der Darstellung einer Messgröße** überlagert und ausdrücklich als **„simuliertes Messrauschen“** bezeichnet. Der zugrunde liegende deterministische Rechenzustand `A_n/B_n` bleibt unangetastet. Das ist keine Behauptung, dass real die Gleichgewichtsmengen fluktuieren; es zeigt eine störungsbehaftete Messung. Eine Anzeige erst nach dem Erreichen eines Schwellenwerts wäre **eine vereinbarte Visualisierungsregel**, kein naturwissenschaftliches Gesetz.

**Prüfen:** Ein-/Ausschalten verändert Rohdaten, M, Gleichgewichtsmodell und CSV-Export **nicht**, sofern nicht ausdrücklich separate Messwerte exportiert werden.

### E2 – Echte stochastische Teilchenfluktuation (fachlich wertvoller, aber schwerer)

**Separater Simulationsmodus** mit einer ganzzahligen Teilchenpopulation `M`, `A`, `B`. Pro diskretem Zeitschritt werden die Hin- und Rückübergänge beispielsweise aus zwei **Binomialverteilungen** gezogen:

- `H ~ Binomial(A_alt, pForward)`
- `R ~ Binomial(B_alt, pBackward)`
- `A_neu = A_alt - H + R`, `B_neu = B_alt + H - R`

Beide Zufallsziehungen beruhen auf den **alten** Beständen. `A+B=M` bleibt bei jedem Schritt erhalten. Fluktuationen treten **nicht erst nach einem Umschaltzeitpunkt „Gleichgewicht erreicht“** auf, sondern sind für endliche Teilchenzahlen grundsätzlich während des gesamten Verlaufs möglich; nahe der stationären Verteilung werden sie besonders instruktiv. `E[H]=pForward*A`, `E[R]=pBackward*B`. Die stationäre *mittlere* Verteilung stimmt im einfachen Modell mit dem deterministischen Gleichgewicht überein, während die einzelnen Werte schwanken.

**Prüfen:** Die Modellart muss klar angezeigt werden. Die ursprüngliche Excel-Referenz bleibt als **deterministischer Modus** erhalten; der stochastische Modus ersetzt oder verfälscht diese Daten nicht. Einzelteilchen und die spätere Apfelvisualisierung können dann fachlich konsistent verknüpft werden.

**Entscheidungsempfehlung:** E1 kann als kritische Reflexionsaufgabe genutzt werden. **E2 ist die saubere Grundlage für die zukünftige Äpfel-Simulation**, sollte aber *nicht* ohne gesonderte fachliche Prüfung als schnelle Workshopänderung ausgegeben werden.

## 7. So verteilen wir Aufgaben bei heterogenen KI-Zugängen

| Gruppe | Empfehlung | Ziel |
|---|---|---|
| Kein eigener KI-Zugang | Partnerarbeit / gemeinsame zentrale Vorführung mit Aufgabenkarte A oder B | Anforderungen formulieren, Code prüfen, Ergebnisse testen |
| Kostenloses Basismodell | **A** oder **B**, ein klarer Auftrag | kleine stabile Erweiterung |
| Besseres Modell / Erfahrung | **C** und ggf. **D** | Datenverarbeitung, Export, didaktische Weiterarbeit |
| Fachlich und technisch fortgeschritten | **E** als Konzept- oder Zusatzprojekt | Modellkritik und zukünftiges stochastisches Modell |

Nicht die Zahl der Funktionen entscheidet über den Erfolg, sondern **ein nachvollziehbarer Mensch-KI-Dialog einschließlich Tests und Korrekturen**.

## 8. Versions- und Dokumentationsstrategie

- **V0.2 wird eingefroren** und als *erste funktionsfähige Rückfallversion* behalten.
- Jede Gruppe arbeitet in einer **eigenen lokalen Kopie**.
- Die Aufgaben **A–E sind noch keine neuen App-Versionen**.
- Wenn wir eine der Änderungen gemeinsam tatsächlich implementieren und testen, erhält sie einen **eigenen Versionsstand und Reproduktions-Prompt**, beispielsweise `V0_3.md`. Darin werden **Ausgangsstand, ursprüngliche Absicht, tatsächliche Korrekturschritte und Abnahmetests** dokumentiert.
- **Nächste Entwicklungsphase nach diesen kleinen Ergänzungen:** Apfelkrieg-Visualisierung (zuerst eigene Bilder/Story, dann optional stochastisches Einzelteilchenmodell), anschließend realitätsnaher Stechheber und abstrakter Vergleich.

