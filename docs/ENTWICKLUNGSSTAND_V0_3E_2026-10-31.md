# GLEICHGEWICHTS-LAB – Entwicklungsstand bis v0.3e

**Stand:** 31. Oktober 2026 · **Kontext:** Schulworkshop Februar 2027 (180 Minuten)  
**Status:** v0.3e nach iterativer fachlich-didaktischer Sichtprüfung als Zwischenstand akzeptiert. Kein abschließender V1-Abnahmetest.

## 1. Ziel und didaktische Leitidee

Vom **Apfelkrieg / der Fallobstschlacht** über die Analogie des **Stechheberversuchs** zum diskreten Modell eines reversiblen Vorgangs **A ⇄ B**: Teilnehmende sollen erkennen, dass im dynamischen Gleichgewicht die gegenläufigen Vorgänge weiterlaufen, obwohl die makroskopischen Mengen praktisch konstant sind. **Gleiche Raten bedeuten nicht gleiche Bestände.**

Die App ist eine **einzelne offlinefähige HTML-Datei**, ohne Server, externe Bibliotheken oder API-Schlüssel. Sie veranschaulicht drei verknüpfte Ansichten: **Geschichte**, **Modell**, **Vergleich**. Ihr Schwerpunkt liegt gegenwärtig auf Analogie und Mathematik; ein physikalisch geometrisch korrekt nachgebildeter Stechheber ist noch nicht implementiert.

## 2. Entwicklung in überprüfbaren kleinen Schritten

| Stand | Wesentliche Ergänzung |
| --- | --- |
| Mathematischer Prototyp v0.1 | Zwei Mengen/Zylinder, diskrete Modellschritte, Parameter, Start/Pause, Einzelschritt, Reset und Stufendiagramm. |
| Mathematischer Prototyp v0.2 | Bessere Gegenstromanzeige, gemeinsam skalierte Ratenbalken, Diagrammansicht „letzte 40 Schritte“ / „volle Laufzeit“; bewahrte Rückfallversion. |
| Story v0.1 | Fünf illustrierte Phasen mit Seiten- und Vogelperspektive; zunächst unabhängig von der Rechnung. |
| Integriert v0.1 | Gemeinsamer Rechenkern für Geschichte, Modell und Vergleich; Live-Werte in allen Ansichten. |
| Integriert v0.2 | Proportionale symbolische Vogelperspektive: insgesamt 60 Kreise in zwei quadratischen Gärten. |
| Integriert v0.3 / v0.3a | Vergleichsdarstellung weiterentwickelt; fortlaufende Kreispositionswechsel, kurze gelbe Hervorhebung und nahe Stationarität ein **rein bildlicher** ±1-Symbol-Puls. |
| Integriert v0.3b | Dynamische Symbolgärten auch im Vergleich, zweites synchrones Stufendiagramm und erste automatische Bildphasensteuerung. |
| **v0.3c → v0.3d → v0.3e** | Bildphasensteuerung nach *aktuellem Mengenanteil* statt Fortschritt zum Endwert; Phasengrenzen anhand der Einzel­schritte fachlich nachjustiert. **v0.3e ist der am 31.10. akzeptierte Stand.** |

## 3. Rechenmodell und Bezugswerte

Für jeden Schritt werden beide Transportmengen **aus denselben alten Beständen** berechnet:

- Hintransport: `H_n = p_hin · A_n`; Rücktransport: `R_n = p_rück · B_n`
- `A_(n+1) = A_n − H_n + R_n`
- `B_(n+1) = B_n + H_n − R_n = M − A_(n+1)`

Damit bleibt **A + B = M** konstant. Die Mengen sind kontinuierliche **Modelleinheiten (ME)**, keine ganzzahlig gezählten Äpfel. Beim **Apfelkrieg-Preset** gelten `M=50`, `A₀=50`, `B₀=0`, `p_hin=0,08`, `p_rück=0,04`. Daraus folgt die stationäre Verteilung **A*=16,67 ME, B*=33,33 ME**. Die ursprünglichen v0.2-Parameter bleiben als zweites Preset verfügbar.

Die App zeigt aktuelle Mengen, für den nächsten Schritt berechnete Gegenströme, die theoretische stationäre Verteilung und die stufenförmige Entwicklung. Hin- und Rücktransport können auch bei fast unveränderten Beständen weiter sichtbar sein.

## 4. Synchronisierung der Bilder in v0.3e

**Eine gemeinsame Funktion** wählt nach jedem Rechenschritt in **Geschichte und Vergleich** die Bildphase aus dem tatsächlichen Anteil `B/M`. Das gilt gleichermaßen für **Einzelschritt und automatischen Lauf**. In „Geschichte“ bleibt manuelles Blättern **zwischen** zwei Rechenschritten möglich. Ein neuer Rechenschritt synchronisiert wieder.

| Anteil B/M im Apfelkrieg-Preset | Bildphase / Bedeutung |
| --- | --- |
| Start oder unter 5 % | I – Ausgangssituation |
| 5 % bis unter 40,5 % | II – Der Junge beginnt |
| 40,5 % bis unter 43 % | III – Gegenoffensive |
| 43 % bis unter 63 % | IV – Noch kein Gleichgewicht |
| ab 63 %, bei beiden positiven Transportanteilen | V – Gleichgewichtsszene |

**Wichtige Kontrollpunkte:** 43 : 7, 37 : 13 und 30 : 20 bleiben in Phase II; die Gegenoffensive beginnt erst bei ungefähr **29 : 21**. Die Bildphase V erscheint um **18 : 32**. Die Schwellen wurden für die vorhandenen **fünf illustrativen Standbilder** abgestimmt und sind **kein allgemeines mathematisches Kriterium**.

**Fachlich unbedingt unterscheiden:** Die automatische **Bildphase V** bezeichnet die **annähernde dargestellte Endverteilung**, nicht schon exakt gleiche Gegenströme. Bei 18 : 32 ergeben sich im Preset beispielsweise `H=1,44` und `R=1,28` ME/Schritt. Die separate Status- und Ratenanzeige entscheidet über die rechnerische Annäherung an Stationarität. Die Einzeläpfel in den Bildern sind nicht exakt ausgezählte Modellteilchen.

## 5. Aktuelle Darstellungen und Modellgrenzen

- **Geschichte:** fünf Bilderpaare, Perspektivenwahl, Beobachtung/Fachfokus/Leitfrage und Live-Modellwerte.
- **Modell:** zwei Zylinder, animierte Transportkugeln, Zahlen/Raten, Stufendiagramm und zwei dynamische Symbolgärten.
- **Vergleich:** zugehörige Bildphase, dieselben 60 proportional gerundeten Bildsymbole, Zylinder, Gegenstromvergleich und synchrones Diagramm.
- **Visualisierungsregel:** Kreise können ihre Plätze trotz nahezu unveränderter Modellmenge tauschen; ein zeitweiliger ±1-Symbol-Puls nahe Stationarität betrifft **nur die Darstellung**, niemals die Rechnung oder das Diagramm.
- **Grenzen:** kein stochastisches Einzelteilchenmodell, keine reale Stechheber-Hydrodynamik und keine exakten Apfelzählungen in den Illustrationen. Bei deutlich abweichenden Anfangsparametern sind die fünf Bildszenen nur sinngemäß passend.

## 6. Für den Februar-Workshop griffbereit

**Vorgehen:** Mit einer funktionierenden Vorlage beginnen → didaktischen Verbesserungswunsch formulieren → kleine KI-gestützte Änderung → konkrete fachliche Tests → Korrektur und Reflexion. Nicht der Einmal-Prompt, sondern die nachvollziehbare Prüfung ist der Lerngegenstand. **Weder bezahlter KI-Zugang noch GitHub-Konto sind Voraussetzung.** Für heterogene Gruppen bleiben die vorbereiteten v0.2-Aufgabenkarten (Tempo, Diagramm-Großansicht, Daten-/Grafikexport, Modellkritik) geeignet.

**Mindestens prüfen:** Einzelschritt = genau ein Modellschritt; `A+B=M`; dieselben Ergebnisse im Automatik- und Einzelschrittmodus; gleiche Gegenströme ≠ gleiche Bestände; Bildphase V ≠ Nachweis eines exakt erreichten Gleichgewichts. Die konkrete Bildphasenfolge wurde in der gemeinsamen Sichtprüfung akzeptiert; ein vollständiger visueller Browser-, Mobil- und Offline-Doppelklick-Abnahmetest ist weiterhin sinnvoll.

**Referenzdateien:**
- [Aktueller Startstand im Repository](../index.html) · [archivierte integrierte v0.3e](../prototyp/integriert-v0.3e/index.html)
- [Entwicklungsjournal](ENTWICKLUNG.md) · [Fallobst-Konzept](FALLOBST_KONZEPT.md)
- [Workshop-Aufgaben v0.2](WORKSHOP_AUFGABEN_V0_2.md) · [Funktionsspezifikation V1](FUNKTIONSSPEZIFIKATION_V1.md)

**Nächster Schritt:** v0.4 ist geplant, aber **nicht** Bestandteil dieses dokumentierten und freigegebenen Zwischenstands.
