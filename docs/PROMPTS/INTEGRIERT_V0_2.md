# Entwicklungs-Prompt: GLEICHGEWICHTS-LAB integriert V0.2

**Datum:** 31. Oktober 2026  
**Status:** Integriert V0.2 implementiert; Syntax-, mathematische und simulierte DOM-/Bedientests durchgeführt. Vollständiger visueller Browser- und lokaler Doppelklick-Test noch offen.  
**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB · Branch `main`  
**Ausgangspunkt:** `prototyp/integriert-v0.1/index.html` (identisch mit der derzeitigen `index.html` im Repository-Hauptverzeichnis)  
**Implementierte Datei:** `prototyp/integriert-v0.2/index.html`  
**Hinweis:** Der folgende Auftrag ist eine rekonstruierte, funktional reproduzierbare Entwicklungsanweisung. Er beansprucht weder Ein-Prompt-Erzeugung noch bitidentische Reproduktion. Tatsächliche Implementierung und Prüfungen sind am Ende getrennt dokumentiert.

## Vollständiger Entwicklungsauftrag an eine KI

Du entwickelst eine **kleine, fachlich überprüfbare Erweiterung** der browserbasierten Chemie-Lernumgebung **GLEICHGEWICHTS-LAB** für SEK I/II. Das Programm veranschaulicht ein dynamisches Gleichgewicht anhand einer Fallobstgeschichte, eines diskreten deterministischen Zwei-Bestände-Modells `A ⇄ B`, zweier Modellzylinder, eines Stufendiagramms und symbolischer Gegenströme.

**Arbeite auf Basis der tatsächlich vorhandenen integrierten V0.1, nicht durch eine Neuprogrammierung von Grund auf.** Lies vor Änderungen das Entwicklungsjournal `docs/ENTWICKLUNG.md`, die V1-Funktionsspezifikation `docs/FUNKTIONSSPEZIFIKATION_V1.md` und `docs/PROMPTS/INTEGRIERT_V0_1.md`.

### 1. Umfang und Versionsschutz

1. Erzeuge ausschließlich eine **neue** lauffähige Version unter `prototyp/integriert-v0.2/index.html`. 
2. Verändere weder die Root-`index.html` noch `prototyp/integriert-v0.1/index.html`, `prototyp/story-v0.1/index.html` oder `prototyp/v0.2/index.html`. Die letztgenannte Datei ist die gesicherte mathematische Workshop-Rückfallversion.
3. Die bestehenden Reiter **Geschichte**, **Modell** und **Vergleich**, die fünf freigegebenen Phasenbilder, die Bildnavigation und die beiden Parameter-Presets müssen unverändert funktionieren.
4. Erweitere **nur den Reiter „Modell“** um den zusätzlichen Bereich **„Symbolische Vogelperspektive“**, vorzugsweise unter der vorhandenen Zylinder-/Diagrammansicht. Kein weiterer Reiter, keine Umgestaltung der bestehenden Story-Bilder.
5. Der Rechenkern, die Zustandsvariable und die vorhandenen Steuerungsfunktionen bleiben die einzige Datenquelle.

### 2. Inhalt und Gestaltung der neuen Ansicht

Zeige **zwei gleich große quadratische Grundstücksflächen** nebeneinander, mit gut erkennbarer gemeinsamer Grenze bzw. einem schematischen Zaun:

- **links: A – Junge**, 
- **rechts: B – Nachbar**.

Beide Grundstücke sind schlicht gestaltete Flächen in ruhigen, kontrastreichen Farben. Auf ihnen liegen **kleine Kreise als symbolische Äpfel**. Es werden **keine KI-generierten Bilder oder neuen Bilddateien** benötigt; eine einfache SVG- oder DOM/CSS-Lösung ist ausreichend. Kreise und Grundstücke müssen auch am Beamer erkennbar sein. Eine korrekte quadratische Geometrie (Breite = Höhe) ist bei allen Bildschirmgrößen zu erhalten.

**Belegungsregel:** Pro Grundstück sind bis zu **60 feste Symbolpositionen** verfügbar, insgesamt werden jedoch **genau 60 sichtbare Kreise** auf beide Grundstücke aufgeteilt. Das bedeutet ausdrücklich **nicht** 60 Kreise je Seite gleichzeitig. Verwende identisch skalierte Kreisgrößen auf beiden Seiten und eine ähnliche räumliche Verteilung.

Die Positionen sind bei jedem Schritt **deterministisch stabil**. Erzeuge nicht bei jedem Rendern neue Zufallskoordinaten. Ein einmalig vorberechnetes, gleichmäßig über die Fläche verstreutes Positionsmuster ist geeignet, solange die Kreise einander nicht störend überlagern und beim Wechsel der Belegungszahl kein zufälliges Flackern entsteht. Die Positionen einer Seite bleiben über den ganzen Versuch dieselben; nur die Anzahl der dort sichtbaren Kreise verändert sich.

Zeige die **exakten Modellwerte A und B in ME** neben/über den Grundstücken. Optional können die gerundeten Kreiszahlen ergänzend als „Bildsymbole“ angegeben werden; sie dürfen nicht als physikalische Äpfelzahl bezeichnet werden.

Direkt unter der Darstellung steht gut lesbar:

> **Modellhinweis:** Die 60 Kreise veranschaulichen die Verteilung der Bestände proportional. Sie stellen keine exakt gezählten Einzeläpfel dar; das Rechenmodell verwendet kontinuierliche Modelleinheiten (ME).

### 3. Mathematische Kopplung: reine Darstellung, kein neuer Rechenkern

Verwende für die Symbolzahl ausschließlich die **aktuellen, ungerundeten Modellbestände** `A` und `B` und die bestehende Gesamtmenge `M > 0`:

```js
const SYMBOL_TOTAL = 60;

function symbolCounts(A, M) {
  const countA = Math.max(0, Math.min(SYMBOL_TOTAL,
    Math.round(SYMBOL_TOTAL * A / M)));
  return { countA, countB: SYMBOL_TOTAL - countA };
}
```

Passe die Namen bei Bedarf an die tatsächliche Struktur des bestehenden Codes an. Entscheidend ist:

- `countA + countB === 60` bei jedem gültigen Modellzustand.
- Die Zählung entsteht aus dem vorhandenen Zustand; **Symbolzahlen werden nicht als unabhängiger Simulationszustand gespeichert**.
- Die Rechnung des Modells bleibt exakt die bisherige simultane Transferregel:
  - `H_n = p_hin * A_n`
  - `R_n = p_rueck * B_n`
  - `A_(n+1) = A_n - H_n + R_n`
  - `B_(n+1) = B_n + H_n - R_n`
  - `A + B = M`
- Die Funktionen `makeInitialState`, `calculateTransfers`, `advanceOneStep` bleiben unverändert, soweit sie in der integrierten V0.1 existieren.
- Die mathematischen Werte dürfen niemals auf ganze Äpfel oder Bildsymbole gerundet werden.
- Die angezeigten Transfermengen H und R beschreiben weiterhin die **für den nächsten Schritt** berechneten Transportmengen.

### 4. Synchronität und Bedienung

Die neue Vogelperspektive wird bei **jedem** vorhandenen Render-/Aktualisierungsvorgang aus dem aktuellen Zustand aufgebaut:

- beim Start der Anwendung mit dem **Apfelkrieg-Preset** (`M=50, A0=50, B0=0, p_hin=0,08, p_rueck=0,04`);
- nach einem **Einzelschritt**;
- während **Start/Pause**;
- nach **Reset**;
- nach Wahl der **V0.2-Werte** (`M=50, A0=50, B0=0, p_hin=0,06, p_rueck=0,04`);
- nach zulässiger Änderung von `M`, Anfangsverteilung oder Transferanteilen;
- nach dem Wechsel zwischen **Geschichte / Modell / Vergleich**.

Ein Reiterwechsel oder eine Bildphasenwahl darf **weder die Berechnung noch Historie oder Parameter verändern**. Die Grafik darf auch bei verborgener Modellansicht beim späteren Einblenden nicht auf einem früheren Schritt stehen.

### 5. Animation: bewusst begrenzter Umfang

**Implementiere in dieser Version keine einzeln über den Zaun wandernden Kreise.** Die Belegung wird nach jedem Rechenschritt neu dargestellt, ohne Einzelobjekt-Identitäten zu behaupten. Falls ein Doppelpfeil zwischen den Grundstücken erscheint, bleibt er statisch und verweist nur auf die bereits im Modell dargestellten beiden Transportrichtungen.

Erhalte die bestehenden gegenläufigen Transportsymbole/-balken **außerhalb** dieser neuen Ansicht unverändert. Auch beim praktisch stationären Zustand muss das vorhandene Modell weiterhin positive beidseitige Transporte zeigen können. Keine neue stochastische Simulation, kein Messrauschen, keine Änderung an Abspieltempo, Diagramm, CSV-Export oder Le Chatelier.

### 6. Technische Qualitätsanforderungen

- **Offlinefähig:** eine eigenständig lauffähige `index.html`; HTML, CSS, Vanilla JavaScript und ggf. Inline-SVG; kein CDN, Backend, Build-Prozess, externer API-Aufruf oder Benutzerkonto.
- Die bestehenden eingebetteten Story-Bilder werden in der neuen Version übernommen, nicht inhaltlich verändert.
- **Responsiv:** Desktop-/Beameransicht übersichtlich, bei 390 px Browserbreite keine horizontale Seitenüberbreite. Beide Grundstücke bleiben quadratisch und ihre Bezeichnungen lesbar.
- **Barrierearm:** A und B nicht ausschließlich über Farbe unterscheiden; numerische Mengen und Modellhinweis als Text; für die grafische Ansicht eine verständliche zugängliche Beschreibung.
- **Performance:** keine unnötigen vollständigen Neuaufbauten großer Bilddaten bei jedem Zeitschritt, keine doppelten Zeitgeber, kein positionsbedingtes Flackern.
- Version der Oberfläche als **„Integriert V0.2“** kennzeichnen. Die Wurzeldatei `index.html` auf `main` bleibt bis zu einer gesonderten Freigabe unverändert.

### 7. Verbindliche fachliche Prüffälle

Prüfe und protokolliere mindestens die folgenden Fälle. Die Symbolzahlen sind Anzeigegrößen, **keine** gerundeten Simulationswerte.

| Fall | M | A | B | Symbole A | Symbole B |
|---|---:|---:|---:|---:|---:|
| Apfelkrieg-Preset, Schritt 0 | 50 | 50 | 0 | 60 | 0 |
| Apfelkrieg-Preset, Schritt 1 | 50 | 46 | 4 | 55 | 5 |
| V0.2-Preset, Schritt 1 | 50 | 47 | 3 | 56 | 4 |
| Gleich große Bestände | 50 | 25 | 25 | 30 | 30 |
| Stationärer Grenzfall des Apfelkriegs | 50 | ca. 16,67 | ca. 33,33 | 20 | 40 |
| Vollständig rechts | 50 | 0 | 50 | 0 | 60 |
| Gesamtbestand 200, alles links | 200 | 200 | 0 | 60 | 0 |

Zusätzlich testen:

1. Jeder Rechenschritt erfüllt weiterhin `A+B=M` (bis auf Gleitkommaabweichungen) und die Summe der sichtbaren Symbole ist **immer 60**.
2. Änderungen der Symbole beeinflussen nie A, B, H, R, die Schrittnummer oder die Historie.
3. Einzelschritt, Start/Pause, Reset, Preset-Wechsel und Parametereingaben halten **Zylinder, Diagramm, Zahlen und Vogelperspektive** konsistent.
4. Bildphasenwechsel und Reiterwechsel behalten den aktuellen Zustand bei.
5. Bei längeren Läufen bleiben die Symbolpositionen stabil; es gibt kein zufälliges Springen.
6. Bei 390 px Bildschirmbreite keine horizontale Überbreite; alle 60 Kreise können auf **einem** Grundstück ohne störende Überlagerung erscheinen.
7. Keine JavaScript-Laufzeitfehler in den geprüften Abläufen.
8. Lokales Öffnen per Doppelklick (`file://`) möglichst am Benutzer-PC verifizieren; falls die Testumgebung das verhindert, diese Grenze **ausdrücklich dokumentieren**, nicht als erfolgreich getestet behaupten.

### 8. Lieferumfang und Dokumentation

Erstelle bei der anschließenden Umsetzung:

1. `prototyp/integriert-v0.2/index.html` als neue, selbstständige HTML-Version;
2. nach Umsetzung und echten Tests eine finale, gegebenenfalls korrigierte Fassung dieses Prompts unter `docs/PROMPTS/INTEGRIERT_V0_2.md` einschließlich **tatsächlich** aufgetretener Probleme und Korrekturen;
3. einen kurzen Eintrag in `docs/ENTWICKLUNG.md` mit Anlass, Änderungen, fachlicher Begründung, real durchgeführten Tests, Grenzen und nächsten Schritten;
4. einen Link auf die neue Version im `README.md`, aber erst wenn sie tatsächlich vorliegt.

**Keine nicht durchgeführten Tests behaupten.** Nenne bei Abschluss die konkret neu angelegten bzw. geänderten Repository-Dateien und den Commit. Die funktionierenden älteren Versionen bleiben unverändert. Eine Änderung der Root-`index.html` erfolgt **nur nach ausdrücklicher Freigabe**.

## Bewusst nicht Bestandteil dieses Auftrags

- Anpassung der fest illustrierten Äpfel in den fünf Story-Bildern;
- gleichzeitige synchronisierte Apfelanimation in der Seitenansicht;
- individuelle, über den Zaun fliegende Äpfel;
- echtes stochastisches Einzelteilchenmodell;
- realitätsnaher Stechheber und Le-Chatelier-Erweiterungen;
- automatische Einordnung freier Parameter in die fünf narrativen Bildphasen.

**Didaktisches Ziel:** Die Bildergeschichte vermittelt eine Analogie; die neue quadratische Vogelperspektive zeigt eine mathematisch gekoppelte **symbolische Bestandsverteilung**; Zylinder, Teilraten und Stufendiagramm bleiben unveränderte Ausgaben desselben deterministischen Modells.


## Tatsächlich implementiert am 31. Oktober 2026

**Neu angelegt:** `prototyp/integriert-v0.2/index.html` auf `main`, als eigenständige Offline-Ein-Datei-App (rund 2,57 MB inklusive der unveränderten eingebetteten Story-Bilder).

**Konkrete Änderungen gegenüber der integrierten V0.1:**

- Die vorhandene HTML-/CSS-/JavaScript-Datei wurde gezielt erweitert, nicht neu geschrieben. Ein neuer Abschnitt „Symbolische Vogelperspektive“ folgt unterhalb der beiden Modellpanels, ausschließlich im Tab „Modell“.
- Zwei gleich große, quadratische Inline-SVG-Grundstücke A (Junge, links) und B (Nachbar, rechts), mit getrennter Grenz-/Zaunlinie und je einem zugänglichen, bei jeder Anzeige aktualisierten Mengentext.
- Pro Grundstück gibt es 60 **feste** SVG-Kreispositionen im 8×8-Raster, in einer festen Permutationsreihenfolge belegt. Es sind insgesamt 60 von 120 möglichen Kreisen **sichtbar**; die nicht belegten Positionen haben SVG-`visibility="hidden"`.
- `appleSymbolCounts(state.a, settings.total)` liefert `countA = clamp(round(60*A/M),0,60)`, `countB=60-countA`.
- `renderAppleBirdView()` wird im bestehenden zentralen `render()` nach dem Stufendiagramm-Rendern aufgerufen. Die SVG-Kreise werden nur beim Initialisieren erzeugt und danach sichtbar/unsichtbar geschaltet.
- Der vorhandene mathematische Funktionsblock `makeInitialState`, `calculateTransfers`, `advanceOneStep` blieb **zeichenidentisch**.
- Beide Story-Presets, drei Tabs, Phasenwahl, Modellzylinder, Balken, Transportkugeln, Kennzahlen und Chartlogik wurden übernommen und nicht in ihrer fachlichen Logik verändert.
- Die Root-`index.html` und alle älteren Prototypen wurden **nicht** überschrieben. Die Zeichnung bildet Bestände ab, keine identifizierbaren, real einzeln wandernden Äpfel.

### Tatsächlich durchgeführte Prüfungen

1. **Syntax:** Der gesamte eingebettete JavaScript-Code der neuen HTML-Datei wurde mit dem JavaScript-Parser (`new Function`) ohne Syntaxfehler geprüft.
2. **Quellcodevergleich:** Die drei ursprünglichen Rechenkern-Funktionen wurden im alten und im neuen HTML verglichen und waren identisch.
3. **Referenzwerte:** Apfelkrieg n=0 (50/0 → 60/0 Symbole); Apfelkrieg n=1 (46/4 → 55/5); V0.2-Preset n=1 (47/3 → 56/4); 25/25 → 30/30; stationärer Sollwert A≈16,67/B≈33,33 → 20/40; A=0 → 0/60; M=200, A=200 → 60/0.
4. **Mathematische Langlaufprüfung:** 500 deterministische Schritte mit Erhaltung von `A+B=M` bis auf floating-point-Toleranz und stets `countA+countB=60`.
5. **Simulierte DOM-/Bedienprüfung (kein echter Browser):** Vollständiges Skript gegen ein DOM-Ersatzmodell ausgeführt. Kontrolliert wurden Initialisierung der 120 SVG-Kreise, sichtbare Symbolzahlen und Beschriftungen, stabile SVG-Positionen, Einzelschritt, Reset, beide Presets, M=200 und geänderte Anfangsverteilung, Tab- und Phasenwechsel ohne Zustandsänderung, Diagrammansicht „Volle Laufzeit“, Start/Pause, Timer und Tastenzustände. Diese Prüfrunde lief ohne ausgelösten JavaScript-Fehler.
6. **GitHub-Nachprüfung:** Neu gespeicherte Datei aus dem Repository erneut gelesen und als eigenständige HTML-Datei mit 2.569.570 Zeichen und Blob-SHA `293518c23f76b491b2d7ee8a590a3a9d1efb4b9d` bestätigt.

### Ausdrücklich noch offen

- Ein **echter visueller Chromium-/Browser-Test** der neuen vollständigen HTML-Oberfläche (insbesondere Layout, Bildüberschneidungen und 390-px-Ansicht) wurde bei dieser Umsetzung **nicht** durchgeführt. Die simulierte DOM-Prüfung ersetzt ihn nicht.
- Der lokale **Doppelklick-/Offline-Test** am Endgerät und eine **didaktische Sichtabnahme** durch den Nutzer sind offen.
- Falls die quadratischen Grundstücke oder die Kreisdichte visuell verbesserungsbedürftig sind, in einer kleinen, separaten Iteration nachbessern.
- Erst nach Freigabe darüber entscheiden, ob die neue Version die aktuelle Root-`index.html` ersetzen soll oder ob eine spätere symbolische Transferanimation sinnvoll ist.

**Versionsprinzip:** Die V0.2 ist ein vorläufiger, implementierter und logisch geprüfter Prototyp; keine abschließende Unterrichtsfreigabe.
