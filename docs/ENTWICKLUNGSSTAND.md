# EQUILIB_LAB – laufender Entwicklungsstand

**Stand:** 2026-11-01  
**Repository:** https://github.com/ekerzendorfer/EQUILIB_LAB  
**Status:** Funktionierende Gleichgewichtseinstellung vom Anwender bestätigt. Der technische Inhalt der aktuellen HTML-Datei wurde bei diesem Zugriff nicht vollständig übertragen; Änderungen am Rechenkern bzw. an der Oberfläche sind daher **nicht** als durchgeführt dokumentiert.

## 1. Didaktisches Ziel

Niederschwelliges, browserbasiertes Workshop-Labor zum dynamischen chemischen Gleichgewicht: Bildgeschichte „Apfelschlacht“ ↔ Stechheber-Modell ↔ diskrete Raten-/Bestandssimulation. Eine einzige HTML-Datei soll nach Möglichkeit weiterhin offline und ohne Installation funktionieren.

## 2. Bestätigter Entwicklungsstand

- Die fünf Phasen der Apfelschlacht-Geschichte sind mit dem Modell synchronisiert; die Übergänge zu Phase III und V wurden insbesondere für den Einzelschrittbetrieb nachjustiert (Stand der integrierten Bildgeschichte: v0.3e).
- Die Gleichgewichtseinstellung wurde danach überarbeitet. **Am 01.11.2026 bestätigt der Anwender, dass die Einstellung nun passt.** Frühere Fehlfunktion: Endwerte der vier Spezies gingen unabhängig von den eingestellten Hin-/Rückanteilen gegen je 0,5.
- Die Zielversion v0.4 erweitert die Modellansicht um eine didaktisch anschauliche, umschaltbare Darstellung.
- Keine weiteren Codeänderungen in dieser Dokumentationsaktualisierung.

## 3. Nächste Umsetzungsschritte (v0.4)

1. **Umschaltbare Bestandsansicht:** bisherige Bestandsdarstellung beibehalten; alternative gemeinsame Reaktionsraum-Ansicht ergänzen, ohne Darstellung und Rechenkern zu vermischen.
2. **Teilchenanimation:** vier Spezies im gemeinsamen Raum, optisch unterscheidbar; Bewegung und ggf. Kollisionen. Zunächst leichte Animation, bei der **der bestehende Rechenkern allein** Reaktionsereignisse/Bestände bestimmt. Eine Kollision darf keine zusätzliche, fachlich unbeabsichtigte Reaktion auslösen. Optional später echte kollisionsbasierte Ereignisvisualisierung.
3. **Fiktive Gleichgewichtskonstante K:** aus den Modellparametern bzw. dem durch diese definierten stationären Zustand berechnen und anzeigen; Definition, Stöchiometrie und Normierung explizit im UI angeben. Als didaktisches Ziel ungefähr 0,1–10; **keine künstliche Begrenzung, die den berechneten Wert verfälscht**. Falls die Parameter außerhalb dieses Bereichs führen, kennzeichnen bzw. den wählbaren Parameterraum passend gestalten.
4. **Tests:** asymmetrische Hin-/Rückanteile, Erhaltung der Gesamtmenge (sofern im Modell vorgesehen), Schritt-/Automatikmodus, Neustart, Story-Synchronisierung, verschiedene Fenstergrößen, Performance und Offline-Betrieb.
5. **Dokumentation:** Ergebnisse und Dateipfade hier nach jedem Umsetzungsschritt aktualisieren.

## 4. Fachliche Klärung vor der K-Berechnung

Die Reaktionsgleichung der vier Spezies, die genaue Definition der beiden Transportparameter und die Bestands-Normierung müssen **aus dem aktuellen Quellcode** abgelesen werden. Erst daraus lässt sich entscheiden, ob z. B. für A + B ⇌ C + D eine Größe K = ([C][D])/([A][B]) sinnvoll ist, oder ob ein anderes Reaktionsschema bzw. ein anderer Modellparameter gilt. Keine Formel ungeprüft an die Oberfläche schreiben.

## 5. Dateien und Versionskontrolle

- Repository: `ekerzendorfer/EQUILIB_LAB`
- Bekannte Pfade: `index.html`, `prototyp/integriert-v0.2/index.html`
- Entwicklungsdokumentation: `docs/ENTWICKLUNGSSTAND.md`
- Aktueller HTML-Code **nicht verändert**. Bei der Dokumentationsarbeit lieferte der Connector für die beiden bekannten HTML-Pfade jeweils leere Inhalte zurück; Ursache noch ungeklärt. Nicht daraus folgern, die veröffentlichte App sei tatsächlich leer.

## 6. Übergabe an den nächsten Chat

Wir entwickeln das GitHub-Projekt EQUILIB_LAB weiter. Lies zuerst `docs/ENTWICKLUNGSSTAND.md` im Repository. Die Gleichgewichtseinstellung funktioniert laut Anwender seit 01.11.2026. Nächste Aufgabe: umschaltbare Bestands- und gemeinsame Reaktionsraum-Ansicht (vier Spezies, animierte Teilchen/Kollisionen) sowie eine aus dem tatsächlichen Reaktionsmodell korrekt abgeleitete, fiktive Gleichgewichtskonstante K, möglichst im Bereich 0,1 bis 10. Bewahre funktionierende Story-Synchronisierung in Einzel- und Automatikschritten. Bevor du Quellcode schreibst, beschaffe und prüfe die **vollständige aktuelle HTML-Datei**, denn beim letzten GitHub-Abruf kam leerer Inhalt zurück. Arbeite in kleinen, fachlich testbaren Schritten. Aktualisiere die Dokumentation nach jedem Schritt, und liefere immer eine kompakte Übergabe mit tatsächlich geänderten Dateien, offenen Punkten und nächster Aufgabe.
