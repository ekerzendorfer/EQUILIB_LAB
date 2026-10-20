# Entwicklungs-Prompt: GLEICHGEWICHTS-LAB integriert V0.1

**Stand:** 20. Oktober 2026  
**Tatsächlich geprüfte Implementierung:** [\`prototyp/integriert-v0.1/index.html\`](../../prototyp/integriert-v0.1/index.html)  
**Ausgangspunkte:** [mathematischer Prototyp V0.2](../../prototyp/v0.2/index.html) und Story-Ansicht V0.1 (fünf akzeptierte, KI-generierte Phasenbilder).  
**Charakter:** Ein **rekonstruierter, reproduzierbarer Entwicklungsauftrag** mit dokumentierten Prüfschritten, kein Anspruch auf einen tatsächlichen Ein-Prompt-Erfolg oder bitidentischen Quellcode.

## Ausgangs-Prompt zur Reproduktion

> Du entwickelst eine browserbasierte, fachlich geprüfte Chemie-Lernumgebung für SEK I/II. Ich stelle dir zwei bereits getestete Vorlagen bereit:
>
> (A) GLEICHGEWICHTS-LAB V0.2: HTML/CSS/JavaScript mit dem diskreten Zwei-Mengen-Modell A⇄B, zwei Zylindern, gegenläufigen Transportkugeln/-balken, Stufendiagramm und vier Parametern;
>
> (B) Story V0.1: fünf visuell freigegebene Phasenbilder der Fallobstschlacht (je Seitenansicht und Vogelperspektive) mit didaktischen Beobachtungen und Leitfragen.
>
> **Ziel:** Verbinde beide in einer **einzigen statischen, offlinefähigen Anwendung** mit den Reitern **Geschichte – Modell – Vergleich**, ohne einen zweiten unabhängigen Rechenkern zu erzeugen. Rechenschritt, Parameter und Ergebnisse müssen bei jedem Ansichtswechsel erhalten bleiben.
>
> **Mathematischer Kern unverändert:** Für den aktuellen Zustand (A, B) und die Transferanteile p_hin und p_rück werden gleichzeitig \`H = p_hin·A\` und \`R = p_rück·B\` berechnet; danach \`A_neu = A - H + R\` und \`B_neu = Gesamtmenge - A_neu\`. A+B bleibt konstant. Verwende die Originalfunktionen \`makeInitialState\`, \`calculateTransfers\`, \`advanceOneStep\` aus V0.2. Die anzuzeigenden Hin-/Rückmengen sind ausdrücklich die **für den nächsten Schritt** berechneten Beträge.
>
> **Eine gemeinsame Steuerung:** Start/Pause, Einzelschritt und Reset sind unabhängig vom aktiven Reiter sichtbar. Die beiden Diagrammoptionen aus V0.2 („Letzte 40 Schritte“ / „Volle Laufzeit“) bleiben erhalten. Parameter bleiben änderbar, führen aber wie in V0.2 zu einem Reset. Während des Laufs sind Parameter gesperrt.
>
> **Story-Preset:** Ergänze eine gesonderte Schaltfläche **„Apfelkrieg-Vorgabe“** mit Gesamtmenge 50 ME, A₀=50, B₀=0, p_hin=0,08 (Junge links), p_rück=0,04 (Nachbar rechts). Das ursprüngliche V0.2-Parameterpreset 50/0/0,06/0,04 bleibt über **„V0.2-Werte“** zugänglich. Das Story-Preset wird beim ersten Laden aktiviert.
>
> **Reiter „Geschichte“:** Die fünf Phasen sind mit Vor-/Zurück-Navigation und einem Phasenwähler zugänglich. Pro Phase werden Bild, beobachtbare Situation, didaktischer Fokus und Leitfrage angezeigt. Gesamt-/Seiten-/Vogelperspektive müssen wählbar bleiben. Zusätzlich **Live-Modellwerte** für Schritt n, A, B sowie H und R anzeigen. Beschrifte, dass diese Werte aus dem Rechenkern stammen und **unabhängig** von der gerade gewählten narrativen Bildphase sind.
>
> **Reiter „Modell“:** Die beiden Zylinder und das originale Stufendiagramm aus V0.2 samt Kennzahlen, Balken und Kugeln unverändert weiterverwenden.
>
> **Reiter „Vergleich“:** Das zur ausgewählten Phase passende Bild mit einer quantitativen Zusammenfassung des aktuell **gleichen** Rechenzustands zeigen: A und B, H und R mit gemeinsamer Balkenskala, mathematische Deutung der Phase und aktuellen Schritt. Keine selbst erfundenen Bild-Messwerte.
>
> **Zentrale didaktische Grenze:** Die akzeptierten KI-generierten Äpfel sind **statische narrative Illustrationen**; ihre am Boden gezeichnete Anzahl und die gezeichneten Flugobjekte hängen in dieser Version **noch nicht** zahlengetreu vom Modell ab. Auch die fünf narrativen Bildphasen dürfen **nicht automatisch** als immer zutreffende Klassifikation einer beliebigen frei gewählten Simulation behauptet werden. Das Ändern der Bildphase ist eine **Bildernavigation** und verändert weder Rechenschritt noch aktuelle Parameter. Dies in der Oberfläche gut sichtbar erläutern.
>
> **Technik:** Nur HTML, CSS, Vanilla JavaScript und die vorhandenen lokalen Bilder. Kein Server, kein Backend, kein API-Schlüssel, keine Laufzeit-CDNs, keine Anmeldung. Biete sowohl eine wartbare Projektfassung mit \`index.html\` + \`assets/\` als auch eine eigenständige HTML-Datei mit eingebetteten Bildern an. Das Referenzprojekt V0.2 selbst darf nicht verändert werden.
>
> **Abgabe:** funktionsfähiger Code, Versionshinweis „Integriert V0.1“, die konkreten Testfälle und ein Hinweis auf die noch nicht implementierte quantitative Synchronisierung einzelner Bildäpfel.

## Tatsächliche Integration und Korrekturschleife

1. Unveränderte Modellfunktionen und die Zylinder-/Diagrammdarstellung aus V0.2 in eine gemeinsam nutzbare Seite übernommen.
2. Die bereits geprüften, einheitlich zugeschnittenen Phasenbilder aus Story V0.1 als lokale Assets bzw. Base64 in Einzel-HTML eingebunden.
3. Die einzige Modellvariable \`state\` speist alle Live-Kennzahlen, Gegenstrombalken und Modellansichten; Phasennavigation ist davon getrennt.
4. Ein einheitlicher Satz von Steuerungsbuttons und zwei benannte Parameter-Presets eingeführt.
5. Browserprüfung zeigte zwei Darstellungsfehler: Ein aktiver Vergleich-Reiter verlor im Hoverzustand seinen ausreichenden Kontrast; in der Bildlegende blieb ein Markdown-Formatierungsrest. Beides in der freigegebenen Datei korrigiert.

## Tatsächlich durchgeführte Browserprüfungen

Chromium/Playwright mit vollständig eingebetteter HTML-Datei (direkte \`file://\`-Navigation wurde in der Testumgebung vom Administrator blockiert, daher isoliert gerenderte HTML-Datei).

- Start mit Story-Preset: **A=50, B=0, H=4,00, R=0,00**.
- Erster Einzelschritt: **A=46,00, B=4,00**.
- Wechsel zu **Vergleich**, Phase II auswählen: Schrittzahl und Modellmengen unverändert.
- Wechsel zu **Modell**: A in Zylinderanzeige identisch, Diagramm-Stufenpfade vorhanden.
- Start/Pause: Schrittzahl wird erhöht, danach stoppt der Timer.
- Zurück zu **Geschichte**: aktuell berechneter Schritt bleibt erhalten.
- „Apfelkrieg-Vorgabe“ setzt Werte wieder auf 50/0 und 0,08/0,04, „V0.2-Werte“ auf 50/0 und 0,06/0,04.
- Wahl „Vogelperspektive“ blendet die Seitenansicht korrekt aus.
- Keine JavaScript-Laufzeitfehler bei den geprüften Bedienabläufen.
- Schmaler Bildschirm (390 px): keine horizontale Seitenüberbreite.
- **Noch offen:** manueller Doppelklick-Test auf dem Endgerät und Unterrichtserprobung.

## Grenzen und nächste kleine Schritte

- Die Phase IV und V sind **Illustrationen einer Modellidee**, keine automatischen Zustandsmarkierungen.
- Die Apfelbestände und Flugäpfel **im Bild** ändern sich noch nicht bei einer Modellfortschreibung.
- Das Modell benutzt kontinuierliche Modelleinheiten und hat kein stochastisches Einzelapfelverhalten.
- Später kann eine synchrone, **modellgesteuerte Apfeldichte in der Vogelperspektive** ergänzt werden. Zunächst muss fachlich und gestalterisch geklärt sein, wie die beweglichen Äpfel als eigene Grafikschicht auf einen Hintergrund gelegt werden, statt einfach mit festen Äpfeln im Bild zu kollidieren.
- Version V0.2 bleibt als **gesicherte erste Workshop-Rückfallversion** unangetastet.

**Dokumentationsprinzip:** Zu jeder neuen Version Quelle, Entwicklungsauftrag, echte Fehlerkorrekturen, Prüffälle und Grenzen sichern.