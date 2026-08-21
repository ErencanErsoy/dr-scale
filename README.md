# Dr. Scale

Skalierungsrechner für das digitale Terminmanagement im Patientenportal.
Entscheidungsunterstützung mit offengelegten Rechenfällen für Krankenhäuser.

**→ [erencanersoy.github.io/dr-scale](https://erencanersoy.github.io/dr-scale/)**

## Forschungszweck

Das Werkzeug setzt ein Bewertungsmodell um, das im Rahmen einer Masterarbeit zur Wirtschaftlichkeit
des digitalen Terminmanagements entwickelt wurde. Es beantwortet, unter welchen wirtschaftlichen
Bedingungen sich die Anbindung einzelner organisatorischer Einheiten und die Gesamtinvestition aus
Sicht des Krankenhausträgers tragen.

Bewertet wird dabei der Prozessabschnitt des digitalen Aufnahmemanagements nach Fördertatbestand 2,
innerhalb dessen die Online-Terminvereinbarung. Für das Behandlungs- und das Entlassmanagement gilt
eine andere Mengen- und Preisbasis, weil dort der stationäre Fall die Bezugsgröße bildet und die
Fallpauschale zwischen Wirkung und Zahlungsstrom tritt.

Nicht beantwortet wird, welcher Anbieter zu wählen ist, ob ein Produkt anderen überlegen ist oder ob
die staatliche Förderung gesamtwirtschaftlich wirksam ist. Bewertet werden ausschließlich Zahlungen
des Trägers. Das Überschreiten einer wirtschaftlichen Schwelle ist eine notwendige, keine
hinreichende Bedingung für eine Anbindung: Organisatorische Umsetzbarkeit und strategische
Priorisierung treten hinzu.

## Ergebnisgrößen

| Größe | Frage | Einheit |
|---|---|---|
| Mindestvolumen `m` | Ab welchem Terminvolumen trägt eine weitere Einheit ihre Anbindung? | Termine je Jahr |
| Break-even `B` | Ab welchem insgesamt angebundenen Volumen trägt sich das Portal? | Termine je Jahr |
| Amortisationsdauer `T` | Nach welcher Zeit ist die Zahlung gedeckt? | Jahre |

Die ersten beiden kommen ohne Kenntnis des angebundenen Volumens aus. Die dritte setzt es voraus und
ist deshalb immer zusammen mit dem unterstellten Volumen zu lesen.

## Modelllogik

Alle Zahlungen werden danach eingeordnet, **mit welcher Größe sie wachsen**. Diese Einteilung ist
vollständig, weil jede Zahlung genau eine Bezugsgröße hat.

| Bezugsgröße | Eingang | Positionen |
|---|---|---|
| je umgestelltem Termin | Nutzen `n` | vermiedener Terminausfall, eingesparte Verwaltungszeit, Entgelt je Onlinebuchung |
| je angebundener Einheit | Anbindungskosten `a` | Einrichtung durch Anbieter oder in Eigenregie, Schulung, Anbindung an Vorsysteme, Test und Abnahme |
| unabhängig von beidem | Fixblock `F` | Investition, Wartung und Lizenzen, Schnittstellenpflege, Betrieb, vermiedener Vergütungsabschlag |

Positionen, die als Arbeitszeit anfallen, werden über Stunden und den Personalkostensatz bewertet,
nicht über einen Kostenwert. Dieselbe Leistung kann je nach Zahlungsweise in verschiedenen Klassen
liegen; maßgeblich ist die Zahlungsweise, nicht die Bezeichnung.

## Formeln

```
n     = (r_off − r_on)/100 · b  +  t/60 · c  −  k     Nutzen je umgestelltem Termin
d_j   = d_0 + (d_H − d_0) · j/H                       Zeitpfad, lineare Interpolation
N(τ)  = Σ_{j≤τ} n · d_j / (1+i)^j                     kumulierter Barwert je Termin
A_j   = g_j / 19 · E                                  vermiedener Vergütungsabschlag
F     = I₀ · (1−f) + Σ K/(1+i)^j − Σ A_j/(1+i)^j      Fixblock
KW(V) = V · N − F                                     Kapitalwert als Gerade
m     = a / N        B = F / N        T = min{τ | V · N(τ) ≥ Zahlung}
```

Der lineare Zeitpfad ist eine Interpolation zwischen dem gemessenen Ausgangswert und der angenommenen
Sättigungsgrenze, kein beobachteter Adoptionsverlauf.

## Eingaben

Die Seitenleiste zeigt voreingestellt **16 Felder**, die dem Modell der Arbeit entsprechen.

| Gruppe | Felder |
|---|---|
| Wirkung je Termin | No-Show-Rate mit und ohne Onlinebuchung, Deckungsbeitrag, Zeitersparnis, Personalkostensatz |
| Digitaler Buchungsanteil | heutiger Wert, Zielwert des Hauses |
| Investition und Kosten | Investitionssumme, Anbindungskosten je Einheit, laufende Kosten, erstes Jahr mit laufenden Kosten |
| Erlöse und Zeitraum | stationäre Erlöse, ambulante Termine, erstes Betrachtungsjahr, Zeitraum, Kalkulationszinssatz |

Über den Schalter **Erweiterte Eingaben** kommen sechs weitere hinzu: durch Fördermittel gedeckter
Anteil, Entgelt je Onlinebuchung, interner Einrichtungsaufwand, Schulungsaufwand, weitere Kosten je
Einheit, weitere laufende Kosten.

Bei den zugerechneten Verfügbarkeitsanforderungen lassen sich die **19 Muss-Anforderungen einzeln
auswählen**, im Wortlaut des Erhebungsinstruments und gruppiert nach Aufnahme-, Behandlungs- und
Entlassmanagement. Die Auswahl schreibt ihre Zahl in das Feld. Voreingestellt ist allein 2.V1, die
Online-Terminvereinbarung, der Gegenstand des Modells. Zehn der 19 entfallen auf das
Aufnahmemanagement, sechs auf das Behandlungs- und drei auf das Entlassmanagement. Alle sind mit null vorbelegt und verändern das Ergebnis nicht,
solange sie ausgeblendet bleiben. Wer nur die Basisansicht ausfüllt, rechnet genau das Modell der
Arbeit.

Zusätzlich lässt sich eine **Liste organisatorischer Einheiten** erfassen, je Zeile Name,
Terminvolumen und Anbindungsjahr. Sie zeigt je Einheit das für ihren Anbindungszeitpunkt geltende
Mindestvolumen, den Beitrag zum Kapitalwert und die Amortisationsdauer. Der Anbindungszeitpunkt wirkt
erheblich, weil eine später angebundene Einheit nur die verbleibenden Jahre des Betrachtungszeitraums
nutzt.

## Herkunft der Werte

Sechs Herkunftsarten werden durchgehend farblich unterschieden: Literatur, Rechtsgrundlage,
Sekundärdaten, Annahme, Festlegung und im Modell Berechnetes. Jeder Wert nennt an Ort und Stelle
seine Herkunft und seine Rechnung.

Voreingestellt ist ein Musterkrankenhaus mit gerundeten Werten ohne empirischen Anspruch. Alle als
einrichtungsspezifisch gekennzeichneten Größen muss jedes Haus selbst erheben.

## Annahmen

Die drei Größen der Nutzenseite sind unterschiedlich gut belegt. Die No-Show-Raten sind gemessen, der
Personalkostensatz folgt einer amtlichen Tabelle, der Deckungsbeitrag ist eine Annahme mit
Größenordnungsanker. Die Zeitersparnis hat keinen Anker und gilt nur für Vorgänge, die durch die
Onlinebuchung tatsächlich ersetzt werden. Die Ergebnisse werden deshalb durchgehend auch ohne sie
ausgewiesen.

Der Zusammenhang zwischen Onlinebuchung und geringerem Terminausfall ist gemessen, ein ursächlicher
Zusammenhang ist nicht belegt.

## Ausgabe

Fünf Abbildungen in wissenschaftlicher Darstellung lassen sich als Vektorgrafik speichern, bei Bedarf
als PNG. Linienarten sind so gewählt, dass die Abbildungen auch im Schwarzweißdruck unterscheidbar
bleiben. Jeder Reiter lässt sich zusätzlich über den Druckdialog als PDF ausgeben.

Die Rechnung selbst lässt sich im Reiter Ergebnisse über die Karte „Rechnung exportieren“
mitnehmen. „Als CSV exportieren“ liefert alle Größen in einem Block mit Semikolon als Trenner
und deutschem Zahlenformat. „Als Excel exportieren“ liefert dieselben Angaben als Arbeitsmappe
mit vier Blättern, Eingaben, Modell, Ergebnisse und Sensitivität, wobei Zahlen als Zahlen und
nicht als Text ankommen.

Die Arbeitsmappe enthält **echte Formeln**, keine ausgerechneten Zahlen. Wer im Blatt Eingaben
einen Wert ändert, bekommt in Excel unmittelbar neue Ergebnisse. Der Aufbau ist fünfteilig:
Eingaben, Jahre mit der Diskontierung und den Zeitpfaden, Modell mit den Größen der Gleichungen,
Ergebnisse mit beiden Schwellen je Rechenfall und Sensitivität. Nur die Sensitivität steht als
Wert, weil jede ihrer Zeilen ein vollständiger zweiter Modelldurchlauf ist. Die CSV-Datei
enthält demgegenüber nur die berechneten Werte.

## Anwendungsbeispiel

Die Werte eines Anwendungsbeispiels sind mit AES-256-GCM verschlüsselt hinterlegt. Der Schlüssel wird
über PBKDF2-HMAC-SHA256 mit 250.000 Runden aus einem Passwort abgeleitet, die Entschlüsselung erfolgt
ausschließlich im Browser über die Web-Crypto-Schnittstelle. Ohne Passwort sind diese Werte auch im
Quelltext nicht lesbar. Das allgemeine Modell ist ohne Passwort vollständig zugänglich.

## Technisches

Die Seite besteht aus `index.html` und der daneben liegenden Tabellenbibliothek
`xlsx.full.min.js`. Beide werden vom selben Server geladen, nichts wird von einem fremden Server
nachgeholt, weder Schriftart noch Bild noch Skript. Diagramme werden als SVG im Browser erzeugt.
Ohne die Bibliothek bleibt die Seite voll benutzbar, nur der Excel-Export meldet dann, dass er
nicht zur Verfügung steht.

### Verwendete Fremdsoftware

`xlsx.full.min.js` ist die SheetJS Community Edition in der Version 0.20.3, unverändert
übernommen von `https://cdn.sheetjs.com`. Sie steht unter der Apache License 2.0, deren
vollständiger Text als `LICENSE-xlsx.txt` beiliegt. Copyright (C) 2012-present SheetJS LLC.
Der übrige Quelltext der Seite stammt vom Verfasser.

## Hinweis

Modellhafte Beispielrechnung unter offengelegten Annahmen. Sie dient der Vorbereitung einer
Entscheidung und ersetzt keine Wirtschaftlichkeitsberechnung nach haushaltsrechtlichen Vorgaben.

---

Erencan Ersoy · Masterarbeit an der Freien Universität Berlin
