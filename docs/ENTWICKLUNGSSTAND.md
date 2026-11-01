# EQUILIB_LAB – laufender Entwicklungsstand und Übergabe

**Stand:** 01.11.2026 · **Projekt:** CHEMIE mit KI – GLEICHGEWICHTS-LAB  
**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB

## Versionen und Freigabezustand

| Version | Pfad | Stand |
|---|---|---|
| v0.3e | `index.html` und `prototyp/integriert-v0.3e/index.html` | Bisher akzeptierte Apfel-/Stechheber-Fassung; Root-Startversion |
| v0.4a | `prototyp/integriert-v0.4a/index.html` | Erste unabhängige Chemie-Ansicht, feste Raten |
| v0.4b | `prototyp/integriert-v0.4b/index.html` | Einstellbare k-Werte, K/Q-Anzeige, umschaltbarer gemeinsamer Reaktionsraum; funktionierende Gleichgewichtseinstellung durch Anwender am 01.11. bestätigt |
| **v0.4c** | `prototyp/integriert-v0.4c/index.html` | **Neue Testversion:** einmalige Eduktzugabe A +0,20 mol/L, K unverändert, Q-Vergleich, Gleichgewichts-Neuberechnung; Browser-/Offline-Sichtabnahme ausständig |

**Direkt öffnen:** https://ekerzendorfer.github.io/EQUILIB_LAB/prototyp/integriert-v0.4c/

## Ziel und feste Leitplanken

Niederschwelliges, lokal ausführbares Lernwerkzeug für den Februar-2027-Workshop: Geschichte (Fallobstschlacht) ↔ Stechheberanalogie ↔ chemisches Reaktionsmodell. Die archivierten Fassungen und die bewährte Phasensynchronisation bleiben unangetastet. Eine einzige autonome HTML-Datei enthält alle zehn Bildausschnitte eingebettet; keine externen Bibliotheken.

## Bestehende Modelle

**Apfel/Stechheber:** `H=pHin*A`, `R=pRueck*B`, `A'=A-H+R`, `B'=B+H-R`, `A+B=M`. Story/Modell/Vergleich einschließlich Bildphasen für Einzel- und Automatikschritte beibehalten.

**Chemie:** Formale Modellreaktion `A + B ⇌ C + D`, jeweils diskret aus dem alten Zustand:

```text
vHin = kHin*cA*cB
vRueck = kRueck*cC*cD
delta = (vHin-vRueck)*dt
cA',cB' = cA-delta,cB-delta
cC',cD' = cC+delta,cD+delta
Kc = kHin/kRueck, Qc = cC*cD/(cA*cB) (falls Nenner > 0)
```

Chemische Regler kHin und kRueck von 0,02 bis 0,20; daher Kc zwischen 0,1 und 10. Kc=1 führt beim Startzustand 1/1/0/0 zu 0,5/0,5/0,5/0,5. Bei abweichenden k-Werten **keine** allgemeine Gleichverteilung. Vier farblich unterschiedene Konzentrationen, Stufendiagramm, Ratenbalken und optionale symbolische, bewegte Teilchen im gemeinsamen Reaktionsraum. Teilchenkollisionen lösen keine selbständigen Rechenschritte aus.

## Neu in v0.4c

- Schaltfläche `A zugeben (+0,20 mol/L)` erlaubt eine einzige Zugabe pro Versuch, auch bei laufender Simulation.
- Die Änderung von c(A) tritt sofort ein; B/C/D werden erst in späteren Reaktionsschritten verändert.
- Q vor und nach Zugabe mit Hinweis auf Q im Verhältnis zu K; **K bleibt bei Stoffzugabe unverändert**.
- Erwartete Gleichgewichtswerte der **vier** Stoffe werden durch Bisektion der Nettorate entlang der gültigen stöchiometrischen Reaktionsgeraden neu bestimmt.
- Stufendiagramm zeigt vertikalen Konzentrationssprung und markiert Zeitpunkt; y-Skala kann über 1,000 mol/L wachsen.
- Getrennte Symbolpunktanzeige ergänzt bei >1 mol/L dynamisch zusätzliche Punkte; gemeinsamer Reaktionsraum passt Symbolzahlen an.
- Bilanzanzeige nach A-Zugabe: `A+C=1,2`, `B+D=1,0` beim ursprünglichen Start 1/1/0/0. Der äußere Eingriff verändert die erste Summe, danach bleiben beide invariant.
- Reset löscht Zugabe und Marker. Slideränderung bei Pause beginnt wie zuvor einen neuen Versuch.
- Der bestehende Apfel-/Stechheber-JavaScript-Block wurde **nicht verändert**; alle zehn eingebetteten Bildquellen blieben bestehen.

**Rechenbeispiel K=1:** Vor Zugabe annähernd A/B/C/D = 0,500. Sofort danach A=0,700, B/C/D=0,500; `Q=0,7142857 < K=1`. Neue stationäre Konzentrationen: A=0,654545, B=0,454545, C=D=0,545455.

## Prüfstatus

JavaScript-Syntaxprüfung, Rechenkern-Tests (erste Runde, 800 Schritte vor Störung und 900 nach Störung), Bilanz-, Nichtnegativitäts-, K=0,1/K=10- und Zielwertprüfungen erfolgreich; alter Apfel-JS-Block textgleich, zehn Bildquellen vorhanden. **Keine** Behauptung einer interaktiven Browser-/Layout- oder Offline-Abnahme.

**Detailliert:** [Prüfprotokoll v0.4c](PRUEFPROTOKOLL_V0_4C_2026-11-01.md).  
**Historie:** [Übergabe v0.4b](Uebergabe_v0.4b.md), [v0.3e-Zwischenstand](ENTWICKLUNGSSTAND_V0_3E_2026-10-31.md).

## Unmittelbarer nächster Schritt

v0.4c im Browser (auch offline) gezielt prüfen: Eingriff bei K=1 nahe Gleichgewicht; alle vier Werte, Bilanz, Q-Abfall, Raten, vertikaler Sprung, beide Teilchendarstellungen; direkt bei Schritt 0 testen (A=1,200, y-Achse >1); Parameterwechsel, Reset, Auto-Modus und Apfelphasen prüfen. Nur entdeckte Fehler in neuer Folgerevision korrigieren. Root erst nach Nutzerfreigabe anfassen. Erst dann über Produktentzug als mögliche weitere Störung entscheiden.

## Technischer GitHub-Hinweis

Die HTML-Dateien sind etwa 2,6 MB groß. Bei `fetch_file` kann deshalb `content` leer sein, **ohne** dass die Datei leer ist. Stattdessen deren Blob-SHA aus dem Contents-Endpunkt holen und `fetch_blob(blob_sha)` nutzen. Beim letzten erfolgreichen Zugriff hatte v0.4b SHA `e5a36f68e6b21ab4260dcfaa20bea656e5041a38`; v0.4c SHA `79c747d8d1e50b589c05c2c960cedc784a560011`. Niemals ein leeres `fetch_file.content` als HTML-Quelle verwenden.

## Übergabeprompt für den nächsten Chat

Wir arbeiten am Repo `ekerzendorfer/EQUILIB_LAB`. Lies zuerst `docs/ENTWICKLUNGSSTAND.md` und `docs/PRUEFPROTOKOLL_V0_4C_2026-11-01.md`. Aktuelle **Testversion v0.4c**: `prototyp/integriert-v0.4c/index.html`, separate Chemieansicht A+B⇌C+D, kHin/kRueck einstellbar, K/Q, vier Bestände, gemeinsamer animierter Reaktionsraum und einmalige Edukt-A-Zugabe (+0,20 mol/L) mit Q-/Zielwertberechnung und vertikalem Konzentrationssprung. Syntax und Rechenfälle bestanden, **visuelle und Offline-Abnahme fehlt**. `main/index.html` ist unverändert v0.3e. Die großen HTML-Blobs über `fetch_blob` abrufen, nicht den leeren `fetch_file.content` verwenden. Zuerst Feedback zur v0.4c einholen und nur gezielte Korrekturen vornehmen. Versionen archivieren, Workshop-taugliche Single-HTML behalten und nach jedem Schritt die Entwicklungsdokumentation plus Übergabe aktualisieren.
