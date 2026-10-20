# GLEICHGEWICHTS-LAB

**Vom Apfelkonflikt über den Stechheberversuch zum dynamischen chemischen Gleichgewicht**

Dieses Repository gehört zum Projekt **CHEMIE mit KI**. Ziel ist eine browserbasierte, lokal ausführbare Lernumgebung, in der drei Repräsentationsebenen **synchron verglichen** werden können:

- **Fallobstschlacht / Apfelkonflikt:** intuitive Analogie für beständigen Hin- und Rücktransport.
- **Stechheberversuch:** diskreter Flüssigkeitstransport zwischen zwei Gefäßen.
- **Abstraktes Modell:** einfacher reversibler Prozess \`A ⇄ B\` mit Mengen- und Geschwindigkeitskurven.

## Aktueller Stand

**Prototypen V0.1, V0.2, Story V0.1 und die integrierte Version V0.1 sind implementiert. Die vollständige V1-Abnahme steht noch aus.**

Die erste Version wird bewusst klein gehalten: eine einzelne \`index.html\` ohne externe Abhängigkeiten, die lokal per Doppelklick im Browser ausgeführt werden kann. Die integrierte Fassung enthält die bereits freigegebenen Story-Bilder direkt in der HTML-Datei. Der Workshop soll an einem geprüften Starterprojekt zeigen, wie eine Lehrkraft zusammen mit KI eine eigene didaktische Verbesserung entwickelt.

## Dokumentation

- [Entwicklungsjournal und Konzeptstand](docs/ENTWICKLUNG.md) – Ausgangsidee, Mathematik, Darstellungsformen, didaktische Entscheidungen, Rückfallkonzept und offene Punkte.
- [**Funktionsspezifikation V1**](docs/FUNKTIONSSPEZIFIKATION_V1.md) – verbindlicher Umfang für den workshopfähigen Kern, Rechenmodell, synchrone Visualisierungen, Offlinebetrieb und 16 Abnahmetests.
- [**Reproduktions-Prompt V0.1**](docs/PROMPTS/V0_1.md) – vollständiger Prompt, Prüfbeispiele und kleinere KI-Entwicklungsschritte.
- [**Workshop-Aufgaben auf Basis V0.2**](docs/WORKSHOP_AUFGABEN_V0_2.md) – Abspieltempo, Diagramm-Großansicht, CSV-/SVG-Export und didaktisch saubere Unterscheidung von Messrauschen und Teilchenfluktuationen.
- [**Fallobstschlacht – Konzept und Storyboard**](docs/FALLOBST_KONZEPT.md) – fünf Phasen, Bildsprache, Zuordnung der Figuren zum Modell, Story-Preset und spätere Integration. Enthält auch einen Konzept-Prompt für die Gestaltung.

## Prototyp V0.1

- [**Offline-App als `index.html`**](prototyp/v0.1/index.html) – lokal herunterladen, per Doppelklick öffnen.
- Frei wählbare Gesamtmenge **M = 10–200 ME (Zehnerschritte)**, anfängliche Verteilung **A₀ 0–M**, B₀=M−A₀, Hin-/Rückanteile und Reset.
- Zwei Modellzylinder, diskrete Stufenlinien, symbolische Gegenströme, Start/Pause/Einzelschritt.
- Der Prompt ist **eine Anleitung zur funktionalen Reproduktion**, kein Anspruch auf bitidentischen KI-Code und kein Protokoll eines Ein-Prompt-Erfolgs.

## Prototyp V0.2 – Änderungen vom 19.10.2026

- [**Aktuelle V0.2 als `index.html`**](prototyp/v0.2/index.html) – Kugelgröße proportional zur Transportmenge (symbolisch), Diagrammschalter **„Letzte 40 Schritte“ / „Volle Laufzeit“**, zwei vertikale Transportbalken auf gemeinsamer Skala.
- [**Änderungs-Prompt V0.2**](docs/PROMPTS/V0_2.md) – reproduzierbare Änderungsbeschreibung, Testfälle und getrennte Aufgaben für schwächere KI-Modelle.
- V0.1 bleibt unverändert für den Vorher-Nachher-Vergleich. V0.2 ist **getesteter Prototyp und erste gesicherte Workshop-Rückfallversion**; noch nicht die abschließend abgenommene V1. Workshop-Änderungen erfolgen nur in eigenen Kopien.


- [**Bildserie Fallobst – Freigabestand I–V**](docs/BILDSERIE_ABNAHME_19_10_2026.md) – alle fünf Bildentwürfe gestalterisch freigegeben; Zuordnung, Modellgrenzen und nächste Implementierungsschritte.
- [**Bildserie Phase I – frühere Prüfung und Korrektur-Prompt**](docs/BILDSERIE_PHASE_I.md) – dokumentiert den früheren, noch fehlerhaften Erstentwurf und die nötige Korrektur.

## Erste integrierte Story-Ansicht V0.1

- [**Story V0.1 – selbstständige HTML-Datei**](prototyp/story-v0.1/index.html): fünf Phasen, einheitliche Seiten-/Vogelperspektiven, drei Reiter **Geschichte / Modell / Vergleich**; offline und ohne zusätzliche Dateien ausführbar. **Noch keine mathematische Modellkopplung**.
- [**Prompt für Story V0.1**](docs/PROMPTS/STORY_V0_1.md) und [Entwicklungsjournal](docs/ENTWICKLUNG.md) dokumentieren den Übergang von der Bildergalerie zur ersten integrierten Ansicht.
- **V0.2 bleibt unverändert** als funktionsfähige mathematische Rückfallebene.

## Integrierter Prototyp V0.1 – 20. Oktober 2026

Die erste **funktionierende Brücke zwischen Bildergeschichte und Rechenkern V0.2** ist verfügbar:

- [**Integrierte Offline-App**](prototyp/integriert-v0.1/index.html): **eine selbstständige HTML-Datei** mit allen zehn eingebetteten Bildausschnitten und dem gemeinsamen Rechenkern.
- [**Entwicklungs-Prompt und Tests**](docs/PROMPTS/INTEGRIERT_V0_1.md): Ausgangsanforderungen, fachliche Grenzen, durchgeführte Browserprüfungen und dokumentierte Korrekturen.
- **Geschichte / Modell / Vergleich**: ein gemeinsamer Rechenschritt, gemeinsame Parameter und Live-Zahlen bei jedem Wechsel.
- **Apfelkrieg-Vorgabe:** M=50 ME, A₀=50, p_hin=0,08, p_rück=0,04; zusätzlich ursprüngliches V0.2-Preset verfügbar.
- **Didaktische Grenze:** Die fünf Bilder bleiben **statische narrative Szenen**. Die gezeichneten Einzeläpfel und die Auswahl einer Bildphase werden **noch nicht automatisch** vom Modellzustand gesteuert. Die daneben gezeigten Werte stammen tatsächlich aus dem gemeinsamen Rechenkern.
- Die ursprüngliche [V0.2](prototyp/v0.2/index.html) bleibt **unverändert** als erste Rückfallversion.

Die App läuft ohne externes Skript oder Server; zur ersten Prüfung wurde sie in Chromium isoliert geladen und interaktiv getestet. Ein lokaler Doppelklick-Test auf einem Nutzer-PC bleibt sinnvoll.

## Einsatz in Fortbildungen

- **Februar 2027:** 180-minütiger Schulworkshop zur KI-gestützten App-Entwicklung.
- **1. April 2027:** 200-minütiger Workshop beim VCÖ-Kongress in Linz.
- **2. April 2027:** »CHEMIE mit KI«-Vortrag, ca. 16 Uhr.

**Leitentscheidung:** Weder ein bezahlter KI-Zugang noch ein GitHub-Konto sind Voraussetzung für die Teilnahme. GitHub-Veröffentlichung wird gegebenenfalls in einem separaten kurzen Onlinekurs behandelt.

## Geplante Entwicklungsstufen

1. **V1:** Diskretes Zwei-Mengen-Modell, Parameter, Einzelschritt, Start/Pause, Reset, Balken und einfache Diagramme.
2. **V2:** Synchrone Visualisierung von Äpfeln, Stechheber und Modell, Aufgaben und Ergebnissicherung.
3. **V3:** Stochastisches Modell, komplexere Gleichgewichte und Le Chatelier.

**Hinweis:** Die bisherige \`EQUILIB.xlsm\`-Ausgangsdatei und externe Videos sind noch **nicht** im Repository abgelegt. Die akzeptierten KI-generierten Story-Bilder liegen eingebettet in den Story- und Integrations-HTML-Dateien; externe Buchabbildungen werden nicht übernommen. Nutzungsrechte an externen Abbildungen sind vor einer eventuellen Veröffentlichung zu klären.
