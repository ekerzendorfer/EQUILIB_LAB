# EQUILIB_LAB – Implementierung und Prüfprotokoll v0.4a

**Stand:** 01.11.2026 · **Status:** neuer, technisch und mathematisch geprüfter Prototyp; **visuelle Browser- und Offline-Abnahme noch ausständig**.

## 1. Einstieg und Versionssicherung

- **Neue Einzel-HTML:** [prototyp/integriert-v0.4a/index.html](../prototyp/integriert-v0.4a/index.html) (GitHub-Blob-SHA `0755053f0f3e0b7c6f46cf2f97fc2190308da6ac`, ca. 2,60 MB).
- **Freigegebener Rückfall:** [v0.3e](../prototyp/integriert-v0.3e/index.html), unverändert.
- **Root `index.html`:** weiterhin v0.3e, noch **kein** Wechsel der Hauptversion.
- Alle fünf Fallobstphasen und **zehn direkt eingebettete Bildausschnitte** bleiben unverändert. **Keine** Datei-Auslagerung, **keine** externen JS-Bibliotheken, Server, APIs oder Accounts.
- Der bestehende Apfel-Rechenkern und die Bildphasenfunktion `chooseComparePhase` wurden **nicht verändert**.
- Verbindlicher Entwurf: [KONZEPT_V0_4_CHEMISCHES_GLEICHGEWICHT.md](KONZEPT_V0_4_CHEMISCHES_GLEICHGEWICHT.md).

## 2. Ergänzte Oberfläche

Vierte Registerkarte **„Chemisches Gleichgewicht“**, zusätzlich zu Geschichte, Modell und Vergleich:

- Separater Chemie-Modus `A + B ⇌ C + D`, mit **eigenen** Tasten Start/Pause, Einzelschritt, Reset und eigenem Zustand.
- Vier Konzentrationen (mol/L), je eine einfache symbolische Punktdarstellung (24 Punkte entsprechen 1 mol/L, Rundung nur in der Anzeige).
- Hin- und Rückrate mit derselben Balkenskala und absoluten Zahlenwerten; Reaktionsquotient `Q_c` und Nettoänderung pro Schritt.
- Gemeinsames SVG-Stufendiagramm für alle vier Stoffe. Bei symmetrischer Ausgangslage liegen A und B bzw. C und D genau übereinander (punktuelle Hervorhebung der Endpunkte).
- Beim Wechsel zwischen Apfel-/Stechheberansichten und Chemie-Modus wird ein jeweils laufender Timer **pausiert**. Die Zustände bleiben voneinander getrennt; die Apfelsteuerung wird im Chemie-Modus ausgeblendet.
- Noch **keine** Parameterwahl und **keine** Gleichgewichtsstörung. Beides erst in späteren, einzeln geprüften Schritten.

## 3. Chemie-Rechenkern (v0.4a)

Feste Modellparameter:

```text
cA(0) = cB(0) = 1 mol/L
cC(0) = cD(0) = 0 mol/L
kHin = kRueck = 0,08 L·mol⁻¹·Schritt⁻¹
Δt = 1 Schritt
Kc = kHin/kRueck = 1 (hier idealisiertes kinetisches Modell)
```

Aktuelle Hin-/Rückrate `vHin = kHin·cA·cB`, `vRueck = kRueck·cC·cD`; für den nächsten Schritt zunächst beide Raten aus **demselben alten Konzentrationszustand** berechnen und `Δξ = (vHin - vRueck)·Δt` bilden. Dann `cA,cB` um `Δξ` vermindern und `cC,cD` um denselben Betrag erhöhen. Große `Δξ`-Beträge werden durch die jeweils verfügbaren Edukt-/Produktkonzentrationen begrenzt. So werden negative Konzentrationen vermieden.

Bei der hier vorliegenden Symmetrie: `cA+cC=1`, `cB+cD=1`. Die Gleichgewichtswerte sind je `0,5 mol/L`; die Teilraten sind **je 0,02 mol·L⁻¹·Schritt⁻¹**, nicht Null.

**Fachliche Grenze:** vereinfachtes Reaktionsmodell, kein beanspruchter elementarer Mechanismus einer konkreten Esterbildung. Konzentrationsquotient als idealisierte Näherung. Die Punktsymbole sind **keine** molekulardynamische oder stochastische Simulation.

## 4. Tatsächlich durchgeführte Prüfungen

**Bestanden (Quellcode/JavaScript-Rechenprüfung):**

1. Die **vollständige JavaScript-Datei** aus der neuen HTML wird durch den JS-Parser akzeptiert.
2. Reale `chemInitialState`-/`chemRates`-/`chemAdvance`-Funktionen **aus dem im Repository abgelegten neuen Code** wurden separat ausgeführt.
3. Start `A=B=1, C=D=0`; Schritt 1 `A=B=0,92, C=D=0,08`.
4. 601 Schritte ohne negative Konzentrationen, mit Erhaltung `A+C=B+D=1` (Toleranz 10⁻¹²); Annäherung an jeweils `0,5`.
5. Stationäre Hin- und Rückraten bleiben beide positiv und betragen ungefähr `0,0200`.
6. `makeInitialState`/Apfel-Rechenkern und `chooseComparePhase` sind gegenüber v0.3e textlich **identisch**.
7. Alle zehn eingebetteten Bildquellen sind im neuen HTML **unverändert enthalten**.
8. Chemie-Ansicht, Bedienelemente und Diagramm sind im HTML vorhanden; keine externen Bild-, Script- oder Stylesheet-Referenzen.

**Noch nicht als bestanden behaupten:** echter Browser-/DOM-Interaktionstest, Bedienbarkeit bei konkreter Bildschirmbreite, Offline-Doppelklicktest am Nutzer-PC, Timing und Sichtprüfung sämtlicher Darstellungen. Eine JavaScript-Syntaxprüfung ersetzt **keinen** visuellen Browsertest.

## 5. Manuelle Abnahme – konkreter Rundgang

1. Neue `prototyp/integriert-v0.4a/index.html` herunterladen und lokal **ohne Internet** durch Doppelklick öffnen.
2. In der **Geschichte** erscheint Phase I; im bestehenden Apfelmodus Einzelschritt und Auto prüfen. Die abgestimmte Bildphasenfolge einschließlich 30:20 (noch II), 29:21 (etwa III), 18:32 (V) muss erhalten bleiben.
3. In **„Chemisches Gleichgewicht“** wechseln: Start A/B = 1,000, C/D = 0,000; nach Einzelschritt A/B = 0,920 und C/D = 0,080. Die Punktsymbole, der Quotient, die beiden Raten und das Diagramm müssen synchron folgen.
4. Start/Pause drücken: Die Werte nähern sich 0,500; die **beiden Raten laufen auf je 0,0200** zu. Kein fälschlicher Stillstand.
5. Reset: Chemie kehrt unabhängig von den Apfelparametern auf ihre Anfangswerte zurück. Beim Ansichtswechsel dürfen keine zwei Timer parallel weiterlaufen.
6. Zurück zur Apfelgeschichte, dort weiterrechnen: Weder Apfelmenge noch Phase dürfen durch Chemieschritte verändert worden sein.
7. Auf Notebook-/Projektoransicht und bei schmalem Fenster Kontrast, Beschriftungen, Diagramm und Bedienbarkeit prüfen.

Erst nach einer solchen gemeinsamen Abnahme ggf. Root-`index.html` auf v0.4a setzen. **v0.3e niemals überschreiben.**

## 6. Nächster kleiner Schritt

Nach Sichtprüfung von v0.4a: fachlich-didaktisches Feintuning, erst danach v0.4b (ausgebaute Teilchenillustration und expliziter Analogievergleich) und schließlich v0.4c (zunächst nur **Eduktzugabe** als Le-Chatelier-Störung). Keine Temperatur- oder Volumenstörung voreilig einbauen.
