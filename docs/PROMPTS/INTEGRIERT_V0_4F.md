# Entwicklungs-Prompt v0.4f – Säurekatalysator

**Datum:** 01.11.2026 · **Basis:** vom Nutzer browsergeprüfte `prototyp/integriert-v0.4e/index.html`.

## Auftrag

Erstelle **in einem neuen Versionsverzeichnis** `prototyp/integriert-v0.4f/index.html` einen offlinefähigen Prototyp mit der vorhandenen v0.4e-Darstellung. **Frühere Versionen und Root-`index.html` nicht verändern.**

1. Ergänze im Chemie-Reiter einen klar beschrifteten Schalter `Säurekatalysator: AUS/EIN`; im Modell steht H₂SO₄ als qualitatives Beispiel.
2. Der Faktor `3` multipliziert **beide** effektiven Reaktionskonstanten `kHin` und `kRueck`. Beim Umschalten ändert sich sofort die Ratenanzeige, nicht aber c(A), c(B), c(C), c(D). Das Gleichgewicht `K=kHin/kRueck` muss unverändert bleiben.
3. Verlangsame unabhängig vom Apfelmodell die **Basisreaktion** durch einen Modelluhrfaktor `0,6`, damit die eingeschaltete Katalyse (1,8-fach gegenüber früherer chemischer Basis) für Unterrichtszwecke beobachtbar bleibt. Die bestehenden numerisch gekoppelten Apfel-/Chemie-Regler dürfen nicht durch einen Katalysator-Klick verändert werden.
4. Reduziere die aus dem Reaktionsraum abgeführte D-Menge von `25 %` auf `10 %` **einmal pro angezeigtem Rechenschritt**, nach der reversiblen Reaktion. Die ×10-Taste ändert nur die Ablaufgeschwindigkeit der UI, nicht die Modellgleichungen.
5. Ergänze violette Ereignismarker mit `Kat EIN/AUS` im Konzentrationsverlauf. Der Eingriff erzeugt **keinen Konzentrationssprung**. Die vorhandenen orangefarbenen A-Zugabe- und türkisfarbenen Wasserentzug-Marker bleiben getrennt.
6. Vermeide numerische Artefakte bei Katalyse und k-Maximalwerten durch `12` interne Teilzeitschritte (Euler), bilanzerhaltend und ohne negative Konzentrationen.
7. Ergänze kurze fachliche Erklärung: qualitative Analogie zur Essigsäure-Ethanol-Veresterung zu Ethylacetat und Wasser, kein echter Mechanismus und keine realen Reaktionszeiten. Temperatur bleibt der getrennten Version v0.4g vorbehalten, diskutierter Bereich **20–80 °C in 10-°C-Schritten**.

## Tests und Abnahmekriterien

- Beide Raten wachsen bei Schalter EIN in *demselben Zustand* exakt auf das Dreifache, `K` ändert sich nicht.
- Geschlossene Zustände mit und ohne Katalysator nähern sich derselben, vom Verhältnis der Basis-k-Werte bestimmten Endlage.
- `A+C`, `B+D` bei geschlossener Reaktion erhalten; bei Wasserentzug `A+C`, `B+C`, `D+gesammelt=C`. Bei einer A-Zugabe entsprechende um `0,20` erhöhte erste Bilanz.
- Keine negativen Stoffkonzentrationen auch bei k=0,20 und K-Randwerten 0,1 / 10.
- Katalysator-Schaltung bei laufender Simulation sowie Reset, A-Zugabe, Wasserauskreisen, Schnelllauf und Anzeigewechsel.
- Alle **10 eingebetteten Bilder** und der ursprüngliche Apfel-/Stechheber-Rechenkern unverändert; vollständiges JS syntaktisch gültig.
- Rechenprüfung klar von der noch nötigen Browser-, Mobil- und Offline-Sichtprüfung unterscheiden.

**Dokumentation:** Prüfprotokoll, Entwicklungsstand und kompakte Übergabe im GitHub-Repo aktualisieren.
