# CHEMIE mit KI / GLEICHGEWICHTS-LAB
## Verbindliche Übergabe in einen neuen Chat

**Stand: 20. Oktober 2026**  
**Projekt-Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB  
**Branch:** `main`  
**Zweck:** Fortsetzung der bereits weit fortgeschrittenen gemeinsamen Entwicklung ohne wiederholtes Neuerklären der Ziele, der bisherigen Entscheidungen und der tatsächlichen GitHub-Dateien.

> **Empfohlener Einstieg im neuen Chat:**  
> „Bitte lies diese Übergabe und prüfe den aktuellen Stand im GitHub-Repository `ekerzendorfer/EQUILIB_LAB`, Branch `main`. Knüpfe unmittelbar an die *Integrierte V0.1* vom 20.10.2026 an. Wir entwickeln in kleinen, fachlich geprüften Schritten und dokumentieren jede neue Version mit Entwicklungs-Prompt und Tests im Repository. Die funktionierende V0.2 und andere ältere Fassungen nicht überschreiben.“

---

## 1. Gesamtzusammenhang: CHEMIE mit KI und Fortbildungen

Das Projekt **CHEMIE mit KI** umfasst browserbasierte, möglichst kostenfreie Lernwerkzeuge, virtuelle Chemielabore, interaktive Simulationen und Messwertauswertung für SEK I und SEK II. Das Applikationsportal liegt unter:

- https://ekerzendorfer.github.io/CHEMIE_KI_LINKS/

Die aktuelle App-Entwicklung **GLEICHGEWICHTS-LAB** dient sowohl dem Unterricht als auch als authentisches Beispiel für eine **KI-unterstützte Entwicklung durch Lehrkräfte**.

Anlässe:

- **Februar 2027:** Workshop an der Schule des Nutzers, ca. **180 Minuten**. Teilnehmende mit höchst unterschiedlichen KI-Zugängen; eventuell ohne eigenen KI-Zugang. Hier soll anhand des Stechheberversuchs und der Fallobstschlacht ein kleines Unterrichtswerkzeug mit KI entwickelt bzw. sinnvoll erweitert werden.
- **1. April 2027:** VCÖ-Kongressworkshop in Linz, **200 Minuten**, ebenfalls praxisorientiert.
- **2. April 2027, ca. 16 Uhr:** **30-minütiger Kongressvortrag „CHEMIE mit KI“**. GLEICHGEWICHTS-LAB illustriert den Mensch-KI-Entwicklungsdialog. Weitere Vortragsteile: reales Brausetabletten-Kinetikexperiment mit WAAGE_LAB, vernetztes digitales Analytiklabor sowie ein geplanter wirklich nützlicher **KI-Laborassistent**.

Grundbotschaft des Vortrags: Die Lehrkraft liefert chemische und didaktische Ideen, definiert Anforderungen, testet, korrigiert und verantwortet das Ergebnis. KI hilft bei Programmierung, Gestaltung, Auswertung und Planung. Ein scheinbarer „Ein-Prompt-Zauber“ darf als kurze dramaturgische Inszenierung erscheinen, wird danach aber **ausdrücklich als Ergebnis vieler Iterationen aufgeklärt**.

---

## 2. Didaktische Leitidee des GLEICHGEWICHTS-LAB

**App-Name:** GLEICHGEWICHTS-LAB  
**Leitsatz:** *Vom Apfelkrieg über den Stechheber zum dynamischen chemischen Gleichgewicht.*

Drei verschiedene Repräsentationsebenen sollen langfristig vergleichbar oder synchron sichtbar sein:

1. **Fallobstschlacht / Apfelkrieg** nach Dickerson/Geiss: Zwei Nachbarn werfen Äpfel über einen Zaun. Das Verhältnis der Mengen hängt von den Geschicklichkeiten bzw. Transportanteilen ab; der Austausch läuft im Gleichgewicht weiter.
2. **Stechheberversuch:** Reales diskretes Hin- und Hertransportieren von Flüssigkeitsvolumina zwischen zwei Gefäßen. Die Volumina und Flüssigkeitsstände verändern sich stufenweise.
3. **Abstraktes Modell:** reversibler Prozess `A ⇄ B`, Darstellung der Mengen, beider Teilraten, des Annäherungsverlaufs und der stationären Verteilung.

Didaktisches Alleinstellungsmerkmal: **Überblendung der drei Niveaus**. Insbesondere sollen auf einem Bildschirm zwei Zylinder mit wechselnden Flüssigkeitsständen, **Stufen- bzw. Balkendiagramme der diskontinuierlichen Entwicklung** und **weiterhin in beide Richtungen fliegende Kugeln/Äpfel im stationären Zustand** sichtbar sein.

Zentrale fachliche Aussagen:

- **Gleiche Mengen** bedeuten *nicht* notwendigerweise Gleichgewicht.
- **Gleiche gegenläufige Transportraten** können zu **ungleichen stationären Beständen** gehören.
- „Dynamisches Gleichgewicht“ bedeutet **fortlaufenden Hin- und Rückprozess**, nicht Stillstand.
- Bei einer **stochastischen Einzelteilchen-Simulation** sind Schwankungen schon während der gesamten Entwicklung möglich; sie beginnen nicht erst künstlich im Gleichgewicht.
- Der reale Stechheber, die Apfelgeschichte und eine chemische Gleichgewichtsreaktion sind **unterschiedliche Modellierungen**, nicht uneingeschränkt physikalisch identische Prozesse. Grenzen der Analogien müssen sichtbar werden.

---

## 3. Mathematischer Rechenkern und feste Prüffälle

Ausgangsbasis war die ältere Excel-Simulation `EQUILIB.XLS`, danach die aktualisierte Datei **`EQUILIB.xlsm`** (u. a. Tabellen `Eingabe`, `Zahlenwerte`, `Grafik 30`, `Grafik 50`). Das diskrete deterministische Modell lautet:

```text
H_n = p_hin  · A_n
R_n = p_rück · B_n

A_(n+1) = A_n - H_n + R_n
B_(n+1) = B_n + H_n - R_n

M = A_n + B_n = konstant
```

Die beiden Transportraten **werden gleichzeitig aus dem Zustand vor dem Schritt** berechnet. Die App zeigt die **für den nächsten Schritt aus den momentanen Beständen berechneten** Hin-/Rücktransporte an.

**Originaler Referenzfall:**

- `M=50`, `A₀=50`, `B₀=0`, `p_hin=0,06`, `p_rück=0,04`.
- Nach Schritt 1: **A=47, B=3**.
- Nach Schritt 2: **A=44,30, B=5,70**.
- Stationäre Modellwerte: **A*=20, B*=30**; Quotient `B*/A*=1,5`.

**Separates Apfelkrieg-Preset:**

- **A = Junge links**, **B = älterer Nachbar rechts**.
- `M=50`, `A₀=50`, `B₀=0`, `p_hin=0,08` (Junge), `p_rück=0,04` (Nachbar).
- Nach Schritt 1: **A=46, B=4**.
- Stationär: **A*≈16,67, B*≈33,33**; auf der Seite des langsameren Nachbarn liegt doppelt so viel.
- Die beiden positiven Teilraten sind im stationären Grenzwert gleich groß.

Gesamtmenge **10 bis 200 Modelleinheiten (ME)** in Zehnerschritten wählbar; Anfangsanteil A von 0 bis M; B=M−A. Die kontinuierlichen Modelleinheiten dürfen **nicht** mit exakt ganzzahlig gezählten Einzeläpfeln verwechselt werden.

Anmerkung zum realen Stechheber: Eine physikalisch genaue Abbildung auf Zylinderquerschnitte, Stechheber-Geometrie und Volumentransfers muss gesondert geprüft werden.

---

## 4. Erprobte Programmstände im GitHub-Repository

### 4.1 Mathematischer Prototyp V0.1 – erster Kern

https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/prototyp/v0.1/index.html

- Einzelne lokal ausführbare `index.html` (HTML, CSS, Vanilla JavaScript).
- Modell A ⇄ B, Eingabe Gesamtbestand, Anfangsverteilung, beide Transportanteile.
- Zwei Modellzylinder, stufiges Diagramm, gegenläufige Transportsymbole.
- Start/Pause, Einzelschritt, Reset.

Reproduktions-Prompt:
https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/PROMPTS/V0_1.md

### 4.2 Mathematischer Prototyp **V0.2 – UNVERÄNDERTER RÜCKFALLSTAND**

https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/prototyp/v0.2/index.html

Vom Nutzer ausführlich getestet und als **erste gesicherte Workshop-Rückfallversion** positiv abgenommen. **Bitte nicht überschreiben.**

Gegenüber V0.1:
- Eine symbolische Kugel je Transportrichtung, in ihrer Größe näherungsweise nach Transportmenge skaliert.
- Zwei zusätzliche farblich passende **vertikale Transportbalken** mit gemeinsamem Maßstab.
- Diagrammschalter zwischen **„Letzte 40 Schritte“** und **„Volle Laufzeit“**, sodass die interessante Anfangsphase später wieder sichtbar wird.
- Die Kugeln transportieren schematisch einen Fluss; keine echte stochastische Einzelteilchenanimation.

Prompt:
https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/PROMPTS/V0_2.md

### 4.3 Story V0.1 – reine Bildergeschichte / App-Oberfläche

https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/prototyp/story-v0.1/index.html

- Alle fünf angenommenen Fallobstbilder als eingebettete, optimierte Bildausschnitte.
- Reiter **Geschichte / Modell / Vergleich**.
- Fünf Phasen mit Navigation, Erläuterungen, Fragen; Umschaltung **Gesamtbild / Seitenansicht / Vogelperspektive**.
- Der Reiter „Modell“ war in dieser Fassung noch ein Platzhalter, der Vergleich qualitativ; **keine quantitative Kopplung**.
- Uneinheitliche Bildtrennungen, insbesondere die **doppelte weiße Trennlinie in Phase III**, wurden beim Übergang zu Story V0.1 durch korrektes Ausschneiden und neu zusammengesetzte Ansichten behoben.

Prompt:
https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/PROMPTS/STORY_V0_1.md

### 4.4 **AKTUELL: Integriert V0.1 – 20. Oktober 2026**

https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/prototyp/integriert-v0.1/index.html

**Diese Datei ist tatsächlich im Branch `main`.** Am 20.10. wurde sie über GitHub-Dateireferenz geprüft; ihr Blob-SHA lautet:

`1682b2303aec2d2e05e0f6546d4a995ce2c85803`

Die rund **2,56 MB große, selbstständige HTML-Datei** mit Bildern ist damit nicht nur als Gesprächsartefakt, sondern tatsächlich im Repository gespeichert.

**Umgesetzte Verbindung:**
- Ein einziger bewährter Rechenkern aus V0.2 mit Modellzustand `state`, eine gemeinsame Steuerung und Historie.
- **Geschichte:** Phasen I–V, beide Bildperspektiven und **Live-Mengen/Transportraten**.
- **Modell:** Zylinder, Transportkugeln/-balken und Stufendiagramm aus V0.2.
- **Vergleich:** gewählte Bildphase und **aktuelle echte Modellwerte** nebeneinander, einschließlich Teilraten und didaktischer Deutung.
- **Story-Preset** 50/0, 0,08/0,04 sowie Schalter für ursprüngliche **V0.2-Werte** 50/0, 0,06/0,04.
- Phasennavigation und Modelllauf bleiben **voneinander unabhängig**. Wechsel des Reiters verändert die Zahlen und Historie nicht.
- Bedienung Start/Pause/Einzelschritt/Reset, freie Modellparameter, Diagrammumschaltung.
- Offlinefähig und ohne externe Laufzeitabhängigkeiten.
- Ein UI-Kontrastfehler eines aktiven Reiters und ein Textformatierungsrest wurden bereits korrigiert.

**Browserprüfungen (Chromium/Playwright) erfolgreich:**
- Anfang Story-Preset A=50, B=0, H=4, R=0.
- Nach Schritt 1 A=46, B=4.
- Wechsel zwischen Geschichte, Modell, Vergleich ohne Zustandsverlust.
- Phasenwahl ohne Änderung der mathematischen Daten.
- Start/Pause, beide Presets, Vogelperspektive und Diagramme.
- Mobile Breite 390 px ohne horizontalen Überlauf.
- Keine JavaScript-Laufzeitfehler bei den geprüften Abläufen.

**Noch nicht durchgeführt:** manueller Test durch Öffnen der HTML-Datei per Doppelklick auf dem Rechner des Nutzers und längere Unterrichtserprobung.

**Wichtige aktuelle Grenze:**
Die fünf Szenen sind weiterhin **statische narrative Bilder**. Die Bildäpfel und die gezeichneten Flugobjekte verändern sich **noch nicht** mit dem Modellzustand. Nur die **danebenstehenden Live-Mess-/Modellwerte** sind synchron. Bildphase ≠ Simulationsschritt. Bei freier Parameterwahl sind die fünf narrativen Phasen nicht automatisch universell gültig.

Reproduktions-/Änderungs-Prompt:
https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/PROMPTS/INTEGRIERT_V0_1.md

---

## 5. Die fünf Phasen und ihre visuelle Grundlage

Alle **fünf KI-generierten Bilder wurden vom Nutzer ausdrücklich akzeptiert** (19.10.2026). Gestalterische Kennzeichen:

- Oben eine **Seitenansicht**, darunter eine **Vogelperspektive** mit gut sichtbarer Apfeldichte.
- Junge links (A), älterer Mann rechts (B), durchgehend gleicher Garten/Zaun/Baum, wiedererkennbare Figuren, freundlicher moderner Illustrationsstil.
- **Keine Vorratskisten**, keine Äpfel-Nachlieferung während des Modelllaufs, keine fest eingebauten Modellzahlen.
- Der erste Phase-I-Entwurf enthielt fälschlicherweise Äpfel im Nachbargarten; die akzeptierte Neufassung zeigt B=0.
- Die Trennung der Perspektiven wurde für die App **einheitlich** gestaltet und ein zusätzlicher weißer Strich in Phase III beseitigt.
- Die angenommenen Bilder sind **gestalterisch freigegeben**, noch keine quantitativ exakten Simulationszustände.

**Bildphasen:**

| Phase | Erzählerische Funktion | Chemisch-didaktische Aussage |
|---|---|---|
| I | Ausgangslage: Äpfel links, rechts leer | Anfangsverteilung |
| II | Der Junge beginnt zu werfen | Hintransport dominiert |
| III | Der Nachbar wirft zurück | Beide Prozesse parallel |
| IV | Ungefähr gleiche Apfelzahlen | Noch kein Gleichgewicht, da Teilraten verschieden |
| V | Rechts mehr Äpfel, beidseitiger Wurf | Gleiche positive Teilraten, makroskopisch konstante Verteilung |

Referenzdokumentation:
- https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/FALLOBST_KONZEPT.md
- https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/BILDSERIE_ABNAHME_19_10_2026.md

Die akzeptierten Bilder sind in den Story-/Integrations-HTML-Dateien eingebettet. **Einzelbilder** sind nicht als separate Dateien im GitHub-Repository abgelegt. Bei späterer Asset-Arbeit können sie aus den vorhandenen lokalen Originalen oder dem damaligen Bild-ZIP geholt werden, falls im neuen Chat vorhanden, sonst aus dem Repository-HTML extrahiert werden.

**Wichtige Materialien / Quellen:**
- Dickerson/Geiss, *Chemie – eine lebendige und anschauliche Einführung*, Apfelkrieg/Fallobstschlacht (ursprüngliche Bilder im Gespräch).
- https://van-der-waals.pc.uni-koeln.de/angewandte-chemiedidaktik/kinetik-und-chemisches-gleichgewicht/apfelkonflikt-20
- https://van-der-waals.pc.uni-koeln.de/angewandte-chemiedidaktik/kinetik-und-chemisches-gleichgewicht/stechheberversuch
- https://chemiedidaktik.uni-wuppertal.de/de/digitale-medien/videos-zu-klassischen-schulversuchen/allgemeine-chemie-i-anorganische-chemie/der-stechheberversuch/
- http://www.unterrichtsmaterialien-chemie.uni-goettingen.de/exp_neu.php?id=2150
- https://www.youtube.com/watch?v=8XzgpEN2bDw

Für öffentliche Anwendungen **eigenständig erzeugte Bilder**, nicht die historischen Buchzeichnungen ohne Lizenzprüfung übernehmen.

---

## 6. Nächste Entwicklungsphase: woran wir exakt anknüpfen

**Unmittelbarer nächster Schritt:** Nutzer soll **Integriert V0.1 lokal öffnen und ansehen**. Besonders die fachliche Plausibilität des Vergleichsmodus und die Verständlichkeit der parallelen Live-Zahlen prüfen.

Erst nach positivem Feedback die **dynamische Kopplung der Apfelverteilung** angehen.

### Empfohlene kleine Etappen für den nächsten Chat

1. **Architektur prüfen:** Die aktuellen Bilder enthalten viele Äpfel *fest* im Hintergrund. Einfach weitere Äpfel darüberzuzeichnen würde die angezeigten Bestände optisch verfälschen. Deshalb zunächst eine **ausreichend neutrale Hintergrundschicht** für Seiten-/Vogelansicht entwerfen, ohne Äpfel oder nur mit unverwechselbar dekorativen Baumfrüchten.
2. **Modellgesteuerte Apfeldichte in der Vogelperspektive:** Ein Overlay aus Punkten/Apfelsymbolen/Clustern mit Mengenverhältnis proportional zu A/M und B/M. Maßstab und Flächen müssen klar definiert sein. Die Excel-Modelleinheiten sind kontinuierlich; die Grafik kann proportional und symbolisch sein, muss aber die Genauigkeit transparent machen.
3. **Erst dann Seitenansicht und Transportbewegungen** an denselben Modellzustand koppeln (je ein klarer Hin- und Rücktransportsymbolstrom, auch bei praktisch stationären Mengen).
4. **Gegenprüfung:** Nach jedem Schritt A+B=M, keine unerklärten zusätzlichen Äpfel, keine divergent laufenden Zustände bei Reiter- oder Bildwechsel, die bestehende V0.2-Formel unverändert.
5. **Optional später:** Stochastischer Einzelapfelmodus mit ganzzahliger Population und binomialen Übergängen; nicht mit dem deterministischen Modell vermischen.

**Nie ungefragt den gesamten Ausbau bis Le Chatelier in einem Schritt programmieren.** Kleine getestete Versionen mit Nutzerfeedback.

---

## 7. Geplante Workshop-Aufgaben – derzeit nur Aufgabenkarten

Auf Basis des mathematischen Rückfallstands **V0.2** (nicht automatisch Teil jeder nächsten Releaseversion):

1. Animations-/Abspieltempo regulieren, **ohne** die mathematischen Transferanteile zu verändern.
2. Diagramm auf Klick groß anzeigen.
3. Daten als **CSV** exportieren (alle Schritte, nicht nur das aktuelle 40er-Fenster).
4. Grafik als **SVG**, optional PNG exportieren.
5. **Rauschen / statistische Fluktuationen:** fachlich unterscheiden zwischen künstlichem Messrauschen und **echten stochastischen Einzelteilchenfluktuationen**.

Diese Erweiterungen wurden ausdrücklich als **Workshopaufgaben stehen gelassen**, noch **nicht** als neue Funktionen implementiert.

Dokumentation:
https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/WORKSHOP_AUFGABEN_V0_2.md

---

## 8. Workshop-Konzept für unterschiedliche KI-Voraussetzungen

**Zentrale Entscheidung:** Keine kostenpflichtige KI, kein bestimmter Anbieter und **kein GitHub-Konto als Voraussetzung**. Die TeilnehmerInnen müssen nicht bei null eine vollständige App entwickeln; sie sollen eine kleine **selbst begründete und fachlich geprüfte Verbesserung** an einem funktionierenden Prototyp erleben.

- **A – Idealfall:** Eigene KI-Zugänge, Arbeit individuell oder in Gruppen.
- **B – Geführter Workshop:** KI-Dialog zentral am Beamer, Teilnehmende formulieren, testen und kritisieren.
- **C – Vorbereiteter Prototyp:** geprüfte Ausgangs- und Zwischenstände, gezielte kleine Verbesserungen.
- **D – Offline-/Notfallmodus:** vorbereitete funktionierende Stände, dokumentierte Prompts und Material; ohne KI-Netzverbindung weiter sinnvoll.

**B + C** gelten als wahrscheinlichster Hauptmodus. GitHub-Publikation bewusst **nicht** Bestandteil der 180 bzw. 200 Minuten; optional später ein separater Mini-Onlinekurs zu GitHub Pages. **GitHub Free** reicht für öffentliche Projekte aus.

Die allgemeine Einführung zu KI im Chemieunterricht sollte kurz bleiben (etwa **10–12 Minuten**): Fachfragen/Unterrichtsmaterial, Datenanalyse, Bilder/Visualisierung, Programmierung, Ausblick KI-Agenten. Schwerpunkt bleibt der aktive Mensch-KI-Entwicklungsdialog.

---

## 9. Weitere Perspektiven (nicht jetzt gleichzeitig programmieren)

**Künftiges vollständiges GLEICHGEWICHTS-LAB:**
- Synchrone drei Darstellungen Fallobst / Stechheber / abstraktes Modell.
- Geführte, teiloffene und offene Aufgabenmodi, Hypothesen, Tests und Ergebnissicherung.
- Realitätsnahes Stechhebermodell mit korrekten diskreten Volumentransfers.
- Stochastische Teilchen-/Apfel-Simulation.
- Reaktionsgleichgewichte über A⇄B hinaus, Störungen, Le Chatelier, ggf. Temperaturabhängigkeit und Katalysatorwirkung; jeweils fachlich differenziert.

**Separater KI-Laborassistent als Kongressthema:**
- Konzeption, Material-/Gerätebedarf, Mengen, Kosten, Beschaffbarkeit.
- Verifizierte Sicherheitsinformationen und Vorbereitung einer Gefährdungsbeurteilung (Freigabe bleibt Lehrkraft).
- Unterrichtliche Prä- und Postexperimentierphase, SchülerInnen-/LehrerInnenversuch, virtuelle Ergänzung, Messwertauswertung und **Ergebnissicherung**.
- Möglichst kostenlos und niedrigschwellig; später eventuell lokal via **Ollama**, auch über Schulnetz – erst auf geeigneter Hardware testen, keine produktiven Schulserver ohne Prüfung verändern.
- Das ist ein **eigener Entwicklungsstrang** und derzeit **kein** schon fertig gebauter Agent.

---

## 10. Dokumentations- und Arbeitsregeln für den neuen Chat

1. **Vor jeder Änderung** den aktuellen Stand auf GitHub `main` prüfen; Dateien bei tatsächlichem Schreibzugriff **direkt im Repository** anlegen bzw. aktualisieren, statt behaupten, etwas sei hochgeladen worden. Wenn eine GitHub-Aktion scheitert: offen sagen, was lokal entstand und was nicht hochgeladen wurde.
2. **V0.2 nicht überschreiben**; auch Story V0.1 und Integriert V0.1 bleiben als historische Versionen erhalten. Nächste Iteration als neue, klar benannte Datei/Version.
3. Zu **jeder echten Version** den vollständigen, **funktional reproduzierbaren Entwicklungs-/Änderungs-Prompt** in `docs/PROMPTS/` ablegen – ohne zu behaupten, genau dieser Prompt habe den endgültigen Code allein erzeugt.
4. **Entwicklungsjournal** `docs/ENTWICKLUNG.md` nach jedem größeren realen Schritt aktualisieren: Anlass, Änderung, fachliche Gründe, Tests, erkannte KI-Fehler, Grenzen, Nächstes.
5. Interaktive App möglichst **offlinefähig, ohne Backend, ohne KI-Zwang und für SEK I/II** nutzen; eine wartbare Fassung mit Assets und möglichst eine komplett selbstständige HTML-Datei anbieten.
6. **Nie ein fachlich überzeugend aussehendes KI-Bild oder einen generierten Code ohne Gegenprüfung freigeben.**
7. **Nicht überstürzt weiterentwickeln.** Der Nutzer möchte bewusst **kleine, getestete Schritte**, gemeinsames Begutachten und danach gezielte Korrekturen.
8. Nicht behaupten, selbstständig zwischen Chats oder während Abwesenheit weiterzuarbeiten. Fortschreibung erfolgt bei aktiver gemeinsamer Arbeit.
9. Wenn im neuen Chat nur diese Übergabe vorliegt, zuerst **das Repository lesen und die neueste Implementierung inspizieren**, ehe neue Anforderungen interpretiert werden.

### Zentrale Repo-Dateien auf einen Blick

- **README:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/README.md
- **Entwicklungsjournal:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/ENTWICKLUNG.md
- **V1-Funktionsspezifikation:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/FUNKTIONSSPEZIFIKATION_V1.md
- **V0.2-Funktionskern:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/prototyp/v0.2/index.html
- **V0.2-Workshopaufgaben:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/WORKSHOP_AUFGABEN_V0_2.md
- **Fallobstkonzept:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/FALLOBST_KONZEPT.md
- **Storyboard/Bildabnahme:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/BILDSERIE_ABNAHME_19_10_2026.md
- **Story V0.1:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/prototyp/story-v0.1/index.html
- **Integriert V0.1 (aktuell):** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/prototyp/integriert-v0.1/index.html
- **Prompt Integriert V0.1:** https://github.com/ekerzendorfer/EQUILIB_LAB/blob/main/docs/PROMPTS/INTEGRIERT_V0_1.md

---

## 11. Sofort einsetzbarer Fortsetzungsprompt

> Wir setzen unser Projekt **GLEICHGEWICHTS-LAB** fort. Lies zuerst die mitgegebene Übergabe und dann das Repository **https://github.com/ekerzendorfer/EQUILIB_LAB**, Branch **main**, insbesondere `docs/ENTWICKLUNG.md`, `docs/FUNKTIONSSPEZIFIKATION_V1.md`, `docs/PROMPTS/INTEGRIERT_V0_1.md` sowie die neueste `prototyp/integriert-v0.1/index.html`.  
>  
> Der aktuelle Stand ist die erste funktionierende **quantitative Kopplung der statischen fünfteiligen Bildergeschichte mit dem unveränderten deterministischen Rechenkern V0.2**. Die Live-Zahlen sind synchron, die fest illustrierten Äpfel sind es noch nicht. Die V0.2 ist unsere erste und **unverändert zu erhaltende Workshop-Rückfallversion**.  
>  
> Arbeite wie bisher **in kleinen, geprüften Schritten**; entwickle erst ein fachlich stimmiges Konzept für die **modellgesteuerte Apfelverteilung in der Vogelperspektive**, bevor neue Grafiken oder Animationen programmiert werden. Falls ich zuerst Rückmeldungen zur integrierten V0.1 gebe, arbeite diese natürlich vorrangig ein. Zu jeder getesteten Version bitte Reproduktions-Prompt, Fehlerkorrekturen und Entwicklungsjournal **direkt im Repository** aktualisieren.

**Ende der Übergabe – Stand 20. Oktober 2026.**