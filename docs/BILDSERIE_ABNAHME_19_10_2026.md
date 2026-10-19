# Bildserie Fallobstschlacht – Abnahme der Entwürfe I–V

**Stand:** 19. Oktober 2026  
**Freigabestand:** Alle fünf **Bildentwürfe** vom Nutzer gestalterisch akzeptiert. Dies ist eine **Storyboard-/Bildstilfreigabe**, **noch keine zahlengetreue Integration in eine dynamische App**. V0.2 bleibt unangetasteter Rückfallstand.

## 1. Zuordnung der Bildentwürfe

Alle Bilder zeigen oben eine Seitenansicht und unten eine Vogelperspektive derselben beiden Gärten. Die Figuren und der große Baum bleiben über alle Phasen wiedererkennbar.

| Phase | Bildstand im Gespräch (PNG-Dateiname) | Didaktischer Schwerpunkt | Bildstatus |
|---|---|---|---|
| I – Ausgangssituation | \`a_wide_illustrated_educational_scene_split_into_t.png\` | Äpfel zu Beginn links (A), rechts leer (B); Nachbar schaut zu | Gestalterisch freigegeben |
| II – Junge beginnt | \`apfelwurf_über_den_gartenzaun.png\` | Vorwärtswurf A→B dominiert; Nachbar reagiert noch nicht | Gestalterisch freigegeben |
| III – Gegenoffensive | \`apfelduell_im_sommergarten.png\` | Beide Richtungen aktiv, unterschiedliche Teilraten | Gestalterisch freigegeben (Stilreferenz) |
| IV – Noch kein Gleichgewicht | \`apfelduell_im_garten.png\` | Ähnliche Bodenbestände, aber noch unterschiedliche Transporte | Gestalterisch freigegeben |
| V – Dynamisches Gleichgewicht | \`apfelduell_im_sonnigen_garten.png\` | Mehr Äpfel auf Nachbarseite B, beide Transporte laufen weiter | Gestalterisch freigegeben |

**Dateistatus:** Die PNGs wurden in der Unterhaltung generiert. Diese Markdown-Datei **verlinkt keine noch nicht in GitHub abgelegten Binärdateien**; eine strukturierte Übernahme der Bilder in einen späteren \`assets/fallobst/\`-Ordner ist als nächster Medienverwaltungsschritt vorgesehen. Die in den Gesprächsdateien auftauchenden generischen Namen wie \`imagegen.png\` sind für die Repo-Ablage durch phasenspezifische Namen zu ersetzen. Phasen- und Dateizuordnung bei der Asset-Übernahme nochmals visuell prüfen.

## 2. Fachliche Freigabegrenzen

Die Zustimmung gilt den **Bildentwürfen** (Stil, Figuren, Handlung und Doppelperspektive). Eine dynamische, quantitativ richtige Darstellung verlangt zusätzliche Arbeit:

- Fall I soll mathematisch den Story-Start \`A₀=50,\ B₀=0\` repräsentieren. Das akzeptierte neue Bild zeigt rechts keine verstreuten Äpfel. Ein Titel ist teilweise direkt in die Phase-I-Grafik eingebettet: Für die dynamische Oberfläche künftig besser eine von der App gezeichnete Überschrift verwenden.
- Die Größen und die Anzahl der in den Bildern fliegenden oder am Boden liegenden Äpfel sind **nicht** exakt gleich den reellwertigen Modelleinheiten aus V0.2. Nicht als exakte Messwerte interpretieren.
- Phase IV: **Bestände A≈B** sind nicht hinreichend für stationäres Gleichgewicht, wenn \`pForward > pBackward\`.
- Phase V: **A*≠B*** und gleiche **mittlere** gegenläufige Teilraten; im deterministischen Modell wird der stationäre Zustand i. A. asymptotisch angenähert. Die Anzahl gezeichneter Wurfobjekte darf keine andere numerische Rate suggerieren.
- Keine Kisten, externen Vorräte oder zusätzliche herunterfallende Äpfel während der geschlossenen Modellrechnung. Äpfel am Baum sind nur Kulisse.
- Gleiche Gartenflächen sind für den späteren direkten Vergleich von *Apfeldichte* zu erhalten.

## 3. Spätere Umsetzung: Standbild versus echte Animation

**Phase A – Statische Bildserie:** Alle fünf Bildkarten in einer kleinen Story-Ansicht zeigen; didaktische Kommentare und Modellzahlen als separate HTML-Ebene.

**Phase B – Quantitative Synchronisierung:** Mehrfach verwendbarer, einheitlicher Gartenhintergrund ohne festgezeichnete Apfelmengen, darüber variable Apfel-/Cluster-Grafiken anhand desselben Modellzustands; die Vogelperspektive visualisiert Boden-Verteilung/Dichte. Der Rechenkern aus V0.2 bleibt Referenz.

**Phase C – Animation:** Fliegende Symbole und zwei Teilraten an den aktuellen Zustand koppeln. Zwischen Views (Geschichte, Modell, Vergleich) wechseln, ohne den Zustand neu zu initialisieren. Das freie Parametermodell darf nicht erzwungenermaßen dieselben fünf narrativen Phasen durchlaufen.

**Phase D – echtes Einzelapfel-Modell (optional, später):** Ganzzahlige stochastische Übergänge mit Fluktuationen, als fachlich klar anderer Modus getrennt vom deterministischen V0.2-Excel-Modell.

## 4. Erkenntnis zur KI-Bildarbeit

Die Korrekturrunden von Phase III und Phase I waren ein praxisnahes Beispiel für die **Notwendigkeit menschlicher Qualitätskontrolle**:
- unerwünschte Vorratskisten, Beschriftungen und inkonsistente Anfangsäpfel mussten wiederholt angesprochen werden;
- sehr begrenzte Bildbearbeitungsaufträge funktionierten besser als Neuinterpretationen der Szene;
- die Akzeptanz einer überzeugenden Illustration ist von der Freigabe eines wissenschaftlich validierten dynamischen Modells zu unterscheiden.

Für den VCÖ-Vortrag können die Iterationen in einer kompakten Vorher-Nachher-Folie genutzt werden (kein „Ein Prompt und alles fertig“).

## 5. Nächster kleiner Schritt

Eine **statische, offlinefähige Bildergalerie** als eigener kleiner Prototyp wäre der risikoarme nächste Integrationsschritt: Phasen I–V einzeln anzeigen, mit wenigen passenden fachlichen Fragen. Erst wenn diese Darstellung mit realen Bildern und deren Dateiablage sauber läuft, beginnen wir die Trennung in Hintergrund und veränderliche Äpfel und die technische Verknüpfung mit der Simulation.

**Wichtig:** V0.2 als Workshop-Rückfallversion nicht überschreiben. Jede neue Implementierung erhält einen eigenen dokumentierten Entwicklungs-Prompt und einen neuen Versionsstand.

## 6. Nachtrag: Statische Galerie und Story-Integration entstanden

Auf die erste offlinefähige Bildergalerie folgte eine **überarbeitete Galerie** mit einheitlich zugeschnittenen Perspektiven; der Nutzer meldete eine **zusätzliche weiße Linie in Phase III**. Die Ursache war die im Originalbild tiefer gelegene Trennzone.

In der anschließend entwickelten **integrierten Story-Ansicht V0.1** wurde diese Bildzone korrekt entfernt und mit einer einzigen standardisierten Trennlinie neu zusammengesetzt. Ebenso wurde die Phase-I-Überschrift aus dem sichtbaren Bildausschnitt entfernt. Die volle Apfelgeschichte ist mit Navigation, Leitfragen und Ansichtswechsel ausgestattet. Der Modellreiter ist noch Platzhalter, der Vergleichsreiter **qualitativ** und **nicht numerisch gekoppelt**.

Zum Entstehungs-Prompt und tatsächlichen Code-Ablagestatus siehe [PROMPTS/STORY_V0_1.md](PROMPTS/STORY_V0_1.md).
