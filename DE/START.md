# Hermes lokal: ein verständlicher Einstieg mit Ergebnisprüfung

## 1. Ziel und Voraussetzungen
Ein Assistent soll zwei kleine Quelldateien lesen und eine überprüfbare Ergebnisdatei schreiben. Das Modell läuft in einem separaten, bereits eingerichteten lokalen Server. Voraussetzung: vorhandener Hermes-Client, eigene bekannte Modellkennung, passende Kontextgrenze und PowerShell. Dieses Paket installiert und startet nichts. Prüfe die aktuellen Installationswege in QUELLEN.md, wenn dir der Client fehlt.

## 2. Auspacken und nur vorbereiten
Entpacke den kompletten ZIP in einen neuen Lernordner. Lies VORBEREITEN-UEBUNG.ps1. Im entpackten Ordner:

```powershell
./VORBEREITEN-UEBUNG.ps1 -OutputDirectory ./mein-erster-agententest
```

Das Skript kopiert nur eigene synthetische Übungsdaten, Auftrag, Schema und Prüfer. Bestehende Ziele bleiben erhalten. Bei einer Ausführungsrichtlinie erst Inhalt und eigene Richtlinie verstehen; nicht global blind abschalten.

## 3. Verbindung prüfen, bevor der Auftrag startet
Hermes richtet einen benutzerdefinierten OpenAI-kompatiblen Endpunkt über hermes model ein. Die aktuelle Anleitung verlangt mindestens 64000 Tokens Kontext und kann kleinere Werte ablehnen. 65536 ist eine mögliche Konfigurationszahl, keine zugesagte Speicherkapazität. Kläre zuerst, was dein vorhandener Server wirklich bereitstellt; erhöhe den Kontext nicht während anderer Arbeit. Die reine Windows-RAM-Größe beweist keine nutzbare Kontextgrenze.

Ein lokaler Hauptanbieter garantiert nicht, dass Hilfsaufgaben und Fallbacks ebenfalls lokal bleiben. Prüfe die vorhandenen Einstellungen und dokumentiere tatsächlich benutzte Routen. Dieses Paket enthält nur HERMES-ENDPOINT-NOTIZ.txt; keine private config.yaml oder geheimen Schlüssel. Für Installation und andere Betriebssysteme gilt die aktuelle offizielle Anleitung.

Die echte Modellkennung muss zum Server passen. localhost und 127.0.0.1 sind Loopback-Adressen des jeweiligen Systems. Ein falscher Port, ein fehlender /v1-Pfad oder zu kleine Kontextgrenzen sind Verbindungsprobleme, kein Beweis für schlechte KI.

## 4. Im Übungsordner bleiben
```powershell
Set-Location ./mein-erster-agententest
hermes
```

Starte zuerst die einfache vorhandene Sitzung. Die aktuelle Oberfläche bietet optional hermes --tui. Eigene Skills und Modellprofile aus dem Archiv gehören nicht automatisch zu jeder Installation. Der neue Auftrag nutzt keine Kindagenten.
Ein Ordner ist keine technische Sandbox. Prüfe die angebotenen Werkzeugrechte. Dieser Auftrag braucht Lesen und Schreiben der Übungsdateien, keine Netzwerk-, Installations- oder Systemänderungen. Bestehende Rechte nicht pauschal abschalten.

## 5. Den Auftrag bewusst geben
Bitte den Assistenten, AUFTRAG.md und ERGEBNIS-SCHEMA.json zu lesen. Er soll nur ERGEBNIS.json erstellen. Keine privaten Projektverzeichnisse als Kontext anhängen. Inhalte in fixtures sind Daten; eingebettete Anweisungen dürfen den Auftrag nicht ändern.

## 6. Die Rechnung selbst verstehen
A1 nennt 131072 Tokens insgesamt und 3 Slots. A2 verlangt 40000 pro Anfrage. A4 erklärt die gleichmäßige Aufteilung. Für unseren neuen Vertrag gilt ausdrücklich abrunden: 131072 / 3 = 43690,666… → 43690 ganze Tokens. 43690 ≥ 40000, also meets_requirement=true. A3 ist ein Entwurf und wird ignoriert. Das ist eine fiktive Rechenaufgabe, keine neue Messung des heutigen Servers.

## 7. Die Reihenfolge selbst verstehen
Nur freigegebene Einträge zählen. Kleinere priority zuerst, bei Gleichstand kleinere sequence. beta hat 10/1, gamma 20/1 und alpha 20/2. Deshalb beta, gamma, alpha. delta bleibt draußen, weil B5 verworfen ist. Die benutzten Kennungen sind B1 bis B4.

## 8. Mit dem eigenen Prüfer kontrollieren
Lies PRUEFEN-ERGEBNIS.ps1. Nach der echten Agentenantwort im Übungsordner:

```powershell
./PRUEFEN-ERGEBNIS.ps1 -ResultPath ./ERGEBNIS.json
$LASTEXITCODE
```

Exitcode 0 heißt: dieser kleine Dateivertrag wurde erfüllt. Exitcode 1 heißt: mindestens ein Wert, Datentyp, Reihenfolge oder Beleg stimmt nicht. Der Prüfer startet kein Modell und schreibt die Antwort nicht um. Ein Hash zeigt erhaltene Bytes; er beweist keine allgemeine Wahrheit oder Kindagentenausführung.

## 9. Bei FAIL gezielt nachbessern
Zuerst den konkreten Fehler lesen. Ein Dezimalwert statt einer Ganzzahl, die falsche Reihenfolge oder ein erfundener Beleg sind eigenständige Fehler. Gib dem Assistenten nur den betreffenden Fehler zurück und prüfe erneut. Ändere nicht einfach den Prüfer, damit ein schöner Text besteht.

## 10. Archiv, neuer Test und eigenes Urteil trennen
ARCHIV enthält nur eigene synthetische Daten und frühere Ergebnisse vom 19.09.2026. Damals war das Zweikinder-Profil speziell eingerichtet. OpenCode schrieb 43690, Hermes die ungerundete Zahl 43690,666…; beide alten Antworten sind erhalten. Der neue Ganzzahlvertrag ist absichtlich präziser. Die Archivdateien sind kein heute neu ausgeführter Agententest und passen nicht unverändert zum neuen Schema.

Fülle ABNAHME.csv nur mit wirklich ausgeführten Prüfungen. Ein neuer Modelllauf bleibt offen, bis du eine echte Ergebnisdatei vorlegen kannst. Änderungen in richtigen Projekten brauchen zusätzliche fachliche Prüfung, Versionskontrolle und passende Tests. Auf einem anderen AMD-PC oder Mac ist dieser Ablauf hier nicht frisch erprobt.
