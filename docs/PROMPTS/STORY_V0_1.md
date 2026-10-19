# GLEICHGEWICHTS-LAB – Reproduktions-Prompt Story V0.1

**19. Oktober 2026 · Stand:** Im Browser getesteter, offlinefähiger Prototyp. **Rechenkern V0.2 wird nicht verändert.**

## Kernprompt

Entwickle eine **responsive, offlinefähige Browser-Lernansicht „GLEICHGEWICHTS-LAB – Fallobstschlacht“** als Integrationsschritt zwischen der bereits akzeptierten fünfteiligen Bildergeschichte und dem später einzubindenden mathematischen Gleichgewichtsmodell.

1. **Reiter:** Geschichte, Modell, Vergleich. Geschichte ist anfangs aktiv. Modell zeigt einen **ehrlich beschrifteten Platzhalter** für den noch separat bestehenden V0.2-Rechenkern (A ⇄ B, Zylinder, Stufenlinien, Teiltransporte). Kein vorgetäuschter Livebetrieb. Vergleich zeigt die gerade gewählte Storyphase mit einer qualitativen und formalen Übertragung auf A ⇄ B, ausdrücklich als **schematische Deutung ohne Live-Werte** bezeichnet.
2. **Geschichte:** fünf Phasen: I Ausgangssituation, II Junge beginnt, III Gegenoffensive, IV ähnliche Bestände, aber ungleiche Raten, V dynamisches Gleichgewicht mit fortlaufenden Gegenströmen. Vor-/Zurück, anklickbare Phasenleiste, didaktischer Fokus, Leitfrage. Phasenwahl bleibt beim Reiterwechsel erhalten.
3. **Bildmodi:** Gesamtbild, Seitenansicht, Vogelperspektive. Einheitliche Bildhöhen und dieselbe Anordnung aller fünf Phasen. In Phase I die im ursprünglichen Bild eingebrannte Überschrift aus dem sichtbaren Bildausschnitt entfernen. Bei allen Bildern die ursprüngliche weiße Trennlinie zwischen beiden Perspektiven vollständig herausschneiden; bei Phase III liegt sie **tiefer** als bei den übrigen. Neue **einzige** Trennlinie in der UI statt doppelter Linie.
4. **Technik:** HTML, CSS, Vanilla JavaScript, kein Backend, kein Node.js, keine Onlinebibliothek, keine Anmeldung. Responsiv, zugängliche Button- und Reitersteuerung, Pfeiltasten. Eine wartbare Ordnerfassung mit lokal gespeicherten optimierten WebP-Bildausschnitten und zusätzlich eine **vollständig selbstständige HTML-Datei mit eingebetteten Bildern** erstellen.
5. **Fachlicher Schutz:** Die Bilder sind **narrative Illustrationen, keine numerisch exakten Apfelzählungen**. Gleiche Bestände implizieren nicht gleiche Transportraten. Das ursprüngliche deterministische V0.2-Modell darf nicht überschrieben oder ohne ausdrückliche Freigabe verändert werden.
6. **Prüfung:** alle fünf Phasen erreichbar; beide Perspektiven pro Phase; Reiterwechsel erhält Phase; in Phase III keine zweite weiße Linie; keine JavaScript-Fehler; keine Netzabhängigkeit oder erfundene Daten.

## Tatsächliche Umsetzung und Dateien

Erstellt am 19.10.2026 in der Chat-Arbeitsumgebung:
- **GLEICHGEWICHTS_LAB_Story_V0_1_OFFLINE.html**: eigenständige Datei (ca. 2,4 MB), Bilder direkt integriert.
- **GLEICHGEWICHTS_LAB_Story_V0_1_OFFLINE.zip**: obige HTML-Datei als Archiv.
- Wartbare Quellstruktur **GLEICHGEWICHTS_LAB_Story_V0_1/index.html** und zehn WebP-Bilder in einem Unterordner assets (je fünf Seiten- und Vogelansichten).

**Repository-Status:** Der erzeugte Binärcode/Bildsatz liegt zunächst als Chat-Artefakt vor; **noch nicht auf GitHub gespeichert**. Diese Datei dokumentiert die Entwicklung. Keine kaputten Repository-Links auf den noch ausstehenden Upload.

## Tests und offene Punkte

In Chromium wurde die eingebettete HTML-Datei mit realen Bilddaten geladen. Erfolgreiche Desktopchecks: Phasen-Navigation I–III, Seiten-/Vogelansicht, Reiter Geschichte–Modell–Vergleich–Geschichte, Tastatur-Navigation, korrekt geladene Bildmaße, keine JavaScript-Fehler. Die Testumgebung blockiert direkte file://-Navigation, weshalb die HTML-Datei mit page.set_content() offline gerendert wurde. Der letzte lokale Doppelklick-Test auf einem normalen Anwender-PC bleibt ausständig.

**Nächster Schritt:** Darstellung gemeinsam begutachten. Danach bei Zustimmung den Modellbereich mit dem tatsächlichen Rechenkern V0.2 verbinden. Die Bildergeschichte bleibt als eigenständige Lehrsequenz erhalten.

Dieser Prompt soll eine funktional entsprechende Variante ermöglichen; er belegt **keinen** tatsächlichen Ein-Prompt-Entwicklungserfolg.
