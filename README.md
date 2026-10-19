# GLEICHGEWICHTS-LAB

**Vom Apfelkonflikt über den Stechheberversuch zum dynamischen chemischen Gleichgewicht**

Dieses Repository gehört zum Projekt **CHEMIE mit KI**. Ziel ist eine browserbasierte, lokal ausführbare Lernumgebung, in der drei Repräsentationsebenen **synchron verglichen** werden können:

- **Fallobstschlacht / Apfelkonflikt:** intuitive Analogie für beständigen Hin- und Rücktransport.
- **Stechheberversuch:** diskreter Flüssigkeitstransport zwischen zwei Gefäßen.
- **Abstraktes Modell:** einfacher reversibler Prozess \`A ⇄ B\` mit Mengen- und Geschwindigkeitskurven.

## Aktueller Stand

**Erster Prototyp V0.1 implementiert, lokal ausführbar; noch keine veröffentlichte oder vollständig abgenommene V1.**

Die erste Version wird bewusst klein gehalten: eine einzelne \`index.html\` ohne externe Abhängigkeiten, die lokal per Doppelklick im Browser ausgeführt werden kann. Der Workshop soll an einem geprüften Starterprojekt zeigen, wie eine Lehrkraft zusammen mit KI eine eigene didaktische Verbesserung entwickelt.

## Dokumentation

- [Entwicklungsjournal und Konzeptstand](docs/ENTWICKLUNG.md) – Ausgangsidee, Mathematik, Darstellungsformen, didaktische Entscheidungen, Rückfallkonzept und offene Punkte.
- [**Funktionsspezifikation V1**](docs/FUNKTIONSSPEZIFIKATION_V1.md) – verbindlicher Umfang für den workshopfähigen Kern, Rechenmodell, synchrone Visualisierungen, Offlinebetrieb und 16 Abnahmetests.
- [**Reproduktions-Prompt V0.1**](docs/PROMPTS/V0_1.md) – vollständiger Prompt, Prüfbeispiele und kleinere KI-Entwicklungsschritte.

## Prototyp V0.1

- [**Offline-App als `index.html`**](prototyp/v0.1/index.html) – lokal herunterladen, per Doppelklick öffnen.
- Frei wählbare Gesamtmenge **M = 10–200 ME (Zehnerschritte)**, anfängliche Verteilung **A₀ 0–M**, B₀=M−A₀, Hin-/Rückanteile und Reset.
- Zwei Modellzylinder, diskrete Stufenlinien, symbolische Gegenströme, Start/Pause/Einzelschritt.
- Der Prompt ist **eine Anleitung zur funktionalen Reproduktion**, kein Anspruch auf bitidentischen KI-Code und kein Protokoll eines Ein-Prompt-Erfolgs.

## Einsatz in Fortbildungen

- **Februar 2027:** 180-minütiger Schulworkshop zur KI-gestützten App-Entwicklung.
- **1. April 2027:** 200-minütiger Workshop beim VCÖ-Kongress in Linz.
- **2. April 2027:** »CHEMIE mit KI«-Vortrag, ca. 16 Uhr.

**Leitentscheidung:** Weder ein bezahlter KI-Zugang noch ein GitHub-Konto sind Voraussetzung für die Teilnahme. GitHub-Veröffentlichung wird gegebenenfalls in einem separaten kurzen Onlinekurs behandelt.

## Geplante Entwicklungsstufen

1. **V1:** Diskretes Zwei-Mengen-Modell, Parameter, Einzelschritt, Start/Pause, Reset, Balken und einfache Diagramme.
2. **V2:** Synchrone Visualisierung von Äpfeln, Stechheber und Modell, Aufgaben und Ergebnissicherung.
3. **V3:** Stochastisches Modell, komplexere Gleichgewichte und Le Chatelier.

**Hinweis:** Die bisherige \`EQUILIB.xlsm\`-Ausgangsdatei und Bilder/Videos sind noch **nicht** in diesem Repository abgelegt. Nutzungsrechte an externen Abbildungen sind vor einer eventuellen Veröffentlichung zu klären.
