# Februar-Workshop 2027 – KI-gestützte App-Entwicklung am GLEICHGEWICHTS-LAB

**Dauer:** 180 Minuten, Präsenzfortbildung an der Schule.  
**Didaktische Leitfrage:** Wie entsteht aus einer schlichten Unterrichtsidee durch **eigene Anforderungen, KI-Unterstützung und fachliche Tests** eine brauchbare App?  
**Ziel:** Nicht die fertige V0.5 möglichst eindrucksvoll vorführen, sondern ein **überschaubares eigenes Entwicklungs- und Prüfverfahren** erfahren.

## Die zwei App-Rollen im Workshop

- **V0.5 – Referenz und Zielbild:** alle vier Module mit Stoffbeständen, Temperatur, Katalyse, Wasserentzug und Konzentrationskurven. Zur Demonstration und als Anlass für Modellkritik. **Nicht** gesamte 2,6-MB-HTML durch neue Gruppenprompt überschreiben lassen.
- **V0.2 – Starterprojekt für Gruppen:** [prototyp/integriert-v0.2/index.html](../prototyp/integriert-v0.2/index.html), offline als Kopie. Hat den bewusst einfacheren A↔B-Rechenkern. Der Starter muss vor dem Workshop auf konkrete vorgeschlagene Aufgaben geprüft werden. Alternativ die noch kleinere [prototyp/v0.2/index.html](../prototyp/v0.2/index.html) nutzen, falls große eingebettete Grafiken oder Modellkomplexität die Bearbeitung erschweren. *Zuvor anhand einer Probegruppe testen.*
- **Aufgabenkarten:** [WORKSHOP_AUFGABEN_V0_2.md](WORKSHOP_AUFGABEN_V0_2.md) für mögliche Programmieraufträge (Tempo, Diagramm, CSV, Grafikexport; stochastische Erweiterung nur als Diskussion). [MC-Arbeitsblatt V0.5](AUSWERTUNGSAUFGABEN_V0_5.md) als Beispiel *didaktischer Nutzungsaufgaben*, nicht als Pflicht-Erweiterung des Codes.

## 180-Minuten-Drehbuch

| Zeit | Phase | Aktivität / Produkt |
|---|---|---|
| 0–15 min | Einstieg | Die Fallobstschlacht zeigen: „Woran erkennst du, dass Gleichgewicht nicht Stillstand bedeutet?“ Erst Hypothesen sammeln, danach eine Modellrechnung laufen lassen. |
| 15–35 min | Vom Bild zur Mathematik | A↔B mit proportionalen Transfers, stationärer Verteilung und Gleichheit der Transporte vergleichen; dann am Chemie-Reiter den Unterschied von Q und K sichtbar machen. **Grenzen der Analogie explizit nennen.** |
| 35–50 min | Entwicklungsauftrag wählen | 2–3er-Teams wählen **eine** kleine Erweiterung des Starterprojekts, schreiben einen Erfolgstest **vor** dem KI-Prompt auf. Keine Lehrkraft benötigt bezahlte Modelle oder GitHub-Konto. |
| 50–90 min | KI-Iteration 1 | Eigenen Prompt eingeben, einzelne Änderungen der HTML-Datei lokal speichern, in einem Browser testen; Mensch bewertet fachliche Richtigkeit und Bedienung. |
| 90–100 min | Pause | Kurze Bildschirmpause; Zwischenstände sichern. |
| 100–130 min | Test und Korrektur | Vorab notierte Prüffälle durchführen; Fehler demonstrieren und **gezielte Folgeprompts** formulieren. Mathematische Invariante des A↔B-Rechenkerns explizit testen. |
| 130–155 min | Vergleich mit V0.5 | Nur ausgewählte Fachideen: Bruttoraten im Gleichgewicht, Katalysator verändert K nicht, Temperatur verändert K(T) etwas, Wasserentzug macht System offen. Eine MC-Szenariokarte als Demonstration von *Vorhersagen vor dem Klicken*. |
| 155–175 min | Kurzpräsentationen | Pro Team ca. 2 Minuten: Unterrichtswunsch, KI-Prompt, technische Änderung, **nachprüfbarer Test** und ein offener Modellvorbehalt. Bei vielen Teams exemplarisch 3–4 Gruppen. |
| 175–180 min | Transfer | Was könnte morgen im Unterricht eingesetzt werden? Ergebnisse lokal archivieren; keine spontane Veröffentlichung. |

## Vorbereitung durch die Workshopleitung

1. **Zwei lokale Offline-Dateien** für Vorführung (V0.5) und Gruppenarbeit (kleiner V0.2-Starter) vorab downloaden und per Doppelklick öffnen. Ohne Zugriff auf GitHub durch Teilnehmende. Die HTML-Dateien sind entsprechend ihrem jeweiligen Versionierungsstand zu prüfen.
2. Einen **komplett durchgespielten Referenzprompt** und einen bewusst fehlerhaften KI-Vorschlag mitbringen: z. B. neuer Geschwindigkeitsregler, der irrtümlich die Transferwahrscheinlichkeit mitändert.
3. Auf jedem Rechner einen gewöhnlichen Texteditor und Browser verfügbar haben; keine Entwicklungsumgebung erforderlich. Gruppenkopien stets unter **neuem Dateinamen** speichern.
4. Ein Einseiter pro Team: Ausgangszustand, konkreter Änderungswunsch, Nicht-Ändern-Regeln, Abnahmetest, Prompt, Korrektur, Schlussreflexion. Ausdrucke der [Aufgaben](WORKSHOP_AUFGABEN_V0_2.md) bereitlegen.
5. KI-Modelle bewusst heterogen nutzen; bei fehlendem Zugang **Partnerarbeit** und gemeinsame Beamer-Demonstration ermöglichen. Nichts hängt an einem bestimmten Anbieter.
6. V0.5 am Projektor (1920×1080, Browserzoom 90–100 %) sowie offline vorher prüfen. Zur Lehrdemonstration 60 °C einstellen, 20→60→80 vergleichen, Katalysator und D-Entzug einzeln schalten.
7. Keine Gesichter, Schülerdaten, Klassenlisten oder Zugangsschlüssel in externe KI-Prompts kopieren.

## Beispiel eines guten KI-Arbeitsauftrags

> Du erhältst eine bereits funktionierende einzelne HTML-Datei für den deterministischen A↔B-Transfer. Ergänze **nur** einen Umschalter langsam/normal/schnell, der die Abspielintervalle ändert, **nicht** die mathematischen Transferanteile. Die Funktion `calculateTransfers` und die Invariante `A+B=M` müssen unverändert bleiben. Gib die kleinste nachvollziehbare Änderung an, beschreibe die betroffenen Stellen und nenne mindestens drei Browsertests. Prüfe speziell Start/Pause, Einzelschritt und Umschalten bei laufender Simulation.

**Korrigierender Folgeprompt (Beispiel):** „Nach Geschwindigkeitswechsel entstehen zwei Timer und die Menge wird zu schnell verändert. Analysiere nur den Timer-Lebenszyklus; ändere nicht die mathematischen Rechenfunktionen. Gib eine reproduzierbare Prüffolge für 100 Schritte.“

## Vier Kriterien der erfolgreichen Gruppe

- **Fachlich:** Kein erfundener Mechanismus; Transfers/Konzentrationen korrekt.
- **Technisch:** Lokale HTML läuft, Pause/Reset/Einzelschritt und ein konkreter Grenzfall funktionieren.
- **Didaktisch:** Eigener Lerngewinn gegenüber der Ausgangsversion.
- **Mensch–KI-Zusammenarbeit:** Eigener Wunsch, Prompt, Prüfung, Korrektur und kritische Reflexion sind dokumentiert.

## Was ausdrücklich nicht zum Pflichtprogramm gehört

Keine Neuerstellung der vollständigen V0.5, keine statistisch exakte Teilchenmodellierung, kein Google/GitHub-Login, kein verpflichtendes Publizieren, keine vollständige thermodynamische Modellierung. Komplexität der Referenzversion und Komplexität des Starterprojekts bewusst trennen.

## Ausblick auf Linz 2027

Für einen 200-Minuten-VCÖ-Workshop kann derselbe Ablauf um einen 20-Minuten-Block erweitert werden: **Gegenüberstellung von Simulation und Experiment** (realer Stechheber, fachlicher Modellfehler, reale Esterbildung). Die pädagogische Hauptaussage bleibt: **erst eigene Hypothese und eigener Test, dann KI-Auswertung und Korrektur.**
