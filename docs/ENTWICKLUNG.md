# GLEICHGEWICHTS-LAB – Entwicklungsjournal und Konzeptstand

**Stand:** 18. Oktober 2026  
**Status:** Konzept-/Workshopplanung, noch kein implementiertes App-Release  
**Projekt:** CHEMIE mit KI · GitHub-Repository: [EQUILIB_LAB](https://github.com/ekerzendorfer/EQUILIB_LAB)

> Diese Datei dokumentiert die wesentlichen Entscheidungen, Ideen, offenen Fragen und fachlichen Prüfungen aus unserer gemeinsamen Entwicklung. Sie ist ausdrücklich **kein** vollständiges Prompt-Protokoll. Fortschreibungen erfolgen bei unseren nächsten aktiven Arbeitsschritten, nicht automatisch im Hintergrund.

## 1. Projektziele und Anlässe

**GLEICHGEWICHTS-LAB** soll eine browserbasierte, möglichst kostenfreie und ohne Installation nutzbare Lernumgebung zum **dynamischen chemischen Gleichgewicht** werden.

Die App erfüllt zwei Rollen:

- **Unterricht:** fachlich korrekte, attraktive Brücke zwischen anschaulicher Analogie, Realmodell und mathematischer Beschreibung.
- **Fortbildung:** praktisches Beispiel, wie Lehrkräfte mithilfe eines *iterativen Mensch-KI-Dialogs* selbst Unterrichtswerkzeuge entwickeln, prüfen und verbessern können.

**Termine / Kontexte:**
- **Februar 2027:** dreistündiger Workshop an der Schule; Teilnehmende mit heterogenen KI-Voraussetzungen.
- **1. April 2027:** 200-minütiger Workshop beim VCÖ-ChemielehrerInnenkongress in Linz.
- **2. April 2027, ca. 16 Uhr:** 30-minütiger Vortrag »CHEMIE mit KI«; das GLEICHGEWICHTS-LAB ist ein Beispiel für KI-gestützte App-Entwicklung.

## 2. Didaktische Leitidee: drei Abstraktionsebenen

Das besondere Merkmal soll die **vergleichende, synchrone Darstellung bzw. Überblendung** dreier Perspektiven sein:

1. **Fallobstschlacht / Apfelkrieg (Dickerson/Geiss):** Zwei Seiten tauschen Äpfel aus. Hin- und Rücktransport hängen von der jeweiligen verfügbaren Menge und den Transportfaktoren ab. Auch bei stabilen Beständen bleibt der Austausch aktiv.
2. **Stechheberversuch:** Zwei Flüssigkeitsgefäße. In diskreten Schritten werden Volumina in beide Richtungen übertragen. Die Wasserstände verändern sich stufenweise und erreichen unter geeigneten Bedingungen eine stationäre Verteilung.
3. **Abstrakte Simulation:** einfachster reversibler Prozess \(A \rightleftharpoons B\), mit Mengen-/Konzentrationsverlauf, Hin- und Rückgeschwindigkeit, Gleichgewichtskonstante und gezielten Störungen.

**Zentrale Lernerkenntnisse:**
- Stationäre makroskopische Mengen bedeuten nicht, dass die gegenläufigen Vorgänge zum Stillstand kommen.
- Im dynamischen Gleichgewicht stimmen Hin- und Rückgeschwindigkeit überein; die Gleichgewichtsmengen müssen **nicht** gleich groß sein.
- Die drei Darstellungsformen sind **Analogien und Modelle**, keine vollständig identischen physikalischen bzw. chemischen Prozesse. Modellgrenzen müssen thematisiert werden.

### Besondere Visualisierungsidee (17.10.)

Parallel sichtbar sollen sein:
- **Zwei transparente Zylinder:** Wasserstände springen bei jedem Transferschritt auf neue Werte.
- **Balken- bzw. Stufendiagramm:** diskontinuierliche Volumen-/Mengenentwicklung bleibt erkennbar, auch während Animationen laufen.
- **Fliegende Kugeln bzw. Äpfel:** Hin- und Rücktransport werden *auch bei konstanten Endwerten* weiterhin gezeigt; zunächst symbolisch, später ggf. stochastisch.
- **Mengen- und Geschwindigkeitskurven:** erlauben den Übergang zur formalen Interpretation.
- Umschalten/Überblenden zwischen den drei Bildwelten, möglichst mit synchronen Parametern und Zeit-/Schrittstand.

Wichtige Präzisierung: Die erste Version ist **deterministisch**; animierte ganze Äpfel dürfen nicht vortäuschen, dass die zugrunde liegende Rechnung bereits ein stochastisches Einzelteilchenmodell ist.

## 3. Mathematischer Ausgangspunkt

Vorliegende Excel-Dateien: ursprünglich \`EQUILIB.XLS\`, danach \`EQUILIB.xlsm\`.

Bisher besprochenes **diskretes Zwei-Mengen-Modell**:

\[
A_{n+1}=A_n-k_{\mathrm{hin}}A_n+k_{\mathrm{rück}}B_n
\]
\[
B_{n+1}=B_n+k_{\mathrm{hin}}A_n-k_{\mathrm{rück}}B_n
\]

Bei \(0\leq k_{\mathrm{hin}},k_{\mathrm{rück}}\leq1\) bleibt die Gesamtmenge \(A+B\) im gezeigten Transfermodell erhalten. Beide Teiltransfers werden aus **demselben Zustand vor dem Schritt** berechnet.

**Kontrollbeispiel:**
- Start: \(A_0=50,\ B_0=0,\ k_{\mathrm{hin}}=0{,}06,\ k_{\mathrm{rück}}=0{,}04\).
- Schritt 1: \(A_1=47,\ B_1=3\).
- Schritt 2: \(A_2=44{,}30,\ B_2=5{,}70\).
- Gesamtmenge stets 50.
- Stationär: \(A^*=20,\ B^*=30\), Verhältnis \(B^*/A^*=k_{\mathrm{hin}}/k_{\mathrm{rück}}=1{,}5\).

Die konkrete geometrisch-physikalische Entsprechung zum Stechheberversuch (Querschnitte, Entnahmehöhen, Volumengrenzen) ist für die realistische Darstellung **noch fachlich zu prüfen**. Auch die Bedeutungen der Koeffizienten dürfen nicht unbesehen als Geschwindigkeitskonstanten realer chemischer Reaktionen ausgegeben werden.

## 4. Entwicklungsstufen

### V1 – Workshopfähiger Kern (Priorität)

Eine einzige lokal ausführbare **\`index.html\`** mit HTML, CSS und JavaScript; keine externen Bibliotheken, kein Build-System, kein Backend und keine API-Schlüssel.

Minimalfunktionen:
- zwei Mengen bzw. Zylinder;
- Parameter für Hin- und Rücktransport;
- Start/Pause, **Einzelschritt**, Reset;
- zahlenmäßige Mengenanzeige;
- diskrete Balken/Verlaufsdiagramme;
- überprüfbare Konservierung der Gesamtmenge;
- sichtbare gegenläufige Transportpfeile oder einfache Kugelanimation.

**Didaktischer Minimalerfolg:** Eine eigene, durch KI unterstützte, fachlich überprüfte Verbesserung an einem lauffähigen Starterprojekt.

### V2 – Didaktisches Highlight
- moderne eigene Fallobst-Illustrationen und ggf. kurzes Erklärvideo;
- realitätsnaher Stechheber;
- synchrone Überblendung/vergleichende Ansichten;
- geführte, teiloffene und offene Aufgaben;
- Ergebnissicherung mit dokumentierten Parametern, Beobachtungen und Aussagen.

### V3 – Fachlicher Ausbau
- stochastische Einzelteilchen-Simulation mit Fluktuationen;
- Störung und Neueinstellung;
- komplexere Gleichgewichte als \(A \rightleftharpoons B\);
- Le Chatelier einschließlich korrekt begründeter Temperaturabhängigkeit;
- Katalysatorwirkung und weitere Transferaufgaben.

## 5. Workshopprinzip: Heterogenität abfedern

Die Teilnehmenden verfügen voraussichtlich über unterschiedliche KI-Anbieter, Modellleistungen und Nutzungslimits; manche haben **keinen** eigenen KI-Zugang.

**Verbindliche Konsequenzen:**
- Kein kostenpflichtiger KI-Account und **kein GitHub-Konto** als Eintrittsvoraussetzung.
- Notebook/PC und moderner Browser genügen; einfacher Texteditor für eigene Codeänderungen.
- **Alle beginnen mit einem getesteten funktionierenden Starterstand**, nicht mit einem leeren Editor und einem umfassenden »Mach mir eine App«-Prompt.
- Gruppenarbeit und zentraler Demonstrations-KI-Zugang sind ausdrücklich vorgesehen.
- Nicht alle müssen dasselbe Zusatzfeature fertigstellen; alle müssen eine fachliche Änderung verstehen und prüfen.
- Lokal geöffnete \`index.html\` muss unabhängig von GitHub und Internet funktionieren.

### Rückfallstufen A–D

- **A:** TN entwickeln in Gruppen mit eigenen KI-Zugängen.
- **B:** Zentral gesteuerter KI-Dialog am Beamer, TN liefern Anforderungen und prüfen Lösungen.
- **C:** Vorbereiteter, teilfertiger Prototyp als Arbeitsgrundlage für gezielte Erweiterungen.
- **D:** Offline-/Netzausfallbetrieb mit getesteten Entwicklungsständen, Materialien und dokumentierten Prompt-Ausschnitten.

**Erwarteter Hauptmodus: B + C.**

### Vorgeschlagene Sicherungsstände

- \`00_START\` – Zahlen/Balken, Einzelschritt und Reset.
- \`01_PARAMETER\` – veränderbare Transportanteile.
- \`02_DIAGRAMM\` – diskrete Verlaufsgrafik.
- \`03_VISUALISIERUNG\` – Zylinder und symbolische Animation.
- \`04_REFERENZ\` – getestete Vorführfassung.

Dies sind **geplante Dateien**, noch keine im Repository vorhandenen Implementierungen.

### Zeitliche Orientierung (Februar, 180 Min.)

- 0–15 min: Kontext, Apfelkonflikt, Ziel.
- 15–35 min: Excel-Modell und Starter-App.
- 35–50 min: Entwicklungsauftrag/Prompt formulieren.
- 50–85 min: erste Änderung, testen.
- 85–95 min: Pause.
- 95–130 min: zweite Runde, Fehlersuche.
- 130–160 min: Ergebnisse vergleichen.
- 160–180 min: didaktische Reflexion und Ausblick.

Die allgemeine KI-Einführung soll **kurz, praxisnah und an die Aufgabe gekoppelt** sein. GitHub-Veröffentlichung wird in einen optionalen **Mini-Onlinekurs** ausgelagert; der Workshop widmet sich dem Entwickeln und Prüfen.

## 6. Bedeutung für den VCÖ-Vortrag

Dramaturgischer Einfall: Aus Excel-Modell und Versuchsbeschreibung wird scheinbar durch einen einzigen Prompt eine vorführbare App. **Nach kurzer Inszenierung wird ausdrücklich offengelegt**, dass mehrere Schritte, Fehler und fachlich-didaktische Prüfungen nötig waren. Kernbotschaft: Nicht der magische Prompt, sondern die Zusammenarbeit von Lehrkraft und KI erzeugt Qualität.

Deshalb werden aussagekräftige Entwicklungsetappen, Zwischenstände und beispielhafte Prompts gesammelt – keine vollständige Transkription jedes Dialogs nötig.

Die vollständige 30-minütige Kongressdramaturgie umfasst zusätzlich ein reales Brausetabletten-/WAAGE_LAB-Experiment, das digitale Analytiklabor und den geplanten KI-Laborassistenten. Das GLEICHGEWICHTS-LAB steht für die **KI-gestützte Entwicklung eines neuen Unterrichtswerkzeugs**.

## 7. Materialien und externe Referenzen

- Ausgangsmodell: \`EQUILIB.xlsm\` (liegt aus dem Gespräch vor; noch nicht ins Repository übernommen).
- Unterrichtsmaterial Göttingen: http://www.unterrichtsmaterialien-chemie.uni-goettingen.de/exp_neu.php?id=2150
- Demonstrationsvideo: https://www.youtube.com/watch?v=8XzgpEN2bDw
- Wuppertal, Stechheberversuch: https://chemiedidaktik.uni-wuppertal.de/de/digitale-medien/videos-zu-klassischen-schulversuchen/allgemeine-chemie-i-anorganische-chemie/der-stechheberversuch/
- Köln, Stechheber: https://van-der-waals.pc.uni-koeln.de/angewandte-chemiedidaktik/kinetik-und-chemisches-gleichgewicht/stechheberversuch
- Köln, Apfelkonflikt 2.0: https://van-der-waals.pc.uni-koeln.de/angewandte-chemiedidaktik/kinetik-und-chemisches-gleichgewicht/apfelkonflikt-20

Originalabbildungen aus Büchern sind didaktische Referenzen; für die öffentliche App sind **eigenständig gestaltete Bilder** und geklärte Bildrechte vorgesehen.

## 8. Entwicklungsjournal (bisherige Wegmarken)

### 17. Oktober 2026 – Von einer Excel-Simulation zum App-Konzept
- Fallobstschlacht, Stechheber und \`A \rightleftharpoons B\` als zusammengehörige Darstellungen identifiziert.
- Name **GLEICHGEWICHTS-LAB** festgelegt.
- Synchrone Zylinder-/Balken-/Apfeltransport-Vision und Erweiterbarkeit beschlossen.
- Reduzierter Workshop-Kern von späterer reichhaltiger App abgegrenzt.
- Idee eingeführt, die Mensch-KI-Entwicklung für Workshop und Kongress zu dokumentieren.

### 18. Oktober 2026 – Heterogene Voraussetzungen ernst nehmen
- Zusätzliche Referenz **Apfelkonflikt 2.0** ergänzt.
- Deterministischer Kern vor späterem stochastischem Modell priorisiert.
- Workshop-Ziel neu gefasst: kleine **funktionierende Erweiterung** statt vollständiger Entwicklung von null.
- Rückfallkonzept A–D, Offlinebetrieb und vorbereitete \`index.html\`-Sicherungsstände.
- GitHub-Konto und kostenpflichtige KI ausdrücklich optional.
- Eigenes Repository \`ekerzendorfer/EQUILIB_LAB\` als zentraler Dokumentationsort eingerichtet.
- GitHub-Publikation der TN-Projekte soll **kein regulärer Workshopteil** sein; stattdessen perspektivisch ein kurzer Onlinekurs.
- Allgemeiner Überblick über KI-Möglichkeiten soll in **wenigen einführenden Minuten** Platz finden.

## 9. Offene Entscheidungen und nächste Schritte

1. Die beiden fachlichen Modelle (Excel-Transfer und konkret realer Stechheber) gegeneinander abgleichen.
2. Minimal-App V1 und fachliche Akzeptanztests endgültig spezifizieren.
3. UI-Anordnung für synchrone Zylinder, Diskretschritte und Symbolteilchen skizzieren.
4. Erste lauffähige \`index.html\` samt Testfällen erzeugen.
5. Sichere Zwischenstände und spezifische KI-Änderungsaufträge für den Workshop vorbereiten.
6. Ein kurzes Einführungssegment »Was KI im Chemieunterricht leisten kann« gestalten.
7. Visuelle Neufassung der Fallobstschlacht mit konsistentem eigenständigem Stil erarbeiten.
8. Test mit verschiedenen kostenlosen KI-Zugängen vor dem Februarworkshop.

**Dokumentationsregel:** Bei jeder relevanten Entwicklungsrunde Status, fachliche Entscheidungen, Probleme/Korrekturen und offene Fragen knapp ergänzen; keine behauptete automatische Hintergrundüberwachung.


### Präzisierung vom 18. Oktober 2026 – allgemeine KI-Einführung und GitHub

**Einstieg (ca. 12 Minuten):** KI nicht als isolierte Chatbot-Demonstration behandeln, sondern in fünf Rollen knapp sichtbar machen: (1) Fachinhalte erklären und kritisch prüfen, (2) differenzierte Aufgaben und Unterrichtsmaterial entwerfen, (3) Bilder/Animationen und Modelle visualisieren, (4) Daten analysieren, (5) eigene Lernwerkzeuge entwickeln. Die Rolle von Agenten kann als Ausblick erscheinen. Nur kurze Beispiele, keine separaten Live-Demos.

**Aktualisierte Zeitidee für den 180-minütigen Workshop:** 12 Minuten KI-Einführung, 18 Minuten Apfelkonflikt/Stechheber und mathematisches Modell, 15 Minuten Starter-App zeigen, 15 Minuten gemeinsamen Änderungsauftrag formulieren, 40 Minuten erste Entwicklungsrunde, 10 Minuten Pause, 40 Minuten zweite Entwicklungsrunde, 20 Minuten Beispiele/Fehlerdiskussion, 10 Minuten Ergebnissicherung und Weiterarbeit. Summe 180 Minuten.

**GitHub Free / Pro:** Der vorhandene kostenlose Plan ist für ein öffentliches Repository und GitHub Pages ausreichend. Pro bringt hauptsächlich zusätzliche Limits und Funktionen, insbesondere für private Repositories, ist aber weder für dieses Projekt noch für die Workshopteilnahme erforderlich. Ein spezieller GitHub-Pages-Minikurs soll bei Interesse **getrennt** angeboten werden; GitHub im Workshop ist kein Muss.
