# Dr. Scale

Browserbasiertes Berechnungstool zur wirtschaftlichen Bewertung der
Online-Terminvereinbarung in Patientenportalen deutscher Krankenhäuser.

**[Dr. Scale öffnen](https://erencanersoy.github.io/dr-scale/)**

## Überblick

Dr. Scale berechnet zwei wirtschaftliche Schwellen:

| Ergebnisgröße | Entscheidungsfrage | Einheit |
|---|---|---|
| Terminschwelle `m` | Welches jährliche Terminvolumen benötigt ein weiterer Krankenhausbereich, damit die monetär bewerteten Vorteile seine Anbindungskosten decken? | Termine je Jahr |
| Portal-Break-even `B` | Ab welchem aggregierten jährlichen Terminvolumen sind die berücksichtigten portalweiten Nettokosten gedeckt? | Termine je Jahr |

Das Modell berücksichtigt Kosten und monetär bewertbare Vorteile aus Sicht des
Krankenhausträgers. Grundlage sind Literaturbefunde zum digitalen
Buchungsanteil, zur Bearbeitungszeit und zu Terminausfällen sowie die
Verfügbarkeitsanforderungen des Fördertatbestands 2 aus der
Digitalisierungsabschlags-Vereinbarung.

## Funktionsumfang

Dr. Scale bietet:

- Anpassbare Kosten-, Nutzungs- und Prozesswerte
- Unmittelbare Berechnung der Terminschwelle und des Portal-Break-even
- Vier kombinierte Szenarien aus digitalem Buchungsanteil und administrativer Zeitersparnis
- Eine Einweg-Sensitivitätsanalyse zentraler Eingangsgrößen
- Eine Einordnung eingegebener Terminvolumina nach Krankenhausbereichen
- Einen schrittweise dargestellten Rechenweg mit Gleichungen und eingesetzten Werten
- Einen Excel-Export mit Eingaben, Formeln, Ergebnissen, Sensitivitätsanalyse und Quellen

## Schnellstart

1. [Dr. Scale öffnen](https://erencanersoy.github.io/dr-scale/).
2. Die voreingestellten Werte des Musterkrankenhauses prüfen.
3. Die blau markierten Eingabewerte an das betrachtete Krankenhaus anpassen.
4. Ergebnisse, Szenarien und Sensitivitätsanalyse auswerten.
5. Den Berechnungsnachweis bei Bedarf als Excel-Datei exportieren.

Alle Ergebnisse werden nach einer Änderung der Eingabewerte automatisch neu
berechnet.

## Modellrahmen

Die Eingangsgrößen sind vier Bereichen zugeordnet:

- Vorteil je digital gebuchtem Termin
- Nutzung und Betrachtungszeitraum
- Kosten des Patientenportals
- Vermiedener Digitalisierungsabschlag

Die Ergebnisse gelten für die jeweils eingesetzten Daten und Annahmen. Das
Überschreiten einer Schwelle zeigt die Deckung der im Modell berücksichtigten
Kosten. Es stellt keine vollständige Bewertung der organisatorischen
Umsetzbarkeit, der strategischen Priorität oder der Qualität eines Anbieters
dar.

## Datengrundlage und Verarbeitung

Voreingestellt ist ein Musterkrankenhaus mit frei gewählten und gerundeten
Werten ohne empirischen Anspruch. Die geschützten Werte des in der
Masterarbeit untersuchten Anwendungsfalls sind verschlüsselt hinterlegt und
können nur mit dem zugehörigen Passwort geladen werden.

Alle Eingaben und Berechnungen werden lokal im Browser verarbeitet. Es werden
keine eingegebenen Daten an einen Server übertragen.

## Technische Umsetzung

Dr. Scale besteht aus einer HTML-Datei und einer lokal bereitgestellten
Tabellenbibliothek. Berechnungen und Diagramme werden unmittelbar im Browser
erzeugt. Es werden keine externen Schriftarten, Bilder oder Skripte
nachgeladen.

Für den Excel-Export wird ExcelJS 4.4.0 verwendet. Die Bibliothek steht unter
der MIT-Lizenz; der zugehörige Lizenztext ist im Repository dokumentiert. Ohne
die Bibliothek bleiben Eingaben, Berechnungen und Diagramme nutzbar, lediglich
der Excel-Export steht dann nicht zur Verfügung.

## Wissenschaftlicher Kontext

Dr. Scale wurde von Erencan Ersoy im Rahmen der Masterarbeit

*Bewertung der Wirtschaftlichkeit von Patientenportalen im Krankenhaus:
Entwicklung eines Bewertungsmodells und empirische Anwendung an der Charité*

an der Freien Universität Berlin entwickelt.

## Version

Der in der Masterarbeit dokumentierte Entwicklungsstand ist Version 1.11
(Tag `v1.11`). Die Versionsangabe wird zusätzlich in der Fußzeile der
Anwendung und in den exportierten Dateien ausgewiesen.

## Zitieren

> Ersoy, E. (2026). *Dr. Scale* (Version 1.11) [Computer software].  
> https://github.com/erencanersoy/dr-scale

## Hinweis

Dr. Scale ist eine modellhafte Berechnung unter offengelegten Daten und
Annahmen. Das Werkzeug unterstützt die Vorbereitung einer Entscheidung,
ersetzt jedoch keine vollständige Wirtschaftlichkeitsuntersuchung nach
haushaltsrechtlichen Vorgaben.
