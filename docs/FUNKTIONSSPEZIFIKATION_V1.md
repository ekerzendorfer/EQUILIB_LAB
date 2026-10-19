# GLEICHGEWICHTS-LAB – Funktionsspezifikation V1

**Version:** 1.0 – Spezifikation, noch keine implementierte Anwendung  
**Stand:** 19. Oktober 2026  
**Projekt:** CHEMIE mit KI · `ekerzendorfer/EQUILIB_LAB`  
**Ziel:** Ein workshopfähiger, fachlich kontrollierbarer, lokal ausführbarer Kern, der spätere Visualisierungen und Gleichgewichtsmodelle nicht verbaut.

---

## 1. Zielbild und didaktisches Grundprinzip

Die erste Version veranschaulicht das **dynamische Gleichgewicht** eines diskreten, reversiblen Zweizustandsmodells. Gleichzeitig sichtbar sind:

1. **Zwei transparente Zylinder / Mengenbehälter** mit schrittweise veränderlichen Flüssigkeitsständen.
2. **Ein diskretes Mengen-Zeit-Diagramm** mit zwei *stufenförmigen* Verläufen, sodass sprunghafte Änderungen nicht zu einer glatten Kurve verwischt werden.
3. **Der gegenläufige Transport** mit zwei Pfeilen und einer einfachen symbolischen Bewegung (Kugeln/Äpfel); auch bei nahezu stationären Gesamtmengen bleiben im *laufenden* Modell die beiden Teiltransfers erkennbar.
4. **Kontrollierbare Zahlen** für Schritt, A, B, Hintransport, Rücktransport und gegebenenfalls Gleichgewichtsstatus.

**Fachlicher Leitsatz:** *Gleichbleibende makroskopische Mengen bedeuten nicht Stillstand: Im dynamischen Gleichgewicht sind die beiden gegenläufigen Transportströme gleich groß und im nichttrivialen Fall weiterhin positiv.*

In V1 sind Zylinder, Mengenbalken und Kugeln **drei Ansichten desselben deterministischen Rechenzustands**; die Animation ist noch **kein** stochastisches Einzelteilchenmodell. Die Überblendung von Fallobst-Illustrationen, realistischem Stechheber und abstrakter A⇄B-Ansicht ist ein Ausbauziel für V2.

## 2. Anwender, Lernziele und Einsatz

- **Zielgruppe:** AHS SEK II, fallweise SEK I in vereinfachter Darstellung; Chemielehrkräfte in Fortbildungen.
- **Einsatz:** Projektion, gemeinsame Modellanalyse, individuelles Experimentieren am Browser, KI-Entwicklungsworkshop.
- **Lernende können:**
  - aus gleichen oder ungleichen Teiltransfers die Änderung der Bestände ableiten;
  - zwischen Mengenverteilung und Transportgeschwindigkeit unterscheiden;
  - erkennen, dass `A*` und `B*` im dynamischen Gleichgewicht ungleich sein können;
  - erklären, warum dieselbe Gesamtmenge erhalten bleibt;
  - Modellgrenzen gegenüber chemischen Reaktionen und dem physischen Stechheber benennen.

## 3. Verbindliches mathematisches Modell

### 3.1 Ausgangspunkt und Bezeichnungen

Das Rechenprinzip folgt der vorhandenen Arbeitsmappe `EQUILIB.xlsm`, Blatt **Eingabe** (`B5:B9`) und Blatt **Zahlenwerte** (Formeln ab Zeile 3).

**Eingaben/Modellgrößen:**

- `n`: diskreter Schrittindex, beginnend bei 0; noch **keine physikalisch kalibrierte Zeit**.
- `A_n`, `B_n`: Mengen in **Modelleinheiten (ME)**, nicht automatisch Stoffmengenkonzentrationen.
- `M = A_n + B_n`: im Basismodell konstante Gesamtmenge.
- `p_hin`, `p_rueck`: dimensionslose, pro Schritt transportierte **Anteile** des jeweiligen Bestands (Excel: `k (Hinreaktion)` und `k (Rückreaktion)`). Die Namen `p` vermeiden die unkritische Gleichsetzung mit physikalischen Geschwindigkeitskonstanten.

### 3.2 Modellschritt

Beide Teiltransfers werden *simultan aus dem alten Zustand* berechnet:

```
hin   = p_hin   * A_n
rueck = p_rueck * B_n
A_n+1 = A_n - hin + rueck
B_n+1 = B_n + hin - rueck
```

- Erhaltungssatz: `A_n + B_n = M` (bis auf numerische Rundung).
- Für `0 ≤ p_hin, p_rueck ≤ 1` entstehen bei nichtnegativen Anfangswerten nichtnegative neue Mengen; **die V1-Oberfläche begrenzt beide Parameter auf 0,00–0,20**.
- Rundung erfolgt ausschließlich bei der **Anzeige**, niemals während der Berechnung.

### 3.3 Stationäre Verteilung

Bei `p_hin > 0` und `p_rueck > 0`:

- `p_hin * A* = p_rueck * B*`
- `A* = M * p_rueck / (p_hin + p_rueck)`
- `B* = M * p_hin / (p_hin + p_rueck)`
- `B* / A* = p_hin / p_rueck`

Dieses Verhältnis wird in V1 **Modell-Gleichgewichtsverhältnis** genannt, **nicht** ohne zusätzliche Modellannahmen thermodynamische Gleichgewichtskonstante.

Bei einem oder beiden Parametern 0 kennzeichnet die App den Zustand als **einseitiger Transfer / kein dynamisches Gleichgewicht** bzw. **kein Transport**; es wird keine positive beidseitige Dynamik suggeriert. Quotienten mit Nenner 0 dürfen nicht berechnet werden.

### 3.4 Praktische Gleichgewichtsanzeige

Ein exakter stationärer Grenzwert wird im iterativen Modell im Allgemeinen erst asymptotisch erreicht. Daher:

- Status zunächst: **»Annäherung an den stationären Zustand«**.
- Anzeige **»praktisch stationär«** nur bei `p_hin > 0`, `p_rueck > 0` und `|hin-rueck| ≤ 0,001 * M` für **drei aufeinanderfolgende Schritte**.
- Der gewählte Schwellenwert wird als **Anzeige-/Modellkonvention** erläutert, nicht als universelles chemisches Gleichgewichtskriterium.
- Automatische Simulation **stoppt nicht** beim Erreichen dieses Status. Die zwei Teilströme und die Animation bleiben aktiv, sofern beide Anteile und Mengen positiv sind.

## 4. Feste Ausgangsparameter und Eingaben

**Default:**

| Größe | Wert | Erläuterung |
| --- | ---: | --- |
| `M` | 50 ME | V1 bleibt der Gesamtbestand konstant |
| `A_0` | 50 ME | Zu Beginn alles links |
| `B_0` | 0 ME | Zu Beginn rechts leer |
| `p_hin` | 0,06 | Anteil von A nach B pro Schritt |
| `p_rueck` | 0,04 | Anteil von B nach A pro Schritt |

**Pflichteingaben der vollständigen V1:**
- Regler `Anfangsmenge A` von 0 bis 50 ME in ganzen Schritten, dazu abgeleitet `B = 50 − A`.
- Regler `Hin-Anteil` und `Rück-Anteil`, jeweils 0,00–0,20 in Schritten von 0,01.
- Werkseitiger Standardzustand mit einem Klick wiederherstellbar.

**Regel:** Die Änderung eines Modellparameters ist in V1 nur im **pausierten Zustand** zulässig und startet ausdrücklich einen **neuen Durchlauf ab Schritt 0** (Historie wird zurückgesetzt). Damit vermeidet V1 noch die fachlich komplexere Darstellung einer Störung mitten im laufenden Prozess. Gezielte Störungen folgen in V2/V3.

## 5. Interaktionsfunktionen (V1)

| Kennung | Funktion | Sollverhalten | Priorität |
| --- | --- | --- | --- |
| F01 | **Einzelschritt** | Rechnet genau einen simultanen Modellschritt und aktualisiert alle Ansichten gemeinsam. | MUSS |
| F02 | **Start/Pause** | Automatischer Lauf mit z. B. einem Schritt pro Sekunde; Pause hält Modell und Bewegungsanimation an. | MUSS |
| F03 | **Reset** | Kehrt auf `n=0` und die zuletzt gewählten Anfangsparameter zurück, leert die Verlaufshistorie. | MUSS |
| F04 | **Standardwerte** | Setzt Default-Eingaben und Modellzustand zurück. | MUSS |
| F05 | **Parameter anpassen** | Nur pausiert; danach Neustart und leere Historie. | MUSS |
| F06 | **Statusfeld** | Schrittnummer, Summenbestand, beide Teiltransfers und Status *Annäherung / praktisch stationär / Sonderfall*. | MUSS |
| F07 | **Animation** | Hin-/Rückpfeile (dauerhaft), einfache laufende Transportsymbole synchron zu Schritten. | MUSS – einfach |
| F08 | **Geschwindigkeit** | Wahl zwischen langsam, normal, schnell. | KANN |
| F09 | **Kurzinfo »Was bedeutet das?«** | Erklärt Modell und Grenzen ohne Anmeldung. | MUSS – kurz |
| F10 | **Vollbild/Projektion** | Beamerfreundliche, hinreichend große Bedienelemente. | KANN |

**Bei wiederholtem Start/Pause/Einzelschritt** dürfen keine doppelten Zeitgeber entstehen. Animation, Zustandswechsel und Historieneintrag müssen pro Schritt atomar erfolgen.

## 6. Benutzeroberfläche und synchrone Visualisierung

### 6.1 Desktop-/Beamer-Layout (Zielansicht)

```
GLEICHGEWICHTS-LAB                [Info / Modellgrenzen]
[Start/Pause] [Einzelschritt] [Reset] [Standard]

┌───────────────────────────┬─────────────────────────────┐
│ ZYLINDER A        B        │ MENGEN-VERLAUF               │
│ Flüssigkeitsstand,         │ A(n), B(n) als Stufenlinien  │
│ Zahlen, zwei Transferpfeile│ und/oder diskrete Balken     │
│   A  ⇄  B                 │ x: Schritt n, y: ME         │
└───────────────────────────┴─────────────────────────────┘

A: 44,30 ME  B: 5,70 ME    Hin: … ME/Schritt   Rück: … ME/Schritt
Schritt: 2   Gesamt: 50 ME   Status: Annäherung

[Anfangsmenge A ▬ ] [Hin-Anteil ▬ ] [Rück-Anteil ▬ ]
```

Auf schmaleren Bildschirmen dürfen die Bereiche untereinander angeordnet werden. Keine horizontal scrollpflichtige Hauptbedienung; nutzbar auf typischen Schul-Notebooks und am Beamer.

### 6.2 Zylinder

- Transparentes, schematisches Gefäßpaar gleicher virtueller Querschnittsfläche.
- Höhe proportional zum jeweiligen Bestand; Skala 0–50 ME.
- Standänderung **sprunghaft pro abgeschlossenem Schritt**; keine geglättete Dauerbewegung als fälschliche kontinuierliche Messung.
- Das **reale** Volumen und der Übertrag durch reale Stechheber sind noch nicht geometrisch kalibriert. In V1 sind die Zylinder explizit **Modellzylinder**.

### 6.3 Mengen-Diagramm

- X-Achse: **Simulationsschritt n**, nicht Zeit in Sekunden.
- Y-Achse: **Menge in Modelleinheiten (ME)**.
- Zwei klar unterscheidbare Stufenlinien oder diskrete Balken (`A_n`, `B_n`); im Diagramm muss die Treppenform erkennbar bleiben.
- Darstellung inklusive `n=0`; Tooltips oder ablesbare Zahlenwerte an aktuellen Schritten.
- Datenreihe darf unbegrenzt laufende Simulation nicht speichertechnisch aufblähen: Anzeige beispielsweise der letzten 100 Schritte, bei korrekter X-Beschriftung des aktuellen Schrittbereichs.

### 6.4 Gegenläufiger Transport / Apfelsymbole

- Zwei dauerhaft sichtbare beschriftete Pfeile `A → B` und `B → A`.
- Bewegte Kugel-/Apfelsymbole für die **Richtungen**, nicht die behauptete exakte Anzahl ganzer Apfelobjekte.
- Geschwindigkeiten/Pfeilstärken dürfen an den berechneten Teiltransfer gekoppelt werden; **Zahlen für `hin` und `rueck` sind verpflichtend**, weil Animationen nur qualitativ sind.
- Auch wenn `A` und `B` visuell konstant bleiben, sind bei positivem beidseitigem Transfer weiter Transportbewegungen zu sehen (während die Simulation läuft).
- Ist ein berechneter Teiltransfer 0, darf in dieser Richtung nicht animiert werden.

### 6.5 Farben und Zugänglichkeit

- A und B werden nicht ausschließlich über Farbe unterschieden; immer eindeutige Texte/Legenden.
- Lesbare Schriften/hoher Kontrast für Projektion; Tastaturbedienung für Grundbuttons.
- Bewegungen respektieren reduzierte Animationseinstellungen, ohne Informationen zu verlieren (Pfeile/Zahlen bleiben erhalten).

## 7. Architektur / technische Vorgaben

### 7.1 Ausführung

- `index.html` als **einzige zwingende Laufzeitdatei** für V1.
- HTML + CSS + Vanilla JavaScript; Diagramm bevorzugt durch integriertes SVG.
- Keine externen Skripte, Fonts, CDNs, Bibliotheken, Bilder oder Netzaufrufe.
- Offline per Doppelklick (`file://`) in aktuellen Browsern lauffähig.
- Kostenlos, ohne Anmeldung, keine persönlichen Daten, kein Konto, kein Backend, kein Build-Schritt.
- Später per GitHub Pages publizierbar, aber **nicht** Bestandteil des Kernworkshops.

### 7.2 Interne Aufteilung – trotz Ein-Datei-Format

Die Datei soll eindeutig getrennte Funktionsbereiche enthalten, zum Beispiel:

1. `settings` und Modelldefinition.
2. `initialState(settings)`.
3. **Reiner Rechenkern:** `calculateTransfers(state, settings)` und `advanceOneStep(state, settings)`; ohne DOM-/Animationszugriff.
4. `history` mit den Zustandswerten und den beiden Teiltransfers pro Schritt.
5. `renderCylinders`, `renderStepChart`, `renderTransfers`, `renderStatus`.
6. `controls` einschließlich Start/Pause/Reset und Parameter-Validierung.
7. `tests` später optional als separates Prüfschema oder im Entwickler-Modus.

Damit bleibt die KI mit **lokal begrenzten Änderungsaufträgen** steuerbar: »Ändere nur die Darstellung; fasse die Rechenfunktion nicht an.«

### 7.3 Vorgeschlagenes Datenmodell

```js
const settings = {
  total: 50,
  initialA: 50,
  pForward: 0.06,
  pBackward: 0.04,
  intervalMs: 1000
};

const state = {
  step: 0,
  a: 50,
  b: 0,
  transferForward: 0,
  transferBackward: 0,
  stationaryConsecutive: 0,
  running: false,
  history: [{ step: 0, a: 50, b: 0, forward: 0, backward: 0 }]
};
```

`transferForward` und `transferBackward` beziehen sich jeweils auf den gerade abgeschlossenen Übergang. Die initiale Verlaufszeile `n=0` besitzt noch keinen abgeschlossenen Transfer. Der Rechenkern lässt sich später gegen andere Modelldefinitionen austauschen, ohne die grundlegenden Diagramm-/Bedienkomponenten neu zu entwerfen.

## 8. Pflicht-Abnahmetests

| Test | Durchführung | Erwartetes Ergebnis |
| --- | --- | --- |
| T01 | Default-Start, einmal Einzelschritt | `A=47,00`, `B=3,00`, `n=1`; Hin=3, Rück=0 |
| T02 | Zweiter Einzelschritt | `A=44,30`, `B=5,70`; Hin=2,82, Rück=0,12 |
| T03 | 60 Default-Schritte | A nahe 20, B nahe 30; Summenbestand 50; Status »praktisch stationär« |
| T04 | Nach T03 drei weitere Schritte | Werte beinahe unverändert, aber beide Teiltransfers bleiben >0 und Animationen laufen im Play-Modus weiter |
| T05 | Startwerte A=25, B=25 und `p_hin=p_rueck=0,05` | Keine Nettoänderung, aber in jeder Richtung Transfer 1,25 ME/Schritt |
| T06 | `p_hin=p_rueck=0` | Keine Änderung, keine aktiven Transporte; **kein** dynamisches Gleichgewicht melden |
| T07 | Nur `p_rueck=0` | Einseitige Übertragung bis zum Grenzbestand; keine irreführende thermodynamische K-Angabe |
| T08 | Reset nach 10 Schritten | `n=0`, Ausgangswerte wiederhergestellt, Diagramm enthält nur Startwert |
| T09 | Parameter ändern bei Pause | Ausdrücklicher Neustart ab `n=0`; Parameter und Diagramm stimmen überein |
| T10 | Start/Pause/Start mehrfach | Kein doppelter Timer, keine übersprungenen Schritte |
| T11 | Internet trennen, HTML lokal öffnen | Alle MUSS-Funktionen arbeiten ohne Netzwerkzugriff |
| T12 | Diagramm nach jedem Schritt | Änderungen erscheinen als **Stufen**, nicht als glatt interpolierte Kurven |
| T13 | Kleine Fließkommareste | Gesamtmenge bleibt bis auf Rechengenauigkeit 50; nie negative Mengen anzeigen |
| T14 | Werte beider Mengen fast stationär | Beide beschrifteten Gegenströme weiterhin sichtbar, kein Stopp bei Statuswechsel |

**Numerischer Prüfmaßstab:** Rechenwerte mit Toleranz z. B. `1e−9 ME`; für die sichtbare Anzeige zwei Nachkommastellen. Vor einer realitätsnahen Stechheberbezeichnung ist die physikalische Geometrie separat zu validieren.

## 9. Workshop-Umfang und gesicherte Zwischenstände

Die **Referenz-V1** wird vor dem Workshop **vollständig umgesetzt und getestet**. Teilnehmende beginnen jedoch bewusst mit einem **reduzierten Starterstand** und ergänzen je nach KI-Zugang nur ein handhabbares Feature.

| Stand | Inhalt | Zweck |
| --- | --- | --- |
| `00_START/index.html` | Zwei Mengen, Zahlenwerte, Einzelschritt, Reset, feste Defaultparameter | Sicheres gemeinsames Fundament |
| `01_PARAMETER/index.html` | Parameterregler und Initialverteilung | Einfacher Änderungsauftrag |
| `02_DIAGRAMM/index.html` | Diskretes Stufendiagramm | Visuell/didaktisch anspruchsvollere Änderung |
| `03_VISUALISIERUNG/index.html` | Zwei Zylinder + gegenläufiger symbolischer Transport | Live-Demo und Erweiterung |
| `04_REFERENZ/index.html` | Alle MUSS-Funktionen und Tests | Rückfallstufe und Vergleichsmaßstab |

**Wichtig:** Diese Verzeichnisnamen sind *geplant* und werden erst mit der Implementierung angelegt. Kein ergebnisoffener Workshop ohne fertig getestete Rückfallvariante.

### Geeignete Workshop-Änderungsaufträge

1. **Einsteiger:** Ergänze eine sichtbare Gesamtmengenanzeige (`A+B`) und eine verständliche Statusmeldung.
2. **Standard:** Ergänze zwei Parameterregler und prüfe die Ergebnisse gegen die Excel-Referenz.
3. **Fortgeschritten:** Ergänze ein Stufendiagramm oder die gegenläufige Animation; der Rechenkern darf nicht verändert werden.

Alle Gruppen sollen mindestens **einen selbst formulierten Änderungsprompt, einen fachlichen Test und ggf. eine Korrekturrunde** dokumentieren. Kostenpflichtiger KI-Zugang und GitHub-Konto bleiben optional.

## 10. Bewusst ausgeschlossen aus V1

- Exakte Nachbildung eines bestimmten realen Stechhebers samt Röhrchen-/Gefäßgeometrie.
- Aufwendige originale/neu illustrierte Apfelkrieg-Szenen und Erklärvideo.
- Drei grafisch vollständig ausgearbeitete Repräsentationsebenen mit weichen Überblendungen.
- Stochastische Einzelteilchenberechnung bzw. Gleichgewichtsfluktuationen.
- Änderungen von Parametern mitten im aktiven Lauf und systematische Le-Chatelier-Experimente.
- Komplexere reversible Reaktionen, Temperaturabhängigkeit, Katalysator, offene Stoffsysteme.
- Automatische KI-Auswertung, Login, Backend, CSV/PDF-Export, komplexer Aufgabenmodus.

Diese Funktionen bleiben **ausbaubar**, sind aber keine versteckten Anforderungen an die Workshop-Starter-App.

## 11. Offene fachliche Entscheidungen vor der Implementierung

1. **Stechheber-Geometrie:** Soll die spätere realistische Ansicht mit identischen Gefäßquerschnitten und Stechheberlängen beginnen? Entsprechung zwischen Höhe und Übertragungsvolumen prüfen.
2. **Darstellung der Stufen:** Stufenlinien **und** Zylinder gemeinsam sind Pflicht; zusätzlich separate Volumentransfer-Balken erst nach Test des Platzbedarfs.
3. **Apfelsymbole:** Für V1 einfache neutrale Kugeln/Bewegungszeichen, für V2 eigene moderne Illustrationen – keine unklare Lizenzübernahme.
4. **Statusanzeige:** Toleranz `0,1 %` des Gesamtbestands für drei Schritte zunächst als V1-Konvention vorgesehen; fachlich/didaktisch bei Prototyptest bewerten.
5. **Bezeichnungen:** Die Excel-Daten werden als Mengen in ME präsentiert. Bezeichnungen `c(A)`, `c(B)`, `K` erst im expliziten Chemie-Modellmodus differenziert einführen.

## 12. Definition of Done: V1

V1 gilt erst als **fertig**, wenn:

- die fünf Kernfunktionen Einzelschritt, Start/Pause, Reset, Parameteränderung und synchrone Anzeige stabil laufen;
- zwei Zylinder, diskretes Diagramm und **beide** gegenläufigen Transporte gleichzeitig lesbar sind;
- das dynamische Gleichgewicht weiterhin aktive Transporte zeigt;
- alle Pflicht-Abnahmetests T01–T14 bestanden sind;
- die App als einzelne Datei **offline** im Browser läuft;
- die Referenzfassung sowie mindestens der minimal lauffähige Starterstand gesichert sind;
- die didaktischen Modellgrenzen in der Oberfläche erläutert sind.

---

### Entwicklungsnotiz – 19.10.2026

Heute wurde die bisherige Konzeptidee in ein überprüfbares V1-Pflichtenheft übersetzt. Der Mathematikkern wurde nochmals direkt mit den Formeln aus `EQUILIB.xlsm` abgeglichen. Bewusst wurde der Unterschied **Modelleinheiten ↔ reale Volumina ↔ chemische Konzentrationen** betont. Die volle synchrone Überblendung von Apfelkonflikt, realem Stechheber und abstrakter Simulation wird als Leitvision erhalten, aber **nicht** in die erste Workshop-Minimalversion gezwungen.