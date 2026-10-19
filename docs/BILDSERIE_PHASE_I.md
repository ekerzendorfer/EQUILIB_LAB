# GLEICHGEWICHTS-LAB – Bildserie, Phase I: Ausgangssituation

**Stand:** 19. Oktober 2026 · **Status:** Bildentwurf generiert, noch **nicht freigegeben**  
**Motiv:** „Vorbereitung zur Fallobstschlacht“  
**Stilanker:** die im Dialog akzeptierte Version der Phase III ohne Vorratskisten, mit Seiten- und Vogelperspektive.

## 1. Was tatsächlich vorliegt

Am 19.10. wurde eine erste Phase-I-Illustration erzeugt: oben eine seitliche Gartenansicht, darunter eine synchrone Vogelperspektive. Junge links (blauer Hoodie, kurze helle Hose), älterer Mann rechts (Mütze, braune Weste), zentraler weißer Gartenzaun und Apfelbaum. **Keine Vorratskisten** oder eingebrannten Texte. Apfeldichte links deutlich höher als rechts. Die PNG-Datei liegt in der Gesprächsablage als \`apfelernte_im_geteilten_garten.png\`; sie wurde **nicht** mit dieser Textdokumentation als Binärdatei ins Repository eingecheckt.

**Rückmeldung steht noch aus; kein stillschweigendes Freigeben der Phase I.**

## 2. Fachliche Sichtprüfung

| Prüfkriterium | Bewertung |
| --- | --- |
| Gleicher grundsätzlicher Zeichenstil / Figuren wie Phase III | weitgehend gelungen |
| Doppelperspektive Seite und Vogelblick | gelungen |
| Jungen-Garten links, Mann-Garten rechts | gelungen |
| Keine Vorratskisten / zusätzlichen externen Apfelquellen | gelungen |
| Keine Textlabels im generierten Bild | gelungen |
| Initialzustand \`A₀=50, B₀=0\` | **nicht erfüllt**: einzelne Äpfel auf der rechten Gartenseite und mindestens ein Apfel in der Hand des Nachbarn |
| Beide Personen werfen noch **nicht** | im Wesentlichen erfüllt |
| Apfelbaum keine aktive Nachlieferung im geschlossenen Simulationsmodell | fachlich später ausdrücklich kennzeichnen |

### Warum die rechte Seite wirklich leer sein sollte

Für den angekündigten **Story-Startzustand** soll gelten:

\`\`\`text
Schritt n=0
A₀ = 50 ME (Junge, links)
B₀ = 0 ME (älterer Mann, rechts)
M  = A + B = 50 ME
\`\`\`

Die Bildwelt darf nicht den Eindruck erwecken, auf Seite B lägen schon Äpfel oder der Mann könne sie vor dem ersten Hintransport bereits aufnehmen. Der stehende Mann ist Beobachter, kein Werfer. In der mathematischen V0.2 sind Einheiten zunächst **kontinuierliche Modelleinheiten**, daher ist die dargestellte Zahl einzelner Bildäpfel ohne zusätzliche Festlegung noch keine exakte numerische Messung.

## 3. Korrekturauftrag für *diesen* Entwurf (gezielte Bildbearbeitung)

> Bearbeite den vorhandenen, akzeptierten Phase-I-Entwurf **als Bildedit**, keine Neugenerierung einer anderen Szene. **Entferne ausschließlich sämtliche Äpfel, die auf der rechten Gartenseite am Boden liegen, sowie den Apfel in der Hand des älteren Mannes.** Die rechte Gartenseite bleibt vor Beginn der Schlacht vollständig frei von am Boden liegenden oder von Personen gehaltenen Äpfeln. Der Mann soll mit leeren Händen zuschauen. Alle bereits links liegenden Äpfel bleiben erhalten. **Bewahre genau den bestehenden Stil, dieselben zwei Figuren, ihre Bekleidung und Körperhaltung, den Baum, die Zaunperspektive, Häuser, Farben, Lichtstimmung und das zweigeteilte Seiten-/Draufsicht-Layout.** Keine neuen Äpfel, keine Vorratskisten, keine Beschriftungen, keine Pfeile. Der Apfelbaum ist bloß Hintergrund. Beide Ansichten müssen konsistent dieselbe Szene darstellen.

**Begründung:** Bei vorigen Bildversuchen haben zu breite Neugenerierungsaufträge Stilabweichungen, Vorratskisten und fest eingebrannte Beschriftungen erzeugt. Deshalb bei Bedarf das bereits vorhandene konkrete Bild **eng begrenzt editieren**.

## 4. Abnahme nach Korrektur

- [ ] Im rechten Garten null Äpfel auf dem Boden (beide Perspektiven).
- [ ] Der Nachbar hält keine Äpfel und wirft noch nicht.
- [ ] Links erkennbar hohe Apfeldichte.
- [ ] Identische Charaktere und Raumstruktur im Vergleich zur akzeptierten Phase III.
- [ ] Keine Vorratskisten, keine Beschriftungen, keine zusätzlich herabfallenden Äpfel.
- [ ] Zwei Ansichten stimmen überein.
- [ ] Nach Freigabe als **Phase-I-Referenz** gesichert; spätere Storybilder an ihr und Phase III ausrichten.

## 5. Einordnung in den Mensch-KI-Dialog

Diese erste Phase-I-Iteration ist ein nützliches Beispiel für einen didaktischen Qualitätscheck: Das Bild wirkt auf den ersten Blick sehr überzeugend, widerspricht aber in einem Detail dem expliziten \`B₀=0\` des mathematischen Startzustands. Die Lehrkraft entscheidet die fachliche Gültigkeit, nicht die Bild-KI.

**Nächster Arbeitsschritt:** Gezielte Bildbearbeitung und Sichtprüfung mit dem Nutzer, anschließend Phase II. Erst danach Phase IV und V als besonders wichtige fachliche Gegenüberstellung.


## 6. Ergebnis nach der Korrekturrunde – 19.10.2026

Der hier dokumentierte Erstentwurf wurde durch eine **neue Phase-I-Fassung** ersetzt. Der Nutzer hat diese als Bildbasis ausdrücklich **akzeptiert**. Der Nachbargarten ist nun frei von auf dem Boden liegenden Äpfeln; der ältere Nachbar hält keinen Apfel. Der Bildentwurf enthält einen Titelbalken, der für die spätere App gegebenenfalls durch HTML-Beschriftung ersetzt wird. Die ältere Checkliste oben wird **als historische Dokumentation des früheren Fehlers** aufbewahrt.

Zusammen mit den weiteren Entwürfen gelten nun **alle Phasen I–V gestalterisch als akzeptiert**. Siehe [Bildserien-Abnahme](BILDSERIE_ABNAHME_19_10_2026.md); die PNG-Dateien sind derzeit noch Gesprächsdateien und **nicht** im Repository abgelegt.
