# EQUILIB_LAB – Übergabe v0.4b (01.11.2026)

## Dateien im Repository

- Aktuelle **Testfassung**: `prototyp/integriert-v0.4b/index.html`. Vollständig offlinefähige Single-HTML-Datei (ca. 2,6 MB durch eingebettete Bildgeschichte).
- Vorgänger: `prototyp/integriert-v0.4a/index.html` (unverändert).
- Bisheriger integrierter Stand v0.3e auf `main` (nicht ersetzt).
- Diese Übergabe: `docs/Uebergabe_v0.4b.md`.

## Modell und Ursache des 0,5-Problems

Reaktion **A + B ⇌ C + D**. Anfang c(A)=c(B)=1,000 mol/L, c(C)=c(D)=0. Konstantes Volumen, Zeitschritt dt=1. Kinetik:
```text
v_hin   = k_hin   * c(A) * c(B)
v_rueck = k_rueck * c(C) * c(D)
delta   = (v_hin - v_rueck) * dt
(A, B, C, D) -> (A-delta, B-delta, C+delta, D+delta)
```
Schrittänderung wird zum Schutz gegen negative Konzentrationen durch verfügbare Stoffmengen begrenzt. A+C und B+D sind konstant 1,000 mol/L. k-Hin/-Rück besitzen im Modell Einheiten L·mol⁻¹·Schritt⁻¹.

**Ursache:** v0.4a verwendete fest eingetragene `kHin = kRueck = 0.08`. Die Transportanteile im Apfelmodell sind unabhängig und haben v0.4a niemals gesteuert. Kinetisches GG bei identischen Raten und symmetrischem Start: A=B=C=D=0,500 mol/L.

## Änderungen in v0.4b

1. Zwei eigene Regler **k_hin** und **k_rueck** im Chemie-Tab. Je 0,02–0,20 in 0,01-Schritten. Während Start gesperrt; Parametereingabe bei Pause setzt den Chemie-Versuch auf Schritt 0 zurück.
2. **Kc = k_hin/k_rueck** wird unmittelbar berechnet, im Bereich von **0,1 bis 10**. Gleichzeitig wird die zu erwartende Gleichgewichtslage angezeigt. Der Reaktionsquotient **Qc = [C][D]/([A][B])** wird unabhängig laufend berechnet (Nenner 0 ⇒ „nicht definiert“). Im Gleichgewicht Qc ≈ Kc.
3. Ratenbalken haben jetzt einen gemeinsamen dynamischen Maximalmaßstab `max(kHin,kRueck)`.
4. Umschaltung **„Vier getrennte Bestände“** (bisherige Symbolpunkte) / **„Gemeinsamer Reaktionsraum“** (Canvas). Raum: 48 Symbolteilchen zu Beginn, alle vier Farben, Bewegung, Reflexion an Grenzen, einfache elastische Stöße und markierte A+B- bzw. C+D-Begegnungen. Gezeigte Teilchenanzahlen beruhen auf 24 gerundeten Symbolen je mol/L, nicht auf Einzelmolekülen.
5. **Wichtig:** Kollisionsereignisse steuern ausdrücklich *nicht* die Reaktionskinetik. Konzentrationsänderungen berechnet ausschließlich das bestehende diskrete Massenwirkungsmodell; Umfärbungen synchronisieren nur die gerundete Bestandsdarstellung. Das ist wissenschaftsdidaktisch eine Veranschaulichung von Begegnungen, keine Teilchen- oder Monte-Carlo-Reaktionssimulation.
6. Apfelgeschichte, Stechheber, Phasensynchronisation, Vergleichsansicht und deren Regler bleiben unangetastet.

## Analytische Erwartungswerte

Für symmetrischen Start gilt im GG `A = B = 1-x`, `C = D = x`, also `Kc = x²/(1-x)²` und `x = sqrt(Kc)/(1+sqrt(Kc))`.

| k_hin | k_rueck | Kc | GG A=B | GG C=D |
|---:|---:|---:|---:|---:|
| 0,08 | 0,08 | 1,00 | 0,500 | 0,500 |
| 0,02 | 0,20 | 0,10 | 0,760 | 0,240 |
| 0,20 | 0,02 | 10,00 | 0,240 | 0,760 |
| 0,08 | 0,04 | 2,00 | 0,414 | 0,586 |

Im Gleichgewicht bleiben v_hin und v_rueck größer als null; die Nettorate nähert sich null.

## Testfolge / Abnahme

1. Chemie-Tab öffnen. Start/Reset: vier Konzentrationen 1/1/0/0; Kc=1,00. Nach genügend Schritten A=B=C=D ungefähr 0,500.
2. Pause, k_hin auf 0,20 und k_rueck auf 0,02: Kc=10,00, vorhergesagte Werte A/B 0,240 und C/D 0,760. Reaktionsverlauf prüfen; Qc nähert sich Kc.
3. Pause, k_hin auf 0,02 und k_rueck auf 0,20: Kc=0,10, Produkte bei 0,240. Werte, Graph und Raten vergleichen.
4. Während Start müssen Slider deaktiviert sein. Bei Slideränderung in Pause: Schritt 0, Anfangsmengen, neue Kurve.
5. Beide Stoffansichten mehrfach wechseln: **kein Sprung im Rechenkern**. Gemeinsamer Reaktionsraum zeigt vier bewegliche Teilchensorten und farblich markierte Kollisionen. Darstellung ist ausschließlich symbolisch.
6. Zurück zur Apfel-/Modell-/Vergleichsansicht: Transportregler und Bildphasen unverändert prüfen. Datei lokal öffnen, ohne Internetverbindung.

## Für den nächsten Chat

**GitHub-Repo:** `ekerzendorfer/EQUILIB_LAB`. **Ausgangspunkt:** `prototyp/integriert-v0.4b/index.html`. **Dokumentation:** `docs/Uebergabe_v0.4b.md`. Die Version ist implementiert, wartet aber auf visuellen Browser-Test und fachliche Freigabe durch den Nutzer. Nach dessen Feedback nur nachvollziehbare, kleine Korrekturen durchführen. Eine neue Version als getrennte HTML-Datei ablegen; v0.3e und v0.4a unverändert lassen. Ziel: niederschwellige, selbstständige, offlinefähige Single-HTML-App für den Februar-Workshop.

**GitHub-Connector-Hinweis:** Bei Dateien um 2,6 MB kann `fetch_file.content` leer sein (Contents-API-Größenbeschränkung), obwohl die Datei existiert. In dem Fall die SHA von `fetch_file` übernehmen und mit `fetch_blob(blob_sha)` den vollständigen Inhalt lesen. Niemals ein leeres `content` als Original verwenden oder damit überschreiben.
