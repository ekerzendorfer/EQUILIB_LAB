# GLEICHGEWICHTS-LAB – Fallobstschlacht: Konzept und Storyboard

**Konzeptstand:** 19. Oktober 2026  
**Ausgangspunkt:** [getesteter Prototyp V0.2](../prototyp/v0.2/index.html)  
**Status:** didaktisches/gestalterisches Konzept; **noch keine Implementierung, Illustration oder Video erzeugt**  
**Rechte:** eigenständige Neubilder; die eingescannten Buchabbildungen dienen nur der fachlichen Orientierung.

## 1. Ziel und zentrale Idee

Die Fallobstschlacht wird als **interaktive fünfteilige Bildergeschichte** umgesetzt und mit dem bestehenden mathematischen Modell synchronisiert. Die Erzählung soll schrittweise in die quantitative Darstellung übergehen, nicht als bloße Dekoration neben der App stehen.

**Didaktische Leitidee:**  
*Gleiche Apfelzahlen bedeuten nicht zwingend Gleichgewicht. Im dynamischen Gleichgewicht sind die gegenläufigen Transportraten gleich groß, obwohl die Bestände auf beiden Seiten unterschiedlich sein können.*

Repräsentationsebenen bleiben:
1. **Narrativ:** Wer wirft wohin und warum?
2. **Makroskopisches Modell:** Änderung der Bestände/Verteilung; zwei gegenläufige Transportraten.
3. **Formal:** Diskrete A⇄B-Simulation mit Mengen, Raten und Stufendiagramm.

Die spätere, realistisch gestaltete **Stechheber-Ebene** kommt dazu, ohne einen zweiten widersprüchlichen Rechenkern zu schaffen.

## 2. Eindeutige Zuordnung A/B und Modellparametern

Um Missverständnisse zu vermeiden, ist die Zuordnung **für den Story-Modus verbindlich**:

| Modell | Erzählung | Position | V0.2-Farbe | Transport |
|---|---|---|---|---|
| A | Äpfel beim **Jungen** | links | Blau (als UI-Markierung) | **A → B**, vom Jungen geworfen, Parameter \`pForward\` |
| B | Äpfel beim **älteren Nachbarn** | rechts | Orange (als UI-Markierung) | **B → A**, vom Nachbarn geworfen, Parameter \`pBackward\` |

Die Äpfel selbst bleiben rot/grün; die UI-Farben dienen der Kennzeichnung der Gartenseiten/Transportraten, nicht zwingend der Apfelfarbe.

In der Geschichte ist der **Junge geschickter**: \`pForward > pBackward\`. Deshalb liegt im stationären Zustand **mehr auf Seite B (älterer Mann)**.

**Story-Demopreset (Vorschlag, gesondert vom Default V0.2):**
- M=50 ME, A₀=50 ME, B₀=0
- \`pForward=0.08\`, \`pBackward=0.04\` (Junge doppelt so effizient).
- Stationärer Mittel-/Modellgrenzwert: A*=16⅔ ME, B*=33⅓ ME; Modellverhältnis B*/A*=2.
- Diese Bruchteile sind ein bewusst thematisierter Grenzfall der **deterministischen** Darstellung; sie sind **keine** wirklich halbierten Äpfel. Die Zahlen werden als Modelleinheiten gekennzeichnet.
- Bestehendes V0.2-Default 50/0 und 0.06/0.04 bleibt unverändert; neue Story-Parameter werden später nur als wählbares Preset angeboten.

## 3. Storyboard: fünf Phasen

### Phase I – Vorbereitungen zum Konflikt

**Szene:** Zaun und Apfelbaum zwischen zwei deutlich markierten Gärten; Junge links, älterer Nachbar rechts. Zu Beginn liegen alle bzw. fast alle zu verteilenden Äpfel auf Seite A. Der Baum bildet den erzählerischen Hintergrund.

**Aussage:** Die anfängliche Verteilung ist ein Anfangszustand, nicht die Gleichgewichtslage.

**Interaktion:** Gesamtsumme und Anfangsverteilung bestimmen; Hypothese: Wo werden am Ende mehr Äpfel liegen?

**Modellbedingung:** \`n=0\`. Wenn der Baum schon zu sehen ist, dürfen während des abgeschlossenen Modells **keine neuen Äpfel mehr herunterfallen**, weil \`A+B=M\` erhalten bleibt.

### Phase II – Der Junge wirft zuerst

**Szene:** Einige Äpfel fliegen links → rechts; auf B erscheinen Äpfel. Der Junge wirft zügiger.

**Aussage:** In einer Richtung entsteht Transport, solange dort Äpfel vorhanden sind. Bei B₀=0 ist der Rücktransport vor Schritt 1 null.

**Interaktion:** Einzelschritt ausführen; Hintransport und Bestand vorher/nachher vergleichen.

**Modellbedingung:** Erste Schritte; zunächst vor allem Hinrichtung. Kein künstlicher Modellschalter „Gegenreaktion erst ab Phase III“ – schon sobald B>0, ist der Rückprozess rechnerisch möglich.

### Phase III – Der Nachbar wirft zurück

**Szene:** Nun fliegen Äpfel in beide Richtungen, die gegensätzlichen Transporte sind durch Pfeile unterscheidbar. Beide Personen bleiben konsistente wiedererkennbare Figuren.

**Aussage:** Der Nettotransport ist Differenz aus Hin- und Rücktransport; die beiden Prozesse laufen gleichzeitig ab.

**Interaktion:** Richtungsbalken zeigen, welche Teilrate größer ist; ein Schritt verändert A/B um deren Differenz.

**Modellbedingung:** B>0 und beide Transportanteile>0.

### Phase IV – Gleiche Apfelzahlen, aber kein Gleichgewicht

**Szene:** Beide Gärten haben **ungefähr gleich viele** Äpfel. Der Junge befördert wegen seines größeren Transferanteils **mehr pro Schritt** nach rechts als der Nachbar zurück nach links.

**Aussage:** **A≈B ist kein Gleichgewichtskriterium**. Nur \`pForward*A ≈ pBackward*B\` kennzeichnet im vorliegenden Modell den stationären Zustand.

**Interaktion:** *Vorhersagefrage:* „Wenn auf beiden Seiten gleich viele Äpfel liegen – was geschieht im nächsten Schritt?“ Beide Raten zahlenmäßig vergleichen, dann einen Schritt ausführen.

**Modellbedingung:** Im Story-Preset wird ein Durchgang durch die Nähe \`A≈B\` sichtbar. Ein diskretes Modell trifft \`A=B\` nicht notwendigerweise exakt. Deshalb **kein künstliches Gleichsetzen oder Überschreiben**. Ein zusätzlicher Demonstrationsknopf könnte später einen gesonderten 25/25-Startzustand mit den gewählten Raten herstellen.

### Phase V – Dynamisches Gleichgewicht

**Szene:** Auf Seite des älteren Nachbarn liegen mehr Äpfel. Trotzdem fliegen weiterhin Äpfel in beide Richtungen, jetzt **gleich viel pro Schritt** (praktisch stationär mit der bekannten Toleranz).

**Aussage:** Die Bestände bleiben makroskopisch praktisch konstant, weil Hin- und Rückrate im Mittel gleich groß sind, **nicht** weil das Werfen aufhört.

**Interaktion:** Animation nicht anhalten; Transportbalken/Kugeln bleiben beidseitig sichtbar. Frage: „Wer hat gewonnen?“ – **Keiner** im Sinn einer endgültig geleerten Seite.

**Modellbedingung:** bestehende V0.2-Statuslogik „praktisch stationär“ (Toleranz, drei Schritte), nicht die Behauptung exakter mathematischer Gleichheit nach endlich vielen Schritten.

## 4. Gestaltungsvorgaben: fünf eigenständige Illustrationen

**Bildsprache (Vorschlag):** moderne, hochwertige 2D-Illustration für SEK I/II; freundlich-humorvoll, klar und auch am Beamer gut lesbar, **kein kindliches Bilderbuch für Vorschulkinder**.

Konstante Bestandteile:
- beide Gärten und der Zaun bilden einen festen, in allen Bildern wiedererkennbaren Raum;
- Junge links mit durchgehender Kleidung/Silhouette, älterer Mann rechts;
- der Apfelbaum in der Mitte bzw. hinter dem Zaun;
- identischer Bildausschnitt und Horizont; ruhiger Hintergrund;
- rote Äpfel vor dem gedeckten Gartenhintergrund gut sichtbar;
- ausreichend freie Flächen für spätere Beschriftung/animierte Pfeile;
- **keine** Beschriftungen, Zahlen oder Gleichungen in die eigentliche Bilddatei einrendern; UI zeichnet diese separat, korrekt und sprachlich austauschbar.

**Formate:** gemeinsames 16:9-Szenenraster, für Desktop/Projektion; später Bildausschnitte für kleinere Bildschirme. Stil- und Figurenreferenz nach dem ersten eigenständigen Bild festlegen.

**Urheberrechtlich:** keine direkte Nachzeichnung der fünf vorliegenden Buchseiten/Bildkompositionen, keine Übernahme ihrer Originalfiguren oder eingebetteten Texttafeln. Die fünf allgemeinen Handlungsmomente werden in einer **eigenen visuellen Komposition** erzählt. Für Zitate und Abbildungen anderer Institutionen separate Lizenzklärung.

**Für KI-gestützte Bilderstellung:** zunächst ein Styleboard/Charakterblatt, danach Szenen I–V mit stabiler Referenz; visuelle Konsistenz prüfen. Erst nach Freigabe Bewegungs- und Videoideen angehen.

## 5. Interaktive App – Integrationskonzept

**Ansichten (künftige App):**
- **„Geschichte“**: großzügige Bildszene + fünf Phasenmarker + 1–2 kurze Fragen.
- **„Modell“**: bestehende V0.2-Zylinder, Transfers und Stufenlinien.
- **„Vergleich“**: Szene und ausgewählte quantitative Anzeige gleichzeitig (für Workshop/Kongress-Projektion besonders attraktiv).
- Später **„Stechheber“**: realistischere Gefäße und explizit modellierte tatsächliche Volumenentnahme.

**Ein Zustand, mehrere Visualisierungen:**
- Werte aus einem unveränderten Modellkern \`advanceOneStep()\`.
- Wechsel zwischen Ansichten **ändert weder den aktuellen Schritt noch die Parameter oder die Historie**.
- Grafiken lesen nur denselben Simulationszustand; keine voneinander unabhängigen Modelle.
- In „Geschichte“ können Bildkarten und Phasen unabhängig von der laufenden Simulation erklärt werden. Die **fünf Phasen sind narrative Interpretationen**, keine universelle Zustandsmaschine für sämtliche frei wählbaren Parameter.
- Bei frei veränderten Parametern (z. B. gleich schnellen Werfern oder A₀=B₀) können bestimmte Szenen wie „Junge zuerst“ oder „Zahlen anfangs gleich“ entfallen. Deshalb gilt die vollständige Fünf-Phasen-Erzählung **nur für das definierte Story-Preset**. In anderen Parameterlagen werden keine falschen Phasen erzwungen.
- Erst wenn die SchülerInnen den Unterschied verstehen, zur formalen Darstellung mit p-Werten und Rate-Relation wechseln.

### Schematische Oberfläche

\`\`\`text
GLEICHGEWICHTS-LAB
[ Geschichte ] [ Modell ] [ Vergleich ] [ später: Stechheber ]

Geschichte/Animation              Zahlen / Forschungsfragen
┌────────────────────────────┐     ┌────────────────────────┐
│   Junge  ->  ||  <-  Mann  │     │ A (Junge):   … ME     │
│       Apfelbaum / Zaun    │     │ B (Nachbar): … ME     │
│      Äpfel auf 2 Seiten   │     │ A→B: …   B→A: …      │
└────────────────────────────┘     └────────────────────────┘

[I] [II] [III] [IV] [V]      [Start] [Pause] [Einzelschritt]
[Optional: Stufendiagramm / gesamter Verlauf / groß]
\`\`\`

## 6. Die Darstellung der Äpfel – Modelltreue

Bis zur späteren stochastischen Version werden rote Äpfel oder Apfelgruppen in der Szene **symbolisch** dargestellt:
- Bestände quantitativ ausschließlich im Zahlen-/Diagrammteil.
- Keine Behauptung „ein Bildapfel entspricht genau einem real geworfenen Apfel“.
- Bei größeren Mengen nicht alle einzelnen 200 Äpfel darstellen; Cluster, Dichte oder grafische Füllbereiche sind ausreichend.
- Die **zwei Transportsymbole** aus V0.2 stehen weiterhin für gegenläufige *Volumen-/Mengenströme*, selbst wenn sie grafisch zu stilisierten fliegenden Äpfeln werden.

**Spätere wissenschaftlich korrektere Alternative:** eigener Modus für *ganzzahlige, stochastische Äpfel* (z. B. Binomialübergänge aus den alten Beständen). Dann sind echte Fluktuationen bei endlicher Teilchenzahl möglich; **das deterministische Referenzmodell bleibt separat erhalten**. Kleine Schwankungen dürfen nicht willkürlich erst nach „Gleichgewicht erreicht“ hinzugefügt werden.

## 7. Entwicklungsphasen und Rückfallstrategie

**S0 – dieses Konzept:** fünf Storyphasen, fachliche Zuordnung, Kunst-/UI-Briefing, keine neue Appdatei.

**S1 – Bildwelt:** eigenständiges Figuren-/Szenenstyleboard; danach fünf konsistente Illustrationen. Entscheidungen zu Stil und Wiedererkennbarkeit im Dialog treffen.

**S2 – statische Einbindung:** ein „Geschichte“-Modul mit fünf Bildkarten und Erläuterungen, unabhängig vom Modell und ohne aufwendige Animation. **V0.2 bleibt unverändert** als erste Rückfallversion.

**S3 – dynamische Verknüpfung:** Story-Preset, Ansichtswechsel ohne Zustandsänderung, Datenanzeigen neben Szenen, symbolische Äpfel bewegen sich synchron zum Modell.

**S4 – erweiterte Didaktik:** Hypothesen-/Aufgabenmodus, Vergleich Phase IV/V, Nachweis Modellgrenzen, Ergebnisfesthaltung.

**S5 – spätere Erweiterungen:** stochastische Äpfel, echtes Stechhebermodell, Le Chatelier und komplexere Gleichgewichte.

**Abnahmefragen für S2/S3:**
1. Erkennt man auf allen fünf Bildern zweifelsfrei, wer auf welcher Seite steht?
2. Bleiben die beiden Personen und der Garten über die Bildfolge identisch?
3. Ist Phase IV (gleiche Bestände, unterschiedliche Raten) mit Phase V (ungleiche Bestände, gleiche Raten) verständlich vergleichbar?
4. Bleibt die Mengenbilanz erhalten? Entstehen keine neuen Äpfel durch den Baum während der Simulation?
5. Werden die A/B-Zuordnung und Pfeilrichtungen korrekt angezeigt?
6. Bleiben Geschichte, Modell und Vergleich beim Umschalten auf demselben Zustand?
7. Laufen beide positiven Transportrichtungen im stationären Zustand sichtbar weiter?
8. Funktioniert mindestens die Basisfassung ohne KI und Internet?
9. Sind externe Abbildungen rechtlich sauber ersetzt und alle KI-generierten Bilder auf fachliche Fehler geprüft?

## 8. Material- und Quellenbasis

- Dickerson/Geiss: *Chemie – eine lebendige und anschauliche Einführung*; vom Nutzer als Bilder/Textauszug bereitgestellt.
- [Universität zu Köln – Apfelkonflikt 2.0](https://van-der-waals.pc.uni-koeln.de/angewandte-chemiedidaktik/kinetik-und-chemisches-gleichgewicht/apfelkonflikt-20): deterministische und stochastische Ansätze samt anspruchsvolleren Erweiterungen.
- [Universität zu Köln – Stechheberversuch](https://van-der-waals.pc.uni-koeln.de/angewandte-chemiedidaktik/kinetik-und-chemisches-gleichgewicht/stechheberversuch).
- [Universität Wuppertal – Stechheberversuch](https://chemiedidaktik.uni-wuppertal.de/de/digitale-medien/videos-zu-klassischen-schulversuchen/allgemeine-chemie-i-anorganische-chemie/der-stechheberversuch/).
- [Vorhandenes V0.2](../prototyp/v0.2/index.html) und [Workshop-Aufgaben](WORKSHOP_AUFGABEN_V0_2.md).

## 9. Konzept-Prompt für die nächste Gestaltungsrunde (kein Release-Prompt)

> Erstelle ein **eigenständiges visuelles Konzept/Styleboard** für eine fünfteilige naturwissenschaftliche Bildergeschichte namens „Die Fallobstschlacht“ für SchülerInnen der SEK I/II. Zwei konsistente, gut unterscheidbare Figuren stehen in zwei Gärten links/rechts eines Zauns: links ein Junge, rechts ein älterer Nachbar. Zwischen den Grundstücken ein Apfelbaum. Stil: moderne hochwertige, freundlich-humorvolle 2D-Illustration, nicht kindlich, kräftige aber gedämpfte Farben, gleicher Kamerablick, ruhiger Hintergrund, Platz für spätere UI-Beschriftung. Die Handlung führt über (I) Anfangsverteilung, (II) zuerst links→rechts, (III) Gegenwerfen, (IV) gleiche Bestände bei **ungleichen** Transportraten, (V) **ungleiche** Bestände bei **gleichen** positiven Transportraten. Erstelle keine Nachzeichnung oder Variation vorhandener Buchzeichnungen, sondern eine eigenständige Bildwelt; keine Schrift/Gleichungen in den Bildern. Zunächst **nur Stil/Charaktere** festlegen, danach die fünf Bilder einzeln und konsistent entwickeln. Fachliche Modellzahlen werden später getrennt in der Web-App erzeugt.

**Versionsregel:** Dieser Prompt beschreibt das nächste **Konzept-/Medienziel**. Wenn aus der Konzeption eine tatsächlich getestete Appversion wird, ist zusätzlich ein **konkreter Änderungs- und Reproduktions-Prompt für genau diese Version** in \`docs/PROMPTS/\` zu speichern.


## 10. Bildfeedback zur ersten Phase-III-Illustration (19.10.2026)

**Rückmeldung des Nutzers:** Die erste moderne Darstellung trifft die ursprüngliche didaktische Intention hervorragend; die **Seitenansicht zusammen mit der Vogelperspektive** soll als gestalterische Ausgangsbasis erhalten bleiben.

**Korrektur:** Die KI hat in den Gärten **Vorratskisten voller Äpfel** erfunden. Diese sind **kein Bestandteil des Modells** und werden aus zukünftigen finalen Illustrationen vollständig entfernt. Zusätzliche Vorratskisten würden die Interpretation eines offenen Systems mit ungezählten Äpfelvorräten begünstigen, während die zugrunde liegende Gesamtmenge im Modell konstant bleiben muss. Der Baum bleibt als **Hintergrund**; nach Simulationsbeginn fallen keine weiteren Äpfel hinzu.

**Zweite Gestaltungsidee angenommen:** Über oder unter der Seitenansicht wird eine **synchron ausgerichtete Draufsicht/Vogelperspektive** auf dieselben Gärten gezeigt, aus der die unterschiedliche *Flächendichte der am Boden liegenden Äpfel* intuitiv erkennbar ist. Beide Gärten sollten möglichst gleich groß sein, sonst ist Zahl nicht gleich Dichte; bei anderen Flächen muss die Darstellung auf Dichte und Fläche achten.

**Technisch wichtiger Folgeschritt für spätere animierte Ansichten:** Zunächst zwei **szenische Hintergrundebenen ohne fest eingebrannte zusätzliche Apfelbestände/Kisten** vorbereiten. Bewegliche bzw. am Boden liegende Äpfel und Transporte werden idealerweise als **separate, vom Modellzustand gesteuerte Grafikobjekte** über den Hintergrund gelegt. Sonst wären veränderte Apfelmengen nur als Standbild vorgetäuscht. Die Bilder dienen vorerst als Stil- und Kompositionsreferenz, nicht als numerisch korrekte Simulation.

**KI-Entwicklungserfahrung:** Bei zwei Bildversuchen wurden die Kisten trotz ausdrücklich gegenteiliger inhaltlicher Anweisung wieder erzeugt; hinzu kamen fest eingebrannte Beschriftungen und teils geänderte Figurengestaltung. Diese Versionen **sind nicht als korrigierte Mastergrafiken freigegeben**. Der Fehler wird als anschauliches Beispiel für die Notwendigkeit von menschlicher Sichtkontrolle dokumentiert.

**Freigabekriterien der nächsten wirklich nutzbaren Illustration:** keine Apfelkisten, keine neuen von außen hinzugefügten Äpfel, gleiche Figuren/Perspektiven, keine fest eingebackenen Formeln oder Modellzahlen, Flächendichten visuell unterscheidbar, dynamische Apfel-Overlay-Schicht möglich.
