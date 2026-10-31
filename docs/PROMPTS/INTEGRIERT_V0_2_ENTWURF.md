# ENTWURF – Entwicklungs-Prompt: GLEICHGEWICHTS-LAB integriert V0.2

**Datum:** 31. Oktober 2026  
**Status:** Freigegebene Konzeptentscheidungen, **noch keine Implementierung und keine neuen Tests durchgeführt**  
**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB · Branch \`main\`  
**Ausgangspunkt:** \`prototyp/integriert-v0.1/index.html\` (identisch mit der derzeitigen \`index.html\` im Repository-Hauptverzeichnis)  
**Zieldatei:** \`prototyp/integriert-v0.2/index.html\`  
**Hinweis:** Dieser Entwurf ist ein reproduzierbarer *Änderungsauftrag*, kein Nachweis einer bereits entstandenen oder getesteten V0.2.

## Vollständiger Entwicklungsauftrag an eine KI

Du entwickelst eine **kleine, fachlich überprüfbare Erweiterung** der browserbasierten Chemie-Lernumgebung **GLEICHGEWICHTS-LAB** für SEK I/II. Das Programm veranschaulicht ein dynamisches Gleichgewicht anhand einer Fallobstgeschichte, eines diskreten deterministischen Zwei-Bestände-Modells \`A ⇄ B\`, zweier Modellzylinder, eines Stufendiagramms und symbolischer Gegenströme.

**Arbeite auf Basis der tatsächlich vorhandenen integrierten V0.1, nicht durch eine Neuprogrammierung von Grund auf.** Lies vor Änderungen das Entwicklungsjournal \`docs/ENTWICKLUNG.md\`, die V1-Funktionsspezifikation \`docs/FUNKTIONSSPEZIFIK_V1.md\` **falls vorhanden** (tatsächlicher Dateiname im Repository: \`docs/FUNKTIONSSPEZIFIKATION_V1.md\`) und \`docs/PROMPTS/INTEGRIERT_V0_1.md\`.

### 1. Umfang und Versionsschutz

1. Erzeuge ausschließlich eine **neue** lauffähige Version unter \`prototyp/integriert-v0.2/index.html\`. 
2. Verändere weder die Root-\`index.html\` noch \`prototyp/integriert-v0.1/index.html\`, \`prototyp/story-v0.1/index.html\` oder \`prototyp/v0.2/index.html\`. Die letztgenannte Datei ist die gesicherte mathematische Workshop-Rückfallversion.
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

Verwende für die Symbolzahl ausschließlich die **aktuellen, ungerundeten Modellbestände** \`A\` und \`B\` und die bestehende Gesamtmenge \`M > 0\`:

\`\`\`js
const SYMBOL_TOTAL = 60;

function symbolCounts(A, M) {
  const countA = Math.max(0, Math.min(SYMBOL_TOTAL,
    Math.round(SYMBOL_TOTAL * A / M)));
  return { countA, countB: SYMBOL_TOTAL - countA };
}
\`\`\`

Passe die Namen bei Bedarf an die tatsächliche Struktur des bestehenden Codes an. Entscheidend ist:

- \`countA + countB === 60\` bei jedem gültigen Modellzustand.
- Die Zählung entsteht aus dem vorhandenen Zustand; **Symbolzahlen werden nicht als unabhängiger Simulationszustand gespeichert**.
- Die Rechnung des Modells bleibt exakt die bisherige simultane Transferregel:
  - \`H_n = p_hin * A_n\`
  - \`R_n = p_rueck * B_n\`
  - \`A_(n+1) = A_n - H_n + R_n\`
  - \`B_(n+1) = B_n + H_n - R_n\`
  - \`A + B = M\`
- Die Funktionen \`makeInitialState\`, \`calculateTransfers\`, \`advanceOneStep\` bleiben unverändert, soweit sie in der integrierten V0.1 existieren.
- Die mathematischen Werte dürfen niemals auf ganze Äpfel oder Bildsymbole gerundet werden.
- Die angezeigten Transfermengen H und R beschreiben weiterhin die **für den nächsten Schritt** berechneten Transportmengen.

### 4. Synchronität und Bedienung

Die neue Vogelperspektive wird bei **jedem** vorhandenen Render-/Aktualisierungsvorgang aus dem aktuellen Zustand aufgebaut:

- beim Start der Anwendung mit dem **Apfelkrieg-Preset** (\`M=50, A0=50, B0=0, p_hin=0,08, p_rueck=0,04\`);
- nach einem **Einzelschritt**;
- während **Start/Pause**;
- nach **Reset**;
- nach Wahl der **V0.2-Werte** (\`M=50, A0=50, B0=0, p_hin=0,06, p_rueck=0,04\`);
- nach zulässiger Änderung von \`M\`, Anfangsverteilung oder Transferanteilen;
- nach dem Wechsel zwischen **Geschichte / Modell / Vergleich**.

Ein Reiterwechsel oder eine Bildphasenwahl darf **weder die Berechnung noch Historie oder Parameter verändern**. Die Grafik darf auch bei verborgener Modellansicht beim späteren Einblenden nicht auf einem früheren Schritt stehen.

### 5. Animation: bewusst begrenzter Umfang

**Implementiere in dieser Version keine einzeln über den Zaun wandernden Kreise.** Die Belegung wird nach jedem Rechenschritt neu dargestellt, ohne Einzelobjekt-Identitäten zu behaupten. Falls ein Doppelpfeil zwischen den Grundstücken erscheint, bleibt er statisch und verweist nur auf die bereits im Modell dargestellten beiden Transportrichtungen.

Erhalte die bestehenden gegenläufigen Transportsymbole/-balken **außerhalb** dieser neuen Ansicht unverändert. Auch beim praktisch stationären Zustand muss das vorhandene Modell weiterhin positive beidseitige Transporte zeigen können. Keine neue stochastische Simulation, kein Messrauschen, keine Änderung an Abspieltempo, Diagramm, CSV-Export oder Le Chatelier.

### 6. Technische Qualitätsanforderungen

- **Offlinefähig:** eine eigenständig lauffähige \`index.html\`; HTML, CSS, Vanilla JavaScript und ggf. Inline-SVG; kein CDN, Backend, Build-Prozess, externer API-Aufruf oder Benutzerkonto.
- Die bestehenden eingebetteten Story-Bilder werden in der neuen Version übernommen, nicht inhaltlich verändert.
- **Responsiv:** Desktop-/Beameransicht übersichtlich, bei 390 px Browserbreite keine horizontale Seitenüberbreite. Beide Grundstücke bleiben quadratisch und ihre Bezeichnungen lesbar.
- **Barrierearm:** A und B nicht ausschließlich über Farbe unterscheiden; numerische Mengen und Modellhinweis als Text; für die grafische Ansicht eine verständliche zugängliche Beschreibung.
- **Performance:** keine unnötigen vollständigen Neuaufbauten großer Bilddaten bei jedem Zeitschritt, keine doppelten Zeitgeber, kein positionsbedingtes Flackern.
- Version der Oberfläche als **„Integriert V0.2“** kennzeichnen. Die Wurzeldatei \`index.html\` auf \`main\` bleibt bis zu einer gesonderten Freigabe unverändert.

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

1. Jeder Rechenschritt erfüllt weiterhin \`A+B=M\` (bis auf Gleitkommaabweichungen) und die Summe der sichtbaren Symbole ist **immer 60**.
2. Änderungen der Symbole beeinflussen nie A, B, H, R, die Schrittnummer oder die Historie.
3. Einzelschritt, Start/Pause, Reset, Preset-Wechsel und Parametereingaben halten **Zylinder, Diagramm, Zahlen und Vogelperspektive** konsistent.
4. Bildphasenwechsel und Reiterwechsel behalten den aktuellen Zustand bei.
5. Bei längeren Läufen bleiben die Symbolpositionen stabil; es gibt kein zufälliges Springen.
6. Bei 390 px Bildschirmbreite keine horizontale Überbreite; alle 60 Kreise können auf **einem** Grundstück ohne störende Überlagerung erscheinen.
7. Keine JavaScript-Laufzeitfehler in den geprüften Abläufen.
8. Lokales Öffnen per Doppelklick (\`file://\`) möglichst am Benutzer-PC verifizieren; falls die Testumgebung das verhindert, diese Grenze **ausdrücklich dokumentieren**, nicht als erfolgreich getestet behaupten.

### 8. Lieferumfang und Dokumentation nach tatsächlicher Implementierung

Erstelle bei der anschließenden Umsetzung:

1. \`prototyp/integriert-v0.2/index.html\` als neue, selbstständige HTML-Version;
2. nach Umsetzung und echten Tests eine finale, gegebenenfalls korrigierte Fassung dieses Prompts unter \`docs/PROMPTS/INTEGRIERT_V0_2.md\` einschließlich **tatsächlich** aufgetretener Probleme und Korrekturen;
3. einen kurzen Eintrag in \`docs/ENTWICKLUNG.md\` mit Anlass, Änderungen, fachlicher Begründung, real durchgeführten Tests, Grenzen und nächsten Schritten;
4. einen Link auf die neue Version im \`README.md\`, aber erst wenn sie tatsächlich vorliegt.

**Keine nicht durchgeführten Tests behaupten.** Nenne bei Abschluss die konkret neu angelegten bzw. geänderten Repository-Dateien und den Commit. Die funktionierenden älteren Versionen bleiben unverändert. Eine Änderung der Root-\`index.html\` erfolgt **nur nach ausdrücklicher Freigabe**.

## Bewusst nicht Bestandteil dieses Auftrags

- Anpassung der fest illustrierten Äpfel in den fünf Story-Bildern;
- gleichzeitige synchronisierte Apfelanimation in der Seitenansicht;
- individuelle, über den Zaun fliegende Äpfel;
- echtes stochastisches Einzelteilchenmodell;
- realitätsnaher Stechheber und Le-Chatelier-Erweiterungen;
- automatische Einordnung freier Parameter in die fünf narrativen Bildphasen.

**Didaktisches Ziel:** Die Bildergeschichte vermittelt eine Analogie; die neue quadratische Vogelperspektive zeigt eine mathematisch gekoppelte **symbolische Bestandsverteilung**; Zylinder, Teilraten und Stufendiagramm bleiben unveränderte Ausgaben desselben deterministischen Modells.
