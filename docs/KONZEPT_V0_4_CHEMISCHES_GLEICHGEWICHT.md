# EQUILIB_LAB – Fach- und Entwicklungsentwurf v0.4

**Stand:** 1. November 2026  
**Status:** Arbeitsentwurf, **noch nicht implementiert**. Grundlage: freigegebene v0.3e und bisherige didaktische Zielsetzung.  
**Ziel:** Den Transfer von der Apfel-/Stechheber-Analogie zu einer **echten chemischen Reaktion** sichtbar und überprüfbar machen, ohne den gesicherten deterministischen Rechenkern und die Bildphasensteuerung v0.3e zu beschädigen.

## 1. Festgelegte Leitplanken

- **Eine HTML-Datei** bleibt das Verteilformat: offline per Doppelklick, keine externen Bibliotheken, Server oder Accounts.
- **v0.3e bleibt unverändert** im Archiv unter `prototyp/integriert-v0.3e/index.html`; Änderungen in einem neuen Versionsstand vornehmen.
- Die bestehenden drei Darstellungen **Geschichte – Modell – Vergleich** behalten ihre Funktion. Apfelbilder und ihre fachlich abgestimmten Phasengrenzen (v0.3e) nicht verändern.
- Die drei inhaltlichen Ebenen **Apfelgeschichte – realer Stechheber – abstrakte Simulation** müssen für Lehrkräfte vergleichbar bleiben. Die gegenwärtige App zeigt bereits Modellzylinder und gegenläufige Transporte, bildet jedoch noch keine validierte reale Stechheber-Hydrodynamik ab.
- **Gleichgewicht bedeutet gleiche Hin- und Rückrate**, nicht zwingend gleiche Stoffmengen bzw. Konzentrationen. Das chemische Modell muss diesen Aspekt sichtbar machen.
- Kleine Entwicklungs- und Abnahmeschritte. Keine gleichzeitige Neugestaltung der ganzen App.

## 2. Vorschlag für die erste chemische Erweiterung (v0.4a)

**Getrennter Chemie-Modus** in derselben HTML-Datei, vorzugsweise zunächst als eigene Ansicht „Chemisches Gleichgewicht“. Die vorhandene Apfel-/Stechheber-Analogie wird dabei **nicht** umgedeutet oder mathematisch auf vier Stoffe verbogen.

Als fachlich transparenter Ausgangsfall dient die reversible Modellreaktion:

```text
A + B ⇌ C + D
```

Dies kann später mit einer **Esterbildung** illustriert werden (z. B. Carbonsäure + Alkohol ⇌ Ester + Wasser). Ein Zahlenbeispiel mit **K = 1** ist zunächst ausdrücklich **ein didaktisch gewähltes abstraktes Modell**, kein ungeprüfter Literaturwert einer konkreten Esterbildung.

### Diskretes kinetisches Modell bei konstantem Volumen

Für einen einfachen, formal massenwirkungsgesetzbasierten Modellansatz:

```text
v_hin,n  = k_hin  · c_A,n · c_B,n
v_rueck,n = k_rueck · c_C,n · c_D,n
Δξ_n = (v_hin,n − v_rueck,n) · Δt

c_A,n+1 = c_A,n − Δξ_n
c_B,n+1 = c_B,n − Δξ_n
c_C,n+1 = c_C,n + Δξ_n
c_D,n+1 = c_D,n + Δξ_n
```

Vorzeichen und Schrittweite müssen so abgesichert werden, dass Konzentrationen nicht negativ werden. **Beide Teilraten stets aus demselben alten Zustand berechnen.**

Bei dieser speziell gewählten Reaktion und idealisierter Modellierung gilt:

```text
Q_c = (c_C · c_D)/(c_A · c_B)
K_c = k_hin/k_rueck   (im kinetischen Gleichgewicht; gleiche Ordnung der Gegenreaktionen)
```

Bei verschwindendem Edukt-Nenner `Q` ausdrücklich als **nicht definiert / Grenzfall** behandeln, nicht als `NaN` anzeigen. Bei realer chemischer Gleichgewichtsthermodynamik sind Aktivitäten und Standardzustände zu berücksichtigen; die Konzentrationsform ist eine didaktische Näherung.

**Vorgeschlagener überprüfbarer Testfall:**

- `c_A,0 = c_B,0 = 1,000 mol/L`, `c_C,0 = c_D,0 = 0`
- `k_hin = k_rueck = 0,08 L·mol⁻¹·Schritt⁻¹`; `Δt = 1 Schritt`.
- Nach Schritt 1: `A = B = 0,920`, `C = D = 0,080 mol/L`.
- Für große Schrittzahlen: `A*=B*=C*=D*=0,500 mol/L`, `K=1`; trotzdem sind beide positiven Teilraten gleich groß.
- Erhalten bleiben bei fehlender äußerer Störung die Summen `c_A+c_C = 1,000` und `c_B+c_D = 1,000 mol/L`. **Nicht** einfach eine „Gesamtmenge der Äpfel“ als stoffspezifische Erhaltung ausgeben.

### Darstellung der ersten Iteration

- Vier unterscheidbare, beschriftete Stoffbestände mit Konzentrationen und Stufendiagramm.
- Zwei gegenläufige **Ratenanzeigen**, die auch bei stationären Konzentrationen sichtbar bleiben.
- Ein einfaches **Teilchensymbolbild** für A, B, C, D; Symbolanzahl ist eine ausdrücklich gerundete Veranschaulichung, **keine stochastische Simulation**.
- Eingaben zunächst auf den Testfall begrenzen. Erst wenn Werte, Erhaltung und Reset nachweislich funktionieren, Parameterwahl erweitern.

**Nicht Teil von v0.4a:** Störknöpfe, Temperaturänderung, realistischer Reaktionsmechanismus, stochastische molekulare Kollisionen, Neugestaltung der bestehenden Geschichte.

## 3. Nächste kleine Schritte nach v0.4a (noch nicht freigegeben)

### v0.4b – Teilchenbild und didaktischer Transfer

- Gegensätzliche Teilprozesse werden gleichzeitig sichtbar, auch nahe der stationären Verteilung.
- Bestände, Raten und Kurven werden **synchron aus demselben Zustand** aktualisiert.
- Fachhinweis: Bildliche Molekülsymbole zeigen Modellbestände; eine direkte Beobachtung realer Molekülreaktionen ist das nicht.
- Vergleich der Analogie A ⇄ B mit A+B ⇄ C+D: **Was wird anschaulich, wo endet die Analogie?**

### v0.4c – Erste Gleichgewichtsstörung nach Le Chatelier

- Zunächst **nur Eduktzugabe** bei laufender Rechnung; Konzentration springt, danach relaxiert das System.
- Das **Reaktionsquotient-Argument** wird unmittelbar dargestellt: Bei Zusatz von A ist `Q<K` (unter geeigneten Ausgangsbedingungen), weshalb die Nettoreaktion zunächst nach rechts läuft.
- Prüfen: Der gestörte Bestand steigt unmittelbar; die übrigen Bestände werden **nicht** künstlich sofort verschoben. Danach bestimmt der gemeinsame Rechenkern die weitere Entwicklung.
- Eine zweite Option **Produktentzug** kann nach erfolgreicher Prüfung ergänzt werden.

### Später, nicht vorschnell in v0.4 hineinziehen

- Temperaturänderung (thermodynamisch mit `K(T)` und Reaktionsenthalpie modellieren; nicht nur eine Geschwindigkeitskonstante ändern).
- Volumen-/Druckänderung nur bei **geeigneten Gasreaktionen** sinnvoll demonstrieren; bei dieser 1+1⇌1+1-Reaktion folgt aus einer idealisierten gleichmäßigen Gas-Kompression wegen `Δν=0` keine Verschiebung des Gleichgewichts.
- Physikalisch begründetes Stechhebermodell separat erarbeiten; die vorhandene Zylinderdarstellung ist nicht automatisch realistische Hydrodynamik.

## 4. Abnahmetests (Pflicht vor Freigabe)

1. Originaler Apfelkrieg-Preset und alle drei bestehenden Ansichten funktionieren unverändert.
2. Bildphasen nach `B/M` bleiben bei Auto- und Einzelschritt synchron: `37:13` und `30:20` Phase II, `29:21` ungefähr Phase III, `18:32` Phase V (illustrierte Annäherung, keine Gleichheitsbehauptung).
3. Chemie-Schritt 1 liefert `0,92/0,92/0,08/0,08` (unter oben genannten Normparametern).
4. Nichtnegative Konzentrationen; ohne äußere Störung korrekte stoffbezogene Erhaltung; Schritt und Auto erzeugen dieselbe Folge.
5. Nicht exakt gleiche Bestände bei anderen `k_hin/k_rueck`-Verhältnissen als Test nach Erweiterung der Parameter.
6. Bei Gleichgewicht **nicht** beide Raten auf Null setzen.
7. Reset, Wechsel zwischen Darstellungen und lokales Offline-Öffnen per **einer einzigen HTML-Datei** funktionieren.
8. Grafiken müssen auf üblichen Projektor-/Notebookbreiten verständlich sein; später Mobiltest.

## 5. Konkrete nächste Entwicklungsaktion

**Zunächst nur v0.4a umsetzen und prüfen.** Dazu den bestehenden Quelltext der v0.3e vollständig inspizieren und den neuen Chemie-Bereich **additiv** ergänzen, ohne die freigegebenen Apfelbilder, Story-Logik und v0.3e-Mathematik zu ändern. Unter `prototyp/integriert-v0.4a/index.html` einen neuen Sicherungsstand anlegen; die Root-Datei erst nach Prüfung entsprechend aktualisieren.

**Hinweis zur Interpretation:** Dieser Text ist der Startvorschlag für die Umsetzung, keine Behauptung, dass v0.4a bereits funktioniert oder vom Nutzer als Detail-Spezifikation abgenommen wurde.
