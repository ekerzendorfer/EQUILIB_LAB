# EQUILIB_LAB – Übergabe für neuen Chat (01.11.2026)

**Projekt:** GLEICHGEWICHTS-LAB / Fallobstschlacht / Stechheber / dynamisches Gleichgewicht  
**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB  
**Freigegebener Arbeitsstand:** **integriert v0.3e vom 31.10.2026**  
**Zielgruppe:** Workshop für Lehrkräfte im Februar 2027 (180 Minuten); später VCÖ Linz 2027.  
**Arbeitsprinzip:** Kleine, einzeln überprüfbare Änderungen; chemisch-mathematische und didaktische Prüfung vor der Freigabe. Bereits akzeptierte Versionen unverändert aufbewahren.

## 1. Verifizierter Repository-Stand

Am 01.11.2026 über den verbundenen GitHub-Zugang geprüft:

- `main/index.html`: **2.582.076 Byte**, Blob-SHA `0c0f93c81e0818d8695685f416645d67f1be4a2b`.
- `prototyp/integriert-v0.3e/index.html`: **identischer Blob-SHA** – derzeit dieselbe App wie die Root-Datei.
- Freigabe-/Dokumentations-Commit vom 31.10.2026: `80b33a22c53762bcfb95ffc32a9d2ac91fda65d4` (»release: integrierte v0.3e und kompakte Workshop-Dokumentation«).
- Maßgeblicher fachlicher Stand: [ENTWICKLUNGSSTAND_V0_3E_2026-10-31.md](ENTWICKLUNGSSTAND_V0_3E_2026-10-31.md).
- Weitere Basisdokumente: [ENTWICKLUNG.md](ENTWICKLUNG.md), [FALLOBST_KONZEPT.md](FALLOBST_KONZEPT.md), [FUNKTIONSSPEZIFIKATION_V1.md](FUNKTIONSSPEZIFIKATION_V1.md), [WORKSHOP_AUFGABEN_V0_2.md](WORKSHOP_AUFGABEN_V0_2.md).

**Wichtig:** v0.3e ist fachlich-didaktisch als Zwischenstand akzeptiert, aber noch kein vollständig browser-, mobil- und offlinegetestetes V1-Release.

## 2. Was v0.3e kann

Eine HTML-App mit drei Reitern, gemeinsamem mathematischem Zustand:

1. **Geschichte:** fünf Szenen der Apfelschlacht, je Seiten- und Vogelperspektive, Fachfragen, aktuelle Modellmengen; automatische Bildphase nach Modellzustand, manuelles Blättern zwischen Rechenschritten weiterhin möglich.
2. **Modell:** zwei Mengen/Zylinder, symbolischer gegenläufiger Transport, Rechenschritte und Stufendiagramm, zwei quadratische Gärten mit insgesamt 60 proportional gerundeten Symbolkreisen.
3. **Vergleich:** Story-Bildphase, synchronisierte Symbolgärten, Modellzylinder/Gegenströme und ein zusätzliches zeitgleiches Stufendiagramm.

Die Symbolkreise können auch bei nahezu stationären Mengen ihre Position wechseln; neu geänderte Kreise werden kurz hervorgehoben (etwa 1–2 Schritte). Ein vereinzelter ±1-Kreis-Puls nahe der Stationarität ist **ausschließlich bildlich**; die deterministische Rechnung bleibt unverändert.

## 3. Verbindliches Rechenmodell und Preset

Beide Gegenströme werden pro Schritt **aus den alten Beständen** berechnet:

```text
H_n = p_hin · A_n
R_n = p_rueck · B_n
A_(n+1) = A_n − H_n + R_n
B_(n+1) = B_n + H_n − R_n
A_n + B_n = M  (konstant)
```

Apfelschlacht-Preset: `M = 50`, `A0 = 50`, `B0 = 0`, `p_hin = 0,08`, `p_rueck = 0,04`. Die stationären Werte sind `A* = 16,67 ME`, `B* = 33,33 ME`. `ME` sind kontinuierliche Modelleinheiten, **keine ganzzahligen Äpfel**. Gleiche Gegenströme bedeuten nicht gleiche Bestände.

## 4. Akzeptierte Bildphasensteuerung v0.3e – NICHT versehentlich verändern

Eine gemeinsame Funktion steuert die Phasen in **Geschichte und Vergleich** nach dem tatsächlichen Anteil `B/M`; identisches Verhalten bei **Einzelschritt und Automatik**:

| Bedingung | Bildphase |
|---|---|
| Start oder B/M < 5 % | I: Ausgangssituation |
| 5 % ≤ B/M < 40,5 % | II: Junge beginnt |
| 40,5 % ≤ B/M < 43 % | III: Gegenoffensive |
| 43 % ≤ B/M < 63 % | IV: Noch kein Gleichgewicht |
| B/M ≥ 63 % und beide Gegenströme positiv | V: Gleichgewichtsszene |

Abgestimmte Beispiele: `43:7`, `37:13` und `30:20` sind **noch Phase II**; Phase III beginnt erst ungefähr bei `29:21`; Phase V erscheint ungefähr bei `18:32`.

**Fachlicher Vorbehalt:** Phase V ist eine **illustrierte Annäherung**, kein Beweis identischer Raten. Bei `18:32` ergeben sich `H = 1,44` und `R = 1,28` ME/Schritt. Die Bildphasen-Schwellen wurden an die vorhandenen Illustrationen angepasst; sie sind **keine allgemeingültigen Gleichgewichtskriterien**.

## 5. Neue Architekturfrage: Bilder aus der HTML-Datei auslagern?

Die App ist derzeit eine **einzelne, offlinefähige HTML-Datei**, mit den **fünf Phasen und zehn Bildausschnitten direkt eingebettet**; dies ist auch in `README.md` beschrieben. Die Root-Datei umfasst ca. **2,58 MB**. Für die weitere Bearbeitung ist eine Trennung von Code und Grafiken empfehlenswert, **aber nicht innerhalb der bereits freigegebenen v0.3e**.

Empfohlener kleiner Refactoring-Schritt (eigenes Zwischenrelease, z. B. `v0.3f`):

- Archiviertes `prototyp/integriert-v0.3e/index.html` **unverändert behalten**; dies bleibt die jederzeit lauffähige **Single-HTML-Workshop-Fallback-Version**.
- Bilddaten aus der HTML-Datei ohne Qualitätsverlust extrahieren, soweit es tatsächlich eingebettete `data:`-Bildquellen sind; **keine Neugenerierung**, keine Veränderung des Bildausschnitts. Vorab Quellstruktur prüfen und die zehn Bildausschnitte den fünf Phasen/Perspektiven zuordnen.
- Bilder zentral unter `assets/fallobst/` ablegen, z. B. `phase-01-seite.png`, `phase-01-vogel.png` ... `phase-05-vogel.png`. Die Endungen müssen den **tatsächlichen Dateiformaten** entsprechen; WebP-Kompression nur nach gesonderter Sichtprüfung.
- Nur die Bildquellen auf **relative Pfade** umstellen (z. B. `assets/fallobst/phase-01-seite.png`), keine Änderung an Rechenmodell, Synchronisierung oder Oberflächenlogik. Falls ein Prototyp unter `prototyp/integriert-v0.3f/` liegt, die Pfade relativ von **diesem** Ordner aus korrekt setzen (z. B. `../../assets/fallobst/...`).
- **Offlinebetrieb bleibt möglich**, allerdings nur, wenn HTML und Bildordner gemeinsam weitergegeben werden (am einfachsten als ZIP mit funktionierender Ordnerstruktur). Eine isolierte HTML-Datei wäre nach dieser Umstellung **nicht mehr vollständig offlinefähig**.
- Die Aufteilung reduziert die HTML-Quelltextgröße und erleichtert KI-/GitHub-Codebearbeitung. Die Bilddaten müssen beim ersten Laden weiterhin übertragen werden; sie verschwinden nicht, sondern liegen nur als separate Dateien vor.

**Entscheidungsvorbehalt:** Für den Anfänger-Workshop kann die einfache Single-HTML-Fassung sinnvoller bleiben. Deshalb **zwei Nutzungswege** erhalten: v0.3e als portable Einzeldatei und eine schlankere modularisierte Entwicklungsfassung. Erst nach erfolgreich geprüfter Auslagerung über einen Wechsel der Hauptdatei `main/index.html` entscheiden.

## 6. Abnahmetests für eine ausgelagerte Fassung

- Alle **fünf Bildphasen × zwei Perspektiven** sind vollständig, korrekt zugeordnet und ohne Crop-/Trennlinienfehler sichtbar (insbesondere Phase I ohne unerwünschte Beschriftung, Phase III ohne doppelte weiße Linie).
- Ansicht **Geschichte** und **Vergleich** zeigen nach jedem Rechenschritt dieselbe korrekte Bildphase.
- Einzelschritt und Auto-Lauf wechseln Bildphasen nach denselben Grenzen; Reset und Preset-Wechsel funktionieren.
- `A+B=M` bleibt erhalten; die Rechenwerte entsprechen v0.3e; Diagramme und 60 Symbolkreise funktionieren unverändert.
- Test auf **GitHub Pages** und lokal per **Doppelklick** auf eine mit Bildern gespeicherte/entpackte Verzeichnisstruktur, möglichst auch bei getrennter Internetverbindung.
- Nach erfolgreichem Test neues Release dokumentieren; **v0.3e nie überschreiben**.

## 7. Nächste fachlich-inhaltliche Stufe

Die nächste inhaltliche Version `v0.4` **erst nach Festlegung ihrer Anforderungen** beginnen, nicht mit ungetestetem Refactoring vermischen. Als längerfristiger Ausbau diskutiert: eine **echte chemische Reaktion**, etwa eine Esterbildung mit sinnvoller Gleichgewichtslage (K in der Größenordnung 1), zunächst nur als Kugelmodell; später Störung des Gleichgewichts nach Le Chatelier (Edukte zugeben, Produkt/Wasser entziehen, Temperaturänderung). Das ist **noch nicht implementiert** und nicht Bestandteil der v0.3e-Abnahme. Chemische Stöchiometrie, Reaktionsquotient, temperaturabhängige Gleichgewichtskonstante und Dynamik sind gesondert fachlich festzulegen.

## 8. Fortsetzungsprompt für den nächsten Chat

> Wir setzen das Projekt **EQUILIB_LAB** auf GitHub fort. Lies zuerst `docs/UEBERGABE_NEUER_CHAT_2026-11-01.md` und `docs/ENTWICKLUNGSSTAND_V0_3E_2026-10-31.md`. Der akzeptierte Stand ist v0.3e; `main/index.html` und `prototyp/integriert-v0.3e/index.html` waren zum Prüfzeitpunkt identisch. Arbeite weiterhin in sehr kleinen, fachlich getesteten Schritten. Als nächstes wollen wir entscheiden bzw. umsetzen, wie die zehn eingebetteten Apfelschlacht-Bildausschnitte ohne Bildänderungen in `assets/fallobst/` ausgelagert werden können, **ohne v0.3e zu verändern**. Beachte, dass für den Februar-Workshop die Single-HTML-Offline-Fassung erhalten bleiben soll. Danach können wir den inhaltlichen Umfang von v0.4 festlegen.

---

**Dokumentationsstand 01.11.2026:** Repository-Struktur, Dateigrößen und v0.3e-Freigabedokument geprüft. Eine Auslagerung der Bilder wurde **noch nicht durchgeführt**; vor der eigentlichen Änderung sind Bildquellen und Dateiformate im aktuellen HTML-Quelltext zu inspizieren.
